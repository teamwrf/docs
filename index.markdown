---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults
title: Home
layout: home
navigation_weight: 1
---

# Notes on NCL: How to use?

## The most important rule in data processing is:
- Look At Your Data
- You can avoid many errors and warnings if you are familiar with your data.
- To get an overview of a file's contents, type either of the following at the command line:
- For a netCDF-3/4, GRIB-1/2 or HDF-4/5 enter:
```
   ncl_filedump <the_filename>
```
- or for netCDF-3/4
```
   ncdump -h <the_filename>
```
