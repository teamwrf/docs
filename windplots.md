---
layout: page
title: Wind Plots
permalink: /windplots/
navigation_weight: 3
---

## at 925 hPa

``` python
;-- read data and set variable references
filename = "HUDHUD/P1C1/wrfout_d01_2014_10_08"
f =  addfile(filename, "r")

filename2 = "HUDHUD/P1C2/wrfout_d01_2014_10_08"
f2 =  addfile(filename2, "r")

;t =  f->MU
  ;u     = f->U(:,10,0:293,0:308)
  ;v     = f->V(:,10,0:293,0:308)

u=wrf_user_getvar(f,"ua",-1)
v=wrf_user_getvar(f,"va",-1)

  U = f2->U(:,10,0:293,0:308)
  V = f2->V(:,10,0:293,0:308)

  pres = wrf_user_getvar(f,"pres",-1)
  pf = pres * 0.01                ; Convert to hPa
  up = wrf_interp_3d_z(u,pf,925.) 
  vp = wrf_interp_3d_z(v,pf,925.) 


;-- open a PNG file
wks = gsn_open_wks("png",get_script_prefix_name())

;-- set resources for contour plots
res                     =  True
res@gsnDraw             =  False        ;-- don't draw plot, yet
res@gsnFrame            =  False        ;-- don't advance frame
res@gsnMaximize         =  True         ;-- maximize plots
res@mpMinLatF = 3.0 ;-- min latitude
res@mpMaxLatF = 27.0 ;-- max latitude
res@mpMinLonF = 73.0 ;-- min longitude
res@mpMaxLonF = 99.0 ;-- max longitude

  res@pmTickMarkDisplayMode = "Always"
  ;res@mpFillOn              =  False          ; turn off map fill
  res@mpOutlineDrawOrder    = "PostDraw"      ; draw continental outline last
  res@mpOutlineBoundarySets = "GeophysicalAndUSStates" ; state boundaries
;
res@tfDoNDCOverlay           = True 
  res@gsnAddCyclic             = False            ; regional data 
  res@vcRefMagnitudeF          = 10.0             ; define vector ref mag
  res@vcRefLengthF             = 0.065            ; define length of vec ref
  res@vcGlyphStyle             = "CurlyVector"    ; turn on curly vectors
  res@vcMinDistanceF           = 0.037            ; thin vectors
  res@vcRefAnnoOrthogonalPosF  = .1               ; move ref vector down

  res@gsnScalarContour         = True
  res@cnFillOn                 = True
  res@cnFillPalette            = "gui_default"    ; set color map
  res@cnLinesOn                = False  
;res@cnFillOn            =  True         ;-- contour fill
res@cnFillPalette       = "cmp_b2r"     ;-- choose color map
res@mpGridAndLimbOn     =  True         ;-- draw grid lines

res@lbLabelBarOn        =  False        ;-- don't draw a labelbar

u1 = up(24,:,:)
v1 = vp(24,:,:)
spd1 = sqrt(u1^2+v1^2) 

u2 = up(32,:,:)
v2 = vp(32,:,:)
spd2 = sqrt(u2^2+v2^2) 

u3 = up(40,:,:)
v3 = vp(40,:,:)
spd3 = sqrt(u3^2+v3^2) 

res@gsnCenterString = "(a)"
plot_1 = gsn_csm_vector_scalar_map(wks,u1,v1,spd1,res);-- create 4 plots time step 1 to 4 (NCL index 0-3)
res@gsnCenterString = "(b)"
plot_2 = gsn_csm_vector_scalar_map(wks,u2,v2,spd2,res)
res@gsnCenterString = "(c)"
plot_3 = gsn_csm_vector_scalar_map(wks,u3,v3,spd3,res)


u11 = U(24,:,:)
v11 = V(24,:,:)
spd11 = sqrt(u11^2+v11^2) 

u21 = U(32,:,:)
v21 = V(32,:,:)
spd21 = sqrt(u21^2+v21^2) 

u31 = U(40,:,:)
v31 = V(40,:,:)
spd31 = sqrt(u31^2+v31^2) 

res@gsnCenterString = "(d)"
plot_4 = gsn_csm_vector_scalar_map(wks,u11,v11,spd11,res);-- create 4 plots time step 1 to 4 (NCL index 0-3)
res@gsnCenterString = "(e)"
plot_5 = gsn_csm_vector_scalar_map(wks,u21,v21,spd21,res)
res@gsnCenterString = "(f)"
plot_6 = gsn_csm_vector_scalar_map(wks,u31,v31,spd31,res)
;u4 = u(30,:,:)
;v4 = v(30,:,:)
;spd4 = sqrt(u4^2+v4^2) 

  ;plot = gsn_csm_vector_scalar_map(wks,u,v,spd,res);-- create 4 plots time step 1 to 4 (NCL index 0-3)
;plot_4 = gsn_csm_vector_scalar_map(wks,u4,v4,spd4,res)
;plot_1 = gsn_csm_contour_map(wks,t(0,:,:),res)
;plot_2 = gsn_csm_contour_map(wks,t(1,:,:),res)
;plot_3 = gsn_csm_contour_map(wks,t(2,:,:),res)
;plot_4 = gsn_csm_contour_map(wks,t(3,:,:),res)

;-- panel resources
pnlres                  =  True
pnlres@gsnPanelLabelBar =  True         ;-- common labelbar
pnlres@gsnPanelXWhiteSpacePercent =  5
pnlres@gsnPanelMainFontHeightF =  0.020 ;-- text font size
;pnlres@gsnPanelMainString = "Wind"

;-- create panel plot
gsn_panel(wks,(/plot_1,plot_2,plot_3,plot_4,plot_5,plot_6/),(/2,3/),pnlres)
```