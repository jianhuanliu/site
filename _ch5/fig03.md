---
layout: post
title: Figure 3
description: A typical preprocessed gather by SI+AS+SVI. 
img: /assets/ch5/thumbnail/ch5_fig03.png
importance: 3
comments: true
---

{% include _mylinks_library.md %}

<script type="text/javascript">
 function showhide(id) {
    var e = document.getElementById(id);
    e.style.display = (e.style.display == 'block') ? 'none' : 'block';
 }
</script>


<img src="{{ '/assets/ch5/ch5_fig03.png' | prepend: site.baseurl | prepend: site.url }}" alt="Figure 03" style="zoom:50%;" />

_Figure 3:_ (a) A typical preprocessed SH-wave shot gather from the field data acquired along Line A using S-wave vibrator as the source. The preprocessing steps include trace editing, band-pass filtering; (b) retrieved Love waves from the gather as shown in Figure 3(a); (c) result after convolution of the data in (b) with a non-stationary matching filter to account for the inaccurancy of retrieval during the procedure of SVI; (d) result after subtraction of Figure 3(c) from Figure 3(a). (e), (f), (g), (h) are the same with (a), (b), (c), (d), but for a common-source gather with a different source position. Every second trace between are presented.
    
---
#### Source code used to reproduce the above figure:
- Type: ```/bin/bash```
- Dependency: [Seismic Unix][SU]
- Data availability: Input data is preparing.   


Subfunction (1): ```t03a_plotsvi_steps.scr```

```sh
#!/bin/bash
#
# plot raw shot gathers, with automatic labelling
# 28-09-2020, J.Liu

WIDTH=4.
HEIGHT=4.

# Figure 2, (a)
fldr=25

size="wbox=$WIDTH hbox=$HEIGHT"
tmax=0.2
clip="perc=99"

dir=firstLine/Preprocessed_Line01/temp

windowing="suwind key=tracf min=10 max=110 j=2"
filtering="sufilter f=5,10,70,80 amp=0,1,1,0"

# (1) raw gather
< $dir/shot_raw_${fldr}.su $windowing |
sunormalize norm=max | $filtering |
supswigp xbox=0.0 ybox=0.0 $size $clip  \
x1beg=0 x1end=$tmax d1num=0.05 n1tic=5 \
d2num=20 n2tic=5 key=tracf \
labelsize=24 label2="Receiver number" label1="Time (s)" > temp/fig03_raw.eps 

# (2) retrieved gather by SVI
< $dir/shot_svi_${fldr}.su $windowing |
sunormalize norm=max | $filtering |
supswigp xbox=0.0 ybox=0.0 $size $clip  \
x1beg=0 x1end=$tmax  d1num=0.05 n1tic=5 \
d2num=20 n2tic=5 key=tracf \
labelsize=24 label2="Receiver number" label1= > temp/fig03_svi.eps 

# (3) retrieved gather after shaping
< $dir/shot_sw_${fldr}.su $windowing |
sunormalize norm=max | $filtering |
supswigp xbox=0.0 ybox=0.0 $size $clip  \
x1beg=0 x1end=$tmax  d1num=0.05 n1tic=5 \
d2num=20 n2tic=5 key=tracf \
labelsize=24 label2="Receiver number" label1= > temp/fig03_sw.eps 

# (4) raw gather after subtraction of SWs
< $dir/shot_as_${fldr}.su $windowing |
sunormalize norm=max | $filtering |
supswigp xbox=0.0 ybox=0.0 $size $clip  \
x1beg=0 x1end=$tmax  d1num=0.05 n1tic=5 \
d2num=20 n2tic=5 key=tracf \
labelsize=24 label2="Receiver number" label1= > temp/fig03_as.eps 

# (5) labeling all the subfigures
dx=0.5; dy=0.2; labelsize=32
xlabel=$(echo 0.0 $dx | awk '{print $1 - $2}')
ylabel=$(echo $HEIGHT $dy | awk '{print $1 + $2}')

pslabel t="(a)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_a.eps
pslabel t="(b)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_b.eps
pslabel t="(c)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_c.eps
pslabel t="(d)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_d.eps

psmerge translate=0,0 scale=1,1 in=temp/fig03_raw.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_a.eps > temp/fig03_raw_label.eps

psmerge translate=0,0 scale=1,1 in=temp/fig03_svi.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_b.eps > temp/fig03_svi_label.eps

psmerge translate=0,0 scale=1,1 in=temp/fig03_sw.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_c.eps > temp/fig03_sw_label.eps

psmerge translate=0,0 scale=1,1 in=temp/fig03_as.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_d.eps > temp/fig03_as_label.eps

#(6) merge into a one file
# calculate (x,y) positions of each subfigs
scale=0.35; dX=0.35
# 1st row
x1=0; y1=0
x2=$(echo $WIDTH $scale $dX| awk '{print $1 * $2 + $3}'); y2=$y1
x3=$(echo $WIDTH $scale $x2 $dX| awk '{print $1 * $2 + $3 + $4}'); y3=$y1
x4=$(echo $WIDTH $scale $x3 $dX| awk '{print $1 * $2 + $3 + $4}'); y4=$y1

psmerge translate=$x1,$y1 scale=$scale,$scale in=temp/fig03_raw_label.eps \
translate=$x2,$y2 scale=$scale,$scale in=temp/fig03_svi_label.eps \
translate=$x3,$y3 scale=$scale,$scale in=temp/fig03_sw_label.eps \
translate=$x4,$y4 scale=$scale,$scale in=temp/fig03_as_label.eps > figs/fig03a.eps

exit
```


Subfunction (2): ```t03b_plotsvi_steps.scr```

```sh
#!/bin/bash
#
# plot raw shot gathers, with automatic labelling
# 28-09-2020, J.Liu

WIDTH=4.
HEIGHT=4.

# Figure 2, (b)
fldr=50

size="wbox=$WIDTH hbox=$HEIGHT"
tmax=0.2
clip="perc=99"

dir=firstLine/Preprocessed_Line01/temp

windowing="suwind key=tracf min=10 max=110 j=2"
filtering="sufilter f=5,10,70,80 amp=0,1,1,0"

# (1) raw gather
< $dir/shot_raw_${fldr}.su $windowing |
sunormalize norm=max | $filtering |
supswigp xbox=0.0 ybox=0.0 $size $clip  \
x1beg=0 x1end=$tmax d1num=0.05 n1tic=5 \
d2num=20 n2tic=5 key=tracf \
labelsize=24 label2=  label1="Time (s)" > temp/fig03_raw.eps 

# (2) retrieved gather by SVI
< $dir/shot_svi_${fldr}.su $windowing |
sunormalize norm=max | $filtering |
supswigp xbox=0.0 ybox=0.0 $size $clip  \
x1beg=0 x1end=$tmax  d1num=0.05 n1tic=5 \
d2num=20 n2tic=5 key=tracf \
labelsize=24 label2=  label1= > temp/fig03_svi.eps 

# (3) retrieved gather after shaping
< $dir/shot_sw_${fldr}.su $windowing |
sunormalize norm=max | $filtering |
supswigp xbox=0.0 ybox=0.0 $size $clip  \
x1beg=0 x1end=$tmax  d1num=0.05 n1tic=5 \
d2num=20 n2tic=5 key=tracf \
labelsize=24 label2=  label1= > temp/fig03_sw.eps 

# (4) raw gather after subtraction of SWs
< $dir/shot_as_${fldr}.su $windowing |
sunormalize norm=max | $filtering |
supswigp xbox=0.0 ybox=0.0 $size $clip  \
x1beg=0 x1end=$tmax  d1num=0.05 n1tic=5 \
d2num=20 n2tic=5 key=tracf \
labelsize=24 label2=  label1= > temp/fig03_as.eps 

# (5) labeling all the subfigures
dx=0.5; dy=0.2; labelsize=32
xlabel=$(echo 0.0 $dx | awk '{print $1 - $2}')
ylabel=$(echo $HEIGHT $dy | awk '{print $1 + $2}')

pslabel t="(e)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_e.eps
pslabel t="(f)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_f.eps
pslabel t="(g)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_g.eps
pslabel t="(h)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_h.eps

psmerge translate=0,0 scale=1,1 in=temp/fig03_raw.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_e.eps > temp/fig03_raw_label.eps

psmerge translate=0,0 scale=1,1 in=temp/fig03_svi.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_f.eps > temp/fig03_svi_label.eps

psmerge translate=0,0 scale=1,1 in=temp/fig03_sw.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_g.eps > temp/fig03_sw_label.eps

psmerge translate=0,0 scale=1,1 in=temp/fig03_as.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_h.eps > temp/fig03_as_label.eps

# (6) merge into a one file
# calculate (x,y) positions of each subfigs
scale=0.35; dX=0.35
# 1st row
x1=0; y1=0
x2=$(echo $WIDTH $scale $dX| awk '{print $1 * $2 + $3}'); y2=$y1
x3=$(echo $WIDTH $scale $x2 $dX| awk '{print $1 * $2 + $3 + $4}'); y3=$y1
x4=$(echo $WIDTH $scale $x3 $dX| awk '{print $1 * $2 + $3 + $4}'); y4=$y1

# merge into one file
psmerge translate=$x1,$y1 scale=$scale,$scale in=temp/fig03_raw_label.eps \
translate=$x2,$y2 scale=$scale,$scale in=temp/fig03_svi_label.eps \
translate=$x3,$y3 scale=$scale,$scale in=temp/fig03_sw_label.eps \
translate=$x4,$y4 scale=$scale,$scale in=temp/fig03_as_label.eps > figs/fig03b.eps

exit

```

Subfunction (3): ```t03_combine.scr```

```sh
#!/bin/bash
#
# combine subfigures for (fldr=25,50)
# 28-09-2020, J.Liu

./t03a_plotsvi_steps.scr
./t03b_plotsvi_steps.scr

HEIGHT=1.0
scale=1.0; dY=0.8

# calculate (x,y) positions of each subfigs
x1=0; y1=0
y2=$(echo $HEIGHT $scale $dY| awk '{print $1 * $2 + $3}'); x2=$x1

# merge into one file
psmerge translate=$x1,$y1 scale=$scale,$scale in=figs/fig03b.eps \
translate=$x2,$y2 scale=$scale,$scale in=figs/fig03a.eps > figs/fig03_merge.eps

open figs/fig03_merge.eps &
```
---

<a href="#top">Back to top</a>
