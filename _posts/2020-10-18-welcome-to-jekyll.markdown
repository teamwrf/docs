---
layout: page
title:  "Plots"
date:   2020-10-18 12:44:31 +0530
categories: ncl updates
---
# Script templates for NCL regridding and graphics

This page contains some NCL scripts that you can download for doing creating visualizations of your data, adding shapefile outlines, adding primitives, or doing ESMF regridding. Most of these are short scripts with a minimal number of resources set.

For more "real world" scripts with lots of graphics, visit the [Examples page](http://www.ncl.ucar.edu/Applications).

- [Plots over maps](http://www.ncl.ucar.edu/Applications/Templates/#PlotsOverMapsTemplates)
- [Plots (not over maps)](http://www.ncl.ucar.edu/Applications/Templates/#PlotsNotOverMapsTemplates)
- [WRF Plots](http://www.ncl.ucar.edu/Applications/Templates/#WRFPlots)
- [Maps only](http://www.ncl.ucar.edu/Applications/Templates/#MapsOnlyTemplates)
- [Adding shapefile outlines to a map plot](http://www.ncl.ucar.edu/Applications/Templates/#AddingShapefileOutlinesTemplates)
- [Attaching primitives (lines, markers, polygons)](http://www.ncl.ucar.edu/Applications/Templates/#AttachingPrimitivesTemplates)
- [ESMF regridding templates](http://www.ncl.ucar.edu/Applications/Templates/#ESMFRegriddingTemplates)


------

**Plots over maps**



- contour_map_nores_template.ncl

   

  \- template for creating contours over a map, no resources are set

  

- vector_map_nores_template.ncl

   

  \- template for creating vectors over a map, no resources are set

  

- contour_map_template.ncl

   

  \- template for creating contours over a map

  

- contour_map_lc_template.ncl

   

  \- template for creating contours over a Lambert Conformal map

  

- vector_map_template.ncl

   

  \- template for creating vectors over a map

  





------

**Plots (not over maps)**



- xy_template.ncl

   

  \- template for creating XY plots

  

- scatter_template.ncl

   

  \- template for creating scatter plots

  

- contour_template.ncl

   

  \- template for creating contour plots

  

- vector_template.ncl

   

  \- template for creating vectors

  





------

**Maps only**



- map_minres_template.ncl

   

  \- template for creating map plots, using a minimal set of resources.

  

- map_template.ncl

   

  \- template for creating map plots, with many resource options included.

  





------

**WRF plots**



- wrf_simple_gsn_template.ncl

   

  \- very basic template for creating a color contour/map plot of WRF data. This script doesn't set many resources.

  

- wrf_contour_map_gsn_template.ncl

   

  \- template for creating color contours over a map of WRF data. This script sets more resources than the "wrf_simple_template.ncl" script, and it also gives you the option to use the WRF map projection information on the file.

  

- wrf_simple_native_template.ncl

   

  \- very basic template for creating color contour/map plot of WRF data, using native projection supplied on WRF output file. This script doesn't set many resources.

  

- wrf_hgt_shapefile_template.ncl

   

  \- template for creating color contours over a map of WRF data, and attaching shapefile outlines from USA and Canada shapefiles downloaded from

   

  http://www.gadm.org/country

  . This script uses WRF functions to do the plotting, and a gsn function to add the shapefile outlines.

  





------

**Adding shapefile outlines to a map plot**



- map_shapefile_template.ncl

   

  \- template for adding shapefile polyline outlines to a map

  

- wrf_hgt_shapefile_template.ncl

   

  \- template for creating color contours over a map of WRF data, and attaching shapefile outlines from USA and Canada shapefiles downloaded from

   

  http://www.gadm.org/country

  . This script uses WRF functions to do the plotting, and a gsn function to add the shapefile outlines.

  





------

**Attaching primitives (lines, markers, polygons)**



- adding_polylines_template.ncl

   

  \- template for attaching polylines to a map plot

  

- adding_polymarkers_template.ncl

   

  \- template for attaching polymarkers to a map plot

  

- adding_polygons_template.ncl

   

  \- template for attaching polygons to a map plot

  





------

**ESMF regridding templates**

**Note:** If you are using NCL version 6.1.0-beta and not 6.1.0, then please consider upgrading to version 6.1.0. Otherwise, be sure to download the latest [ESMF_regridding.ncl](http://www.ncl.ucar.edu/Applications/Files/ESMF_regridding.ncl) script before using these templates. This file should be used in place of the "$NCARG_ROOT/lib/ncarg/nclscripts/esmf/ESMF_regridding.ncl" one provided in V6.1.0-beta.

For more ESMF regridding examples, you can visit the the [ESMF Regridding examples page](http://www.ncl.ucar.edu/Applications/ESMF.shtml).



- rectilinear ---> 5 degree grid

   

  (

  ESMF_rect_to_5deg.ncl

  )

  

- rectilinear ---> curvilinear

   

  (

  ESMF_rect_to_curv.ncl

  )

  

- rectilinear ---> unstructured

   

  (

  ESMF_rect_to_unstruct.ncl

  )

  

- curvilinear ---> 1 degree grid

   

  (

  ESMF_curv_to_1deg.ncl

  )

  

  

- curvilinear ---> rectilinear

   

  (

  ESMF_curv_to_rect.ncl

  )

  

- curvilinear ---> curvilinear

   

  (

  ESMF_curv_to_curv.ncl

  )

  

- curvilinear ---> unstructured

   

  (

  ESMF_curv_to_unstruct.ncl

  )

  

- curvilinear ---> WRF

   

  (

  ESMF_curv_to_WRF.ncl

  )

  

- unstructured ---> 0.25 degree grid

   

  (

  ESMF_unstruct_to_0.25deg.ncl

  )

  

  

- unstructured ---> rectilinear

   

  (

  ESMF_unstruct_to_rect.ncl

  )

  

- unstructured ---> curvilinear

   

  (

  ESMF_unstruct_to_curv.ncl

  )

  

- WRF ---> rectilinear

   

  (

  ESMF_WRF_to_rect.ncl

  )

  

- WRF ---> curvilinear

   

  (

  ESMF_WRF_to_curv.ncl

  )

  

- generic template

   

  (

  ESMF_regrid_template.ncl

  ) - uses the single

   

  **ESMF_regrid**

   

  function

  

- generic template

   

  (

  ESMF_regrid_with_weights_template.ncl

  ) - uses the

   

  **ESMF_regrid_with_weights**

   

  function to do the regridding. You must already have the weights file to use this.

  

- **generic template** ([ESMF_template.ncl](http://www.ncl.ucar.edu/Applications/Templates/ESMF_template.ncl)) - does the regridding in several steps