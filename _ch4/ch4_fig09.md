---
layout: post
title: Figure 9
description: 3D view of subsurface structures
img: /assets/ch4/thumbnail/ch4_fig09.png
importance: 9
comments: true
---

{% include _mylinks_library.md %}

<script type="text/javascript">
 function showhide(id) {
    var e = document.getElementById(id);
    e.style.display = (e.style.display == 'block') ? 'none' : 'block';
 }
</script>


<img src="{{ '/assets/ch4/ch4_fig09.png' | prepend: site.baseurl | prepend: site.url }}" alt="Figure 09" style="zoom:80%;" />

_Figure 9:_ 3D view of subsurface structures.
    
---
#### Source code used to reproduce the above figure:
- Type: ```/bin/bash```
- Dependency: [Seismic Unix][SU]
- Data availability: Input data is preparing.


##### Subfunction (1): ```t09a_3dVS_models.scr```
```sh
#!/bin/bash
#
# 3d view of subsurface (with automatic labelling!)
# 20-11-2020, J. Liu

stage=$1

clip="perc=99"

dir1=Paper4_ostia_NEW/shortLine/par_masw_q15_till5st
dir2=Paper4_ostia_NEW/longLine/par_masw_q15_till5st

data11=$dir1/model_L/modelTest_vs_stage_${stage}.bin
data22=$dir2/model_L/modelTest_vs_stage_${stage}.bin

# (0) Cut the PML boundaries in the model
rm -f temp/cube.bin
sfbin2rsf n1=50 n2=160 d1=1 d2=1 bfile=$data11 |
sfput n1=50 n2=160 |
sfwindow n1=40 n2=135 f2=14 |
sfrsf2bin > temp/side.bin

sfbin2rsf n1=50 n2=300 d1=1 d2=1 bfile=$data22 |
sfput n1=50 n2=300 |
sfwindow n1=40 n2=275 f2=14 |
sfreverse which=2 verb=y |
sfrsf2bin > temp/front.bin

cat temp/cube.bin temp/front.bin > temp/cube.bin

# make top face with zeros
sunull nt=275 ntr=135 |
suzero value=132 itmax=275 | sustrip > temp/null.bin

cmap="bhls=0.666666,.5,1 ghls=.3333,.5,1 whls=0,.5,1"
geometry="xbox=0 ybox=0 size1=3 size2=8 size3=4"

# (1) pscube
pscube < temp/cube.bin n1=40 n2=275 n3=135 angle=30 \
front=temp/front.bin side=temp/side.bin top=temp/null.bin faces=1 \
d1=0.25 f1=0.0 d1num=2 n1tic= label1="Depth (m)" \
d2=0.25 f2=0.0 d2num=10 n2tic=5 label2="Line B (m)" \
d3=0.25 f3=0.0 d3num=10 f3num=5 n3tic=5 label3="Line A (m)" \
legend=0 lstyle=horibottom lwidth=4 ly=-1 lx=1 \
$geometry $cmap $clip \
units="S-wave velocity (m)" labelsize=24 > temp/cube_${stage}.eps

# (2) labeling
HEIGHT=3
dx=1.5; dy=-0.2; labelsize=32
xlabel=$(echo 0.0 $dx | awk '{print $1 - $2}')
ylabel=$(echo $HEIGHT $dy | awk '{print $1 + $2}')

x2=$(echo 8 $dx | awk '{print $1 - 1.4*$2}')
y2=$(echo 0.0 | awk '{print $1}')

pslabel t="(a)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_a.eps
pslabel t="[5~10] " f="Times-Bold" t="Hz" nsub=2 size=$labelsize > temp/label_aa.eps

psmerge translate=0,0 scale=1,1 in=temp/cube_${stage}.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_a.eps \
    translate=$x2,$y2 scale=1,1 in=temp/label_aa.eps > temp/cube_label_${stage}.eps

# merge into file
#scale=0.5

#x1=0.0; y1=0.0
#psmerge translate=$x1,$y1 scale=$scale,$scale rotate=0. in=temp/cube_label_${stage}.eps > figs/cube.eps 

#open figs/cube.eps &

```



<br>

##### Main function: ```t09_combine.scr```


```sh
#!/bin/bash
#
# combine 3d subsurface at different stages
# J. Liu

stage1=1
stage2=3 
stage3=5

./t09a_3dVS_models.scr  $stage1
./t09a_3dVS_models.scr  $stage2
./t09a_3dVS_models.scr  $stage3

HEIGHT=3.1
scale=0.5; dY=0.01

# calculate (x,y) positions of each subfigs
x1=0; y1=0
y2=$(echo $HEIGHT $scale $dY| awk '{print $1 * $2 + $3}'); x2=$x1
y3=$(echo $HEIGHT $scale $dY $y2| awk '{print $1 * $2 + $3 +$4}'); x3=$x1

# merge into one file
psmerge translate=$x1,$y1 scale=$scale,$scale in=temp/cube_label_${stage3}.eps \
translate=$x2,$y2 scale=$scale,$scale in=temp/cube_label_${stage2}.eps \
translate=$x3,$y3 scale=$scale,$scale in=temp/cube_label_${stage1}.eps > figs/fig09_merge.eps

open figs/fig09_merge.eps &

```

---

<a href="#top">Back to top</a>
