# **Input/Output Model Datasets**

<div style="text-align: justify">

In order to execute the SURF-NEMO package, the user has to provide several input datasets. These include the bathymetry datasets containing the seafloor elevation, the coastline datasets delineating borders between land and sea areas, the initial condition dataset containing the initial values of model-predicted variables and the boundary condition datasets containing the values of the variables needed to impose the boundary conditions on flows of mass, momentum and energy for the primitive equation at the surface and lateral open boundaries of the domain.
In <a href="#fig-interface-schematic">Figure 5.1</a> are summarized the interfaces and the external forcings acting on a typical computational domain.

<div class="d-flex justify-content-center">
   <figure id="fig-interface-schematic" class="figure text-center">
      <a href="../assets/img/CondContorno.png">
         <img src="../assets/img/CondContorno.png" alt="../assets/img/CondContorno.png" width="100%">
      </a>
      <figcaption class="figurenum">Schematized representation of the interface and external forcing acting on a typical computational domain.</figcaption>
   </figure>
</div>

</div>

## **Input Datasets**

<div style="text-align: justify">

The input model datasets are provided in the classic <a href="https://www.unidata.ucar.edu/software/netcdf/docs/netcdf_introduction.html" target="_blank">NetCDF</a>
format for bathymetry, initial and lateral boundary condition.
NetCDF is a widely used file format in atmospheric and oceanic research which allows storage of different types of array based data, along with a short data description.
The coastline datasets are instead provided in <a href="https://www.esri.com/library/whitepapers/pdfs/shapefile.pdf" target="_blank">Shapefile</a> format, a digital vector data format for geographic information system (GIS) software.

SURF allows also to use, if needed, two different model type of input data during the execution (i.e. analysis data for the spinup time and forecast data after).
The user has to set-up few parameters in the configuration file <code> setParFree.json </code> in order to specify the values of path/filename, dimensions/variables
name and characteristics of data.

</div>

### **Bathymetry Dataset**

<div style="text-align: justify">

The bathymetry dataset contains the sea floor elevation. This dataset is required to generate the child meshmask file. The user needs to set-up the required parameters in the sections <code>set_dataDownlBat</code> of the configuration file.
The data are distributed on a curvilinear spherical grid (regular or not) within a region containing the nested domain.

<div class="row mx-0">
   <div class="col-6 ps-0">
         The bathymetry file contains the elevation variable (in meters) at a certain horizontal resolution.
         The elevation is relative to a specific reference level and can
         increases (positive) or decreases (negative) with increasing water depth.
         The coordinate variables (latitude/longitude) can be a one- or two-dimensional array.
         An example of CDL text representation of this file is shown in <a href="#cdl-bathymetry">Listing 5.1</a>.
   </div>
   <div class="col-6 pr-0" style="font-size:16px">
      <div id="cdl-bathymetry" class="highlight-NETCF">
<pre><code class="mycode">netcdf bathymetry_filename {
dimensions:
   x = 300;
   y = 200;
variables: \\
   float lon(y,x);
      lon: units = &quot;degrees_east&quot;;
   float lat(y,x);
      lat: units = &quot;degrees_north&quot;;
   float elevation(y,x);
      elevation: units = &quot;m&quot;;
}
</code></pre>
<p class="caption">Listing 5.1: Example of a netCDF file for bathymetry.</p>
      </div>
   </div>
</div>

<!-- <p><div class="clearer"></div></p> -->

The user needs to specify the following logical parameters in section <code><span class="pre">set_dataDownlBat_fileName</span></code> of the user-configuration file:

<ul class="simple">
   <li>
      <code class="docutils literal notranslate"><span class="pre">fileBat_lcompression</span></code> if the file to download is compressed (.gzip) or not,</li>
   <li>
      <code class="docutils literal notranslate"><span class="pre">fileBat_llonFlip</span></code> if the longitude coordinate is defined in the rage [0:360] or [-180:+180],
   </li>
   <li>
      <code class="docutils literal notranslate"><span class="pre">fileBat_llatInv</span></code> if the dataset contains latitude decreasing through the pole,
   </li>
   <li>
      <code class="docutils literal notranslate"><span class="pre">fileBat_ldepthIncr</span></code> if the dataset contains seafloor elevation (positive) increases with increasing water depth,
   </li>
   <li>
      <code class="docutils literal notranslate"><span class="pre">fileBat_lkeepSrcFull</span></code> if the original downloaded file needs to be deleted after cutted in the nested domain.
   </li>
</ul>

The available input bathymetry datasets inside the surf package is the General Bathymetric Chart of the Oceans (<a href="https://www.gebco.net/" target="_blank">GEBCO</a>), a publicly available bathymetry data sets with global coverage at 30 arc-second resolution.

</div>

### **Coastline Dataset**

<div style="text-align: justify">

The coastline dataset contains borders between land and sea areas and is stored into shapefiles.
The coastline is required in the child meshmask generation phase.
The user needs to set-up the required parameters in the sections <code class="docutils literal notranslate"><span class="pre">set_dataDownlCoast</span></code> of the configuration file.

The available input coastline datasets inside the surf packages is the Global Self-consistent Hierarchical High-resolution Geography (<a href="https://www.ngdc.noaa.gov/mgg/shorelines/gshhs.html" target="_blank">GSHHG</a>) dataset produced by the National Oceanic and Atmospheric Association (NOAA). The datasets include 20 shapefiles which provides a consistent set of hierarchically arranged closed polygons from which the shorelines are constructed.
The GSHHS data are split into separate shapefiles at five different resolutions:

<ul class="simple">
   <li>the highest resolution is designated '<b>f</b>' (full) with a resolution of xx m,</li>
   <li>the next highest appears as '<b>h</b>' (high) with a resolution of xx m,</li>
   <li>the (intermediate) '<b>i</b>' with a resolution of xx m,</li>
   <li>the (low) '<b>l</b>' with a resolution of xx m,</li>
   <li>the (coarse) '<b>c</b>' with a resolution of xx m.</li>
</ul>
For each level of resolution Shorelines are organized into four levels:
boundary between land and ocean (<b>L1</b>), boundary between lake and land (<b>L2</b>),
boundary between island-in-lake and lake (<b>L3</b>), and boundary between pond-in-island and island (<b>L4</b>).
These datasets use the geographic coordinate system WGS84 (simple latitudes and longitudes; decimal degrees.

</div>

### **Initial Condition Datasets**

<div style="text-align: justify">

In order to start a model run, the initial values for the model prognostic variables need to be specified.
These include temperature, salinity, sea surface height, zonal and meridional velocity components fields.
Initial condition datasets are normally provided by coarse grid model outputs.
The user needs to set-up the required parameters in the sections <code class="docutils literal notranslate"><span class="pre">set_dataDownlOceIC</span></code> of the configuration file.
The data can be distributed on a curvilinear spherical grid (regular or not) with unstaggered or staggered Arakawa-C grid arrangement within a region containing the nested domain.
The model assumes that all the input ocean variables are defined on the same grid.

<div class="row mx-0">
   <div class="col-6 ps-0">
      <p>The coarse-resolution ocean files contain the following variables at a certain horizontal resolution.</p>
      <ul class="simple">
      <li><p>Potential Temperature [<span class="math">\(C\)</span>],</p></li>
      <li><p>Salinity [<span class="math">\(PSU\)</span>],</p></li>
      <li><p>Sea surface height [<span class="math">\(m\)</span>],</p></li>
      <li><p>Zonal velocity [<span class="math">\(ms^{-1}\)</span>],</p></li>
      <li><p>Meridional Velocity [<span class="math">\(ms^{-1}\)</span>].</p></li>
      </ul>
      <p>An example of CDL text representation of this file is shown in <a href="#cdl-oceic">Listing 5.2</a>.</p>
   </div>
   <div class="col-6 pr-0" style="font-size:16px">
      <div id="cdl-oceic" class="highlight-NETCF">
<pre><code class="mycode">netcdf fields_filename {
dimensions:
   x = 40 ;
   y = 35 ;
   z = 72 ;
   time = UNLIMITED ; // (1 currently)
variables:
   float lont(y, x) ;
      lont:units = "degrees_east" ;
   float latt(y, x) ;
      latt:units = "degrees_north" ;
   float deptht(z) ;
      deptht:units = "m" ;
   double time(time) ;
      time_counter:units = "seconds since
                   1970-01-01 00:00:00" ;
   float temperature(time, z, y, x) ;
      temperature:units = "degC" ;
}
dimensions :
x = 677;
y = 253;
z = 72;
t = UNLIMITED; // (7 currently)
variables : \\
float lont(x);
      lont: units = &quot;degrees_east&quot;;
float latt(y);
      latt: units = &quot;degrees_north&quot;;
float deptht(z);
      deptht: units = &quot;m&quot;;
double time(t);
       time: units = &quot;seconds since
                1970-01-01 00:00:00&quot;;
float temperature(t,z,y,x);
      temperature: units = &quot;degC&quot;;
}
</code></pre>
<p class="caption">Listing 5.2: Example of a netCDF file for the Initial Condition temperature</p>
      </div>
   </div>
</div>

<!-- <p><div class="clearer"></div></p> -->

In order to perform the extrapolation (SOL) of ocean fields
(see <a href="#ch2_Work-Flow-of-SURF-NEMO-platform_sec3_Input-data-regridding">section 2.3</a>),
the parent land-sea mask file needs to be provided as input datasets.
The user needs to set-up the required parameters in the sections <code class="docutils literal notranslate"><span class="pre">set_dataDownlOceICMesh</span></code> of the configuration file.

<div class="row mx-0">
   <div class="col-6 ps-0">
      <p>This file contains all the information of the coarse-resolution ocean model grids and it includes the following variables:</p>
      <ul class="simple">
         <li><p>longitude on TUVF grid points [<span class="math">\(degree\)</span>],</p></li>
         <li><p>latitude on TUVF grid points [<span class="math">\(degree\)</span>],</p></li>
         <li><p>depth on TUVF grid points [<span class="math">\(m\)</span>],</p></li>
         <li><p>land-sea mask on TUVF grid points [0-1],</p></li>
         <li><p>scalefactor on TUVF grid points [<span class="math">\(m\)</span>],</p></li>
         <li><p>scalefactor on TUVF grid points [<span class="math">\(m\)</span>],</p></li>
         <li><p>scalefactor on TUVF grid points [<span class="math">\(m\)</span>].</p></li>
      </ul>
      <p>An example of CDL text representation of this file is shown in <a href="#cdl-oceicmask">Listing 5.3</a>.</p>
   </div>
   <div class="col-6 pr-0" style="font-size:16px">
      <div id="cdl-oceicmask" class="highlight-NETCF">
<pre><code class="mycode">netcdf meshmask_filename {
dimensions :
   x = 677;
   y = 253;
   z = 72;
   t = UNLIMITED; // (7 currently)
variables : \\
   float lon(y,x);
   float lat(y,x);
   float lev(z);
   double time(t);
   byte tmask(t,z,y,x);
   byte umask(t,z,y,x);
   byte vmask(t,z,y,x);
   byte fmask(t,z,y,x);
   float glamt(t,y,x);
   float glamu(t,y,x);
   float glamv(t,y,x);
   float glamf(t,y,x);
   float gphit(t,y,x);
   float gphiu(t,y,x);
   float gphiv(t,y,x);
   float gphif(t,y,x);
   double e1t(t,y,x);
   double e1u(t,y,x);
   double e1v(t,y,x);
   double e1f(t,y,x);
   double e2t(t,y,x);
   double e2u(t,y,x);
   double e2v(t,y,x);
   double e2f(t,y,x);
   double e3t(t,z,y,x);
   double e3u(t,z,y,x);
   double e3v(t,z,y,x);
   double e3w(t,z,y,x);
}
</code></pre>
<p class="caption">Listing 5.3: Example of a netCDF file for the Initial Condition meshmask.</p>
      </div>
   </div>
</div>

</div>

### **Lateral Open Boundary Condition Datasets**

<div style="text-align: justify">

In order to integrate the primitive equations, the NEMO ocean model needs to impose appropriate
boundary conditions at the ocean-ocean interface (i.e. the sides of the domain not bounded by land).
Lateral Open Boundary values for the model prognostic variables need to be specified for all the simulation period.
These include temperature, salinity, sea surface height, and velocity fields.
The user needs to set-up the required parameters in the sections <code>set_dataDownlOceBC_preSpinup</code> and <code>set_dataDownlOceBC_postSpinup</code> of the configuration file.
The data can be distributed on a curvilinear spherical grid (regular or not) with unstaggered or staggered Arakawa-C grid arrangement within a region containing the nested domain.
The model assumes that all the input ocean variables in pre- and post- spinup period are defined on the same grid.

<div class="row mx-0">
   <div class="col-6 ps-0">
      <p>The coarse-resolution ocean files contain the following variables at a certain
      horizontal resolution and temporal frequency.</p>
      <ul class="simple">
      <li><p>Potential Temperature [<span class="math">\(C\)</span>],</p></li>
      <li><p>Salinity [<span class="math">\(PSU\)</span>],</p></li>
      <li><p>Sea surface height [<span class="math">\(m\)</span>],</p></li>
      <li><p>Zonal velocity [<span class="math">\(ms^{-1}\)</span>],</p></li>
      <li><p>Meridional Velocity [<span class="math">\(ms^{-1}\)</span>].</p></li>
      </ul>
      <p>An example of CDL text representation of this file is shown in <a href="#cdl-ocebc">Listing 5.4</a>.</p>
   </div>
   <div class="col-6 pr-0" style="font-size:16px">
      <div id="cdl-ocebc" class="highlight-NETCF">

<pre><code class="mycode">netcdf fields_filename {
dimensions :
   x = 677;
   y = 253;
   z = 72;
   t = UNLIMITED; // (7 currently)
variables : \\
   float lont(x);
         lont: units = &quot;degrees_east&quot;;
   float latt(y);
         latt: units = &quot;degrees_north&quot;;
   float deptht(z);
         deptht: units = &quot;m&quot;;
   double time(t);
          time: units = &quot;seconds since
                   1970-01-01 00:00:00&quot;;
   float temperature(t,z,y,x);
         temperature: units = &quot;degC&quot;;
}
</code></pre>
<p class="caption"> Listing 5.4: Example of a netCDF file for Open boundary Condition temperature. </p>
      </div>
   </div>
</div>

<!-- <p><div class="clearer"></div></p> -->

<p>In order to perform the extrapolation (SOL) of ocean fields
(see  <a href="#ch2_Work-Flow-of-SURF-NEMO-platform_sec3_Input-data-regridding">section 2.3</a>),
the parent land-sea mask file needs to be provided as input datasets.
The user needs to set-up the required parameters in the sections <code class="docutils literal notranslate"><span class="pre">set_dataDownlOceBCMesh</span></code> of the configuration file.</p>
<div class="row mx-0">
   <div class="col-6 ps-0">
      <p>This file contains all the information of the coarse-resolution ocean model grids
      and it includes the following variables:</p>
      <ul class="simple">
      <li><p>longitude on TUVF grid points [<span class="math">\(degree\)</span>],</p></li>
      <li><p>latitude on TUVF grid points [<span class="math">\(degree\)</span>],</p></li>
      <li><p>depth on TUVF grid points [<span class="math">\(m\)</span>],</p></li>
      <li><p>land-sea mask on TUVF grid points [0-1],</p></li>
      <li><p>scalefactor on TUVF grid points [<span class="math">\(m\)</span>],</p></li>
      <li><p>scalefactor on TUVF grid points [<span class="math">\(m\)</span>],</p></li>
      <li><p>scalefactor on TUVF grid points [<span class="math">\(m\)</span>].</p></li>
      </ul>
      <p>An example of CDL text representation of this file is shown in <a href="#cdl-ocebcmask">Listing 5.5</a>.</p>
   </div>
   <div class="col-6 pr-0" style="font-size:16px">
      <div id="cdl-ocebcmask" class="highlight-NETCF">
<pre><code class="mycode">netcdf meshmask_filename {
dimensions :
   x = 677;
   y = 253;
   z = 72;
   t = UNLIMITED; // (7 currently)
variables : \\
   float lon(y,x);
   float lat(y,x);
   float lev(z);
   double time(t);
   byte tmask(t,z,y,x);
   byte umask(t,z,y,x);
   byte vmask(t,z,y,x);
   byte fmask(t,z,y,x);
   float glamt(t,y,x);
   float glamu(t,y,x);
   float glamv(t,y,x);
   float glamf(t,y,x);
   float gphit(t,y,x);
   float gphiu(t,y,x);
   float gphiv(t,y,x);
   float gphif(t,y,x);
   double e1t(t,y,x);
   double e1u(t,y,x);
   double e1v(t,y,x);
   double e1f(t,y,x);
   double e2t(t,y,x);
   double e2u(t,y,x);
   double e2v(t,y,x);
   double e2f(t,y,x);
   double e3t(t,z,y,x);
   double e3u(t,z,y,x);
   double e3v(t,z,y,x);
   double e3w(t,z,y,x);
}
</code></pre>
<p class="caption"> Listing 5.5: Example of a netCDF file for the Initial Condition meshmask. </p>
      </div>
   </div>
</div>

</div>

### **Tidal Datasets for the open boundaries**

<div style="text-align: justify">

For the barotropic solution, there is also the option to use tidal harmonic forcing at open boundaries in addition to other external data.
These include the constituents for amplitude and phase of surface height and velocity.
The user needs to set-up the required parameters in the sections <code>set_dataDownlTide</code> of the configuration file.
The data are distributed on a regular curvilinear spherical grid with unstaggered or staggered Arakawa-C grid arrangement within a region containing the nested domain.
The model assumes that all the input tidal harmonic variables are defined on the same grid.

<div class="row mx-0">
   <div class="col-6 ps-0">
      <p>The barotropic tide files contain for each harmonic constituents the following variables at a certain
      horizontal resolution.</p>
      <ul class="simple">
      <li><p>Tidal elevation complex amplitude, Real and Imaginary part [<span class="math">\(mm\)</span>],</p></li>
      <li><p>Tidal WE transport complex amplitude, Real and Imaginary part [<span class="math">\(cm^2/s\)</span>],</p></li>
      <li><p>Tidal SN transport complex amplitude, Real and Imaginary part [<span class="math">\(cm^2/s\)</span>],</p></li>
      </ul>
      <p>An example of CDL text representation of this file is shown in <a href="#cdl-ocebc">Listing 5.6</a>.</p>
   </div>
   <div class="col-6 pr-0" style="font-size:16px">
      <div id="cdl-ocebc" class="highlight-NETCF">
<pre><code class="mycode">netcdf uv.k1_tpxo8_atlas_30c_v1 {
dimensions:
   nx = 10800 ;
   ny = 5401 ;
variables:
   double lon_u(nx) ;
      lon_u:units = "degree_east" ;
   double lat_u(ny) ;
      lat_u:units = "degree_north" ;
   double lon_v(nx) ;
      lon_v:units = "degree_east" ;
   double lat_v(ny) ;
      lat_v:units = "degree_north" ;
   int uRe(nx, ny) ;
      uRe:units = "centimeter^2/sec" ;
   int uIm(nx, ny) ;
      uIm:units = "centimeter^2/sec" ;
   int vRe(nx, ny) ;
      vRe:units = "centimeter^2/sec" ;
   int vIm(nx, ny) ;
      vIm:units = "centimeter^2/sec" ;
}
</code></pre>
<p class="caption"> Listing 5.6: Example of a netCDF file for the Zonal and meridional Tidal transport for the constituent K1. </p>
      </div>
   </div>
</div>

<!-- <p><div class="clearer"></div></p> -->

<p>The tidal model bathymetry file needs to be provided as input datasets.
The user needs to set-up the required parameters in the sections
<code class="docutils literal notranslate"><span class="pre">set_dataDownlTideMesh</span></code> of the configuration file.</p>
<div class="row mx-0">
   <div class="col-6 ps-0">
      <p>This file contains all the information of the tidal model grids and depth grid
      and it includes the following variables:</p>
      <ul class="simple">
      <li><p>longitude on TUV grid points [<span class="math">\(degree\)</span>],</p></li>
      <li><p>latitude on TUV grid points [<span class="math">\(degree\)</span>],</p></li>
      <li><p>Bathymetry at TUV grid points [<span class="math">\(m\)</span>].</p></li>
      </ul>
      <p>An example of CDL text representation of this file is shown in <a href="#cdl-ocebcmask">Listing 5.7</a>.</p>
   </div>
   <div class="col-6 pr-0" style="font-size:16px">
      <div id="cdl-ocebcmask" class="highlight-NETCF">
<pre><code class="mycode">netcdf grid_tpxo8atlas_30_v1 {
dimensions:
   nx = 10800 ;
   ny = 5401 ;
variables:
   double lon_z(nx) ;
      lon_z:units = "degree_east" ;
   double lat_z(ny) ;
      lat_z:units = "degree_north" ;
   double lon_u(nx) ;
      lon_u:units = "degree_east" ;
   double lat_u(ny) ;
      lat_u:units = "degree_north" ;
   double lon_v(nx) ;
      lon_v:units = "degree_east" ;
   double lat_v(ny) ;
      lat_v:units = "degree_north" ;
   float hz(nx, ny) ;
      hz:units = "meter" ;
   float hu(nx, ny) ;
      hu:units = "meter" ;
   float hv(nx, ny) ;
      hv:units = "meter" ;
}
</code></pre>
<p class="caption"> Listing 5.7: Example of a netCDF file for the Initial Condition meshmask. </p>
      </div>
   </div>
</div>

<!-- <p><div class="clearer"></div></p> -->

The available input barotropic tide datasets inside the surf packages are derived from the Topex Poseidon cross-over (<a href="https://www.tpxo.net/global/tpxo8-atlas" target="_blank">TPX08-ATLAS</a>) global inverse tide model obtained with
the software package OTIS (OSU Tidal Inversion Software) implementing methods described in Egbert and Erofeeva, 2002.
The TPX08 tidal model consists of a multi-resolution bathymetric grid solution,
with a 1/6 solution in the global open ocean, and a 1/30 local resolution solution to improve modelling in complex shallow-water environments.
It includes complex amplitudes of the tide sea-surface elevations and transports for eight primaries (M2, S2, N2, K2, K1, O1, P1, Q1),
two long-period (Mf, Mm) and 3 non-linear (M4, MS4, MN4) harmonic constituents.

</div>

### **Atmospheric Forcing Datasets**

<div style="text-align: justify">

In order to integrate the primitive equations, the NEMO ocean model needs to impose appropriate boundary
conditions on flows of mass, momentum and energy at the atmosphere-ocean interface. It must be provided
on the integration domain the following six fields:

<ol>
   <li><p>the zonal components of the surface ocean stress,</p></li>
   <li><p>the meridional components of the surface ocean stress,</p></li>
   <li><p>the heat fluxes from solar Qsr,</p></li>
   <li><p>the heat fluxes from non-solar Qns radiation,</p></li>
   <li><p>the water flows exchanged with the atmosphere (E-P) (the evaporation minus precipitation budget).</p></li>
</ol>
<p>In addition an optional field:</p>
<ol start="7">
   <li><p>the atmospheric pressure at the ocean surface (pa).</p></li>
</ol>
<p>The NEMO ocean model provides different ways to provide the first six fields to the ocean which are controlled
by namelist variables (see NEMO Manual).
The choice of the atmospheric forcing formulation in SURF platform is obtained by setting the parameter
<code>sbc_iformulat</code> in the user configuration file:</p>
<ul>
   <li><p><code>sbc_iformulat=0</code> for the MFS bulk formulae,</p></li>
   <li><p><code>sbc_iformulat=1</code> for the the Flux formulation,</p></li>
   <li><p><code>sbc_iformulat=2</code> for the CORE bulk formula.</p></li>
</ul>
<p>The data are distributed on a regular unstaggered grid within a region containing the nested domain.
The model assumes that input atmospheric variables in pre- and post- spinup period are defined on the same
mesh but allowed different mesh for different variables.
The user needs to set-up the required parameters in the sections <code>set_dataDownlAtm_preSpinup</code> and <code>set_dataDownlAtm_postSpinup</code> of the configuration file.</p>

<div class="subsubsection" id="atmospheric-forcing-dataset-for-the-mfs-bulk-formulae">
   <p>(1) The choice of <b>MFS bulk formulae</b> is obtained by setting the parameter <code>sbc_iformulat=0</code> in the user configuration file.</p>
   <div class="row mx-0">
      <div class="col-6 ps-0">
         <p>The atmospheric forcing files contain the following variables at a certain horizontal resolution and
         temporal frequency:</p>
         <ul class="simple">
            <li><p class="my-2">10 m zonal wind component [<span class="math">\(ms^{-1}\)</span>],</p></li>
            <li><p class="my-2">10 m meridional wind component [<span class="math">\(ms^{-1}\)</span>],</p></li>
            <li><p class="my-2">2m Air Temperature [<span class="math">\(K\)</span>],</p></li>
            <li><p class="my-2">2m Dew Point Temperature [<span class="math">\(K\)</span>],</p></li>
            <li><p class="my-2">Mean Sea Level Pressure [<span class="math">\(Pa\)</span>],</p></li>
            <li><p class="my-2">Total Cloud Cover [%].</p></li>
            <li><p class="my-2">Total Precipitation [<span class="math">\( m \)</span>].</p></li>
         </ul>
         <p>An example of CDL text representation for the atmospheric forcing file
         with temporal frequency of 3 hours is shown in box in <a href="#cdl-atm-mfs">Listing 5.8</a>.</p>
      </div>
      <div class="col-6 pr-0" style="font-size:16px">
         <div id="cdl-atm-mfs" class="highlight-NETCF">
<pre><code class="mycode">netcdf atmFields_filename {
dimensions :
   lon = 245;
   lat = 73;
   time = UNLIMITED; // (8 currently)
variables : \\
   float lon(lon);
         lon: units = &quot;degrees_east&quot;;
   float lat(lat);
         lat: units = &quot;degrees_north&quot;;
   float time(time);
         time: units = &quot;seconds since
                  1970-01-01 00:00:00&quot;;
   float T2M(time,lat,lon);
         T2M: units = &quot;K&quot;;
}
</code></pre>
<p class="caption"> Listing 5.8: Example of a netCDF file for the Atmospheric Forcing temperature. </p>
         </div>
      </div>
   </div>
</div>

<div class="subsubsection" id="atmospheric-forcing-dataset-for-the-core-bulk-formulae">
   <p>(2) The choice of <b>Core bulk formulae</b> is obtained by setting the parameter <code>sbc_iformulat=2</code> in the user configuration file.</p>
   <div class="row mx-0">
      <div class="col-6 ps-0">
         <p>The atmospheric forcing files contain the following variables at a certain horizontal resolution
         and temporal frequency:</p>
         <ul class="simple">
            <li><p class="my-2">10 m zonal wind component [<span class="math">\(ms^{-1}\)</span>],</p></li>
            <li><p class="my-2">10 m meridional wind component [<span class="math">\(ms^{-1}\)</span>],</p></li>
            <li><p class="my-2">2m Temperature [<span class="math">\(K\)</span>],</p></li>
            <li><p class="my-2">2m Specific humidity [<span class="math">\(\%\)</span>],</p></li>
            <li><p class="my-2">Incoming long-wave radiation [<span class="math">\(W m^{-2}\)</span>],</p></li>
            <li><p class="my-2">Incoming short-wave radiation [<span class="math">\(W m^{-2}\)</span>],</p></li>
            <li><p class="my-2">Total precipitation (liquid+solid) [<span class="math">\(Kg m^{-2} s^{-1}\)</span>],</p></li>
            <li><p class="my-2">Solid precipitation [<span class="math">\(Kg m^{-2} s^{-1}\)</span>].</p></li>
         </ul>
         <p>An example of CDL text representation for the atmospheric forcing file
         with temporal frequency of 3 hours is shown in box in <a href="#cdl-atm-core">Listing 5.9</a>.</p>
      </div>
      <div class="col-6 pr-0" style="font-size:16px">
         <div id="cdl-atm-core" class="highlight-NETCF">
<pre><code class="mycode">netcdf atmFields_filename {
dimensions :
   lon = 245;
   lat = 73;
   time = UNLIMITED; // (8 currently)
variables : \\
   float lon(lon);
         lon: units = &quot;degrees_east&quot;;
   float lat(lat);
         lat: units = &quot;degrees_north&quot;;
   float time(time);
         time: units = &quot;seconds since
                  1970-01-01 00:00:00&quot;;
   float T2M(time,lat,lon);
         T2M: units = &quot;K&quot;;
}
</code></pre>
<p class="caption"> Listing 5.9: Example of a netCDF file for the Atmospheric Forcing temperature. </p>
         </div>
      </div>
   </div>
</div>

<div class="subsubsection" id="atmospheric-forcing-dataset-for-the-flux-formulation">
   <p>(3) The choice of <b>Flux formulation</b> is obtained by setting the parameter <code>sbc_iformulat=1</code> in the user configuration file.</p>
   <div class="row mx-0">
      <div class="col-6 ps-0">
         <p>The atmospheric forcing files contain the following
         variables at a certain horizontal resolution and
         temporal frequency:</p>
         <ul class="simple">
            <li><p class="my-2">Zonal wind stress [0 - 1],</p></li>
            <li><p class="my-2">Meridional Wind stress [0 - 1],</p></li>
            <li><p class="my-2">Total heat flux [0 - 1],</p></li>
            <li><p class="my-2">Solar Radiation Penetration [0 - 1],</p></li>
            <li><p class="my-2">Mass flux exchanged [0 - 1],</p></li>
            <li><p class="my-2">Surface Temperature [0 - 1],</p></li>
            <li><p class="my-2">Surface Salinity [0 - 1].</p></li>
         </ul>
         <p>An example of CDL text representation for the atmospheric forcing file
         with temporal frequency of 3 hours is shown in box in <a href="#cdl-atm-flux">Listing 5.10</a>.</p>
      </div>
      <div class="col-6 pr-0" style="font-size:16px">
         <div id="cdl-atm-flux" class="highlight-NETCF">
<pre><code class="mycode">netcdf atmFields_filename {
dimensions :
   lon = 245;
   lat = 73;
   time = UNLIMITED; // (8 currently)
variables : \\
   float lon(lon);
         lon: units = &quot;degrees_east&quot;;
   float lat(lat);
         lat: units = &quot;degrees_north&quot;;
   float time(time);
         time: units = &quot;seconds since
                  1970-01-01 00:00:00&quot;;
   float T2M(time,lat,lon);
         T2M: units = &quot;K&quot;;
}
</code></pre>
<p class="caption"> Listing 5.10: Example of a netCDF file for the Atmospheric Forcing temperature. </p>
         </div>
      </div>
   </div>
</div>

<p>In order to perform the extrapolation (SOL) of atmospheric fields
(see  <a href="#ch2_Work-Flow-of-SURF-NEMO-platform_sec3_Input-data-regridding">section 2.3</a>),
the atmospheric meshmask file needs to be provided as input datasets.
The user needs to set-up the required parameters in the sections <code>set_dataDownlAtmMesh</code> of the configuration file.</p>
<div class="row mx-0">
   <div class="col-6 ps-0">
      <p>The atmospheric meshmask file contains the land-sea mask [0-1] variable.</p>
      <p>An example of CDL text representation of the atmospheric land-sea mask is shown in <a href="#cdl-atm-flux-mask">Listing 5.11</span></a>.
      The time dimension and coordinate variable can also be omitted.</p>
   </div>
   <div class="col-6 pr-0" style="font-size:16px">
      <div id="cdl-atm-flux-mask" class="highlight-NETCF">

<!-- <figure id="cdl-atm-flux-mask"> -->
<pre><code class="mycode">netcdf meshmask_filename {
dimensions :
   lon = 245;
   lat = 73;
   time = UNLIMITED; // (1 currently)
variables : \\
   float lon(lon);
         lon: units = &quot;degrees_east&quot;;
   float lat(lat);
         lat: units = &quot;degrees_north&quot;;
   float time(time);
         time: units = &quot;seconds since
                  1970-01-01 00:00:00&quot;;
   float LSM(time,lat,lon);
         LSM: units = &quot;0-1&quot;;
}
</code></pre>
<p class="caption"> Listing 5.11: Example of a netCDF file for the Atmospheric Forcing meshmask. </p>
      </div>
   </div>
</div>

</div>

## **Output Datasets**

The output model datasets are provided in the NetCDF format ..
the meshmask file, the output files for T, U ,V, W grids and the restart file.

### **Meshmask dataset**

<div class="row mx-0">
   <div class="col-6 ps-0">
      This file contains all the information of the child ocean model grids
      and it includes the following variables:
      <ul class="simple">
      <li>longitude on TUVF grid points [<span class="math">\(degree\)</span>],</li>
      <li>latitude on TUVF grid points [<span class="math">\(degree\)</span>],</li>
      <li>depth on TUVF grid points [<span class="math">\(m\)</span>],</li>
      <li>land-sea mask on TUVF grid points [0-1],</li>
      <li>scalefactor on TUVF grid points [<span class="math">\(m\)</span>],</li>
      <li>scalefactor on TUVF grid points [<span class="math">\(m\)</span>],</li>
      <li>scalefactor on TUVF grid points [<span class="math">\(m\)</span>].</li>
      </ul>
      An example of CDL text representation of this file is shown in <a href="#cdl-oceoutmask">Listing 5.21</a>.
   </div>
   <div class="col-6 pr-0" style="font-size:16px">
      <div id="cdl-oceoutmask" class="highlight-NETCF">
<pre><code class="mycode">netcdf meshmask_filename {
dimensions :
   x = 677;
   y = 253;
   z = 72;
   t = UNLIMITED; // (7 currently)
variables : \\
   float lon(y,x);
   float lat(y,x);
   float lev(z);
   double time(t);
   byte tmask(t,z,y,x);
   byte umask(t,z,y,x);
   byte vmask(t,z,y,x);
   byte fmask(t,z,y,x);
   float glamt(t,y,x);
   float glamu(t,y,x);
   float glamv(t,y,x);
   float glamf(t,y,x);
   float gphit(t,y,x);
   float gphiu(t,y,x);
   float gphiv(t,y,x);
   float gphif(t,y,x);
   double e1t(t,y,x);
   double e1u(t,y,x);
   double e1v(t,y,x);
   double e1f(t,y,x);
   double e2t(t,y,x);
   double e2u(t,y,x);
   double e2v(t,y,x);
   double e2f(t,y,x);
   double e3t(t,z,y,x);
   double e3u(t,z,y,x);
   double e3v(t,z,y,x);
   double e3w(t,z,y,x);
}
</code></pre>
<p class="caption">Listing 5.21: CDL example for the meshmask datasets.</p>
      </div>
   </div>
</div>

### **Ocean Output Datasets**

<p>…contains:</p>

(1) This output file SURF_1h_YYYYMMDD0_YYYYMMDD1_grid_T contains hourly fields defined on the Arakawa-T grid within the chid nested domain.

<div class="row mx-0">
   <div class="col-6 ps-0">
      <p> This file contains the following variables:</p>
      <ul class="simple">
         <li>Temperature [<span class="math">\(C\)</span>],</li>
         <li>Salinity [<span class="math">\(PSU\)</span>],</li>
         <li>Sea Surface temperature [<span class="math">\(C\)</span>],</li>
         <li>Sea Surface salinity [<span class="math">\(PSU\)</span>],</li>
         <li>Sea Surface Height [<span class="math">\(m\)</span>],</li>
         <li>Net Upward Water Flux [<span class="math">\(Kg=m2=s\)</span>],</li>
         <li>concentration/dilution water flux [<span class="math">\(Kg=m2=s\)</span>],</li>
         <li>Surface Salt Flux [<span class="math">\(Kg=m2=s\)</span>],</li>
         <li>Net Downward Heat Flux [<span class="math">\(W=m2\)</span>],</li>
         <li>Shortwave Radiation [<span class="math">\(W=m2\)</span>],</li>
         <li>Turbocline Depth [<span class="math">\(m\)</span>],</li>
         <li>Mixed Layer Depth 0.01 [<span class="math">\(W=m2\)</span>],</li>
         <li>Ice fraction [<span class="math">\(0;1\)</span>],</li>
         <li>wind speed at 10m [<span class="math">\(m=s\)</span>],</li>
         <li>Surface Heat Flux: Damping [<span class="math">\(W=m2\)</span>],</li>
         <li>Surface Water Flux: Damping [<span class="math">\(Kg=m2=s\)</span>],</li>
         <li>Surface salt flux: damping [<span class="math">\(Kg=m2=s\)</span>],</li>
         <li>Bowl Index[<span class="math">\(W point\)</span>].</li>
      </ul>
      <p>An example of CDL text representation of this file is shown in <a href="#cdl-outT">Listing 5.22</a>.</p>
   </div>
   <div class="col-6 pr-0" style="font-size:16px">
      <div id="cdl-outT" class="highlight-NETCF">
<pre><code class="mycode">netcdf fields_filename {
dimensions :
   lon = 677;
   lat = 253;
   depth = 72;
   time = UNLIMITED; // (7 currently )
variables : \\
   float lont (x);
         lont : units = &quot; degrees_east &quot;;
   float latt (y);
         latt : units = &quot; degrees_north &quot;;
   float deptht (z);
         deptht : units = &quot;m&quot;;
   double time (t);
         time : units = &quot; seconds since
                   1970-01-01 00:00:00&quot;;
   float temperature (t, z, y, x);
         temperature : units = &quot; degC &quot;;
}
</code></pre>
<p class="caption">Listing 5.22: CDL example for the bdyV_u3d data.</p>
      </div>
   </div>
</div>

<!-- <p><div class="clearer"></div></p> -->

(2) This output file SURF_1h_YYYYMMDD0_YYYYMMDD1_grid_U contains hourly fields defined on the Arakawa-U grid within the chid nested domain.

<div class="row mx-0">
   <div class="col-6 ps-0">
      <p> This file contains the following variables: </p>
      <ul class="simple">
         <li><p>Zonal Current [<span class="math">\(m/s\)</span>],</p></li>
         <li><p>Wind Stress along zonal-axis [<span class="math">\(N/m^2\)</span>],</p></li>
      </ul>
      <p>An example of CDL text representation of this file is shown in <a href="#cdl-outU">Listing 5.23</a>.</p>
   </div>
   <div class="col-6 pr-0" style="font-size:16px">
      <div id="cdl-outU" class="highlight-NETCF">
<pre><code class="mycode">netcdf fields_filename {
dimensions :
   lon = 677;
   lat = 253;
   depth = 72;
   time = UNLIMITED; // (7 currently )
variables : \\
   float lont (x);
         lont : units = &quot; degrees_east &quot;;
   float latt (y);
         latt : units = &quot; degrees_north &quot;;
   float deptht (z);
         deptht : units = &quot;m&quot;;
   double time (t);
         time : units = &quot; seconds since
                   1970-01-01 00:00:00&quot;;
   float temperature (t, z, y, x);
         temperature : units = &quot; degC &quot;;
}
</code></pre>
<p class="caption">Listing 5.23: CDL example for the bdyV_u3d data.</p>
      </div>
   </div>
</div>

<!-- <p><div class="clearer"></div></p> -->

(3) This output file SURF_1h_YYYYMMDD0_YYYYMMDD1_grid_V contains hourly fields defined on the Arakawa-V grid within the chid nested domain.

<div class="row mx-0">
   <div class="col-6 ps-0">
      <p> This file contains the following variables: </p>
      <ul class="simple">
         <li><p>Meridional Current [<span class="math">\(m/s\)</span>],</p></li>
         <li><p>Wind Stress along meridional-axis [<span class="math">\(N/m^2\)</span>],</p></li>
      </ul>
      <p>An example of CDL text representation of this file is shown in <a href="#cdl-outU">Listing 5.23</a>.</p>
   </div>
   <div class="col-6 pr-0" style="font-size:16px">
      <div id="cdl-outV" class="highlight-NETCF">
<pre><code class="mycode">netcdf fields_filename {
dimensions :
   lon = 677;
   lat = 253;
   depth = 72;
   time = UNLIMITED; // (7 currently)
variables : \\
   float lont(x);
         lont: units = &quot;degrees_east&quot;;
   float latt(y);
         latt: units = &quot;degrees_north&quot;;
   float deptht(z);
         deptht: units = &quot;m&quot;;
   double time(t);
         time: units = &quot;seconds since
                  1970-01-01 00:00:00&quot;;
   float temperature(t,z,y,x);
         temperature: units = &quot;degC&quot;;
}
</code></pre>
<figcaption>Listing 5.24: CDL example for the bdyV_u3d data.</figcaption>
</figure>
         </div>
      </div>
   </div>

   <!-- <p><div class="clearer"></div></p> -->

(4) This output file SURF_1h_YYYYMMDD0_YYYYMMDD1_grid_W contains hourly fields defined on the Arakawa-W grid within the chid nested domain.

   <div class="row mx-0">
      <div class="col-6 ps-0">
         <p> This file contains the following variables: </p>
         <ul class="simple">
            <li><p>Vertical velocity [<span class="math">\(m/s\)</span>],</p></li>
            <li><p>Vertical Eddy Viscosity [<span class="math">\(m^2/s\)</span>],</p></li>
            <li><p>Vertical Eddy Diffusivity [<span class="math">\(m^2/s\)</span>].</p></li>
         </ul>
         <p>An example of CDL text representation of this file is shown in <a href="#cdl-outU">Listing 5.23</a>.</p>
      </div>
      <div class="col-6 pr-0" style="font-size:16px">
         <div id="cdl-outV" class="highlight-NETCF">
<pre><code class="mycode">netcdf fields_filename {
dimensions :
   lon = 677;
   lat = 253;
   depth = 72;
   time = UNLIMITED; // (7 currently)
variables : \\
   float lont(x);
         lont: units = &quot;degrees_east&quot;;
   float latt(y);
         latt: units = &quot;degrees_north&quot;;
   float deptht(z);
         deptht: units = &quot;m&quot;;
   double time(t);
         time: units = &quot;seconds since
                  1970-01-01 00:00:00&quot;;
   float temperature(t,z,y,x);
         temperature: units = &quot;degC&quot;;
}
</code></pre>
<figcaption>Listing 5.24: CDL example for the bdyV_u3d data.</figcaption>
</figure>
         </div>
      </div>
   </div>

   <!-- <p><div class="clearer"></div></p> -->

### **Restart dataset**

The restart file can be used as initial conditions for research ...

<div class="row mx-0">
   <div class="col-6 ps-0">
      <p>This file contains all the information of the child ocean model grids
      and it includes the following variables:</p>
      <ul class="simple">
      <li><p>longitude on TUVF grid points [<span class="math">\(degree\)</span>],</p></li>
      <li><p>latitude on TUVF grid points [<span class="math">\(degree\)</span>],</p></li>
      <li><p>depth on TUVF grid points [<span class="math">\(m\)</span>],</p></li>
      </ul>
      <p>An example of CDL text representation of this file is shown in <a href="#cdl-oceoutmask">Listing 5.21</a>.</p>
   </div>
   <div class="col-6 pr-0" style="font-size:16px">
      <div id="cdl-oceoutmask" class="highlight-NETCF">
<pre><code class="mycode">netcdf SURF_restart_20141005 {
dimensions:
x = 94 ;
y = 79 ;
z = 120 ;
t = UNLIMITED ; // (1 currently)
variables:
float nav_lon(y, x) ;
float nav_lat(y, x) ;
float nav_lev(z) ;
double time_counter(t) ;
double kt ;
double ndastp ;
double adatrj ;
double utau_b(t, y, x) ;
double vtau_b(t, y, x) ;
double qns_b(t, y, x) ;
double emp_b(t, y, x) ;
double sfx_b(t, y, x) ;
double sbc_hc_b(t, y, x) ;
double sbc_sc_b(t, y, x) ;
double qsr_hc_b(t, z, y, x) ;
double fraqsr_1lev(t, y, x) ;
double rdt ;
double rdttra1 ;
double ub(t, z, y, x) ;
double vb(t, z, y, x) ;
double tb(t, z, y, x) ;
double sb(t, z, y, x) ;
double rotb(t, z, y, x) ;
double hdivb(t, z, y, x) ;
double sshb(t, y, x) ;
double un(t, z, y, x) ;
double vn(t, z, y, x) ;
double tn(t, z, y, x) ;
double sn(t, z, y, x) ;
double rotn(t, z, y, x) ;
double hdivn(t, z, y, x) ;
double sshn(t, y, x) ;
double rhop(t, z, y, x) ;
}
</code></pre>
<p class="caption">Listing 5.21: CDL example for the restart datasets.</p>
      </div>
   </div>
</div>
