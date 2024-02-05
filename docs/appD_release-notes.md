# **Release Notes**

surf_nemo - Version 1.01 "What's New"
(released on 2020-11-08)
All notable changes to this package will be documented here.

### Added

- Regridding of the barotropic tide fields (elevation, zonal and merdional velocity) (in 'run_regriddataTideBC.jl')
- Extraction of the tide on the lateral open boundary (in 'run_regriddataTideBC.jl')
- Rotation of the ocean velocity components when parent model is defined on a distorted curvilinear spherical grid (add rotateUV and interpUV packages in the utilities directory)
- Several parameters in the configuration file setParFree.json

### Changed

- Split the main.ncl procedure in 5 indipendent macrotask: run_childMeshMask.ncl,
  regriddataAtm.ncl,run_regriddataOceIC.ncl run_regriddataTideBC.jl,run_oce.ncl
- Rewritten several procedure from ncl to julia programming language
