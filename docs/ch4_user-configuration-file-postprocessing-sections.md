# **User Configuration File - Postprocessing Sections**

<p>In this chapter we continue to explore the contents of the configuration file. In particular we will examine in details the sections B used to manage the post-processing procedures for the visualization of input/output datasets, the comparison of child/parent fields and the comparison of the simulation result with insitu or satellite datasets.</p>

## **Input parameters for selecting the figure to generate**

### **Section set_lplot**

<p>The section set_lrun contains the logical parameters to activate/deactivate specific plot.</p>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lplot_domain</code></div>
<div class="col-8 pr-0"><p>Enable/disable the plotting of the user defined Domains.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lplot_indata</code></div>
<div class="col-8 pr-0"><p>Enable/disable the plotting of the Input Bat,Atm,OceIC,OceBC data.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lplot_extrapdata</code></div>
<div class="col-8 pr-0"><p>Enable/disable the plotting of the Extrapolated Atm,OceIC,OceBC data.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lplot_intUVdata</code></div>
<div class="col-8 pr-0"><p>Enable/disable the plotting of the Interpolated OceIC(U,V),OceBC(U,V) data.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lplot_rotUVdata</code></div>
<div class="col-8 pr-0"><p>Enable/disable the plotting of the Rotated OceIC(U,V),OceBC(U,V) data.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lplot_regriddata</code></div>
<div class="col-8 pr-0"><p>Enable/disable the plotting of the Regridded Bat,Atm,OceIC,OceBC,OceBCbdy data.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lplot_outdata</code></div>
<div class="col-8 pr-0"><p>Enable/disable the plotting of the Output Ocean data.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lplot_chlVSpar</code></div>
<div class="col-8 pr-0"><p>Enable/disable the plotting of the child VS. parent Ocean fields.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: False</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lplot_surfVSctd</code></div>
<div class="col-8 pr-0"><p>Enable/disable the plotting of the surf VS. ctd Ocean fields.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: False</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lplot_surfVSmooring</code></div>
<div class="col-8 pr-0"><p>Enable/disable the plotting of the surf VS. mooring Ocean fields.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lplot_surfVSferrybox</code></div>
<div class="col-8 pr-0"><p>Enable/disable the plotting of the surf VS. ferrybox Ocean fields.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: False</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lplot_surfVSsat</code></div>
<div class="col-8 pr-0"><p>Enable/disable the plotting of the surf VS. satellite Ocean fields.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: False</p></div>
</div>

### **Section set_visual_lplot**

<p>The section set_lrun contains the logical parameters to activate/deactivate specific plot.</p>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lplotChildMesh</code></div>
<div class="col-8 pr-0"><p>Enable/disable the plotting of the Child MeshMask fields.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lplotBat</code></div>
<div class="col-8 pr-0"><p>Enable/disable the plotting of the Bathymetry fields.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lplotAtm</code></div>
<div class="col-8 pr-0"><p>Enable/disable the plotting of the Atmspheric fields.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lplotOceIC</code></div>
<div class="col-8 pr-0"><p>Enable/disable the plotting of the Initial Condition Ocean fields.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lplotOceBC</code></div>
<div class="col-8 pr-0"><p>Enable/disable the plotting of the Open Boundary Condition Ocean fields.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lplotOceBCbdy</code></div>
<div class="col-8 pr-0"><p>Enable/disable the plotting of the Open Boundary Condition Ocean fields.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lplotTide</code></div>
<div class="col-8 pr-0"><p>Enable/disable the plotting of the Tidal fields.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lplotTidebdy</code></div>
<div class="col-8 pr-0"><p>Enable/disable the plotting of the Tidal fields.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lplotOceOut</code></div>
<div class="col-8 pr-0"><p>Enable/disable the plotting of the Output Ocean fields.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: False</p></div>
</div>

## **Input parameters for figure properties**

### **Section set_lplot**

<p>The section set_visual_fileImg contains the logical parameters to .</p>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">fileImg_type</code></div>
<div class="col-8 pr-0"><p>Type of the image file to generate.</p>
                        <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: png</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">fileImg_wkWidth</code></div>
<div class="col-8 pr-0"><p>Horizontal resolution (number of pixels) of the image file.</p>
                        <p><code>Type</code>: int &nbsp; <code>Ref.Value</code>: 2400</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">fileImg_wkHeight</code></div>
<div class="col-8 pr-0"><p>Vertical resolution (number of pixels) of the image file.</p>
                        <p><code>Type</code>: int &nbsp; <code>Ref.Value</code>: 2400</p></div>
</div>

### **Section set_visual_lvis**

<p>The section set_visual_lvis contains the logical parameters to .</p>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lvis_title</code></div>
<div class="col-8 pr-0"><p>Enable/disable the visibility of a given string as the main title.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lvis_mplotDif</code></div>
<div class="col-8 pr-0"><p>Enable/disable the plotting of the Bathymetry fields.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lvis_leftString</code></div>
<div class="col-8 pr-0"><p>Enable/disable the visibility of a given string above the plot’s upper boundary and left.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lvis_rightString</code></div>
<div class="col-8 pr-0"><p>Enable/disable the visibility of a given string above the plot’s upper boundary and right.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lvis_axisLab</code></div>
<div class="col-8 pr-0"><p>Enable/disable the visibility of the X an Y axis title.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lvis_tickmarks</code></div>
<div class="col-8 pr-0"><p>Enable/disable the visibility of the right, left, top and bottom tick marks.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lvis_borders</code></div>
<div class="col-8 pr-0"><p>Enable/disable the visibility of the right, left, top and bottom borders.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lvis_mapFillOn</code></div>
<div class="col-8 pr-0"><p>Enable/disable the visibility of the map area fill.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lvis_mapOutlineOn</code></div>
<div class="col-8 pr-0"><p>Enable/disable the visibility of the map area outlines.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lvis_vecRefAnnoOn</code></div>
<div class="col-8 pr-0"><p>Enable/disable the visibility of the reference vector annotation.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lvis_labbarOn</code></div>
<div class="col-8 pr-0"><p>Enable/disable the visibility of the LabelBar.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lvis_labbarLabelsOn</code></div>
<div class="col-8 pr-0"><p>Enable/disable the visibility of the LabelBar.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lvis_panelbarOn</code></div>
<div class="col-8 pr-0"><p>Enable/disable the visibility of the PannelBar.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lvis_infoContourOn</code></div>
<div class="col-8 pr-0"><p>Enable/disable the visibility of the info contour.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lvis_grid</code></div>
<div class="col-8 pr-0"><p>Enable/disable the visibility of the mesh grid.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lvis_myCoastline</code></div>
<div class="col-8 pr-0"><p>Enable/disable the visibility of the user coastline.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lvis_fillcurves</code></div>
<div class="col-8 pr-0"><p>Enables the filling of the area between two curves.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">lvis_boxNest</code></div>
<div class="col-8 pr-0"><p>Enable/disable the visibility of the nest rectangular box.</p>
                        <p><code>Type</code>: bool &nbsp; <code>Ref.Value</code>: True</p></div>
</div>

### **Section set_visual_graph**

<p>The section set_visual_graph contains the logical parameters to .</p>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">graph_projection</code></div>
<div class="col-8 pr-0"><p>Projection used for the map transformation. (es. CylindricalEquidistant,Mercator,...).</p>
                        <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: Mercator</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">graph_fillMode</code></div>
<div class="col-8 pr-0"><p>How ContourPlot performs fill: (=AreaFill), (=RasterFill),(=CellFill).</p>
                        <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: AreaFill</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">graph_minDistVec</code></div>
<div class="col-8 pr-0"><p>Minimum distance (in NDC space) that is to separate the data locations of neighboring vectors.</p>
                        <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 0.015</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">graph_thickArrowVec</code></div>
<div class="col-8 pr-0"><p>Thickness of the line used to draw vector line arrows.</p>
                        <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 2.0</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">graph_refMagnVecAtm</code></div>
<div class="col-8 pr-0"><p>Reference magnitude used for the wind vector field.</p>
                        <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 3.0</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">graph_refMagnVecOce</code></div>
<div class="col-8 pr-0"><p>Reference magnitude used for the current vector field.</p>
                        <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 0.6</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">graph_styleVec</code></div>
<div class="col-8 pr-0"><p>Style of glyph used to represent the vector magnitude and direction: (=LineArrow) ... (=CurlyVector) ....</p>
                        <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: CurlyVector</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">graph_iPlOrient</code></div>
<div class="col-8 pr-0"><p>Panels orientation in the multi plots figure: (=0)vertical, (=1)horizontal.</p>
                        <p><code>Type</code>: int &nbsp; <code>Ref.Value</code>: 1</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">graph_nlevsBar</code></div>
<div class="col-8 pr-0"><p>Number of the ....</p>
                        <p><code>Type</code>: int &nbsp; <code>Ref.Value</code>: 21</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">graph_polymarkerSize</code></div>
<div class="col-8 pr-0"><p>Size used to draw the marker in the polymarker plots.</p>
                        <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 0.01</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">graph_markLineMode</code></div>
<div class="col-8 pr-0"><p>Draw the curves using lines only (=Lines), markers only (=Markers), both lines and markers (=MarkLines).</p>
                        <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: MarkLines</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">graph_lineThick</code></div>
<div class="col-8 pr-0"><p>Thickness of the line used to draw the curves.</p>
                        <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 2.5</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">graph_markerSize</code></div>
<div class="col-8 pr-0"><p>Size used to draw the marker in the xy-plots.</p>
                        <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 0.01</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">graph_markers</code></div>
<div class="col-8 pr-0"><p>Style of the markers in the xy-plots.</p>
                        <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 16</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">graph_boxThick</code></div>
<div class="col-8 pr-0"><p>Thickness of the line used to draw the box.</p>
                        <p><code>Type</code>: float &nbsp; <code>Ref.Value</code>: 8.0</p></div>
</div>
<div class="row mx-0">
<div class="col-3 pl-0"><code class="mycode">graph_boxColor</code></div>
<div class="col-8 pr-0"><p>Color of the line used to draw the box.</p>
                        <p><code>Type</code>: string &nbsp; <code>Ref.Value</code>: red</p></div>
</div>
