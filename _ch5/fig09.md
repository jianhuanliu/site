---
layout: post
title: Figure 9
description: Subsurface VS models by FWI.
img: /assets/ch5/thumbnail/ch5_fig09.png
comments: true
---

{% include _mylinks_library.md %}

<script type="text/javascript">
 function showhide(id) {
    var e = document.getElementById(id);
    e.style.display = (e.style.display == 'block') ? 'none' : 'block';
 }
</script>


<img src="{{ '/assets/ch5/ch5_fig09.png' | prepend: site.baseurl | prepend: site.url }}" alt="Figure 09" style="zoom:100%;" />

_Figure 9:_ Field experiment result of $V_S$ from data as in Figure 3(a) and Figure a(c). (a) initial S-wave velocity model used for inversion; (b) inverted result at banwidth of 5-10 Hz, 20-30 Hz, 40-50 Hz, respectively. (good to put the initial model as a separate figure)
    
---
#### Source code used to reproduce the above figure:
- Type: ```/bin/bash```
- Dependency: [Seismic Unix][SU]
- Data availability: Input data is preparing.   


```sh
#!/bin/bash
#
# plot inverted models by FWI (with automatic labelling!)
# 01-12-2020, J. Liu

HEIGHT=4.0
WIDTH=$(echo 30 9.75 $HEIGHT | awk '{print $1*$3/$2}') 
size="width=$WIDTH height=$HEIGHT"
LHEIGHT=$(echo $HEIGHT | awk '{print $1 * 1.0}')
LWIDTH=0.15

# contour ploting
pcsize="wbox=$WIDTH hbox=$HEIGHT"

# sample colormap:  red, green, blue
#cmap="bhls=0.666666,.5,1 ghls=.3333,.5,1 whls=0,.5,1"
cmap="whls=0.666666,.5,1 ghls=.3333,.5,1 bhls=0,.5,1"
clip="perc=99"

# initial model build by MASW (short line)
dir1=firstLine/par_masw_vs_sig3
dir2=firstLine/par_masw_raw_vs_sig3

data1=$dir1/model_L5/modelTest_vs_stage_1.bin
data2=$dir1/model_L5/modelTest_vs_stage_3.bin
data3=$dir1/model_L5/modelTest_vs_stage_5.bin

data4=$dir2/model_L5/modelTest_vs_stage_1.bin
data5=$dir2/model_L5/modelTest_vs_stage_3.bin
data6=$dir2/model_L5/modelTest_vs_stage_5.bin

# Initial model by MASW
# n1, depth direction; n2, x direction

# (0) Cut the PML boundaries in the model
sfbin2rsf n1=40 n2=215 d1=1 d2=1 bfile=$data1 |
sfwindow n1=35 n2=205 f2=9 | sfrsf2bin > temp/data1.bin

sfbin2rsf n1=40 n2=215 d1=1 d2=1 bfile=$data2 |
sfwindow n1=35 n2=205 f2=9 | sfrsf2bin > temp/data2.bin

sfbin2rsf n1=40 n2=215 d1=1 d2=1 bfile=$data3 |
sfwindow n1=35 n2=205 f2=9 | sfrsf2bin > temp/data3.bin

sfbin2rsf n1=40 n2=215 d1=1 d2=1 bfile=$data4 |
sfwindow n1=35 n2=205 f2=9 | sfrsf2bin > temp/data4.bin

sfbin2rsf n1=40 n2=215 d1=1 d2=1 bfile=$data5 |
sfwindow n1=35 n2=205 f2=9 | sfrsf2bin > temp/data5.bin

sfbin2rsf n1=40 n2=215 d1=1 d2=1 bfile=$data6 |
sfwindow n1=35 n2=205 f2=9 | sfrsf2bin > temp/data6.bin

# (1) Inverted models (SW,1st)
< temp/data1.bin psimage d1=0.25 d2=0.25 n1=35  \
$cmap n1tic=2 n2tic=5 \
$size xbox=0.0 ybox=0.0 \
legend=0 lstyle=vertright lheight=$LHEIGHT lwidth=$LWIDTH  \
units="S-wave velocity (m/s)" lbeg=100 lend=400 \
label1="Depth (m)" label2="Lateral location(m)" labelsize=28 \
d1num=2 d2num=5 $clip \
bps=24 title= > temp/fig10_a.eps

# (2) Inverted models (SW,3st)
< temp/data2.bin psimage d1=0.25 d2=0.25 n1=35  \
$cmap n1tic=2 n2tic=5 \
$size xbox=0.0 ybox=0.0 \
legend=0 lstyle=vertright lheight=$LHEIGHT lwidth=$LWIDTH \
units="S-wave velocity (m/s)" lbeg=100 lend=400 \
label1="Depth (m)" label2= labelsize=28 \
d1num=2 d2num=5 $clip \
bps=24 title= > temp/fig10_b.eps

# (3) Inverted models (SW,5st)
< temp/data3.bin psimage d1=0.25 d2=0.25 n1=35  \
$cmap n1tic=2 n2tic=5 \
$size xbox=0.0 ybox=0.0 \
legend=0 lstyle=vertright lheight=$LHEIGHT lwidth=$LWIDTH  \
units="S-wave velocity (m/s)" lbeg=100 lend=400 \
label1="Depth (m)" label2= labelsize=28 \
d1num=2 d2num=5 $clip \
bps=24 title= > temp/fig10_c.eps

# (3.1) Contour plotting
< temp/data3.bin pscontour d1=0.25 d2=0.25 n1=35 dc=100 \
$pcsize xbox=0.0 ybox=0.0 \
cwidth=2.0 nlabelc=0 axescolor=white >temp/fig10_cc.eps

# (4) Inverted models (RAW,1st)
< temp/data4.bin psimage d1=0.25 d2=0.25 n1=35 \
$cmap n1tic=2 n2tic=5 \
$size xbox=0.0 ybox=0.0 \
legend=0 lstyle=vertright lheight=$LHEIGHT lwidth=$LWIDTH  \
units="S-wave velocity (m/s)" lbeg=100 lend=400 \
label1= label2="Lateral location (m)" labelsize=28 \
d1num=2 d2num=5 $clip \
bps=24 title= > temp/fig10_d.eps

# (5) Inverted models (RAW,3st)
< temp/data5.bin psimage d1=0.25 d2=0.25 n1=35 \
$cmap n1tic=2 n2tic=5 \
$size xbox=0.0 ybox=0.0 \
legend=0 lstyle=vertright lheight=$LHEIGHT lwidth=$LWIDTH  \
units="S-wave velocity (m/s)" lbeg=100 lend=400 \
label1= label2= labelsize=28 \
d1num=2 d2num=5 $clip \
bps=24 title= > temp/fig10_e.eps

# (6) Inverted models (RAW,5st)
< temp/data6.bin psimage d1=0.25 d2=0.25 n1=35 \
$cmap n1tic=2 n2tic=5 \
$size xbox=0.0 ybox=0.0 \
legend=1 lstyle=horibottom lwidth=5 lx=-3.0 ly=-1.0 \
units="S-wave velocity (m/s)" \
label1= label2= labelsize=28 \
d1num=2 d2num=5 $clip \
bps=24 title= > temp/fig10_f.eps

# (7) labeling all the subfigures
dx=1.0; dy=0.25; labelsize=40
xlabel=$(echo 0.0 $dx | awk '{print $1 - $2}')
ylabel=$(echo $HEIGHT $dy | awk '{print $1 + $2}')

x2=$(echo $WIDTH $dx | awk '{print $1 - 2.0*$2}')
y2=$(echo 0.0 | awk '{print $1}')

pslabel t="(a)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_a.eps
pslabel t="(b)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_b.eps
pslabel t="(c)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_c.eps
pslabel t="(d)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_d.eps
pslabel t="(e)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_e.eps
pslabel t="(f)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_f.eps

pslabel t="[5~20] " f="Times-Bold" t="Hz" nsub=2 size=28 > temp/label_aa.eps
pslabel t="[5~40] " f="Times-Bold" t="Hz" nsub=2 size=28 > temp/label_bb.eps
pslabel t="[5~60] " f="Times-Bold" t="Hz" nsub=2 size=28 > temp/label_cc.eps

psmerge translate=0,0 scale=1,1 in=temp/fig10_a.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_a.eps \
    translate=$x2,$y2 scale=1,1 in=temp/label_aa.eps > temp/fig10_a_label.eps

psmerge translate=0,0 scale=1,1 in=temp/fig10_b.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_c.eps \
    translate=$x2,$y2 scale=1,1 in=temp/label_bb.eps > temp/fig10_b_label.eps

psmerge translate=0,0 scale=1,1 in=temp/fig10_c.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_e.eps \
    translate=$x2,$y2 scale=1,1 in=temp/label_cc.eps > temp/fig10_c_label.eps

psmerge translate=0,0 scale=1,1 in=temp/fig10_d.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_b.eps \
    translate=$x2,$y2 scale=1,1 in=temp/label_aa.eps > temp/fig10_d_label.eps

psmerge translate=0,0 scale=1,1 in=temp/fig10_e.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_d.eps \
    translate=$x2,$y2 scale=1,1 in=temp/label_bb.eps > temp/fig10_e_label.eps

psmerge translate=0,0 scale=1,1 in=temp/fig10_f.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_f.eps \
    translate=$x2,$y2 scale=1,1 in=temp/label_cc.eps > temp/fig10_f_label.eps

# calculate (x,y) positions of each subfigs
scale=0.35; dX=0.4; dY=0.35

# 1st column
x1=0; y1=0
y2=$(echo $HEIGHT $scale $dY | awk '{print $1 * $2 + $3}'); x2=$x1
y3=$(echo $HEIGHT $scale $dY $y2 | awk '{print $1 * $2 + $3 + $4}'); x3=$x1

# 2st column
x4=$(echo $WIDTH $scale $dX | awk '{print $1 * $2 + $3}'); y4=$y1
x5=$(echo $WIDTH $scale $dX | awk '{print $1 * $2 + $3}'); y5=$y2
x6=$(echo $WIDTH $scale $dX | awk '{print $1 * $2 + $3}'); y6=$y3

# merge two into one file
psmerge translate=$x1,$y1 scale=$scale,$scale rotate=0. in=temp/fig10_c_label.eps \
translate=$x1,$y1 scale=$scale,$scale rotate=0. in=temp/fig10_cc.eps \
translate=$x2,$y2 scale=$scale,$scale rotate=0. in=temp/fig10_b_label.eps \
translate=$x3,$y3 scale=$scale,$scale rotate=0. in=temp/fig10_a_label.eps \
translate=$x4,$y4 scale=$scale,$scale rotate=0. in=temp/fig10_f_label.eps \
translate=$x5,$y5 scale=$scale,$scale rotate=0. in=temp/fig10_e_label.eps \
translate=$x6,$y6 scale=$scale,$scale rotate=0. in=temp/fig10_d_label.eps \
translate=$x4,$y4 scale=$scale,$scale rotate=0. in=temp/fig10_cc.eps > figs/fig10a_merge.eps

open figs/fig10a_merge.eps &

```
---

<a href="#top">Back to top</a>

