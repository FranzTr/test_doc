# **User Configuration File - Preprocessing Sections**

<div style="text-align: justify">

To execute the SURF-NEMO package, the user must input several model parameters to select a specific simulation region, the simulation period, horizontal and vertical turbulence schemes, input datasets, interpolation methods, etc.
These parameters are used to conduct the pre- and post-processing phases and to populate the Fortran namelist required to execute the NEMO-OPA code.
These choices are made by specifying the values of the input model parameters in the user configuration file "<code>setParFree.json</code>", where all the free-user input parameters are grouped in different sections according to their functionality. In this chapter we provide details of each section of the configuration file and specify the admissible values, the unit measures and the “reference value” used for the test case experiment for each parameter (see Section 6.4).
Some of the input model parameters are fixed and defined inside the SURF source package in the file
"<code>setParFix</code>" (see <a href="#reference-configuration">Appendix A</a> for more details)

</div>

## **Configuration file and JSON Object Structure**

<div style="text-align: justify">

The user configuration file has a JavaScript Object Notation (JSON)-based format. JSON is a simple,
text-based method of storing and transmitting structured data. This format is "self-describing",
easy to understand and can support complex data types and structures. It is commonly used for configuration files in web applications.
JSON syntax is derived from JavaScript object notation syntax and can contain either an array of values
or an object (an associative array of name/value pairs also referred to as properties). An array is surrounded by
square brackets, [ and ], and contains a comma-separated list of values. An object is surrounded by curly
brackets,{ and }, and contains a comma-separated list of name/value pairs. A name/value pair consists of
a field name (in double quotes), followed by a colon (:), followed by the field value. A value in an array or
object can be of type number (integer or floating-point), string (in double-quotes), boolean (true or false),
another array (surrounded by square brackets, [ and ]), another object (surrounded by curly brackets, and
), or null.
The JSON configuration file defined for the SURF-NEMO package is shown in <a href="#fig-json">Figure 3.1</a>.
At the top level, we have created the “sections” array, which is an object with just one name/value pair.
This array contains various objects. Each object contains three properties: a title that reflects the contents
of the section, a four-digit alphanumeric identifier ID (id = A001, A002, etc. for pre-processing sections and
id = B001, B002, etc. for post-processing sections) and an array of items delimited by square brackets.
Each element of the “items” array is an object that is identified by a name, a value, a data type
(int, float, double, bool and string) and a brief description of the corresponding parameter.

</div>

<div class="d-flex justify-content-center">
    <figure id="fig-json" class="figure text-center">
    <a href="../assets/img/jsonFile.png">
        <img src="../assets/img/jsonFile.png" alt="../assets/img/jsonFile.png" width="100%">
    </a>
    <figcaption class="figurenum">JSON representation for the SURF-NEMO user-configuration file.</figcaption>
    </figure>
</div>

## **Genearal Input parameters**

### **Section set_surf**

<p>The section set_surf contains the following two parameters:</p>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">nnest</code></div>
    <div class="col-8 pr-0"><p>Number of nesting domain.</p>
    <p><code>Type</code>: int &nbsp; <code>Ref.Value</code>: 1 &nbsp; <code>Range</code>: 1, 2, 3</p></div>
    </div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">nameNestDomain</code></div>
    <div class="col-8 pr-0"><p>Name of the nest domain to simulate.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: gulfTaranto</p></div>
</div>

### **Section set_lrun**

<p>The section set_lrun contains the logical parameters to activate/deactivate specific tasks.</p>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">lrun_childMeshMask</code></div>
    <div class="col-8 pr-0"><p>Enables the execution of the CHILD-MESHMASK GENERATION task.</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">lrun_regridPreAtm</code></div>
    <div class="col-8 pr-0"><p>Enables the execution of the ATMOSPHERIC-DATA-REGRIDDING task.</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">lrun_regridPreOceIC</code></div>
    <div class="col-8 pr-0"><p>Enables the execution of the OCEAN-IC-DATA-REGRIDDING phase.</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">lrun_regridPreOceBC</code></div>
    <div class="col-8 pr-0"><p>Enables the execution of the OCEAN-BC-DATA-REGRIDDING phase.</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">lrun_regridPreTideBC</code></div>
    <div class="col-8 pr-0"><p>Enables the execution of the TIDE-BC-DATA-REGRIDDING phase.</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">lrun_regridPreWeights</code></div>
    <div class="col-8 pr-0"><p>Enables the computation/copy of WEIGHT-FILEs for input_fields REMAPPING (if lrun_regridPre=True).</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">lrun_ocean</code></div>
    <div class="col-8 pr-0"><p>Enables the execution of the NEMO codes.</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">lrun_regridOutUV</code></div>
    <div class="col-8 pr-0"><p>Enables the execution of the output-UV_fields REMAPPING (from UV GRID to T-GRID).</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: False</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">lrun_regridOutUVWeghts</code></div>
    <div class="col-8 pr-0"><p>Enables the computation/copy of WHEGHT-FILEs for output-UV_fields REMAPPING (if lrun_regridOutUV-True).</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: False</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">lrun_shapFiltBat</code></div>
    <div class="col-8 pr-0"><p>Enables the execution of the SHAPIRO Filter for Bathymetric datasets.</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">lrun_shapFiltOce</code></div>
    <div class="col-8 pr-0"><p>Enable the execution of the SHAPIRO Filter fo Ocean datasets.</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: False</p></div>
</div>

<!-- ===================================================================================================== -->

## **Input parameters for spatial grid generation**

### **Section set_xyGrid**

<p>The section set_xyGrid contains the free input parameters required for the generation of the horizontal model grid.</p>

<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">gr_xygridSpec</code></div>
    <div class="col-8 pr-0"><p>Parameters specification for the horizontal grid: if = 0, the grid is function of the 5 variables (lam0,phi0,nlam,nphi,dxy) if = 1, the grid is function of the 5 variables (lam0,phi0,lam1,phi1,dxy)..</p>
    <p><code>Type</code>: int &nbsp; <code>Ref.Value</code>: 0 &nbsp; <code>Range</code>: 0, 1</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">gr_jpidta</code></div>
    <div class="col-8 pr-0"><p>Number of grid points in zonal direction to specify if xygridSpec=0 (if =NOTUSED, parameter not read).</p>
    <p><code>Type</code>: int &nbsp; <code>Ref.Value</code>: 94</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">gr_jpjdta</code></div>
    <div class="col-8 pr-0"><p>Number of grid points in meridional direction to specify if xygridSpec=0 (if =NOTUSED, parameter not read).</p>
    <p><code>Type</code>: int &nbsp; <code>Ref.Value</code>: 79</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">gr_ppglam0</code></div>
    <div class="col-8 pr-0"><p>Longitude of the first raw and column T-point to specify if xygridSpec=0,1.</p>
    <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 16.4375</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">gr_ppglam1</code></div>
    <div class="col-8 pr-0"><p>Longitude of the last raw and column T-point to specify if xygridSpec=1 (if =NOTUSED, parameter not read).</p>
    <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: NOTUSED</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">gr_ppgphi0</code></div>
    <div class="col-8 pr-0"><p>Latitude of the first raw and column T-point to specify if xygridSpec=0,1.</p>
    <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 38.9375</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">gr_ppgphi1</code></div>
    <div class="col-8 pr-0"><p>Latitude of the last raw and column T-point to specify if xygridSpec=1 (if =NOTUSED, parameter not read).</p>
    <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: NOTUSED</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">gr_jp_cfg</code></div>
    <div class="col-8 pr-0"><p>Child model resolution (1/gr_jp_cfg) to specify if xygridSpec=0,1.</p>
    <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 48.</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">gr_jp_cfg_father</code></div>
    <div class="col-8 pr-0"><p>Father model resolution (1/gr_jp_cfg_father).</p>
    <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 16.</p></div>
</div>

### **Section set_zGrid**

<p>The section set_zGrid contains the free input parameters used to generate the vertical grid.</p>

<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">gr_jpkdta</code></div>
    <div class="col-8 pr-0"><p>Number of vertical levels.</p>
    <p><code>Type</code>: int &nbsp; <code>Ref.Value</code>: 120</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">gr_zgridSpec</code></div>
    <div class="col-8 pr-0"><p>Parameters specification for the vertical grid: if = 0, the grid is function of the 5 variables (hh0,h1,hsur,hcr,hth) if = 1, the grid is function of the 4 variables (dzmin,hmax,hcr,hth).</p>
    <p><code>Type</code>: int &nbsp; <code>Ref.Value</code>: 1. &nbsp; <code>Range</code>: 0, 1</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">gr_ppsur</code></div>
    <div class="col-8 pr-0"><p>Parameter h_sur for the z-coord. trasformation to specify if zgridSpec=0 (if =NOTUSED, parameter not read).</p>
    <p><code>Type</code>: double &nbsp; <code>Ref.Value</code>: NOTUSED</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">gr_ppa0</code></div>
    <div class="col-8 pr-0"><p>Parameter h_0 for the z-coordinate trasformation to specify if zgridSpec=0 (if =NOTUSED, parameter not read).</p>
    <p><code>Type</code>: double &nbsp; <code>Ref.Value</code>: NOTUSED</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">gr_ppa1</code></div>
    <div class="col-8 pr-0"><p>Parameter h_1 for the z-coordinate trasformation to specify if zgridSpec=0 (if =NOTUSED, parameter not read).</p>
    <p><code>Type</code>: double &nbsp; <code>Ref.Value</code>: NOTUSED</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">gr_ppkth</code></div>
    <div class="col-8 pr-0"><p>Parameter h_th which gives the approximate layer number above which stretching will be maximum (usually of order nz/2) to specify if zgridSpec=0,1.</p>
    <p><code>Type</code>: double &nbsp; <code>Ref.Value</code>: 100</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">gr_ppacr</code></div>
    <div class="col-8 pr-0"><p>Parameter h_cr which gives the grid stretching factor (the highest gr_ppacr, the smallest the stretching) to specify if zgridSpec=0,1.</p>
    <p><code>Type</code>: double &nbsp; <code>Ref.Value</code>: 30</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">gr_ppdzminw</code></div>
    <div class="col-8 pr-0"><p>Depth of the top (first) model layer depth of second 'w' level to specify if zgridSpec=1 (if =NOTUSED, parameter not read).</p>
    <p><code>Type</code>: double &nbsp; <code>Ref.Value</code>: 2.8</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">gr_pphmaxw</code></div>
    <div class="col-8 pr-0"><p>Maximum depth of the ocean depth of the last 'w' level (set to 0.0 to be computed) to specify if zgridSpec=1 (if =NOTUSED, parameter not read).</p>
    <p><code>Type</code>: double &nbsp; <code>Ref.Value</code>: 0.0</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">gr_dbletanh</code></div>
    <div class="col-8 pr-0"><p>Enables the use of the double tanh function for vertical coordinates.</p>
    <p><code>Type</code>: bool. &nbsp; <code>Ref.Value</code>: False.</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">gr_ppa2</code></div>
    <div class="col-8 pr-0"><p>Parameter h_2 to specify if gr_dbletanh=True (if =NOTUSED, parameter not read).</p>
    <p><code>Type</code>: double &nbsp; <code>Ref.Value</code>: NOTUSED</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">gr_ppkth2</code></div>
    <div class="col-8 pr-0"><p>Parameter h_th2 if gr_dbletanh=True (if =NOTUSED, parameter not read).</p>
    <p><code>Type</code>: double &nbsp; <code>Ref.Value</code>: NOTUSED</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">gr_ppacr2</code></div>
    <div class="col-8 pr-0"><p>Parameter h_cr2 if gr_dbletanh=True (if =NOTUSED, parameter not read).</p>
    <p><code>Type</code>: double &nbsp; <code>Ref.Value</code>: NOTUSED</p></div>
</div>

<!-- ===================================================================================================== -->

## **Input parameters for date and time simulation**

### **Section set_dateTime**

<p>This section of the JSON file contains the free input parameters used to define the period and time discretization of the simulation.</p>

<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">start_date</code></div>
    <div class="col-8 pr-0"><p>Initial date of the simulation (the run starts at 00:00).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: 20141005</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">ndays</code></div>
    <div class="col-8 pr-0"><p>Total number of simulation days.</p>
    <p><code>Type</code>: int &nbsp; <code>Ref.Value</code>: 2</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">ndays_spinup</code></div>
    <div class="col-8 pr-0"><p>Number of spin-up days.</p>
    <p><code>Type</code>: int &nbsp; <code>Ref.Value</code>: 1 &nbsp; <code>Range</code>: 0:ndays</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">dom_rdt</code></div>
    <div class="col-8 pr-0"><p>Simulation 'baroclinic' time step (...40, 48, 50, 60, 72, 80, 90, 100, 120, 144...).</p>
    <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 150.</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">runMan_write</code></div>
    <div class="col-8 pr-0"><p>Frequency of write in the output file express as the number of simulation time step.</p>
    <p><code>Type</code>: int &nbsp; <code>Ref.Value</code>: 24</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">dom_btAuto</code></div>
    <div class="col-8 pr-0"><p>Enables the automatically definition of baro-timestep to be just below a user defined maximum courant number dom_btCmax.</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: False</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">dom_btCmax</code></div>
    <div class="col-8 pr-0"><p>Maximum courant number (allowed if dom_btAuto=True).</p>
    <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 0.8</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">dom_baro</code></div>
    <div class="col-8 pr-0"><p>Number of iterations of barotropic mode during dom_rdt (allowed if dom_btAuto=False).</p>
    <p><code>Type</code>: int &nbsp; <code>Ref.Value</code>: 100</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">runMan_rstart</code></div>
    <div class="col-8 pr-0"><p>Start from rest (False) or from a restart file (True).</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">ndays_xsimu</code></div>
    <div class="col-8 pr-0"><p>Number of days per each restart simulation.</p>
    <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 1</p></div>
</div>

<!-- ===================================================================================================== -->

## **Input parameters for surface and lateral boundary conditions**

### **Section set_sbc**

<p>This section of the JSON file contains the free input parameters used to define surface boundary condition.</p>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">sbc_iformulat</code></div>
<div class="col-8 pr-0"><p>Surface boundary condition formulation to be used (=0)MFS bulk formulat,(=1)fluxform+ssRest,(=2)CORE formulation.</p>
                        <p><code>Type</code>: int &nbsp; <code>Ref.Value</code>: 0 &nbsp; <code>Range</code>: 0, 1, 2</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">sbc_ltimeInterp</code></div>
<div class="col-8 pr-0"><p>Activate, or not, the time interpolation (=False) steplike shape forcing (=True) broken line shape forcing.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">sbc_zreftemp</code></div>
<div class="col-8 pr-0"><p>Reference height (m) for the Air Temperature and humidity (for the CORE formulation).</p>
                        <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 10.</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">sbc_zrefwind</code></div>
<div class="col-8 pr-0"><p>Reference height (m) for the wind vector (for the CORE formulation).</p>
                        <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 10.</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">sbc_aprdyn</code></div>
<div class="col-8 pr-0"><p>Enables the inclusion of atmospheric pressure gradien in ocean and ice Eqs..</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: False</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">sbc_sclapr</code></div>
<div class="col-8 pr-0"><p>Scaling factor to convert atmospheric presure from hPa to Pa.</p>
                        <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 1.</p></div>
</div>

### **Section set_obc**

<p>This section of the JSON file contains the free input parameters used to define lateral open boundary conditions.</p>

<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">obc_dyn2d</code></div>
    <div class="col-8 pr-0"><p>Algorithm of boundary condition for barotropic solution: flather.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: flather &nbsp; <code>Range</code>: flather</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">obc_dyn2d_dta</code></div>
    <div class="col-8 pr-0"><p>Boundary data to use: (=0)Initial condition (=1)external data (=2)tidal forcing (=3)xternal data+tidal.</p>
    <p><code>Type</code>: int &nbsp; <code>Ref.Value</code>: 1 &nbsp; <code>Range</code>: 0, 1, 2 ,3</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">obc_dyn3d</code></div>
    <div class="col-8 pr-0"><p>Algorithm of boundary condition for baroclinic velocities: frs, orlanski.</p>
    <p><code>Type</code>: string  &nbsp; <code>Ref.Value</code>: frs &nbsp; <code>Range</code>: frs, orlanski</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">obc_dyn3d_dta</code></div>
    <div class="col-8 pr-0"><p>Boundary data to use: (=0)Initial condition (=1)external data.</p>
    <p><code>Type</code>: int &nbsp; <code>Ref.Value</code>: 1 &nbsp; <code>Range</code>: 0, 1</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">obc_tra</code></div>
    <div class="col-8 pr-0"><p>Algorithm of boundary condition for active tracers: frs, orlanski.</p>
    <p><code>Type</code>: string  &nbsp; <code>Ref.Value</code>: frs &nbsp; <code>Range</code>: frs, orlanski</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">obc_tra_dta</code></div>
    <div class="col-8 pr-0"><p>Boundary data to use: (=0)Initial condition (=1)external data.</p>
    <p><code>Type</code>: int &nbsp; <code>Ref.Value</code>: 1 &nbsp; <code>Range</code>: 0, 1</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">obc_rimwidth</code></div>
    <div class="col-8 pr-0"><p>Width of the FRS zone.</p>
    <p><code>Type</code>: int &nbsp; <code>Ref.Value</code>: 1</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">obc_ltimeInterp</code></div>
    <div class="col-8 pr-0"><p>Activate, or not, the time interpolation (=False) steplike shape forcing (=True) broken line shape forcing.</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">obc_lvelCorr</code></div>
    <div class="col-8 pr-0"><p>Activate the Integral Contraint method to preserve the total transport after the interpolation.</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: False</p></div>
</div>

### **Section set_tide**

<p>This section of the JSON file contains the free input parameters used to define the tidal components which can be added both as the equilibrium tidal sea level and/or only at the lateral boundaries</p>

<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">latBtide_lPot</code></div>
    <div class="col-8 pr-0"><p>Enables the use of tidal potential forcing.</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">latBtide_K1</code></div>
    <div class="col-8 pr-0"><p>Name of the Lunar diurnal K1 tidal component (if =NOTUSED, component not used).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: K1 &nbsp; <code>Range</code>: K1</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">latBtide_O1</code></div>
    <div class="col-8 pr-0"><p>Name of the Lunar diurnal O1 tidal component (if =NOTUSED, component not used).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: O1 &nbsp; <code>Range</code>: O1</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">latBtide_P1</code></div>
    <div class="col-8 pr-0"><p>Name of the Solar diurnal P1 tidal component (if =NOTUSED, component not used).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: P1 &nbsp; <code>Range</code>: P1</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">latBtide_Q1</code></div>
    <div class="col-8 pr-0"><p>Name of the Larger lunar elliptic diurnal Q1 tidal component (if =NOTUSED, component not used).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: Q1 &nbsp; <code>Range</code>: Q1</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">latBtide_K2</code></div>
    <div class="col-8 pr-0"><p>Name of the Lunisolar semidiurnal K2 tidal component (if =NOTUSED, component not used)</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: K2 &nbsp; <code>Range</code>: K2</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">latBtide_M2</code></div>
    <div class="col-8 pr-0"><p>Name of the Principal lunar semidiurnal M2 tidal component (if =NOTUSED, component not used).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: M2 &nbsp; <code>Range</code>: M2</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">latBtide_N2</code></div>
    <div class="col-8 pr-0"><p>Name of the Larger lunar elliptic semidiurnal N2 tidal component (if =NOTUSED, component not used).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: N2 &nbsp; <code>Range</code>: N2</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">latBtide_S2</code></div>
    <div class="col-8 pr-0"><p>Name of the Principal solar semidiurnal S2 tidal component (if =NOTUSED, component not used).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: S2 &nbsp; <code>Range</code>: S2</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">latBtide_M4</code></div>
    <div class="col-8 pr-0"><p>Name of the Shallow water overtides of principal lunar M4 tidal component (if =NOTUSED, component not used).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: M4 &nbsp; <code>Range</code>: M4</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">latBtide_Mm</code></div>
    <div class="col-8 pr-0"><p>Name of the Lunar monthly Mm tidal component (if =NOTUSED, component not used).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: Mm &nbsp; <code>Range</code>: Mm</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">latBtide_Mf</code></div>
    <div class="col-8 pr-0"><p>Name of the Lunisolar fortnightly Mf tidal component (if =NOTUSED, component not used).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: Mf &nbsp; <code>Range</code>: Mf</p></div>
</div>

<!-- ===================================================================================================== -->

## **Input parameters for physical parametrization**

### **Section set_eos**

<p>This section of the JSON file contains the free input parameters used to define equation of state of sea water.</p>

<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">eos_type</code></div>
<div class="col-8 pr-0"><p>type of equation of state and Brunt-Vaisala frequency: (=-1)TEOS-10, (=0)EOS-80, (=1)S-EOS.</p>
                        <p><code>Type: int</code> &nbsp; <code>Ref.Value</code>: 0 &nbsp; <code>Range</code>: -1, 0, 1</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">eos_useCT</code></div>
<div class="col-8 pr-0"><p>Enables the use of Conservative Temp. ==> surface CT converted in Pot. Temp. in sbcssm.</p>
                        <p><code>Type: bool</code> &nbsp; <code>Ref.Value</code>: False</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">eos_a0</code></div>
<div class="col-8 pr-0"><p>S-EOS coefficients: thermal expension coefficient.</p>
                        <p><code>Type: float</code> &nbsp; <code>Ref.Value</code>: 0.1655</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">eos_b0</code></div>
<div class="col-8 pr-0"><p>S-EOS coefficients: saline expension coefficient.</p>
                        <p><code>Type: float</code> &nbsp; <code>Ref.Value</code>: 0.76554</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">eos_lambda1</code></div>
<div class="col-8 pr-0"><p>S-EOS coefficients: cabbeling coeff in T^2  (=0 for linear eos).</p>
                        <p><code>Type: float</code> &nbsp; <code>Ref.Value</code>: 0.05952</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">eos_lambda2</code></div>
<div class="col-8 pr-0"><p>S-EOS coefficients: cabbeling coeff in S^2  (=0 for linear eos).</p>
                        <p><code>Type: float</code> &nbsp; <code>Ref.Value</code>: 0.00074914</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">eos_mu1</code></div>
<div class="col-8 pr-0"><p>S-EOS coefficients: thermobaric coeff. in T (=0 for linear eos).</p>
                        <p><code>Type: float</code> &nbsp; <code>Ref.Value</code>: 0.0001497</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">eos_mu2</code></div>
<div class="col-8 pr-0"><p>S-EOS coefficients: thermobaric coeff. in S (=0 for linear eos).</p>
                        <p><code>Type: float</code> &nbsp; <code>Ref.Value</code>: 1.109e-05</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">eos_nu</code></div>
<div class="col-8 pr-0"><p>S-EOS coefficients: cabbeling coeff in T*S  (=0 for linear eos).</p>
                        <p><code>Type: float</code> &nbsp; <code>Ref.Value</code>: 0.0024341</p></div>
</div>

<!-- ===================================================================================================== -->

### **Section set_botFric**

<p>This section of the JSON file contains the free input parameters used to define the bottom friction</p>

<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">botB_bfri2</code></div>
<div class="col-8 pr-0"><p>Bottom drag coefficient (non linear case).</p>
                        <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 1.e-3</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">botB_bfeb2</code></div>
<div class="col-8 pr-0"><p>Bottom turbulent kinetic energy background (m^2/s^2).</p>
                        <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 2.5e-3</p></div>
</div>

<!-- ===================================================================================================== -->

### **Section set_xyturbTracers**

<p>This section of the JSON file contains the free input parameters used to define the parameterization of lateral subgrid-scale diffusion for tracers. </p>

<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">tra_typeOperator</code></div>
    <div class="col-8 pr-0"><p>Type of the operator used (0)laplacian, (1)bilaplacian.</p>
    <p><code>Type</code>: int &nbsp; <code>Ref.Value</code>: 0 &nbsp; <code>Range</code>: 0, 1</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">tra_eddycoeffSpec</code></div>
    <div class="col-8 pr-0"><p>Horizontal eddy coeff. specification (0)def. by coeff. tra_eddycoeff_child, (1)def. from coeff. tra_eddycoeff_father according fat/child coeff. relation.</p>
    <p><code>Type</code>: int &nbsp; <code>Ref.Value</code>: 0 &nbsp; <code>Range</code>: 0, 1</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">tra_eddycoeff_child</code></div>
    <div class="col-8 pr-0"><p>Horizontal eddy diffusivity (>0 (m2/s) laplacian or < 0 (m4/s2) bilaplacian) of the child model (if =NOTUSED, parameter not read).</p>
    <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 80.</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">tra_eddycoeff_father</code></div>
    <div class="col-8 pr-0"><p>Horizontal eddy diffusivity (>0 (m2/s) laplacian or < 0 (m4/s2) bilaplacian) of the father model to be used in fat/child coeff. relation (if =NOTUSED, parameter not read).</p>
    <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: NOTUSED</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">tra_factor</code></div>
    <div class="col-8 pr-0"><p>Factor to be used in fat/child coeff. relation (if laplacian:(a_child=factor*???), if bilaplacian:(a_child=factor*a_fat(Dx_child/Dx_fat)^4)).</p>
    <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 1</p></div>
</div>

<!-- ===================================================================================================== -->

### **Section set_xyturbMomentum**

<p>This section of the JSON file contains the free input parameters used to define the parameterization of lateral subgrid-scale viscosity for momentum. </p>

<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">dyn_typeOperator</code></div>
    <div class="col-8 pr-0"><p>type of the operator used (0)laplacian, (1)bilaplacian.</p>
    <p><code>Type</code>: int &nbsp; <code>Ref.Value</code>: 1 &nbsp; <code>Range</code>: 0, 1</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">dyn_eddycoeffSpec</code></div>
    <div class="col-8 pr-0"><p>horizontal eddy coeff. specification (0)def. by coeff. dyn_eddycoeff_child, (1)def. from coeff. dyn_eddycoeff_father according fat/chld coeff. relation.</p>
    <p><code>Type</code>: int &nbsp; <code>Ref.Value</code>: 1 &nbsp; <code>Range</code>: 0, 1</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">dyn_eddycoeff_child</code></div>
    <div class="col-8 pr-0"><p>horizontal eddy viscosity (>0 (m2/s) laplacian or < 0 (m4/s2) bilaplacian) of the child model (if =NOTUSED, parameter not read).</p>
    <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: NOTUSED</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">dyn_eddycoeff_father</code></div>
    <div class="col-8 pr-0"><p>horizontal eddy viscosity (>0 (m2/s) laplacian or < 0 (m4/s2) bilaplacian) of the father model to be used in fat/child coeff. relation (if =NOTUSED, parameter not read).</p>
    <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: -0.5e10</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">dyn_factor</code></div>
    <div class="col-8 pr-0"><p>factor to be used in father/child coeff. relation (if laplacian:(a_child=factor*???), if bilaplacian:(a_child=factor*a_fat(Dx_child/Dx_fat)^4)).</p>
    <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 1.</p></div>
</div>

<!-- ===================================================================================================== -->

### **Section set_zturb**

<p>This section of the JSON file contains the free input parameters used to define the vertical eddy viscosity and diffusivity coefficients</p>

<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">zdyn_avm0</code></div>
    <div class="col-8 pr-0"><p>Vertical eddy viscosity [m2/s] (background Kz if not 'key_zdfcst').</p>
    <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 1.2e-5</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">zdyn_avt0</code></div>
    <div class="col-8 pr-0"><p>Vertical eddy diffusivity [m2/s] (background Kz if not 'key_zdfcst').</p>
    <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 1.2e-6</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">zdyn_avevd</code></div>
    <div class="col-8 pr-0"><p>Evd mixing coefficient [m2/s].</p>
    <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 10.</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">zdynric_avmri</code></div>
    <div class="col-8 pr-0"><p>Maximum value of the vertical viscosity.</p>
    <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 1.e-2</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">zdynric_alp</code></div>
    <div class="col-8 pr-0"><p>Vertical eddy viscosity [m2/s] (background Kz if not 'key_zdfcst').</p>
    <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 5.</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">zdynric_ric</code></div>
    <div class="col-8 pr-0"><p>Vertical eddy viscosity [m2/s] (background Kz if not 'key_zdfcst').</p>
    <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 2.</p></div>
</div>

<!-- ===================================================================================================== -->

## **Input parameters for downloading input datasets**

### **Section set_dataDownlCoast_urlName**

<p>This section of the JSON file contains the parameters needed to make up the URL that is required to access the input coastline datasets from a local or remote ropository.</p>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlCoast_usr</code></div>
    <div class="col-8 pr-0"><p>Username to access the coastline datasets from a remote ftp server.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: usr</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlCoast_pwd</code></div>
    <div class="col-8 pr-0"><p>Password to access the coastline datasets from a remote ftp server.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: pwd</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlCoast_urlbase</code></div>
    <div class="col-8 pr-0"><p>Parametric urlname (i.e. ftp:/... or file:///...) for the coastline datasets. Parameters: (RESCOAST).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: file:///scratch/surf/surf_datasets/current/coastline/GSHHS_shp/(RESCOAST)</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlCoast_resol</code></div>
    <div class="col-8 pr-0"><p>Name for spatial resolution used to replace the substring (RESCOAST) on the parametric urlname (if =NOTUSED, parameter not read).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: h &nbsp; <code>Range</code>: f, h, i, l, c</p></div>
</div>

### **Section set_dataDownlCoast_fileName**

<p>This section of the JSON file contains the parameters for the FILENAMEs of the input coastline datasets.</p>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileCoast_lland</code></div>
    <div class="col-8 pr-0"><p>Enables the use of the land coastline.</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileCoast_filebaseLand</code></div>
    <div class="col-8 pr-0"><p>Files name for NOAA coastline datasets contains boundary between land and ocean (if fileCoast_lland=True). Parameters: (RESCOAST).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: GSHHS_(RESCOAST)_L1.shp</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileCoast_llake</code></div>
    <div class="col-8 pr-0"><p>Enables the use of the lake coastline.</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: False</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileCoast_filebaseLake</code></div>
    <div class="col-8 pr-0"><p>Files name for NOAA coastline datasets contains boundary between lake and land (if fileCoast_llake=True). Parameters: (RESCOAST).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: GSHHS_(RESCOAST)_L2.shp</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileCoast_lislandlake</code></div>
    <div class="col-8 pr-0"><p>Enables the use of the islelake coastline.</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: False</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileCoast_filebaseIslandlake</code></div>
    <div class="col-8 pr-0"><p>Files name for NOAA coastline datasets contains boundary between island-in-lake and lake (if fileCoast_lislandlake=True). Parameters: (RESCOAST).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: GSHHS_(RESCOAST)_L3.shp</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileCoast_resol</code></div>
    <div class="col-8 pr-0"><p>Name for spatial resolution used to replace the substring (RESCOAST) on the parametric file name (if =NOTUSED, parameter not read).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: h</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileCoast_lcompression</code></div>
    <div class="col-8 pr-0"><p>(=True) if datasets you want to download are gzip compressed files (*.gz).</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: False</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileCoast_lkeepSrcFull</code></div>
    <div class="col-8 pr-0"><p>(=True) if you want to keep in your disk the downloaded uncutted datasets.</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>

### **Section set_dataDownlBat_urlName**

<p>This section of the JSON file contains the parameters needed to make up the URL that is required to access the input bathymetry datasets from a local or remote ropository.</p>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlBat_usr</code></div>
    <div class="col-8 pr-0"><p>Username to access the bathymetric datasets from a remote ftp server.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: usr</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlBat_pwd</code></div>
    <div class="col-8 pr-0"><p>Password to access the bathymetric datasets from a remote ftp server.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: pwd</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlBat_urlbase</code></div>
    <div class="col-8 pr-0"><p>Parametric urlname (i.e. ftp:/... or file:///...) for the bathymetric datasets. Parameters: (RESOL).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: usr</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlBat_resol</code></div>
    <div class="col-8 pr-0"><p>Name for spatial resolution used to replace the substring (RESOL) on the parametric urlname (if =NOTUSED, parameter not read).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: h</p></div>
</div>

### **Section set_dataDownlBat_fileName**

<p>This section of the JSON file contains the parameters for the FILENAME of the input bathymetry datasets.</p>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileBat_filebase</code></div>
    <div class="col-8 pr-0"><p>Parametric filename for the source bathymetric datasets. Parameters: (RESBAT).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: macroMED_bathyGEBCO.nc</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileBat_resol</code></div>
    <div class="col-8 pr-0"><p>Name for spatial resolution used to replace the substring (RESBAT) on the parametric file name (if =NOTUSED, parameter not read).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: NOTUSED</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileBat_lcompression</code></div>
    <div class="col-8 pr-0"><p>(=True) if datasets you want to download are gzip compressed files (*.gz).</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: False</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileBat_llonFlip</code></div>
    <div class="col-8 pr-0"><p>(=True) if longitude coord. is in the 0 to 360 range and (=False) if longitude is in -180:+180 range.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: macroMED_bathyGEBCO.nc</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileBat_llatInv</code></div>
    <div class="col-8 pr-0"><p>(=True) if the dataset contains latitude decreasing through the pole.</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: False</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileBat_ldepthIncr</code></div>
    <div class="col-8 pr-0"><p>(=True) if the dataset contains sea floor elevation (positive) increases with increasing water depth.</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: False</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileBat_lkeepSrcFull</code></div>
    <div class="col-8 pr-0"><p>(=True) if you want to keep in your disk the downloaded uncutted datasets.</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: False</p></div>
</div>

### **Section set_dataDownlBat_varName**

<p>This section of the JSON file contains the parameters for the VARIABLE-NAMEs of the input bathymetry datasets.</p>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">srcDimBat_lon</code></div>
    <div class="col-8 pr-0"><p>Name of the dimension for the longitude.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: lon</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">srcDimBat_lat</code></div>
    <div class="col-8 pr-0"><p>Name of the dimension for the latitude.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: lat</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">srcCrdBat_lon</code></div>
    <div class="col-8 pr-0"><p>Name of the coordinate variable for the longitude.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: lon</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">srcCrdBat_lat</code></div>
    <div class="col-8 pr-0"><p>Name of the coordinate variable for the latitude.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: lat</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">srcVarBat_elev</code></div>
    <div class="col-8 pr-0"><p>Name of the variable for the Sea Floor Elevation.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: elevation</p></div>
</div>

### **Section set_dataDownlAtmMesh_urlName**

<p>This section of the JSON file contains the parameters needed to make up the URL that is required to access the input atmospheric meshmask datasets from a local or remote ropository.</p>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlAtmMesh_usr</code></div>
    <div class="col-8 pr-0"><p>Username to access the input atmospheric meshmask datasets from a remote ftp server.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: usr</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlAtmMesh_pwd</code></div>
    <div class="col-8 pr-0"><p>Password to access the input atmospheric meshmask datasets from a remote ftp server.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: pwd</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlAtmMesh_urlbase</code></div>
    <div class="col-8 pr-0"><p>Parametric urlname (i.e. ftp:/... or file:///...) for input atmospheric meshmask datasets. Parameters: (FIELD),YYYY(p)MM(p)DD(p).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: file:///scratch/surf/indata_offline/gulfTaranto_20141005/data/data00/indata/atmosphere/srcFull</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlAtmMesh_velU</code></div>
    <div class="col-8 pr-0"><p>Name for the Zonal Air Velocity used to replace the substring (FIELD) on the parametric urlname.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: v10m</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlAtmMesh_velV</code></div>
    <div class="col-8 pr-0"><p>Name for the Meridional Air Velocity used to replace the substring (FIELD) on the parametric urlname.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: v10m</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlAtmMesh_mslp</code></div>
    <div class="col-8 pr-0"><p>Name for the Mean Sea-Level Pressure used to replace the substring (FIELD) on the parametric urlname.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: mslp</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlAtmMesh_cloudCov</code></div>
    <div class="col-8 pr-0"><p>Name for the Total Cloud Cover used to replace the substring (FIELD) on the parametric urlname.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: tcc</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlAtmMesh_temp</code></div>
    <div class="col-8 pr-0"><p>Name for the Air Temperature used to replace the substring (FIELD) on the parametric urlname.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: t2m</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlAtmMesh_dpTemp</code></div>
    <div class="col-8 pr-0"><p>"Name for the Dewpoint Temperature used to replace the substring (FIELD) on the parametric urlname.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: d2m</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlAtmMesh_prec</code></div>
    <div class="col-8 pr-0"><p>Name for the Total Precipitation used to replace the substring (FIELD) on the parametric urlname.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: precip</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlAtmMesh_tauU</code></div>
    <div class="col-8 pr-0"><p>Name for the Zonal Wind Stress used to replace the substring (FIELD) on the parametric urlname.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: tauU</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlAtmMesh_tauV</code></div>
    <div class="col-8 pr-0"><p>Name for the Meridional Wind Stress used to replace the substring (FIELD) on the parametric urlname.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: tauV</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlAtmMesh_qtot</code></div>
    <div class="col-8 pr-0"><p>Name for the Total Heat Flux used to replace the substring (FIELD) on the parametric urlname.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: qtot</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlAtmMesh_qsr</code></div>
    <div class="col-8 pr-0"><p>Name for the Solar Radiation Penetration used to replace the substring (FIELD) on the parametric urlname.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: qsr</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlAtmMesh_emp</code></div>
    <div class="col-8 pr-0"><p>Name for the Mass Flux Exchanged used to replace the substring (FIELD) on the parametric urlname.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: emp</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlAtmMesh_tempS</code></div>
    <div class="col-8 pr-0"><p>Name for the Surface Temperature used to replace the substring (FIELD) on the parametric urlname.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: sst</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlAtmMesh_salS</code></div>
    <div class="col-8 pr-0"><p>Name for the Surface Salinity used to replace the substring (FIELD) on the parametric urlname.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: sss</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlAtmMesh_umid</code></div>
    <div class="col-8 pr-0"><p>Name for the Air Umidity used to replace the substring (FIELD) on the parametric urlname.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: umid</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlAtmMesh_radLW</code></div>
    <div class="col-8 pr-0"><p>Name for the Long Wave Radiation used to replace the substring (FIELD) on the parametric urlname.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: lwrd</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlAtmMesh_radSW</code></div>
    <div class="col-8 pr-0"><p>Name for the Short Wave Radiation used to replace the substring (FIELD) on the parametric urlname.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: swrd</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">urlAtmMesh_snow</code></div>
    <div class="col-8 pr-0"><p>Name for the Solid Precipitation used to replace the substring (FIELD) on the parametric urlname.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: snow</p></div>
</div>

### **Section set_dataDownlAtmMesh_fileName**

<p>This section of the JSON file contains the parameters needed to make up the FILENAMEs of the input atmospheric meshmask datasets.</p>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileAtmMesh_filebase_velU</code></div>
    <div class="col-8 pr-0"><p>Parametric filename for the Zonal Air Velocity datasets before the spinup-time (if sbc_iformulat=0,2). Parameters: YYYY(p)MM(p)DD(p),YYYY(i)MM(i)DD(i),YYYY(i-1)MM(i-1)DD(i-1),YYYY(i+1)MM(i+1)DD(i+1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: YYYY(i)MM(i)DD(i)-ECMWF---AM0125-MEDATL-bYYYY(i+1)MM(i+1)DD(i+1)_an-fv05.00.nc</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileAtmMesh_filebase_velV</code></div>
    <div class="col-8 pr-0"><p>Parametric filename for the Meridional Air Velocity datasets before the spinup-time (if sbc_iformulat=0,2). Parameters: YYYY(p)MM(p)DD(p),YYYY(i)MM(i)DD(i),YYYY(i-1)MM(i-1)DD(i-1),YYYY(i+1)MM(i+1)DD(i+1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: YYYY(i)MM(i)DD(i)-ECMWF---AM0125-MEDATL-bYYYY(i+1)MM(i+1)DD(i+1)_an-fv05.00.nc</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileAtmMesh_filebase_mslp</code></div>
    <div class="col-8 pr-0"><p>Parametric filename for the Mean Sea-Level Pressure datasets before the spinup-time (if sbc_iformulat=0 or/and sbc_aprdyn). Parameters: YYYY(p)MM(p)DD(p),YYYY(i)MM(i)DD(i),YYYY(i-1)MM(i-1)DD(i-1),YYYY(i+1)MM(i+1)DD(i+1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: YYYY(i)MM(i)DD(i)-ECMWF---AM0125-MEDATL-bYYYY(i+1)MM(i+1)DD(i+1)_an-fv05.00.nc</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileAtmMesh_filebase_cloudCov</code></div>
    <div class="col-8 pr-0"><p>Parametric filename for the Total Cloud Cover datasets before the spinup-time (if sbc_iformulat=0). Parameters: YYYY(p)MM(p)DD(p),YYYY(i)MM(i)DD(i),YYYY(i-1)MM(i-1)DD(i-1),YYYY(i+1)MM(i+1)DD(i+1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: YYYY(i)MM(i)DD(i)-ECMWF---AM0125-MEDATL-bYYYY(i+1)MM(i+1)DD(i+1)_an-fv05.00.nc</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileAtmMesh_filebase_temp</code></div>
    <div class="col-8 pr-0"><p>Parametric filename for the Air Temperature datasets before the spinup-time (if sbc_iformulat=0,2). Parameters: YYYY(p)MM(p)DD(p),YYYY(i)MM(i)DD(i),YYYY(i-1)MM(i-1)DD(i-1),YYYY(i+1)MM(i+1)DD(i+1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: YYYY(i)MM(i)DD(i)-ECMWF---AM0125-MEDATL-bYYYY(i+1)MM(i+1)DD(i+1)_an-fv05.00.nc</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileAtmMesh_filebase_dpTemp</code></div>
    <div class="col-8 pr-0"><p>Parametric filename for the Dewpoint Temperature datasets before the spinup-time (if sbc_iformulat=0). Parameters: YYYY(p)MM(p)DD(p),YYYY(i)MM(i)DD(i),YYYY(i-1)MM(i-1)DD(i-1),YYYY(i+1)MM(i+1)DD(i+1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: YYYY(i)MM(i)DD(i)-ECMWF---AM0125-MEDATL-bYYYY(i+1)MM(i+1)DD(i+1)_an-fv05.00.nc</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileAtmMesh_filebase_prec</code></div>
    <div class="col-8 pr-0"><p>Parametric filename for the Total Precipitation datasets before the spinup-time (if sbc_iformulat=0,2). Parameters: YYYY(p)MM(p)DD(p),YYYY(i)MM(i)DD(i),YYYY(i-1)MM(i-1)DD(i-1),YYYY(i+1)MM(i+1)DD(i+1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: YYYY(i)MM(i)DD(i)_YYYY(i+1)MM(i+1)DD(i+1)-ECMWF---AM025-MEDATL-bYYYY(i)MM(i)DD(i)_fc00-fv02.00_PREC.nc</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileAtmMesh_filebase_tauU</code></div>
    <div class="col-8 pr-0"><p>Parametric filename for the Zonal Wind Stress datasets before the spinup-time (if sbc_iformulat=1). Parameters: YYYY(p)MM(p)DD(p),YYYY(i)MM(i)DD(i),YYYY(i-1)MM(i-1)DD(i-1),YYYY(i+1)MM(i+1)DD(i+1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: NOTUSED</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileAtmMesh_filebase_tauV</code></div>
    <div class="col-8 pr-0"><p>Parametric filename for the Meridional Wind Stress datasets before the spinup-time (if sbc_iformulat=1). Parameters: YYYY(p)MM(p)DD(p),YYYY(i)MM(i)DD(i),YYYY(i-1)MM(i-1)DD(i-1),YYYY(i+1)MM(i+1)DD(i+1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: usr</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileAtmMesh_filebase_qtot</code></div>
    <div class="col-8 pr-0"><p>Parametric filename for the Total Heat Flux datasets before the spinup-time (if sbc_iformulat=1). Parameters: YYYY(p)MM(p)DD(p),YYYY(i)MM(i)DD(i),YYYY(i-1)MM(i-1)DD(i-1),YYYY(i+1)MM(i+1)DD(i+1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: usr</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileAtmMesh_filebase_qsr</code></div>
    <div class="col-8 pr-0"><p>Parametric filename for the Solar Radiation Penetration datasets before the spinup-time (if sbc_iformulat=1). Parameters: YYYY(p)MM(p)DD(p),YYYY(i)MM(i)DD(i),YYYY(i-1)MM(i-1)DD(i-1),YYYY(i+1)MM(i+1)DD(i+1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: usr</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileAtmMesh_filebase_emp</code></div>
    <div class="col-8 pr-0"><p>Parametric filename for the Mass Flux Exchanged datasets before the spinup-time (if sbc_iformulat=1). Parameters: YYYY(p)MM(p)DD(p),YYYY(i)MM(i)DD(i),YYYY(i-1)MM(i-1)DD(i-1),YYYY(i+1)MM(i+1)DD(i+1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: usr</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileAtmMesh_filebase_tempS</code></div>
    <div class="col-8 pr-0"><p>Parametric filename for the Surface Temperature datasets before the spinup-time (if sbc_iformulat=1). Parameters: YYYY(p)MM(p)DD(p),YYYY(i)MM(i)DD(i),YYYY(i-1)MM(i-1)DD(i-1),YYYY(i+1)MM(i+1)DD(i+1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: usr</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileAtmMesh_filebase_salS</code></div>
    <div class="col-8 pr-0"><p>Parametric filename for the Surface Salinity datasets before the spinup-time (if sbc_iformulat=1). Parameters: YYYY(p)MM(p)DD(p),YYYY(i)MM(i)DD(i),YYYY(i-1)MM(i-1)DD(i-1),YYYY(i+1)MM(i+1)DD(i+1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: usr</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileAtmMesh_filebase_umid</code></div>
    <div class="col-8 pr-0"><p>Parametric filename for the Air Umidity datasets before the spinup-time (if sbc_iformulat=1). Parameters: YYYY(p)MM(p)DD(p),YYYY(i)MM(i)DD(i),YYYY(i-1)MM(i-1)DD(i-1),YYYY(i+1)MM(i+1)DD(i+1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: usr</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileAtmMesh_filebase_radLW</code></div>
    <div class="col-8 pr-0"><p>Parametric filename for the Long Wave Radiation datasets before the spinup-time (if sbc_iformulat=1). Parameters: YYYY(p)MM(p)DD(p),YYYY(i)MM(i)DD(i),YYYY(i-1)MM(i-1)DD(i-1),YYYY(i+1)MM(i+1)DD(i+1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: usr</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileAtmMesh_filebase_radSW</code></div>
    <div class="col-8 pr-0"><p>Parametric filename for the Short Wave Radiation datasets before the spinup-time (if sbc_iformulat=1). Parameters: YYYY(p)MM(p)DD(p),YYYY(i)MM(i)DD(i),YYYY(i-1)MM(i-1)DD(i-1),YYYY(i+1)MM(i+1)DD(i+1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: usr</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileAtmMesh_filebase_snow</code></div>
    <div class="col-8 pr-0"><p>Parametric filename for the Solid Precipitation datasets before the spinup-time (if sbc_iformulat=1). Parameters: YYYY(p)MM(p)DD(p),YYYY(i)MM(i)DD(i),YYYY(i-1)MM(i-1)DD(i-1),YYYY(i+1)MM(i+1)DD(i+1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: usr</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileAtmMesh_lcompression</code></div>
    <div class="col-8 pr-0"><p>(=True) if the datasets you want to download are gzip compressed files (*.gz).</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: False</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileAtmMesh_llonFlip</code></div>
    <div class="col-8 pr-0"><p>(=True) if the longitude coord. is in the 0 to 360 range (=False) if longitude is in -180:+180 range.</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: False</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileAtmMesh_llatInv</code></div>
    <div class="col-8 pr-0"><p>(=True) if the dataset contains latitude decreasing through the pole.</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">fileAtmMesh_lkeepSrcFull</code></div>
    <div class="col-8 pr-0"><p>(=True) if you want to keep in your disk the downloaded uncutted datasets.</p>
    <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>

### **Section set_dataDownlAtmMesh_varName**

<p>This section of the JSON file contains the parameters for the VARIABLE-NAMEs of the input atmospheric meshmask datasets.</p>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">srcDimAtmMesh_lon</code></div>
    <div class="col-8 pr-0"><p>Name of the dimension for the longitude.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: lon</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">srcDimAtmMesh_lat</code></div>
    <div class="col-8 pr-0"><p>Name of the dimension for the latitude.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: lat</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">srcDimAtmMesh_time</code></div>
    <div class="col-8 pr-0"><p>Name of the dimension for the time.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: time</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">srcCrdAtmMesh_lon</code></div>
    <div class="col-8 pr-0"><p>Name of the coordinate variable containing the longitude.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: lon</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">srcCrdAtmMesh_lat</code></div>
    <div class="col-8 pr-0"><p>Name of the coordinate variable containing the latitude.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: lat</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">srcCrdAtmMesh_time</code></div>
    <div class="col-8 pr-0"><p>Name of the variable containing time coordinate.</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: time</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">srcVarAtmMesh_mask</code></div>
    <div class="col-8 pr-0"><p>Name of the variable containing the Land Sea Mask (if sbc_iformulat=0,2).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: LSM</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">srcVarAtmMesh_lont</code></div>
    <div class="col-8 pr-0"><p>Name of the variable containing longitude coordinate of T-points (if sbc_iformulat=1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: NOTUSED</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">srcVarAtmMesh_lonu</code></div>
    <div class="col-8 pr-0"><p>Name of the variable containing longitude coordinate of U-points (if sbc_iformulat=1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: NOTUSED</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">srcVarAtmMesh_lonv</code></div>
    <div class="col-8 pr-0"><p>Name of the variable containing longitude coordinate of V-points (if sbc_iformulat=1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: NOTUSED</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">srcVarAtmMesh_latt</code></div>
    <div class="col-8 pr-0"><p>Name of the variable containing latitude coordinate of T-points (if sbc_iformulat=1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: NOTUSED</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">srcVarAtmMesh_latu</code></div>
    <div class="col-8 pr-0"><p>Name of the variable containing latitude coordinate of U-points (if sbc_iformulat=1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: NOTUSED</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">srcVarAtmMesh_latv</code></div>
    <div class="col-8 pr-0"><p>Name of the variable containing latitude coordinate of V-points (if sbc_iformulat=1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: NOTUSED</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">srcVarAtmMesh_maskt</code></div>
    <div class="col-8 pr-0"><p>Name of the variable containing the Land Sea Mask of T-points (if sbc_iformulat=1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: NOTUSED</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">srcVarAtmMesh_masku</code></div>
    <div class="col-8 pr-0"><p>Name of the variable containing the Land Sea Mask of U-points (if sbc_iformulat=1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: NOTUSED</p></div>
</div>
<div class="row mx-0">
    <div class="col-3 pl-0"><code class="mycode">srcVarAtmMesh_maskv</code></div>
    <div class="col-8 pr-0"><p>Name of the variable containing the Land Sea Mask of V-points (if sbc_iformulat=1).</p>
    <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: NOTUSED</p></div>
</div>
