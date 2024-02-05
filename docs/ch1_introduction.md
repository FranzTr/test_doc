# **Introduction**

<div style="text-align: justify">
    <p>The Structured and Unstructured grid Relocatable ocean platform for Forecasting (SURF) is an open-source package designed to generate high-resolution, nested model set-ups for oceanic forecasts over limited domains of interest. It is designed to be set up by relatively non-expert users in any region of the World Ocean using a configuration file. The package will enable limited area ocean forecasts to be run on any commercially available personal computer or laptop.
    SURF requires coarser-resolution ocean forecasts for the initial and boundary conditions and atmospheric forcing to force the circulation. </p>
    <p>This User Guide describes the overall design of the structured grid component of the SURF platform based on the
    <a href="https://www.nemo-ocean.eu" target="_blank">NEMO</a> ocean model (SURF-NEMO).
    In addition to step-by-step information about running the platform, the User Guide gives a detailed description of the scripts organization and the data structures, so that SURF can be modified/integrated by users.
    This User Guide gives also provides a case study using available input datasets for bathymetry, the coastline, atmospheric forcing, and the coarser-resolution parent ocean model along with output datasets to check the correct implementation of the software.</p>
    <p>Information about the SURF numerical platform is also provided on the home page</p>
    <p><a class="reference external" href="https://www.surf-platform.org" target="_blank">https://www.surf-platform.org</a></p>
    <p>SURF also contains the unstructured grid model SHYFEM, which will be explained in a future update of the User Guide.</p>
</div>

## **Relocatable ocean modelling system**

<div style="text-align: justify">
    SURF-NEMO (Trotta et al. 
    <a href="https://doi.org/10.1016/j.dsr2.2016.05.004" class="text-decoration-none" target="_blank">2016</a>,
    <a href="https://doi.org/10.3389/fmars.2021.642815" class="text-decoration-none" target="_blank">2021</a>)
    provides a numerical platform for forecasting hydrodynamic and thermodynamic
    fields at high spatial and temporal resolutions. SURF-NEMO is designed to be embedded in any region of a larger-scale
    ocean prediction system, at coarser-resolution, and includes multiple nesting capabilities (i.e., consecutive nested
    models can be implemented with increasing grid resolutions), starting with the first nesting in a large-scale ocean
    model and reaching horizontal grid resolutions of a few hundred metres. For each nesting, the parent coarse-grid model
    provides the initial and lateral boundary conditions for the SURF child components.</p>

    <p>This relocatable ocean model system is intended to be a valuable tool that supports other Decision Support System
    (DSS) that may require hydrodynamic, temperature and salinity forecasts at high resolution, such as oil spill monitoring,
    search and rescue operations, navigation routing, fisheries and tourism.</p>

</div>

## **Virtual Machine Environment**

<div style="text-align: justify">
    <p>SURF-NEMO is based on a virtual machine environment in which the hydrodynamic NEMO model and several pre-
    and post-processing tools are connected to the required input fields and the numerical outputs of the limited area simulation.
    The Installation Chapter <a href="#download-and-install-surf-virtual-machine">(6.1)</a> provides details of
    how to download and install the package.</p>
    <p>A virtual machine is a software-based computer that enables the emulation of operating systems with
    "virtual" access to hardware resources such as CPU, RAM, networking and storage. The operating
    system that runs inside a virtual machine is called the <em>guest</em>, which appears in a window on your computer's
    own operating system, commonly referred to as the <em>host</em>.</p>
    <p>The virtualization software used is the free and open-source Oracle VM VirtualBox package, on which
    the Debian Linux operating system was installed.</p>
    <p>Virtual machines offer many advantages and can encapsulate an entire PC environment including the operating
    system, applications and all data, inside a single file. As a packaged application, it is easier to set up
    than installing a full suite of software that must work together. The virtual machine can be distributed
    as a ready-made and fully configured system, anf thus has advantages for configuration and distribution.
    A virtual machine can also run on various hardware platforms.</p>
</div>

## **Source Code**

<div style="text-align: justify">
    <p>The SURF source codes are contained in a package distributed as a tar.gz archive. The archive
    contains the NEMO code, the pre- and post-processing codes and a template user-configuration file.
    The Installation Chapter <a href="#download-and-install-surf-packages">(6.2)</a> describes how to download
    and install the package.</p>
    <p>NEMO consists of open-source code written in Fortran 90 and is parallelized with a domain decomposition using
    the MPI library. The model outputs from the SURF-NEMO simulations are all in NetCDF format.</p>
    <p>The pre- and post-processing code are developed in Julia, NCL, Python and Fortran programming languages.
    The NetCDF Operator (NCO) and Climate Data Operators (CDO) are used to facilitate the manipulation of the NetCDF datasets.
    These tools are specifically developed and optimised for SURF to reduce the computation latency and to ensure
    efficient memory usage. Currently, pre- and post-processing can only be run in serial mode
    (i.e., only executed on one processor). The structure of the SURF source code package is shown in
    <a href="#appB_structure-of-the-surf-directory">appendix B</a>.</p>
</div>
