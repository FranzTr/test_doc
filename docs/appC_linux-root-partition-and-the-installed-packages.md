# **Linux Root Partition and the installed packages**

<p> As shown in  <a href="#disk-partitions-mounted-on-the-surf-virtual-machine">chapter 6.1.1</a>
the VM surf is divided into two partitions:
the disk <code>/dev/sda</code> "mounted" in the root directory <code>/</code> and
the disk <code>/dev/sdb</code> "mounted" in the directory <code>/scratch</code>.
The root partition contains Debian GNU/Linux operating system (version 10.7).</p>

## **Debian partition**

<p> The operating system installed in the Virtual Machine is <a href="https://www.debian.org/" target="_blank">Debian</a>.
Debian is a free operating system (OS) that use the Linux kernel. It comes with over 59000 packages, precompiled software bundled up in a nice format for easy installation on your machine.</p>

<p> In the current VM is installed Debian 10 buster. You can find the list of packages <a href="https://packages.debian.org/jessie/allpackages" target="_blank">here</a>.</p>

## **Installed packages**

### **CDO - (v1.8.1)**

<p> The Climate Data Operator (<a href="https://code.mpimet.mpg.de/projects/cdo" target="_blank">CDO</a>)
software is a collection of many operators for standard processing of
climate and forecast model data. The operators include simple statistical and arithmetic functions, data
selection and subsampling tools, and spatial interpolation. CDO was developed to have the same set of
processing functions for GRIB [GRIB] and NetCDF [NetCDF] datasets in one package.</p>

### **curl - (v7.52.1)**

<p> <a href="https://curl.haxx.se/" target="_blank">curl</a> is free and open source software used in command lines or scripts to transfer files/data from or to a server using FTP, HTTP, HTTPS, SCP, SFTP, SMB and other supported protocols on Linux or Unix-like system. </p>

### **HDF5 - (v1.8.18)**

<p> The Hierarchical Data Format (<a href="https://www.hdfgroup.org/downloads/hdf5/" target="_blank">HDF5</a>) is a data model, library, and file format for storing and managing data. It supports an unlimited variety of datatypes, and is designed for flexible and efficient I/O and for high volume and complex data. HDF5 is portable and is extensible, allowing applications to evolve in their use of HDF5. The HDF5 Technology suite includes tools and applications for managing, manipulating, viewing, and analyzing data in the HDF5 format. </p>

### **Julia - (v1.4.1)**

<p> <a href="https://julialang.org/" target="_blank">Julia</a> is a high-level, high-performance, dynamic programming language. While it is a general purpose language and can be used to write any application, many of its features are well-suited for high-performance numerical analysis and computational science. </p>

### **MPICH2 - (v3.2)**

<p> <a href="https://www.mpich.org/" target="_blank">MPICH</a>, formerly known as MPICH2, is a freely available, high performance and widely portable implementation of the Message Passing Interface (MPI) standard.
    It efficiently supports different computation and communication platforms including commodity clusters, SMPs, massively parallel systems, and high-speed networks.</p>

### **NCL - (v6.4.0)**

<p> The NCAR Command Language (<a href="https://www.ncl.ucar.edu/" target="_blank">NCL</a>) is a free interpreted language designed specifically for scientific data processing and visualization. </p>

### **Ncview - (v2.1.7)**

<p> <a href="http://cirrus.ucsd.edu/~pierce/software/ncview/index.html" target="_blank">Ncview</a> is a visual browser for netCDF format files. Typically you would use ncview to get a quick and easy, push-button look at your netCDF files. You can view simple movies of the data, view along various dimensions, take a look at the actual data values, change color maps, invert the data, etc.  </p>

### **NetCDF - (4.4.1.1)**

<p> Network Common Data Form (<a href="https://www.unidata.ucar.edu/software/netcdf/" target="_blank">NetCDF</a>) is a set of software libraries and machine-independent data formats that support the creation, access, and sharing of array-oriented scientific data. It is also a community standard for sharing scientific data. </p>

### **Python - (3.6.9)**

<p> <a href="https://www.unidata.ucar.edu/software/netcdf/" target="_blank">Python</a> is an interpreted, high-level, general-purpose programming language. </p>

### **Szip - (v2.1)**

<p> <a href="https://support.hdfgroup.org/doc_resource/SZIP/" target="_blank">Szip</a> compression software, providing lossless compression of scientific data.  </p>

### **UDUNITS - (v2.2.24)**

<p> The <a href="https://www.unidata.ucar.edu/software/udunits/#home" target="_blank">UDUNITS</a> package supports units of physical quantities. Its C library provides for arithmetic manipulation of units and for conversion of numeric values between compatible units. The package contains an extensive unit database, which is in XML format and user-extendable. The package also contains a command-line utility for investigating units and converting values.</p>

### **XIOS**

<p> <a href="https://forge.ipsl.jussieu.fr/ioserver" target="_blank">XIOS</a> is library designed to manage NETCDF outputs of climate models.</p>

### **zlib - (v1.2.11)**

<p> The <a href="https://zlib.net/" target="_blank">zlib</a> compression library provides in-memory compression and decompression functions, including integrity checks of the uncompressed data. </p>
