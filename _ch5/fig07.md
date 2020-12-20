---
layout: post
title: Figure 7
description: Average frequency spectrum of field data.
img: /assets/ch5/thumbnail/ch5_fig07.png
comments: true
---

{% include _links_library.md %}

<script type="text/javascript">
 function showhide(id) {
    var e = document.getElementById(id);
    e.style.display = (e.style.display == 'block') ? 'none' : 'block';
 }
</script>


<img src="{{ '/assets/ch5/ch5_fig07.png' | prepend: site.baseurl | prepend: site.url }}" alt="Figure 07" style="zoom:100%;" />


_Figure 7:_ Average frequency spectrum of the 105 common-source gathers similar to data as in Figure 3(c)

---
#### Source code used to reproduce the above figure:
- Type: ```/bin/bash```
- Dependency: [Seismic Unix][SU]
- Data availability: Input data is preparing.   

```sh
#!/bin/bash
#
# plot average spectrum of collected gathers
# 24-11-2020, J.Liu 

WIDTH=5; HEIGHT=2.5
size="wbox=$WIDTH hbox=$HEIGHT"

dir=firstLine/Preprocessed_Line01
#data=$dir/dreumel_LIN01_xcor_pre.su
data=$dir/LIN01_shots_raw.su

filtering="sufilter f=5,10,70,80 amp=0,1,1,0"
 
< $data suwind key=fldr min=1 max=105 |
suwind key=tracf min=1 max=120 | $filtering |
suresamp rf=1 |sustack key=dt |
sufft | suamp mode=amp | sunormalize norm=max | 
suwind itmax=20 |
supsgraph xbox=0 ybox=0 $size labelsize=18 \
n1tic=5 d1num=10 n2tic=5 d2num=0.2 grid1=dash grid2=dash \
linewidth=2 linecolor=blue label1="Frequency (Hz)" \
label2="Normalised Amplitude" style=normal > temp/fig04_amp.ps

scale=0.5; dH=0.5
b_x=0; b_y=0
a_x=0; a_y=$(echo $HEIGHT $scale $dH| awk '{print $1 * $2 + $3}')
echo a_y=$a_y

# merge into one file
psmerge translate=$a_x,$a_y scale=$scale,$scale in=temp/fig04_amp.ps  > figs/fig04_merge.ps

open figs/fig04_merge.ps &

```
---


<a href="#top">Back to top</a>
