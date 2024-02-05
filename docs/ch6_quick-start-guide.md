# **Getting Started with SURF-NEMO**

<div style="text-align: justify">
This chapter describes how you can quickly get started with the SURF platform. We show how to download and install the SURF Virtual Machine and all the SURF packages. We describe how to compile (if needed) the source codes.
We present how to execute a case study (template) experiment in the Gulf of Taranto and view the results.
Finally we show how the user-configuration file of a template experiment can be modified in order to
execute and analysis new experiments.
The template experiment makes it easier to run the model without detailed knowledge of the underlying
scientific basis. Only a limited number of default values need to be changed for most applications.
A more specific scientific background is required if for example, the user intends to perform experiments with different turbulence or numerical schemes or with alternative settings of model parameters.
It is then recommended to read first the NEMO Model Description document and relative article.
See also the video tutorials available online <a href="https://www.surf-platform.org/tutorial.php" target="_blank">here</a> explain the basic features of the SURF platform and designed for beginners who want to learn SURF step by step.
</div>

## **Download and Install SURF Virtual Machine**

<div style="text-align: justify">
The SURF platform will be provided as a Virtual Machine (VM). It is packaged and distributed as a ZIP Compressed Archive file (with a .zip extension).
The general scheme adopted to manage the versions provides that the releases contain in the name indications of the version in the format:
```bash
surf_vm_VERSION.zip
```
where VERSION is a number (e.g. surf_vm_1.01.zip for the current version). The instructions below explain how to download, install and configure the SURF VM in Oracle VirtualBox

<div class="row mx-0">
  <div class="col-6 ps-0">
    <ul>
        <li>Navigate to <a target="_blank" href="https://www.virtualbox.org/">https://www.virtualbox.org/</a> and click on <em>Downloads</em> button.
        Choose the <code>VirtualBox base package</code> (version &gt;=6) corresponding to the host
        operating system of your computer (i.e. Windows, Mac, Linux).
        Save the corresponding file on your computer, double-click it to open it, and follow the installation instructions.
        </li>
    </ul>
  </div>
  <div class="col-6 pr-0">
      <figure id="fig-vm-install0" class="figure text-center">
          <a href="../assets/img/VM_install_VitualBoxsite_v2.png">
            <img src="../assets/img/VM_install_VitualBoxsite_v2.png" alt="../assets/img/VM_install_VitualBoxsite_v2.png" width="100%">
          </a>
          <figcaption class="figurenum">Downloads VirtualBox base package.</figcaption>
      </figure>
  </div>
</div>

<div class="row mx-0">
  <div class="col-6 ps-0">
    <ul>
      <li>In addition to the base package, download also the <code>Extension Packs</code>.
          This package provides additional functionality to the base package, such as virtual USB device, remote desktop support, ecc.
          To install this extension, simply double-click on the package file and follow the installation instructions.
          Please install the same version extension pack as your installed version of the VirtualBox base package.
      </li>
    </ul>
  </div>
<div class="col-6 pr-0">
    <!-- <div class="d-flex justify-content-center"> -->
      <figure id="fig-vm-install0" class="figure text-center">
          <a href="../assets/img/VM_install_VirtualBoxExtentionPacks.png">
            <img src="../assets/img/VM_install_VirtualBoxExtentionPacks.png" alt="../assets/img/VM_install_VirtualBoxExtentionPacks.png" width="100%">
          </a>
          <figcaption class="figurenum">Downloads VirtualBox Extension Packs.</figcaption>
      </figure>
    <!-- </div> -->
  </div>
</div>

<div class="row mx-0">
  <div class="col-6 ps-0">
    <ul>
        <li>
          Download the current version (v1.01) of the SURF virtual machine from
          <a href="https://www.surf-platform.org/download.php" target="_blank">SURF web-page</a>.
          In the virtual machines is installed the Debian GNU/Linux 8.11 operating system.
          The Guest Additions have been also installed to optimize the guest operating system for better performance and usability.
          Extract than the package in your VirtualBox directory which Oracle VM VirtualBox creates in the current system user's home directory
          (i.e. <code>/Users/USERNAME/VirtualBox VMs/</code> for Mac user).
          ```bash
          unzip surf_1.01.zip
          ```
        </li>
    </ul>
  </div>
<div class="col-6 pr-0">
    <!-- <div class="d-flex justify-content-center"> -->
      <figure id="fig-vm-install1" class="figure text-center">
          <a href="../assets/img/VM_install_downlVMsurf.png">
            <img src="../assets/img/VM_install_downlVMsurf.png" alt="../assets/img/VM_install_downlVMsurf.png" width="100%">
          </a>
          <figcaption class="figurenum">Downloads SURF Virtual Machine.</figcaption>
      </figure>
    <!-- </div> -->
  </div>
</div>

<div class="row mx-0">
  <div class="col-6 ps-0">
    <ul>
        <li>Open the VirtualBox software. From the menu, choose <em>Machine</em> &gt; <em>add</em> and navigate to the file <code>surf.vbox</code>.
        This file is an XML file that contains settings of the Machine.
        This will add the Virtual Machine <code>surf</code> to the list of Virtual Machine</li>
    </ul>
  </div>
  <div class="col-6 pr-0">
    <!-- <div class="d-flex justify-content-center"> -->
      <figure id="fig-vm-install2" class="figure text-center">
          <a href="../assets/img/VM_install_openVMsurf.png">
            <img src="../assets/img/VM_install_openVMsurf.png" alt="../assets/img/VM_install_openVMsurf.png" width="100%">
          </a>
          <figcaption class="figurenum">Add SURF-VM in VirtualBox.</figcaption>
      </figure>
    <!-- </div> -->
  </div>
</div>

<div class="row mx-0">
  <div class="col-6 ps-0">
    <ul>
      <li>To start the VM surf, you can double-click on its entry in the list in the VirtualBox Manager window or select its entry and press the <em>Start</em> button at the top of the window. A window opens.
        The VM Login should look like the
        <a class="reference internal" href="#fig-vm-install3">
            <span class="std std-numref">figure 6.5</span>
        </a>.
        In the login dialogue box enter:
        <ul>
          <li><em>surf</em> as login</li>
          <li><em>surf2019</em> as an initial password</li>
        </ul>
        You are now logged into the VM.
      </li>
    </ul>
  </div>
  <div class="col-6 pr-0">
    <!-- <div class="d-flex justify-content-center"> -->
        <figure id="fig-vm-install3" class="figure text-center">
          <a href="../assets/img/VM_install_login.png">
              <img src="../assets/img/VM_install_login.png" alt="../assets/img/VM_install_login.png" width="100%">
          </a>
          <figcaption class="figurenum">Start SURF-VM.</figcaption>
        </figure>
    <!-- </div> -->
  </div>
</div>

</div>

### **Disk Partitions mounted on the SURF Virtual Machine**

<div style="text-align: justify">
The SURF Virtual Machine package contains two VDI (VirtualBox Disk Image) files:
<ul class="simple">
  <li><code>surf.vdi</code> containing the Debian GNU/Linux operating system (version 10.3)</li>
  <li><code>surf_scratch.vdi</code> thought to contain source code files, datasets sample and experiments.</li>
</ul>
From the guest operating system you can see the list of partitions by typing the following command:
```bash
sudo fdisk -l
```
It is divided into two main partitions:
<ul class="simple">
  <li>the disk <code>/dev/sda</code> "mounted" as filesystems to the root directory <code>/</code></li>
  <li>the disk <code>/dev/sdb</code> "mounted" in the directory <code>/scratch</code>.</li>
</ul>
Optionally you can mount other physical hard disks with VirtualBox (see the <a href="https://www.virtualbox.org/manual/ch05.html" target="_blank">VirtualBox Manual</a> for details).
VirtualBox has the ability to <b> mount a shared folder between host and guest</b>
in order to access files of your host system from within the guest system. There are a few steps involved:
<div class="row mx-0">
  <div class="col-6 ps-0">
      <ul>
        <li>Shut down the virtual OS before you can edit settings.</li>
        <li>Select the surf VM in the VirtualBox Manager and click Settings.</li>
        <li>Select Shared Folders, and click the Plus button to add a new shared folder. Specify the host folder you want to share.</li>
        <li>Select auto-mount and then click OK.</li>
        <li>You can now re-start the VM surf. The shared folder is mounted into the /media directory, along with the prefix "sf_".</li>
      </ul>
  </div>
  <div class="col-6 pr-0">
      <!-- <div class="d-flex justify-content-center"> -->
        <figure id="fig-vm-install3" class="figure text-center">
            <a href="../assets/img/VM_install_sharefolder.png">
              <img src="../assets/img/VM_install_sharefolder.png" alt="../assets/img/VM_install_sharefolder.png" width="100%">
            </a>
            <figcaption class="figurenum">Mount shared folders.</figcaption>
        </figure>
      <!-- </div> -->
  </div>
</div>

</div>

### **Changing Configuration on the SURF Virtual Machine**

<div style="text-align: justify">

By default, the VM surf is configurated as in table <a class="reference internal" href="#tab-configvm"> <span class="std std-numref">Table 6.1</span> </a>.
You can keep all defaults parameters or if it is not adequate for your application you can change settings.
To change the configuration you need to shut down the virtual OS before you can edit settings.

<div class="row mx-0">
  <div class="col-6 ps-0">
    <ul>
      <li>Select the surf VM in the VirtualBox Manager, right-click it and choose <em>Setting</em>.</li>
      <li>increase/decrease the number of cores based on your performance desires.</li>
      <li>increase/decrease the number of GB of RAM allocated to your VM according to the size of your computational domain.</li>
      <li>increase/decrease the video memory and scale factor of your screen</li>
    </ul>
  </div>
  <div class="col-6 pr-0">
      <div class="d-flex justify-content-center">
        <figure id="fig-vm-install4" class="figure text-center">
            <a href="../assets/img/VM_install4.png">
              <img src="../assets/img/VM_install4.png" alt="../assets/img/VM_install4.png" width="100%">
            </a>
            <figcaption class="figurenum">Change VM configurations.</figcaption>
        </figure>
      </div>
  </div>
</div>

If you want to add more storage space to a VM you can also expande the virtual hard disk. There are a few steps involved:

<div class="row mx-0">
  <div class="col-6 ps-0">
    <ul>
        <li> With the VM Power off, open a terminal and move to the location of the surf_scratch.vdi file that you want to resize,
        </li>
        <li> At the terminal prompt, type the command:
        ```bash
        VBoxManage modifyhd surf_scratch.vdi
         --resize SIZE_MB
        ```
        </li>
    </ul>
  </div>
  <div class="col-6 pr-0">
    <div class="d-flex justify-content-center">
        <figure id="fig-vm-install5" class="figure text-center">
          <a href="../assets/img/VM_install5.png">
              <img src="../assets/img/VM_install5.png" alt="../assets/img/VM_install5.png" width="100%">
          </a>
          <figcaption class="figurenum">Enlarge the virtual disk.</figcaption>
        </figure>
    </div>
  </div>
</div>

<div class="row mx-0">
  <div class="col-6 ps-0">
    <ul>
        <li> Restart the SURF VM and open the GParted application from the Application Menu </li>
        <li> Select the /dev/sdb partition (an unlocated drive space is now available). Resize to the unalocated area</li>
    </ul>
  </div>
  <div class="col-6 pr-0">
    <!-- <div class="d-flex justify-content-center"> -->
        <figure id="fig-vm-install5" class="figure text-center">
          <a href="../assets/img/VM_install5.png">
              <img src="../assets/img/VM_install5.png" alt="../assets/img/VM_install5.png" width="100%">
          </a>
          <figcaption class="figurenum">Enlarge the virtual disk.</figcaption>
        </figure>
    <!-- </div> -->
  </div>
</div>

<table class="table table-hover" id="tab-configvm">
  <caption class="text-center"> Table 6.1 Virtual Machine Summary Fields. </caption>
  <thead>
  <tr>
    <th>Parameter</th>
    <th>Description</th>
    <th>Values</th>
  </tr>
  </thead>
  <tbody>
  <tr>
    <td>Name</td>
    <td>Name given the VM</td>
    <td>surf</td>
  </tr>
  <tr>
    <td>Guest OS</td>
    <td>Operating system running on this VM</td>
    <td>Debian Linux</td>
  </tr>
  <tr>
    <td>Memory</td>
    <td>Amount of memory available to this VM</td>
    <td>2 [GB]</td>
  </tr>
  <tr>
    <td>Cores</td>
    <td>Number of CPU cores being used by this VM</td>
    <td>2</td>
  </tr>
  <tr>
    <td>Disk Capacity</td>
    <td>Total disk capacity available to this VM</td>
    <td>40 [GB]</td>
  </tr>
  <tr>
    <td>Network Adapters</td>
    <td>Number of network adapters available to this VM</td>
    <td>1</td>
  </tr>
  <tr>
    <td>IP Address</td>
    <td>IP address assigned to the VM</td>
    <td>x</td>
  </tr>
  </tbody>
</table>

</div>

## **Download and Install SURF packages**

<div style="text-align: justify">
Once logged in, open a new terminal window and go to the directory <code>/scratch</span></code>.
The scratch directory follows the directory structure as shown in <a href="#fig-surftree">Fig. B.1</a>. The VM you have installed does not contain the SURF
packages (source codes and static datasets) and you need to download and install them. The SURF packages are
packaged and distributed as a GZIP Compressed Tar Archive file (with a .tar.gz extension). The general scheme
adopted to manage the versions provides that the releases contain in the name indications of the version in
the format:
```bash
packageName_<VERSION>.tar.gz
```
where &ltVERSION&gt is a number (e.g. <i>surf_nemo_1.01.tar.gz</i> for the current version of the surf_nemo package).
The instructions below explain how to install the package in the VM:
<ul>
    <li>
      Once logged in the VM surf, download the current version of the SURF-NEMO (surf_nemo_1.01.tar.gz)
      and SURF-DATASETS (surf_datasets_1.01.tar.gz) packages directly from the
      <a class="reference external" href="https://www.surf-platform.org">SURF web-page</a>
      and save it in the directory <code>/scratch/surf/surf_install/releases/</code>
      (for simplicity, we abbreviate this location as <code>$SURF_RELEASES</code>).
    </li>
    <li>
      Go to the directory <code>$SURF_RELEASES</code> and run the installation bash script
      <code>install.sh</code> followed by the package name. For the SURF-NEMO packages type:
      ```bash
      cd $SURF_RELEASES ; install.sh surf_nemo_1.01.tar.gz
      ```
      For the SURF-DATASETS packages type:
      ```bash
      cd $SURF_RELEASES ; install.sh surf_datasets_1.01.tar.gz
      ```
      The installation process will extract the archive in the directory <code>/scratch/surf/surf_nemo/</code> and
      <code>/scratch/surf/surf_datasets/</code>, respectively, and will create a symbolic link <code>current</code> in this directory
      that points to the extracted folder (for simplicity, we abbreviate this location as <code>$SURF_NEMO</code>, <code>$SURF_DATASETS</code>, respectively).
    </li>
</ul>
For a detailed description of the directory structure and contents of each package refer to the <a href="#appB_Scratch-Partition-and-its-directory-structures">Appendix B</a>.
</div>

## **Compiling the source code**

<div style="text-align: justify">

After the installation of the SURF-NEMO package is finished, you need to compile the source codes in order
to create the executable files needed to perform specific tasks. The executable files should not be recreated
unless you need to modify the source code. The compilation is performed with the Unix/Linux make utility
using the following tools: (1) fortran 90 compiler, (2) C-preprocessor cpp, (3) a compiled MPI library for
simulations in parallel mode. (4) a compiled netCDF library to read and write data in portable netCDF
format. All these tools are already present and compiled in the SURF platform.
To compile the source codes go to the directory <code>/scratch/surf/surf_nemo/current/scripts/</code> and run the compilation bash script <code>compile.sh</code> followed by the package name (or by the word 'all' to compile all the packages):

```bash
cd /scratch/surf/surf_nemo/current/scripts; ./compile_codes.sh all
```

Compilation could take a few minutes and it will create the executable files for each program present in the SURF-NEMO package.

</div>

## **Running the case study: Gulf of Taranto**

<div style="text-align: justify">

As case study we implement the SURF platform in the Gulf of Taranto in the northern Ionian Sea (fig xx).
The nesting simulation starts on 5 October 2014 at 00:00 and run until 7 October 2014 at 24:00.
In order to execute this case study experiment, you can follow these steps:

<ul>
    <li>
      Download the input datasets (gulfTaranto_20141005.tar.gz) of this case study directly from the web-repository
      (<a class="reference external" href="https://www.surf-platform.org">https://www.surf-platform.org</a>)
      and extract it in the directory <code>/scratch/surf/indata_offline/</code>
      ```bash
      tar -zxvf gulfTaranto_20141005.tar.gz
      ```
      Note If you want to change the local repository path to some other location of your choice make sure to change the path in the configuration file.
    </li>
    <li>
      Create a new folder in the directory <code>/scratch/from_GUI/</code> and let's call it gulfTaranto_20141005.
      This is the Experiment ID name which uniquely identifies the experiment.
      ```bash
      cd /scratch/from_GUI/; mkdir gulfTaranto_20141005
      ```
    </li>
    <li>
      Copy the template configuration file <code>/scratch/surf/surf_nemo/current/setParFree.json</code> in the
      directory <code>/scratch/from_GUI/gulfTaranto_20141005/</code> which contains the configuration for this case study.
      ```bash
      necd; cp setParFree.json /scratch/from_GUI/gulfTaranto_20141005/
      ```
    </li>
    <li>
      After that, from the directory <code>/scratch/surf/surf_nemo/current/scripts/</code>, you just need to execute
      the Julia script <code>run_exp.jl</code> followed by the experiment ID <code>gulfTaranto_20141005</code>
      ```bash
      julia run_exp.jl gulfTaranto_20141005
      ```
      This will create the folder gulfTaranto_20141005 in the directory <code>/scratch/surf/experiments/</code>
      with a directory tree as in fig.x.1 (refer to the <a href="#appB_Scratch-Partition-and-its-directory-structures">Appendix B</a> for more details)
    </li>
</ul>
You can activate/deactivate specific tasks by setting logical parameters to True/False
in the section <code>set_lrun</code> of the configuration file <code>setParFree.json</code>
<div class="row mx-0">
  <div class="col-6 ps-0">
      <code>lrun_childMeshmask</code> to  enable the execution of the CHILD-MESHMASK GENERATION task. <br>
      <code>lrun_regridPreAtm</code> to enable the execution of the ATMOSPHERIC-DATA-REGRIDDING task. <br>
      <code>lrun_regridPreOceIC</code> to enable the execution of the OCEAN-IC-DATA-REGRIDDING task. <br>
      <code>lrun_regridPreOceBC</code> to enable the execution of the OCEAN-BC-DATA-REGRIDDING task. <br>
      <code>lrun_regridPreWeights</code> if you want to compute (=True) or just copy (=False) the WEIGHT-FILEs for REMAPPING in the Regridding phase. <br>
      <code>lrun_ocean</code> to enable the execution of the NEMO code.

  </div>

  <div class="col-6 pr-0" style="font-size:16px">
    <div class="highlight-JSON">
<pre><code class="mycode">{
&quot;id&quot;:&quot;A001&quot;,&quot;title&quot;:&quot;set_lrun&quot;,
"items": [
      {"name": "lrun_childMeshMask",
      "value": "True"
      },
      {"name": "lrun_regridPreAtm",
      "value": "True"
      },
      {"name": "lrun_regridPreOceIC",
      "value": "True"
      },
      {"name": "lrun_regridPreOceBC",
      "value": "True"
      },
      {"name": "lrun_regridPreWeights",
      "value ": "True"
      },
      {"name": "lrun_ocean",
      "value": "True"
      }
   ]
}
</code></pre>
    </div>
  </div>

</div>

</div>

## **Post-processing the results**

<div style="text-align: justify">

The surf package is provided together with open source tools for data visualization and post-processing your data.
You will find the free software packages NcView with a graphical user interface
and a suite of procedure using NCAR Graphics package with NCL and Python interface you can call from Command Line.
However, it is very well possible to use other (free or commercial)
graphic software such as Pynoply or several scripting languages such as Julia, IDL, Matlab, as long
as they can read the netCDF format.

</div>

### **Visualizing the results with Ncview**

<div style="text-align: justify">

Ncview is a tool for visualizing netCDF data files. It is very easy to use, because of its graphical user interface.
However, its possibilities are limited. Typically you would use ncview to get a quick and easy, push-button
look at your netCDF files. You can view simple movies of the data, view along various dimensions, take a
look at the actual data values, change colour maps, invert the data, etc.
In order to start this program type ncview followed by the filename of the dataset you want to visualize,
example type the following command:

```bash
ncview SURF_1h_20141006_20141006_grid_T.nc
```

An example of the user interface in NcView is given in figure <a href="#fig-ncview">Fig. 6.7</a>

<div class="d-flex justify-content-center">
  <figure id="fig-ncview" class="figure text-center">
      <a href="../assets/img/ncview.png">
        <img src="../assets/img/ncview.png" alt="../assets/img/ncview.png" width="100%">
      </a>
      <figcaption class="figurenum">Screenshot of using NcView.</figcaption>
  </figure>
</div>

</div>

### **Analyzing and Visualizing results using NCAR graphic packages**

<div style="text-align: justify">

NCAR Graphics is a collection of graphics libraries that support the display of scientific data. One possible
interface available for visualizing data with these libraries is with the NCAR Command Language (NCL),
an open-source interpreted programming language, developed at NCAR and designed for the analysis and
visualization of geoscientific data.
The SURF-NEMO package include, as postprocessing, a suite of NCL functions to visualize the input/output
datasets, compare the child/parent fields, compare the simulation result with in-situ or satellite datasets and
convert datasets.

<figure class="figure text-center">
  <div class="d-flex justify-content-center">
      <figure id="fig-test1-velxy">
        <a href="../assets/img/velxy_z000_t035.png">
            <img src="../assets/img/velxy_z000_t035.png" alt="../assets/img/velxy_z000_t035.png" width="100%">
        </a>
        <figcaption>(A) Surface current.</figcaption>
      </figure>
      <figure id="fig-test1-tempxy">
        <a href="../assets/img/tempxy_z000_t035.png">
            <img src="../assets/img/tempxy_z000_t035.png" alt="../assets/img/tempxy_z000_t035.png" width="100%">
        </a>
        <figcaption>(B) Surface temperature.</figcaption>
      </figure>
      <figure id="fig-test1-tempxz">
        <a href="../assets/img/tempxz_y000_t035.png">
            <img src="../assets/img/tempxz_y000_t035.png" alt="../assets/img/tempxz_y000_t035.png" width="100%">
        </a>
        <figcaption>(C) Cross-section of temperature.</figcaption>
      </figure>
  </div>
  <figcaption class="figurenum">Example figure generated using NCAR graphic packages.</figcaption>
</figure>

In order to Post-processing the results of an existing experiment, you need to execute the Julia script
<code>run_postProc.jl</code> followed by the experiment ID. Example for the case study experiment type the following command:

```bash
julia run_postproc.jl gulfTaranto_20141005
```

You can activate/deactivate specific tasks by setting logical parameters to True/False in the sections
<code>set_lrun_post</code> and <code>set_visual_lplot</code> of the configuration file <code>setParFree.json</code>

<div class="row mx-0">
  <div class="col-6 ps-0">
    <code>lrun_visDom</code> to  enable the plotting of the user-defined domains.<br>
    <code>lrun_visIndata</code> to  enable the plotting of the Indata Bat, Atm, OceIC, OceBC fields.<br>
    <code>lrun_visExtrapdata</code> to enable the plotting of the Extrapdata Atm, OceIC, OceBC fields.<br>
    <code>lrun_visRegriddata</code> to enable the execution of the OCEAN-IC-DATA-REGRIDDING task.<br>
    <code>lrun_visOutdata</code> to enable the execution of the OCEAN-BC-DATA-REGRIDDING task.<br>
    <code>lrun_chlVSpar</code> if you want to compute (=True) or just copy (=False) the WEIGHT-FILEs for REMAPPING in the Regridding phase.<br>
    <code>lrun_surfVSctd</code> enables the execution of the NEMO code.<br>
    <code>lrun_surfVSsat</code> enables the execution of the NEMO code.<br>
    <code>lrun_surfVSmooring</code> enables the execution of the NEMO code.<br>
    <code>lrun_surfVSferrybox</code> enables the execution of the NEMO code.<br>
  </div>
  <div class="col-6 pr-0" style="font-size:16px">
    <div class="highlight-JSON">
<pre><code class="mycode">{
  &quot;id&quot;:&quot;B000&quot;,&quot;title&quot;:&quot;set_lrun_post&quot;,
  "items": [
     {"name": "lrun_visDom",
     "value": "True"
     },
     {"name": "lrun_visIndata",
     "value": "True"
     },
     {"name": "lrun_visExtrapdata",
     "value": "True"
     },
     {"name": "lrun_visRegriddata",
     "value": "True"
     },
     {"name": "lrun_visOutdata",
     "value ": "True"
     },
     {"name": "lrun_chlVSpar",
     "value": "True"
     },
     {"name": "lrun_surfVSctd",
     "value": "True"
     },
     {"name": "lrun_surfVSsat",
     "value": "True"
     },
     {"name": "lrun_surfVSmooring",
     "value": "True"
     },
     {"name": "lrun_surfVSferrybox",
     "value": "True"
     }
  ]
}
</code></pre>
    </div>
  </div>
</div>

<div class="row mx-0">
  <div class="col-6 ps-0">
    <code>lplotMesh</code> to  enable plotting of the Child MeshMask fields.<br>
    <code>lplotBat</code> to enable the plotting of the Bathymetry fields.<br>
    <code>lplotAtm</code> to enable the plotting of the Atmospheric fields.<br>
    <code>lplotOceIC</code> to enable the plotting of the Initial Condition Ocean fields.<br>
    <code>lplotOceBC</code> to enable the plotting of the Open Boundary Condition Ocean fields.<br>
    <code>lplotOceBCbdy</code> to enable the plotting of the Open Boundary Condition Ocean fields.<br>
    <code>lplotOceOut</code> to enable the plotting of the Output Ocean fields.<br>
  </div>
  <div class="col-6 pr-0" style="font-size:16px">
    <div class="highlight-JSON">

<pre><code class="mycode">{
   &quot;id&quot;:&quot;B001&quot;,&quot;title&quot;:&quot;set_visual_lplot&quot;,
      "items": [
      {"name": "lplotMesh",
      "value": "True"
      },
      {"name": "lplotBat",
      "value": "True"
      },
      {"name": "lplotAtm",
      "value": "True"
      },
      {"name": "lplotOceIC",
      "value": "True"
      },
      {"name": "lplotOceBC",
      "value": "True"
      },
      {"name": "lplotOceBCbdy",
      "value": "True"
      },
      {"name": "lplotOceOut",
      "value": "True"
      }
   ]
}
</code></pre>

    </div>

  </div>

</div>

</div>

### **Make a new experiments**

Let's assume you want to study the circulation of the Sermilik fjord in Greenland
from 1 February 2017 at 00:00 to 7 February 2017 at 24:00 ... add more details.

<ul>
  <li>
      Choose the name of experiment ID (e.g. <code>greenlandFjord_20170201</code>) and create the folder
      ```bash
      cd /scratch/from_GUI/; mkdir greenlandFjord_20170201
      ```
  </li>
  <li>
      Copy the template configuration file <code>/scratch/surf/surf_nemo/current/setParFree.json</code> in the
      directory <code>/scratch/from_GUI/greenlandFjord_20170201</code>
      ```bash
      cp /scratch/surf/surf_nemo/current/setParFree.json ./greenlandFjord_20170201/
      ```
  </li>
  <li>
      Modify the user configuration file <code>setParFree.json</code> according to your needs
      <code class="mycode">
        param1 = xxx <br>
        param2 = xxx <br>
        param3 = xxx <br>
        param4 = xxx
      </code>
  </li>
  <li>
      From the directory <code>/scratch/surf/surf_nemo/current/scripts/</code>, execute
      the Julia script <code>run_exp.jl</code> followed by the experiment ID <code>greenlandFjord_20170201</code>
      ```bash
      cd /scratch/surf/surf_nemo/current/scripts/;
      julia run_exp.jl greenlandFjord_20170201
      ```
  </li>
  <li>
      After running the simulation, you can display the simulation results by using
      the Julia script <code>run_postproc.jl</code> followed by the experiment ID <code>greenlandFjord_20170201</code>
      ```bash
      cd /scratch/surf/surf_nemo/current/scripts/;
      julia run_postproc.jl greenlandFjord_20170201
      ```
  </li>
</ul>
In principle you can simply use the template model and modify it to your needs, and not be too much
concerned with the input files they create. But our advice is never to use the template model as black boxes.
It is therefore important to understand how the codes work, which options they have and how their input
files are structured.

### **Multiple downscaling experiments**

SURF-NEMO package includes multiple nesting capability (i.e. consecutive nested models can be
implemented with increasing grid resolutions).
Let's assume you want to downscale from an existing experiment (e.g. from the template experiment
<code>gulfTaranto_20141005</code>)
in order to increase the spatial resolution to 800m ... add details.

<ul>
  <li>
      Go to the existing experiment directory
      ```bash
      cd /scratch/surf/experiments/gulfTaranto_20141005/
      ```
  </li>
  <li>
      Modify the user configuration file <code>setParFree.json</code> according to your needs
      <code class="mycode">
        param1 = xxx <br>
        param2 = xxx <br>
        param3 = xxx <br>
        param4 = xxx
      </code>
  </li>
  <li>
      From the directory <code>/scratch/surf/experiments/gulfTaranto_20141005/code/ocean/scripts/</code>,
      execute the Julia script <code>run_exp.jl</code> followed by the experiment ID <code>gulfTaranto_20141005</code>
      ```bash
      cd /scratch/surf/experiments/gulfTaranto_20141005/code/ocean/scripts/;
      julia run_exp.jl gulfTaranto_20141005
      ```
  </li>
  <li>
      After running the simulation, you can display the simulation results by using the julia script
      <code>run_postproc.jl</code> followed by the experiment ID <code>gulfTaranto_20141005</code>
      ```bash
      julia run_postproc.jl gulfTaranto_20141005
      ```
  </li>
</ul>
