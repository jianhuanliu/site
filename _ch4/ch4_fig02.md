---
layout: post
title: Figure 2
description: Acquisition geometry used in field.
img: /assets/ch4/thumbnail/ch4_fig02.png
importance: 2
comments: true
---

{% include _mylinks_library.md %}

<script type="text/javascript">
 function showhide(id) {
    var e = document.getElementById(id);
    e.style.display = (e.style.display == 'block') ? 'none' : 'block';
 }
</script>


<img src="{{ '/assets/ch4/ch4_fig02.png' | prepend: site.baseurl | prepend: site.url }}" alt="Figure 02" style="zoom:100%;" />

_Figure 2:_ Source-receiver geometry used to acquire 2D seismic data along the Line A and Line B as indicated in Figure 1 in a roll-along mode. The triangles represent vertical, single-component component geophones we used to recored the seismic data. Every fouth source and receiver positions are displayed.
    
---
#### Source code used to reproduce the above figure:
- Type: ```/bin/bash```
- Dependency: [Seismic Unix][SU]
- Data availability: Input data is preparing.

```sh
#!/bin/bash
#
# acquisition geometry of Ostia fieldwork (with automatic labelling!)
# 28-09-2020, J.Liu

# size of short Line 
SWIDTH=4.0; SHEIGHT=4.0
short="wbox=$SWIDTH hbox=$SHEIGHT"

# size of long Line 
WIDTH=7.5; HEIGHT=6.0
long="wbox=$WIDTH hbox=$HEIGHT"

data1=data/ostia_edited_shortLine.su
data2=data/ostia_edited_longLine.su

# (1) geometry of shortLine
< $data1 suchw key1=sx key2=sx b=0.0001 |
suchw key1=gx key2=gx b=0.0001 |
suchart key1=gx key2=sx outpar=pfile > temp/plot_data

psgraph < temp/plot_data par=pfile  \
    xbox=0.0 ybox=0.0 $short \
    x1beg=-1 x1end=40 x2beg=-1 x2end=40 \
    grid1=dot grid2=dot label1="Receivers (m)" label2="Sources (m)" \
    labelsize=20 title= \
    linewidth=0 marksize=4 mark=6 linecolor=red > temp/short_geo.eps

# (2) geometry of longLine
< $data2 suwind key=fldr min=1 max=57 |
suchw key1=sx key2=sx b=0.0001 |
suchw key1=gx key2=gx b=0.0001 |
suchart key1=gx key2=sx outpar=pfile > temp/plot_data

psgraph < temp/plot_data par=pfile  \
    xbox=0.0 ybox=0.0 $long \
    x1beg=-1 x1end=75 x2beg=-1 x2end=60 \
    grid1=dot grid2=dot label1="Receivers (m)" label2= \
    labelsize=20 title= \
    linewidth=0 marksize=4 mark=6 linecolor=red > temp/long_geo.eps

# (3) labeling all the subfigures
dx=0.4; dy=0.2; labelsize=32
xlabel=$(echo 0.0 $dx | awk '{print $1 - $2}')
y1label=$(echo $SHEIGHT $dy | awk '{print $1 + $2}')
y2label=$(echo $HEIGHT $dy | awk '{print $1 + $2}')

pslabel t="(a)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_a.eps
pslabel t="(b)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_b.eps

psmerge translate=0,0 scale=1,1 in=temp/short_geo.eps \
    translate=$xlabel,$y1label scale=1,1 in=temp/label_a.eps > temp/short_geo_a.eps

psmerge translate=0,0 scale=1,1 in=temp/long_geo.eps \
    translate=$xlabel,$y2label scale=1,1 in=temp/label_b.eps > temp/long_geo_b.eps


# calculate (x,y) positions of each subfigs
scale=0.5; dX=0.5
# 1st row
x1=0; y1=0
x2=$(echo $SWIDTH $scale $dX | awk '{print $1 * $2 + $3}');
y2=0

# merge into one figure
psmerge translate=$x1,$y1 scale=$scale,$scale in=temp/short_geo_a.eps \
translate=$x2,$y2 scale=$scale,$scale in=temp/long_geo_b.eps > figs/fig02_merge.eps

open figs/fig02_merge.eps & 

```
---

<a href="#top">Back to top</a>
