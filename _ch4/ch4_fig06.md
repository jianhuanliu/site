---
layout: post
title: Figure 6
description: Dispersion curve inversion by NA algorithm.
img: /assets/ch4/thumbnail/ch4_fig06.png
importance: 6
comments: true
---

{% include _mylinks_library.md %}

<script type="text/javascript">
 function showhide(id) {
    var e = document.getElementById(id);
    e.style.display = (e.style.display == 'block') ? 'none' : 'block';
 }
</script>


<img src="{{ '/assets/ch4/ch4_fig06.png' | prepend: site.baseurl | prepend: site.url }}" alt="Figure 06" style="zoom:70%;" />

_Figure 6:_ Initial VS model build by 2D MASW.
    
---
#### Source code used to reproduce the above figure:
- Type: ```/bin/bash```
- Dependency: [Seismic Unix][SU]
- Data availability: Input data is preparing.

```sh
#!/bin/bash
#
# Initial Vs model estimated by MASW
# 28-09-2020, J.Liu

HEIGHT=4.0
WIDTH=$(echo 39.75 15 $HEIGHT | awk '{print $1*$3/$2}') 
size="width=$WIDTH height=$HEIGHT"
LHEIGHT=$(echo $HEIGHT | awk '{print $1 * 0.95}')
LWIDTH=0.15

# sample colormap:  red, green, blue
cmap="bhls=0.666666,.5,1 ghls=.3333,.5,1 whls=0,.5,1"
clip="perc=99"

# initial model build by MASW (short line)
dir=Paper4_ostia_NEW/shortLine/par_masw_q15_till5st

data0=$dir/make_model/model_init.vs

# Initial model by MASW
# n1, depth direction; n2, x direction

sfbin2rsf n1=50 n2=160 d1=1 d2=1 bfile=$data0 |
sfwindow n2=100 f2=30 n1=24 | sfrsf2bin > temp/data1.bin

< temp/data1.bin \
psimage d1=0.25 d2=0.25 n1=24 f2=5 \
$cmap n1tic=5 n2tic=5 d1num=2 d2num=5 \
$size xbox=0.0 ybox=0.0 \
legend=1 lstyle=vertright lheight=$LHEIGHT lwidth=$LWIDTH \
units="S-wave velocity (m/s)" \
label1="Depth (m)" label2="Line A (m)" labelsize=24 \
$clip \
bps=24 title= > temp/fig06_a.ps

# calculate (x,y) positions of each subfigs
scale=0.35; dX=0.4; dY=0.25
# 1st row
x1=0; y1=0

# merge two into one file
psmerge translate=$x1,$y1 scale=$scale,$scale rotate=0. in=temp/fig06_a.ps > figs/fig06_merge.eps

open figs/fig06_merge.eps &

```

---

<a href="#top">Back to top</a>
