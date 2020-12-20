---
layout: post
title: Figure 07
description: Q parameter estimation.
img: /assets/ch4/thumbnail/ch4_fig07.png
importance: 7
comments: true
---

{% include _mylinks_library.md %}

<script type="text/javascript">
 function showhide(id) {
    var e = document.getElementById(id);
    e.style.display = (e.style.display == 'block') ? 'none' : 'block';
 }
</script>


<img src="{{ '/assets/ch4/ch4_fig07.png' | prepend: site.baseurl | prepend: site.url }}" alt="Figure 07" style="zoom:100%;" />

_Figure 7:_ Q parameter estimation.
    
---
#### Source code used to reproduce the above figure:
- Type: ```/bin/bash```
- Dependency: [Seismic Unix][SU]
- Data availability: Input data is preparing. 


```sh
#!/bin/bash
#
# plot misfit values for different Q values.
# 01-11-2020, J. Liu

rm -f temp/log.*

dir=Paper4_ostia_NEW/par_masw_EstQ
data=$dir/misfit.dat

# get the line numbers
num=$(wc -l $data | awk '{printf $1}') 
((Num=$num+1))

# read only the fourth column
cat $data | awk '{printf $1 "\n"}' > temp/log.ascii 

# convert to binary file
a2b < temp/log.ascii > temp/log.bin

# (1), ploting (X-windwos)
< temp/log.bin sfnormbin n1=$num |
xgraph n=$num d1=5 f1=5 x1beg=2 x1end=52 \
x2beg=0.4 x2end=1.09 linecolor=2 linewidth=1 mark=5 marksize=6 \
width=400 height=300 grid1=dot grid2=dot \
label1="Q" label2="Normalized misfit" \
style=normal &

# (2), ploting (PS)
< temp/log.bin sfnormbin n1=$num |
psgraph n=$num \
x1beg=2 x1end=52 f1=5 d1=5 n1tic=5 d1num=10 \
x2beg=0.4 x2end=1.09 n2tic=5 d2num=0.1 \
linecolor=black linewidth=2 mark=5 marksize=10 \
grid1=dot grid2=dot \
xbox=0 ybox=0 wbox=5.0 hbox=5.0 \
label1="Q" label2="Normalized misfit" \
labelsize=24 \
style=normal > temp/fig07_shape.eps

scale=0.5
x1=0; y1=0
# merge into one file
psmerge translate=$x1,$y1 scale=$scale,$scale in=temp/fig07_shape.eps > figs/fig07.eps

open figs/fig07.eps &

```
---

<a href="#top">Back to top</a>
