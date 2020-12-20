---
layout: post
title: Figure 08
description: Source-wavelet estimation.
img: /assets/ch4/thumbnail/ch4_fig08.png
importance: 8
comments: true
---

{% include _mylinks_library.md %}

<script type="text/javascript">
 function showhide(id) {
    var e = document.getElementById(id);
    e.style.display = (e.style.display == 'block') ? 'none' : 'block';
 }
</script>


<img src="{{ '/assets/ch4/ch4_fig08.png' | prepend: site.baseurl | prepend: site.url }}" alt="Figure 08" style="zoom:100%;" />

_Figure 8:_ Estimation of source wavelets by deconvolution.
    
---
#### Source code used to reproduce the above figure:
- Type: ```/bin/bash```
- Dependency: [Seismic Unix][SU]
- Data availability: Input data is preparing.


```sh
#!/bin/bash
#
# plot estimated source wavelets by deconvolution
# 28-09-2020, J.Liu

HEIGHT=3
WIDTH=5.5

clip="perc=99"
dir=Paper4_ostia_NEW/shortLine/par_masw_q15_till5st/wavelet
fd1=1; fd2=37

rm -f temp/wavelet.bin
for ((fldr=$fd1; fldr<=$fd2; fldr++)) do
    a2b < $dir/wavelet_shot_${fldr}.dat n1=1 >> temp/wavelet.bin 
done

# mkdir empty trace
sunull nt=6000 ntr=$fd2 dt=0.00005 |
sustrip head=temp/new_head > temp/dummy_data

# paster data & header
supaste < temp/wavelet.bin ns=6000 \
head=temp/new_head > temp/wavelet.su

tmax=0.3
< temp/wavelet.su sushw key=tracf a=1 b=1 |
suresamp rf=0.1 |
suwind tmax=$tmax | sunormalize norm=max |
supswigp xbox=0.0 ybox=0.0 wbox=$WIDTH hbox=$HEIGHT $clip  \
x1beg=0 x1end=$tmax f1=0 d1=0.0005 d1num=0.1 n1tic=5 \
f2=1 d2num=10 n2tic=5 title= \
labelsize=18 label2="Shot number" label1="Time (s)" > temp/fig08_a.eps

# merge into one file
scale=0.5
psmerge translate=0,0 scale=$scale,$scale in=temp/fig08_a.eps > figs/fig08.eps

open figs/fig08.eps &
```
---

<a href="#top">Back to top</a>
