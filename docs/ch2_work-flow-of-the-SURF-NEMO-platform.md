# **Workflow of the SURF-NEMO platform**

<div style="text-align: justify">
    <p>The schematic work-flow diagrams in <a href="#fig-workflow-schematic">Fig. 2.1</a> shown the step involved in the SURF-NEMO numerical platform.
    The steps in the most recent version release are grouped as follows:</p>

   <ol>
      <li>
         <p><b>Initialization</b>: the user specifies the values of the input simulation parameters for the ocean model in the configuration file (horizontal and vertical grids, subgrid scale parameterizations, etc.) for the specific experiment selected.</p>
      </li>
      <li>
         <p><b>Access and download of the input datasets</b>: this is an automated step in which the input datasets for the selected simulation period are downloaded from remote or local data repositories, as specified in the configuration file. The input data are the bathymetry, the coastline, the atmospheric forcing and the coarse resolution parent ocean model for the initial and lateral boundary condition datasets.</p>
      </li>
      <li>
         <p><b>Spatial numerical grid generation</b>: this is an automated step that generates the horizontal and vertical grid for the nested model.</p>
      </li>
      <li>
         <p><b>Input data regridding</b>: this is an automated step that generates the bottom topography, surface forcing, initial and open lateral boundary conditions datasets on the child grid.</p>
      </li>
      <li>
         <p><b>Forecast</b>: another automated step in which the NEMO code is exectuted to produce the final outputs.</p>
      </li>
      <li>
         <p><b>Post-processing</b>: in this step the visualization and analysis procedures of the final outputs are considered. Different options of postoprocessing are available, i.e. comparing parent/child fields, comparing the simulation results with in-situ or satellite datasets and converting the datasets into what?</p>
      </li>
   </ol>

   <div class="d-flex justify-content-center">
      <figure id="fig-workflow-schematic" class="figure text-center">
         <a href="../assets/img/workflow_schematic.png">
            <img src="../assets/img/workflow_schematic.png" alt="../assets/img/workflow_schematic.png" width="60%">
         </a>
         <figcaption class="figurenum">Work-flow of the Relocatable SURF-NEMO platform.</figcaption>
      </figure>
   </div>

   <p>The graphical calling function flow shown in <a href="#fig-workflow-sequential">Figure 2.2</a> represent
   all paths traversed through a program during its execution and shows how the program is completed from start to finish,
   step-by-step. The six macro-tasks identified are: (1) child meshmask generation; (2) atmospheric data regridding;
   (3) ocean IC data regridding; (4) ocean BC data regridding and OBC data extraction; (5) ocean model simulation;
   and (6) visualization and data analysis.</p>

   <div class="d-flex justify-content-center">
      <figure id="fig-workflow-sequential" class="figure text-center">
         <a href="../assets/img/workflow_sequential.png">
            <img src="../assets/img/workflow_sequential.png" alt="../assets/img/workflow_sequential.png" width="55%">
         </a>
         <figcaption class="figurenum">Graphical calling function flow of the Relocatable SURF-NEMO platform.</figcaption>
      </figure>
   </div>

   <p>The computational tasks are not independent of each other. The dependency flow graph of the macrotasks is given
   in <a href="#fig-workflow-dependency">Figure 2.3</a>.
   Each node (from A to F) represents a macro-task and the solid edges represent data dependencies among these macro-tasks.
   From node A, tree edge can take us to node B, node C and D. Node E can begin once all the lower nodes are completed.</p>

   <div class="d-flex justify-content-center">
      <figure id="fig-workflow-dependency" class="figure text-center">
         <a href="../assets/img/workflow_dependency.png">
            <img src="../assets/img/workflow_dependency.png" alt="../assets/img/workflow_dependency.png" width="100%">
         </a>
         <figcaption class="figurenum">Dependency flow graph of macro-tasks.</figcaption>
      </figure>
   </div>

</div>

## **Setting up the input model parameters**

<div style="text-align: justify">
    <p>The first task executed by each macro-task consists of setting up the values of the input model parameters,
      which are obtained from the configuration files <code>setParFree.json</code> and <code>setParFixed.json</code>.
      The configuration file structure and the input parameters are described in
      <a href="#ch3_user-configuration-file-preprocessing-sections">Chapter 3</a> and
      <a href="#appA_reference-configuration">Appendix A</a>.
      In this phase, the <code>read_inJsonFree</code> and <code>read_inJsonFixed</code> procedures are executed
      to respectively define the user-free and fixed input parameters required to execute the NEMO model and all of
      the pre- and post-processing tasks.
      The procedures <code>set_pathData</code> and <code>set_fileData</code> are also called to define all of the paths
      and file names used by the program for the specific numerical simulation.
    </p>
</div>

## **Child Meshmask Generation**

<div style="text-align: justify">
      <p>The child grid is generated after the model configuration phase. The NEMO model uses the Arakawa C grid for
      spatial discretization, with the state variables defined on the staggered grid illustrated
      in <a href="#fig-arakawa-grid">Figure 2.4</a>. In the C grid the scalar quantities (temperature T, salinity S, pressure p,
      density <span class="math">\(\rho\)</span>) are defined at the center of each grid volume. The velocity field components (zonal u, meridional
      v and vertical w) are shifted by half a grid width in their respective direction so that they are defined at
      the edges of the grid volumes. The procedures executed in this phase are:</p>
      <ul class="simple">
         <li><p>Generation of the child 2D-mesh.</p></li>
         <li><p>Interpolation of the source bathymetric dataset on the generated child grid.</p></li>
         <li><p>Generation of the child 3D-meshmask.</p></li>
      </ul>

      <div class="d-flex justify-content-center">
         <figure id="fig-arakawa-grid" class="figure text-center">
            <a href="../assets/img/ArakawaC.png">
               <img src="../assets/img/ArakawaC.png" alt="../assets/img/ArakawaC.png" width="100%">
            </a>
            <figcaption class="figurenum">The staggered Arakawa C-grid used by NEMO ocean model.</figcaption>
         </figure>
      </div>

</div>

### **Horizontal grid**

<div style="text-align: justify">
    <p>The horizontal grid generation is managed by the NEMO-MESH code. SURF uses ONLY a rectangular
    (or latitude-longitude) grid in a spherical coordinate system <span class="math">\(\lambda,\varphi\)</span>.
    The horizontal grid (expressed in degrees) is generated by specifying the number of points
    <span class="math">\(n_{\lambda}\)</span> and <span class="math">\(n_{\varphi}\)</span>,respectively, in zonal and
    meridional directions, and the respective grid sizes <span class="math">\(\Delta\lambda\)</span> and
    <span class="math">\(\Delta\varphi\)</span> (in degrees) and the longitude and latitude <span class="math">\((\lambda,\varphi)_{1,1}\)</span>
    of the first row and first column of the T grid. On the <span class="math">\(\lambda\varphi\)</span> plane,
    the location of the T points of the grid are:</p>
    <span class="math">$$
    \begin{equation}
    \begin{array}{ll}
        \lambda_{i,j} = \lambda_{11} + (i-1) \Delta \lambda   \hspace{0.5cm} \mbox{with} \hspace{0.2cm} i=1.....n_\lambda
        \\
        \varphi_{i,j} = \varphi_{11} + (j-1) \Delta \varphi   \hspace{0.5cm} \mbox{with} \hspace{0.2cm} j=1.....n_\varphi
    \end{array}
    \end{equation}
    $$</span>
    <p>The u, v points of the grid are shifted by half a grid width in the zonal e/o meridional direction, as indicated
    in <a class="reference internal" href="#fig-arakawa-grid"><span class="std std-numref">Fig. 2.4</span></a>.</p>

</div>

### **Bathymetry regridding**

<div style="text-align: justify">
    In this phase the bathymetric dataset is interpolated on the child grid, which is required to generate the 3D meshmask.
    The procedures in this phase are:</p>

    <ul class="simple">
        <li><p>Accessing and downloading the source bathymetry and the coastline datasets.</p></li>
        <li><p>Manipulating the bathymetry dataset.</p></li>
        <li><p>The spatial interpolation of the source bathymetric on the child grid.</p></li>
    </ul>

</div>

#### **Access the bathymetry and coastline datasets**

<div style="text-align: justify">
    <p>A procedure for checking if the necessary input datasets are present in the experiment directory
    <code>$PATH_IDEXP/data/data00/indata/</code> is executed.
    If some of the requested data are not present then the procedures <code>downlCoastlineInfile</code> and
    <code>downlBathyInfile</code> are automatically executed to download the coastline and the bathymetry,
    respectively, from remote or local data repositories as specified in the configuration file
    <code>setParFree.json</code>.</p>
</div>

#### **Manipulating and smoothing bathymetry**

<div style="text-align: justify">

<p>Before conducting the spatial interpolation on the child grid, the source bathymetry data product can be
manipulated if specified in the configuration file setParFree.json. Several methods can be used:</p>
<ul class="simple">
    <li>
        <p>Add a constant value to the surface elevation for the whole nested region
        (e.g., an inland body of water with water level below the global ocean level such as the Caspian Sea).</p>
    </li>
    <li>
        <p>Set maximum and minimum values that are different from the source value
        (e.g., if a minimum depth of 5 metres or a maximum depth of less than the actual depth is required).</p>
    </li>
    <li>
        <p>Define the land/sea interface grid points according to the input coastline.</p>
    </li>
    <li>
        <p>Set maximums and minimums inside sub-regions (e.g., to mask a specific area)</p>
    </li>
    <li>
        <p>Smooth out bathymetry variations with the Shapiro filter.
        This is a high order horizontal filter that efficiently removes small scale grid noise without affecting
        the physical structures of a field. A Shapiro filter of a 2N order of accuracy is applied to a variable
        based on the expression:</p>
    <span class="math">$$
    \begin{equation}
        \label{eq:shapiro_filter}
        \tilde{w_i} = F^{2N}(w_i) =  \left[  I + (-1)^{N-1}  \frac{\delta^{2N}}{2^{2N}}  \right] (w_i) = w_i + (-1)^{N-1}  \frac{\delta^{2N} w_i}{2^{2N}}
    \end{equation}
    $$</span>
    <p> where <span class="math">\(\tilde{w_i}\)</span> is the filtered value of variable <span class="math">\(w\)</span>
    at point <span class="math">\(x_i\)</span>, <span class="math">\(I\)</span> is the identity operator and <span class="math">\(\delta^{2N}\)</span>
    is the even composition of the standard difference operator <span class="math">\(\delta\)</span>
    (<a href="#bib_richtmyer1957">Richtmyer, 1957</a>).
    This filter is a discrete symmetric operator with a (2N + 1) point stencil.
    It acts as a low-pass filter that preserves the low-frequency content (i.e., largest wavelengths)
    and completely dissipates the high-frequency content (i.e., shortest wavelengths) from the original field.</a></p></li>
</ul>

</div>

#### **Interpolation of bathymetric data**

<p> The spatial interpolation of the source bathymetric dataset on the child grid can be conducted after the
manipulation of the source bathymetry phase. The procedures are based on the Spherical Coordinate Remapping and Interpolation Package
(<a href="https://github.com/SCRIP-Project/SCRIP" target="_blank">SCRIP</a>) code.
The interpolation methods available are listed and described in <a href="#interpolation-methods">Section 3</a>.</p>

### **Meshmask and Vertical grid**

<div style="text-align: justify">

<p>The vertical grid generation is managed by the NEMO-MESH code. The type of vertical grid used in SURF
corresponds to geopotential z-coordinate levels with partial bottom cell representation of the bathymetry. After
the bathymetry <span class="math">\(z = H(\lambda,\varphi)\)</span> and the number of levels <span class="math">\(n_{z}\)</span>
have been specified, the vertical location of w- and
t-levels (expressed in metres) are defined, except in the bottom layer, from the following analytic expression:</p>
<span class="math">$$
\begin{equation}
    z(k) = h_{sur} - h_{0} k - h_{1} log [cosh (( k - h_{th}) h_{cr})]
\end{equation}
$$</span>
<p>where the coefficients <span class="math">\(h_{sur}\)</span>, <span class="math">\(h_0\)</span>,
<span class="math">\(h_1\)</span>, <span class="math">\(h_{th}\)</span> and <span class="math">\(h_{cr}\)</span>
are the parameters to be specified.
<span class="math">\(h_{cr}\)</span> represents the stretching factor of the grid and
<span class="math">\(h_{th}\)</span> is the approximate model level at which maximum stretching occurs.
This expression enables stretched z-coordinate vertical levels to be defined,
which are smoothly distributed along the water column, with appropriate thinning designed to better resolve the surface and intermediate layers.
Through partial cell parameterization, the thickness of the bottom layer can vary as a function of the geographical
location <span class="math">\((x,y)_{i,j}\)</span> which allows a better representation of the real bathymetry.</p>

<figure class="figure text-center">
<div class="d-flex justify-content-center">
    <figure id="fig-grid-xy">
        <a href="../assets/img/meshOceTUVxy_FC.png">
            <img src="../assets/img/meshOceTUVxy_FC.png" alt="../assets/img/meshOceTUVxy_FC.png" width="100%">
        </a>
        <figcaption>(A) Horizontal grid.</figcaption>
    </figure>
    <figure id="fig-grid-z">
        <a href="../assets/img/meshOceTz.png">
            <img src="../assets/img/meshOceTz.png" alt="../assets/img/meshOceTz.png" width="100%">
        </a>
        <figcaption>(B) Vertical T-grid.</figcaption>
    </figure>
</div>
<figcaption class="figurenum">Example of horizontal (left) and vertical (right) numerical grid with, respectively,
grid sizes of <span class="math">\(\Delta\lambda\)</span> and <span class="math">\(\Delta\varphi\)</span> in horizontal and <span class="math">\(\Delta z\)</span> in vertical direction.</figcaption>
</figure>

</div>

## **Input data Regridding**

<div style="text-align: justify">

<p>Regridding, also called remapping, is the process of changing the grid (from a source to a destination grid)
underlying the field data values while preserving the qualities of the original data. In this section we describe
the spatial extrapolation and interpolation procedure used in in SURF to remap the input fields on the child grid.
This phase will generate the surface forcing, initial and open lateral boundary condition datasets on the child grid.
The procedures in this phase are:</p>
<ul class="simple">
    <li><p>Accessing and downloading the input datasets</p></li>
    <li><p>Rotation of the vector fields (if required)</p></li>
    <li><p>Extrapolation of the input datasets</p></li>
    <li><p>Spatial interpolation of the source dataset on the child grid</p></li>
    <li><p>Lateral Open Boundary Condition dataset generation</p></li>
</ul>

</div>

### **Access and download of the input datasets**

<div style="text-align: justify">

<p>A procedure for checking if the necessary input datasets are in the experiment directory
<code>$PATH_IDEXP/data/</code> is executed.
If any of the requested data are not present then the procedures <code>downlAtmSrc</code>,
<code>downlOceICSrc</code> and <code>downlOceBCSrc</code> are automatically executed to respectively download
the atmospheric forcing and the initial and lateral boundary condition datasets for the selected period of
the simulation from remote or local data repositories, as specified in the configuration file <code>setParFree.json</code>.</p>

</div>

### **Rotation of horizontal velocity u, v**

<div style="text-align: justify">

<p>When the parent coarse resolution model is defined on a rotated or a curvilinear grid
(e.g., the global tripolar grid, <a href="#fig-orca-global">Fig. 2.6(a)</a>)
one more step is required to interpolate the horizontal velocity fields on the child grid.
In an ocean model with a “distorted” grid, the velocity vectors are obtained according to the direction of
the grid lines. In a staggered Arakawa C grid system, the velocity field components are defined at the cell edges
(the gray arrows in <a href="#fig-rotvector">Fig. 2.6(b)</a>).
A rotation in the latitudinal and longitudinal directions of the velocity components must be applied
to change the vectors from the local system <span class="math">\((x,y)\)</span> to a geographical
system <span class="math">\((x^{'},y^{'})\)</span>, so that U gives the zonal component (W-E direction) and V the meridional component (S-N
direction) of the velocity vector. Therefore, to transform the <span class="math">\((x,y)\)</span>
coordinates to the <span class="math">\((x^{'},y^{'})\)</span> coordinates, the vectors must be rotated according to
vectors need to be rotated according to</p>

<span class="math">$$
\begin{equation}
\begin{array}{ll}
U^{'}(x*{t}^{'},y*{t}^{'}) = U(x*{t},y*{t})_cos(\alpha_{t}) - V(x*{t},y\_{t})*sin(\alpha*{t})
\\
V^{'}(x*{t}^{'},y*{t}^{'}) = U(x*{t},y*{t})\*sin(\alpha*{t}) + V(x*{t},y*{t})\*cos(\alpha\_{t})
\end{array}
\end{equation}

$$
</span>
<p>For parent models with rotated rectangle grids, the angle is almost constant.
For those with curvilinear tripolar grids (as shown in <a href="#fig-orca-global">Fig. 2.6(a)</a>)
the angle will vary within each grid cell.</p>

<figure class="figure text-center">
<div class="d-flex justify-content-center">
    <figure id="fig-orca-global">
        <a href="../assets/img/orca_grid.png">
            <img src="../assets/img/orca_grid.png" alt="../assets/img/orca_grid.png" width="130%">
        </a>
        <figcaption>(A)</figcaption>
    </figure>
    <figure id="fig-rotvector">
        <a href="../assets/img/rotvector.png">
            <img src="../assets/img/rotvector.png" alt="../assets/img/rotvector.png" width="70%">
        </a>
        <figcaption>(B)</figcaption>
    </figure>
</div>

<figcaption class="figurenum">Example of curvilinear grid. Panel A gives an example of a tripolar grid.
Panel B gives the horizontal velocity components defined on the source curvilinear grid (black arrows) and on the destination rectilinear lat/lon grid (red arrows) after the rotation. </figcaption>
</figure>

</div>

### **Extrapolation methods**

<div style="text-align: justify">

<p>The extrapolation procedure used in SURF is referred to as the sea-over-land (SOL) procedure,
and provides the ocean field values for areas near the coastline where the parent model solutions are not defined.
The SOL procedure iteratively extrapolates the ocean quantities on the land grid-points, so they can be interpolated
on the child grid. This also applies to several atmospheric fields and takes into account the atmospheric land-sea mask,
to avoid land contaminations near the land-sea boundaries.</p>
<p>The SOL procedure is applied to the coarse resolution ocean fields to extrapolate the salinity,
temperature, sea surface height and current fields to the land points. The ocean fields in the nested-grid points
near to the coast can then be defined (by interpolation). The procedure applied for the atmospheric forcing
fields takes into account the atmospheric land-sea mask to ensure there is no contamination from the land atmospheric
fields to the sea points.</p>
<p>The source code is provided in the directory <code>$PATH_SURFNEMO/utilities/extrapol/seaoverland</code>.</p>

</div>

### **Interpolation methods**

<div style="text-align: justify">

<p>The extrapolation procedure described in the previous section provides the input data for the interpolator.
The procedures are based on the Spherical Coordinate Remapping and Interpolation Package
(<a href="https://github.com/SCRIP-Project/SCRIP" target="_blank">SCRIP</a>)
code. SCRIP is a software package that computes addresses and weights for remapping and interpolating
fields between grids in spherical coordinates. The package should work for any grid on the surface of a
sphere. SCRIP currently supports five remapping options:</p>
<ul class="simple">
<li><p><b>Conservative remapping</b>: First- and second-order conservative remapping, as described by Jones (1999, Monthly Weather Review, 127, 2204-2210).</p></li>
<li><p><b>Bilinear interpolation</b>: Slightly generalized to use a local bilinear approximation (only logically rectangular grids).</p></li>
<li><p><b>Bicubic interpolation</b>: Similarly generalized (only logically rectangular grids).</p></li>
<li><p><b>Distance-weighted averaging</b>: The inverse-distance-weighted average of a user-specified number of nearest neighbour values.</p></li>
<li><p><b>Particle remapping</b>: A conservative particle (Monte-Carlo-like) remapping scheme</p></li>
</ul>
<p>The source code can be found in the directory <code>$PATH_SURFNEMO/nemo/NEMOGCM/TOOLS/WEIGHTS</code>.</p>
<p>Regridding can be separated into two stages. The first stage is the generation of an interpolation weight matrix
that describes how points in the source grid contribute to points in the destination grid. The second stage is
the multiplication of values on the source grid by the interpolation weight matrix to produce the appropriate
values on the destination grid.</p>
<p>The SCRIP spatial interpolation procedure is applied to the input fields for the generated bathymetry,
atmospheric forcing and initial and boundary conditions files that are necessary to run the NEMO code.
The generated files are stored in the directory <code>$PATH_EXP/IDEXP/data/</code>.</p>

</div>

### **Lateral Open Boundary Condition**

<div style="text-align: justify">

<p>The lateral open boundary condition for the selected nested-domain is implemented using the BDY module of NEMO.
Two numerical algorithms are used to treat open boundary conditions depending on the prognostic simulated variables.
The Flather scheme (<a href="#bib_oddo2008">Oddo and Pinardi, 2008</a>) is used for barotropic velocities,
while the flow relaxation scheme (<a href="#bib_engerdahl1995">Engerdahl, 1995</a>) is considered for baroclinic velocities, active tracers and sea surface height.
In our formulation, we provide external data along straight open boundary lines, and the relaxation area is equal
to one internal grid point. As the parent coarse resolution ocean model provides only the total velocity field,
the interpolated total velocity field in the child grid is split into barotropic and baroclinic components.
An integral constraint method is imposed to preserve the total transport after the interpolation.</p>
<p>This process involves the following steps: (1) defining the open boundary geometry
(for each of the T, U and V grids) and physical fields (active tracers, sea-surface height, barotropic and
baroclinic velocities) at the open boundary points using the geometry_bdy and fields_bdy procedures,
respectively; (2) writing these data arrays to the files that are necessary to run the NEMO code.
The algorithms used for the different fields are the Flather radiation scheme for the barotropic velocities
and the sea surface height and the Flow relaxation scheme for the baroclinic velocities and active tracers.
The generated files are stored in the directory <code>$PATH_EXP/IDEXP/data/</code>.</p>

</div>

### **Integral Constraint at the open boundary**

<div style="text-align: justify">

<p>The downscaling is designed to ensure that the volume transport across the open boundary (OB) of the child
model matches that across the corresponding section of the parent model. At the eastern/western boundaries
U-Points are imposed using the following conditions
<span class="math">
$$

\begin{equation}
\begin{array}{ll}
\int*{y_2}^{y_1} \int*{-H*{child}}^{\eta*{child}} U*{child} dz dy = \int*{y*2}^{y_1} \int*{-H*{parent}}^{\eta*{parent}} U\_{parent} dz dy
\end{array}
\end{equation}

$$
</span>
where <span class="math">\(y_1, y_2\)</span> are the extremes of the open boundary section;
<span class="math">\(\eta_{child}, H_{child}\)</span> are the surface elevation and the bathymetry of the child model at the boundary, respectively;
<span class="math">\(\eta_{parent}, H_{parent}\)</span> are the surface elevation and the bathymetry of the parent model at the boundary, respectively; and
<span class="math">\(U_{parent},U_{child}\)</span> are the parent/child total zonal velocities (normal velocity to the W/E boundaries).
The corrected velocity component normal to the boundary <span class="math">\(V_{child}\)</span> is given
(see <a href="#bib_pin2003">N. Pinardi et al., 2003</a>) by:
<span class="math">
$$

\begin{equation}
\begin{array}{ll}
U*{child} (x,y,z,t) = U*{interp} - U\_{correction}
\end{array}
\end{equation}

$$
</span>
where <span class="math">\(U_{interp}\)</span> is the <span class="math">\(U_{parent}\)</span>
interpolated on the child open boundary points and the velocity correction is given by
<span class="math">
$$

\begin{equation}
\begin{array}{ll}
U*{correction} = \frac{M*{interp} - M\_{parent}}{S}
\end{array}
\end{equation}

$$
</span>
where <span class="math">\( M_{interp} = \int_{y_2}^{y_1} \int_{-H_{child}}^{\eta_{child}} U_{interp} dz dy \)</span> is the volume transport across the OB,
the <span class="math">\( M_{parent} = \int_{y_2}^{y_1} \int_{-H_{parent}}^{\eta_{parent}} U_{parent} dz dy \)</span> is the volume transport across the corresponding OB
and <span class="math">\( S = \int_{y_2}^{y_1} \int_{-H_{child}}^{\eta_{child}} dz dy \)</span> is the area of the section.
These conditions are similarly imposed for the meridional velocity at the northern/southern boundaries (V-Points).
The Integral Constraint procedure ensures that the interpolation does not modify the net transport across the child model lateral open boundary.

</div>

## **Model run**

<div style="text-align: justify">

<p>Finally, the NEMO code is numerically integrated by the SURF platform. The output files are continuously updated,
given a fixed output frequency, throughout the execution of the program.
The logfile is a text file NEMO produces that contains data on how far the run has advanced by providing the time step.
After the model run is completed, the output files are stored in the experiment directory
<code>$PATH_IDEXP/data/data00/outdata/</code> (see <a href="#appB_Scratch-Partition-and-its-directory-structures">appendix B</a>).</p>

</div>

## **Post-processing**

<div style="text-align: justify">

<p>In this step the visualization and analysis procedures of the forecast are considered.
These can be activated after the execution of each macro-task. The user can visualize the input,
regridded and output datasets, compare parent/child fields and convert the model output datasets.</p>

</div>
$$
