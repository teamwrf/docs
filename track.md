---
layout: page
title: Track in WRF output
permalink: /track/
navigation_weight: 3
---

``` python
load "teamwrf_res.ncl"

 a = addfile("/mnt/c/Work/Test/HUDHUD/P1C1/wrfout_d01_2014_10_08","r")
 b = addfile("/mnt/c/Work/Test/HUDHUD/P1C2/wrfout_d01_2014_10_08","r")
  ;a = addfile("wout","r")
  lat2d = a->XLAT(0,:,0:308)
  lon2d = a->XLONG(0,:,0:308)

  blat2d = b->XLAT(0,:,0:308)
  blon2d = b->XLONG(0,:,0:308)
  
  dimll = dimsizes(lat2d)
  nlat  = dimll(0)
  mlon  = dimll(1)
  lat = wrf_user_getvar(a,"lat",0)
  lon = wrf_user_getvar(a,"lon",0)
  
  
  ; date = (/1512,1600,1612,1700,1712,1800,1812,1900/)
 date = (/0800,0803,0806,0809,0812,0815,0818,0821,0900,0903,0906,0909,0912,0915,0918,0921,1000,1003,1006,1009,1012,1015,1018,1021,1100,1103,1106,1109,1112,1115,1118,1121,1200,1203,1206,1209,1212,1215,1218,1221,1300/)
 sdate = sprinti("%4.0i",date)
 ;print(sdate)
  nTime = dimsizes(wrf_user_list_times(a))
  ndate=nTime

    
  time = new(ndate,string)
  imin = new(ndate,integer)
  jmin = new(ndate,integer)
  smin = new(ndate,integer)
  bimin = new(ndate,integer)
  bjmin = new(ndate,integer)
  bsmin = new(ndate,integer)
 ; sdate = new(ndate,integer)
  
 do i = 0,ndate-1
 sdate(i) = i
  slp = wrf_user_getvar(a,"slp",i)	
  bslp = wrf_user_getvar(b,"slp",i)
  dims = dimsizes(slp)
  bdims = dimsizes(bslp)

  slp1d     = ndtooned(slp)
  bslp1d     = ndtooned(bslp)

  smin(i) = minind(slp1d)      ; 6692 in wout file
  bsmin(i) = minind(bslp1d) 

    minij     = ind_resolve(ind(slp1d.eq.min(slp)),dims)
    bminij     = ind_resolve(ind(bslp1d.eq.min(bslp)),bdims)

    imin(i) = minij(0,0)
    jmin(i) = minij(0,1)

	  bimin(i) = bminij(0,0)
    bjmin(i) = bminij(0,1)
	;xx=lon2d(imin,jmin)
	;yy=lat2d(imin,jmin)
	;printVarSummary(slp)
   ; print(min(slp)+ " ("+ imin(i) +","+ jmin(i) +") " )
end do
; Graphics section

  wks=gsn_open_wks("png","MYtrack1")          ; Open PS file.
  gsn_define_colormap(wks,"BlGrYeOrReVi200")  ; Change color map.

;copied res
res = True

             ; Maximize plot in frame.
;res@tiMainString = "WOUT FILE"       ; Main title

;WRF_map_c(a,res,0)                          ; Set up map resources
                                              ;    (plot options)
;plot = gsn_csm_map(wks,res)                 ; Create a map.
 plot = wrf_map(wks,a,res)
;plot = wrf_contour(a,wks,slp,my)
 
  ; Set up resources for polymarkers.
  gsres                = True
  gsres@gsMarkerIndex  = 16                  ; filled dot
  gsres@gsMarkerSizeF = 0.005               ; default - 0.007
  cols                  = (/5,160,40/)

; Set up resources for polylines.
  res_lines                      = True
  res_lines@gsLineThicknessF     = 2.           ; 3x as thick

  dot  = new(ndate,graphic)    ; Make sure each gsn_add_polyxxx call
  bdot  = new(ndate,graphic) 
  line = new(ndate,graphic)    ; is assigned to a unique variable.
  bline = new(ndate,graphic)
  ; Loop through each date and add polylines to the plot.
  do i = 0,ndate-2
     res_lines@gsLineColor           = cols(0)
     xx=(/lon2d(imin(i),jmin(i)),lon2d(imin(i+1),jmin(i+1))/)
     yy=(/lat2d(imin(i),jmin(i)),lat2d(imin(i+1),jmin(i+1))/)
     line(i) = gsn_add_polyline(wks,plot,xx,yy,res_lines)
  end do


   ;Loop through each date and add polylines to the plot.
  do i = 0,ndate-2
     res_lines@gsLineColor           = cols(1)
     bxx=(/blon2d(bimin(i),bjmin(i)),blon2d(bimin(i+1),bjmin(i+1))/)
     byy=(/blat2d(bimin(i),bjmin(i)),blat2d(bimin(i+1),bjmin(i+1))/)
   bline(i) = gsn_add_polyline(wks,plot,bxx,byy,res_lines)
  end do

x = (/0800,0806,0812,0818,0900,0906,0912,0918,1000,1006,1012,1018,1100,1106,1112,1118,1200,1206,1212,1218,1300/)
y = (/12,12.5,12.8,13.2,13.7,13.9,14.1,14.1,14.40,14.80,15.20,15.50,15.90,16.10,16.20,16.40,17.20,17.60,18.00,18.70,19.50/)
z = (/93,92.5,91,90.2,89.2,88.8,88.4,87.9,87.6,87,86.7,86.4,85.7,85.1,84.8,84.7,84.2,83.4,82.7,82.3,81.5/)
  xnTime = dimsizes(x)
  xdot  = new(xnTime,graphic)    ; Make sure each gsn_add_polyxxx call
  xline = new(xnTime,graphic)    ; is assigned to a unique variable.

 do i = 0,xnTime-2
     res_lines@gsLineColor           = cols(2)
     xx=(/z(i),z(i+1)/)
     yy=(/y(i),y(i+1)/)
     xline(i) = gsn_add_polyline(wks,plot,xx,yy,res_lines)
 end do



  lon1d = ndtooned(lon2d)
  lat1d = ndtooned(lat2d)
 blon1d = ndtooned(blon2d)
  blat1d = ndtooned(blat2d)

; Loop through each date and add polymarkers to the plot. OBS
  do i = 0,ndate-1
    ; print("dot:"+lon1d(smin(i))+","+lat1d(smin(i)))
     gsres@gsMarkerColor  = cols(0)  ; blue color
   ;  dot(i)=gsn_add_polymarker(wks,plot,lon1d(smin(i)),lat1d(smin(i)),gsres)
  end do

; Loop through each date and add polymarkers to the plot. OBS
 ; do i = 0,ndate-1
    ; print("dot:"+lon1d(smin(i))+","+lat1d(smin(i)))
 ;    gsres@gsMarkerColor  = cols(1)  ; red color
 ;    bdot(i)=gsn_add_polymarker(wks,plot,blon1d(bsmin(i)),blat1d(bsmin(i)),gsres)
;  end do

; Loop through each date and add polymarkers to the plot.
 ; do i = 0,xnTime-1
    ; print("dot:"+lon1d(smin(i))+","+lat1d(smin(i)))
;     gsres@gsMarkerColor  = cols(2)  ; green color
;     xdot(i)=gsn_add_polymarker(wks,plot,z(i),y(i),gsres)
;  end do


; Date (Legend)
  txres               = True
  txres@txFontHeightF = 0.015
  txres@txFontColor   = cols(0)

  txid1 = new(ndate,graphic)
; Loop through each date and draw a text string on the plot.
 ; do i = 0, ndate-1
 ;    txres@txJust = "CenterRight"
 ;    ix = smin(i) - 4
 ;   ; print("Eye:"+ix)
 ;    if(i.eq.1) then
 ;       txres@txJust = "CenterLeft"
 ;       ix = ix + 8
 ;    end if
 ;  ;  txid1(i) = gsn_add_text(wks,plot,sdate(i),lon1d(ix),lat1d(ix),txres)
 ; end do

; Add marker and text for legend. (Or you can just use "pmLegend" instead.)
  txres@txJust = "CenterLeft"
nexp=1
  txid2 = new(nexp,graphic)
  pmid2 = new(nexp,graphic)
  ;do i = 0,nexp-1
  ;   gsres@gsMarkerColor  = cols(i)
  ;   txres@txFontColor    = cols(i)
  ;   ii = ((/129,119,109/))  ; ilat
  ;   jj = ((/110,110,110/))  ; jlon
  ;   ji = ii*mlon+jj         ; col x row
  ;   pmid2(i) = gsn_add_polymarker(wks,plot,lon1d(ji(i)),lat1d(ji(i)),gsres)
  ;   txid2(i) = gsn_add_text(wks,plot,".",lon1d(ji(i)+5),lat1d(ji(i)),txres)
  ;end do
 ; plor_map = gsn_map(wks, , res)()
  draw(plot)
  frame(wks)
  ```