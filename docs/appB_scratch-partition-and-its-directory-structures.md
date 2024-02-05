# **Scratch Partition and its directory structures**

<p> As shown in  <a href="#disk-partitions-mounted-on-the-surf-virtual-machine">chapter 6.1.1</a>
the VM surf is divided into two partitions:
the disk <code>/dev/sda</code> "mounted" in the root directory <code>/</code> and
the disk <code>/dev/sdb</code> "mounted" in the directory <code>/scratch</code>.
The scratch partition contains all the SURF packages and follows
the directory structure as shown in <a href="#fig-surftree">figure B.1</a>: The up-to-date version release is structured as follow:</p>
<ul>
    <li>
        The directory <code>surf_install/</code> contains the utilities necessary to manage all the operations of creation
        and installation of each package of the SURF platform.
    </li>
    <li>
        The directory <code>surf_datasets/</code> contains a list of static input datasets needed to run the SURF_NEMO
        package. With 'static' we mean here datasets which do not depend on the selected simulation
        period; i.e. bathymetry, coastline, parent meshmask, weight for remapping, meshmask and bathymetry
        remapped on the child grid.
    </li>
    <li>
        The directory <code>surf_nemo/</code> contains the sources code of the SURF-NEMO package.
    </li>
    <li>
        The directory <code>experiments/</code> contains all the experiments you have executed.
    </li>
</ul>
<p>We describe here the contents of these directories.</p>

<div class="d-flex justify-content-center">
    <figure id="fig-surftree">
        <a href="../assets/img/surf_tree01.png">
        <img src="../assets/img/surf_tree01.png" alt="../assets/img/surf_tree01.png" width="100%">
        </a>
        <figcaption>Fig. B.1 SURF package directories tree.</figcaption>
    </figure>
</div>

## **The surf_install directory structure**

<p>The SURF-INSTALL package is pre-installed in the SURF platform and it is located in the directory
<code>/scratch/surf/surf_install</code>. The folder <code>surf_install_1.00</code> has the directory
structure as in <a href="#fig-surftree">figure B.1</a>:</p>
<ul>
    <li>The folder <code>scripts/</code> containing the bash scripts to install (<code>install.sh</code>)
    and to create (<code>dorelease.sh</code>) packages release.</li>
    <li>The text file <code>ChangeLog.txt</code> containing documentation of all notable changes to the 'surf_install' package.</li>
    <li>The text file <code>ReadMe.txt</code> describing of the contents of the 'surf_install' package.</li>
    <li>The bash file <code>vertion.sh</code> containing the version number of the 'surf_install' package.
    This number is displayed in the upper-right corner of VM desktop</li>
</ul>

## **The surf_nemo directory structure**

<p>Once installed (see  <a href="#download-and-install-surf-packages">section 6.2</a>),
the SURF-NEMO package is located in the directory <code>/scratch/surf/surf_nemo/</code>.
The folder <code>surf_nemo_1.00</code> has the directory structure as in <a href="#fig-surftree">figure B.1</a>:</p>

<ul>
    <li>
    The folder <code>nemo/</code> contains the source code of the NEMO ocean model (v3.6).
    </li>
    <li>
    The folder <code>scripts/</code> contains the scripts for the pre- and post-processing needed to execute the relocatable SURF model.
    </li>
    <li>
    The folder <code>utilities/</code> contains the source code of several utility functions used for specific tasks in the pre-/post-processing.
    </li>
    <li>
    The json file <code>setParFree.json</code> of the template configuration file for the case study experiment.
    </li>
    <li>
    The text file <code>ChangeLog.txt</code> containing the documentation of all notable changes to the 'surf_nemo' package.
    </li>
    <li>
    The text file <code>ReadMe.txt</code> describing of the contents of the 'surf_nemo' package.
    </li>
    <li>
    The text file <code>Licence.txt</code> containing the product licensing information.
    </li>
    <li>
    The bash file <code>vertion.sh</code> containing the version number of the 'surf_nemo' package. This number is displayed in the upper-right corner of VM desktop.
    </li>
</ul>

## **The surf_datasets directory structure**

<p>Once installed (see section xx), the SURF-DATASETS package is located in the directory <code>/scratch/surf/surf_datasets</code>.
The folder <code>surf_datasets_1.00</code> has the directory structure as in <a href="#fig-surftree">figure B.1</a>:</p>

<ul>
    <li>
    The folder <code>bathymetry/</code> contains the GEBCO Bathymetric datasets at 30 arc seconds resolution.
    </li>
    <li>
    The folder <code>coastline/</code> contains the GSHHG coastline datasets provided by the NOAA National Geophysical Data Center (NGDC).
    </li>
    <li>
    The folder <code>meshmask/</code> contains the meshmask files of the parent ocean model and atmosphere source.
    </li>
    <li>
    The folder <code>experiments_regrid/</code> used when you want execute the SURF platform operationally.
    It contains the weight files for remapping ocean and atmospheric input data, the meshmask and
    bathymetry remapped on the child grid.
    </li>
    <li>
    The text file <code>ChangeLog.txt</code> containing the documentation of all notable changes to the 'surf_datasets' package.
    </li>
    <li>
    The text file <code>ReadMe.txt</code> describing of the contents of the 'surf_datasets' package.
    </li>
    <li>
    The bash file <code>vertion.sh</code> containing the version number of the 'surf_datasets' package.
    This number is displayed in the upper-right corner of VM desktop.
    </li>
</ul>

## **The experiments directory**

<p> Once the experiment is executed (i.e. expID), it is located in the directory <code>/scratch/surf/experiments/</code>.
The folder <code>expID</code> has the directory structure as in <a href="#fig-surftree">figure B.1</a>:</p>

<ul>
    <li>
    A copy of the configuration file <code>setParFree.json</code> (copied from the directory surf/from_GUI/expID/).
    </li>
    <li>
    The folder <code>code/</code> contains a copy of the source code (from the directory surf/surf_nemo/current/)
    used to execute the simulation.
    </li>
    <li>
    The folder <code>data/</code> contains all the data used in the experiment:
    the original input data (<code>data/indata/</code>),
    the extrapolated data (<code>data/extrapoldata/</code>), the regridded data (<code>data/regriddata/</code>)
    and the output data (<code>./data/outdata/</code>)
    The input datasets are downloaded from a local or web repositories for the selected period of simulation.
    </li>
    <li>
    The folder <code>figure/</code> contains all the plots of the original input data (<code>figure/indata/</code>),
    extrapolated data (<code>figure/extrapoldata/</code>), regridded data (<code>figure/regriddata/</code>),
    output data (<code>./figure/outdata/</code>), comparison between child and the parent coarse resolution data,...
    </li>
</ul>
