---
layout: post
title: Figure 10
description: Evolution of misfit function during FWI.
img: /assets/ch5/thumbnail/ch5_fig10.png
comments: true
---

{% include _mylinks_library.md %}

<script type="text/javascript">
 function showhide(id) {
    var e = document.getElementById(id);
    e.style.display = (e.style.display == 'block') ? 'none' : 'block';
 }
</script>


<img src="{{ '/assets/ch5/ch5_fig10.png' | prepend: site.baseurl | prepend: site.url }}" alt="Figure 10" style="zoom:80%;" />

_Figure 10:_ Evolution of misfit value calculated with equation (1) during FWI.
    

---
#### Source code used to reproduce the above figure:
- Type: ```/bin/bash```
- Dependency: [Seismic Unix][SU]
- Data availability: Input data is preparing.   


```sh
#!/bin/bash
#
# plot misfit function during FWI.
# 28-09-2020, J.Liu

rm -f temp/log.*

dir=firstLine/par_masw_vs_sig3
data=$dir/LOG_L.dat

# get the line numbers
num=$(wc -l $data | awk '{printf $1}') 
((Num=$num+1))

# read only the fourth column
cat $data | awk '{printf $5 "\n"}' > temp/log.ascii 

# convert to binary file
a2b < temp/log.ascii > temp/log.bin

# (1), ploting (X-windwos)
< temp/log.bin \
xgraph n=$num d1=1 f1=1 x1beg=1 x1end=$num \
x2beg= x2end= linecolor=2 linewidth=1 mark=5 marksize=6 \
width=500 height=500 grid1=dot grid2=dot \
label1="Iteration" label2="Misfit value" \
style=normal &

# (2), ploting (PS)
< temp/log.bin \
psgraph n=$num \
x1beg=1 x1end=$num f1=1 d1=1 n1tic=5 d1num=10 \
x2beg= x2end= n2tic=5 d2num= \
linecolor=black linewidth=1 mark=5 marksize=5 \
grid1=dot grid2=dot \
xbox=0 ybox=0 wbox=5.0 hbox=5.0 \
label1="Iterations" label2="Misfit" \
labelsize=24 \
style=normal > temp/fig09_shape.eps

scale=0.5
x1=0; y1=0
# merge into one file
psmerge translate=$x1,$y1 scale=$scale,$scale in=temp/fig09_shape.eps > figs/fig09.eps

open figs/fig09.eps &

```
---

<a href="#top">Back to top</a>

