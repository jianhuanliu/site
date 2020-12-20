---
layout: post
title: Figure 12
description: Evolution of misfit function.
img: /assets/ch4/thumbnail/ch4_fig12.png
importance: 12
comments: true
---

{% include _mylinks_library.md %}

<script type="text/javascript">
 function showhide(id) {
    var e = document.getElementById(id);
    e.style.display = (e.style.display == 'block') ? 'none' : 'block';
 }
</script>


<img src="{{ '/assets/ch4/ch4_fig12.png' | prepend: site.baseurl | prepend: site.url }}" alt="Figure 12" style="zoom:80%;" />

_Figure 12:_ Evolution of misfit function.
    
---
#### Source code used to reproduce the above figure:
- Type: ```/bin/bash```
- Dependency: [Seismic Unix][SU]
- Data availability: Input data is preparing.


##### Subfunction (1): ```t12a_misfit.scr```
```sh
#!/bin/bash
#
# plot misfit function during FWI (with automatic labelling)
# 28-09-2020, J.Liu

rm -f temp/log.*

dir=Paper4_ostia_NEW/shortLine/par_masw_q15_till5st
data=$dir/LOG_TEST.dat

# get the line numbers
num=$(wc -l $data | awk '{printf $1}') 
((Num=$num+1))

# read only the fourth column
cat $data | awk '{printf $5 "\n"}' > temp/log.ascii 

# convert to binary file
a2b < temp/log.ascii n1=1 > temp/log.bin

echo num=$num
# (1), ploting (X-windwos)
< temp/log.bin \
xgraph n=$num d1=1 f1=1 x1beg=1 x1end=$num \
x2beg= x2end= linecolor=2 linewidth=1 mark=5 marksize=6 \
width=500 height=500 grid1=dot grid2=dot \
label1="Cumulative iterations" label2="Misfit value" \
style=normal &

# (2), ploting (PS)
< temp/log.bin \
psgraph n=$num \
x1beg=1 x1end=$num f1=1 d1=1 n1tic=5 d1num=5 \
x2beg= x2end= n2tic=5 d2num= \
linecolor=black linewidth=1 mark=5 marksize=5 \
grid1=dot grid2=dot \
xbox=0 ybox=0 wbox=5.0 hbox=5.0 \
label1="Cumulative iterations" label2="Misfit value" \
labelsize=24 \
style=normal > temp/fig12a_shape.eps

# (3), labeling all the subfigures
dx=0.4; dy=0.2; labelsize=32
xlabel=$(echo 0.0 $dx | awk '{print $1 - $2}')
ylabel=$(echo 5.0 $dy | awk '{print $1 + $2}')

pslabel t="(a)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_a.eps

psmerge translate=0,0 scale=1,1 in=temp/fig12a_shape.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_a.eps > temp/fig12_a_label.eps

scale=0.35
x1=0; y1=0
# merge into one file
psmerge translate=$x1,$y1 scale=$scale,$scale in=temp/fig12_a_label.eps > figs/fig12a.eps

#open figs/fig12a.eps &

```



<br>

##### Main function: ```t12_combine.scr```


```sh
#!/bin/bash
#
# combine two subfigures
./t12a_misfit.scr
./t12a_misfit.scr

WEIGHT=5
scale=1.0; dX=2.35

# calculate (x,y) positions of each subfigs
x1=0; y1=0
x2=$(echo $WIDTH $scale $dX| awk '{print $1 * $2 + $3}'); y2=$y1

# merge into one file
psmerge translate=$x1,$y1 scale=$scale,$scale in=figs/fig12a.eps \
translate=$x2,$y2 scale=$scale,$scale in=figs/fig12b.eps > figs/fig12_merge.eps

zap xgraph
open figs/fig12_merge.eps &

```

---

<a href="#top">Back to top</a>
