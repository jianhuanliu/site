---
layout: post
title: Figure 4
description: Shot gathers and their dispersion images.
img: /assets/ch4/thumbnail/ch4_fig04.png
importance: 4
comments: true
---

{% include _mylinks_library.md %}

<script type="text/javascript">
 function showhide(id) {
    var e = document.getElementById(id);
    e.style.display = (e.style.display == 'block') ? 'none' : 'block';
 }
</script>


<img src="{{ '/assets/ch3/ch4_fig04.png' | prepend: site.baseurl | prepend: site.url }}" alt="Figure 04" style="zoom:80%;" />

_Figure 4:_ Shot gathers and their corresponding dispersion images.
    
---
#### Source code used to reproduce the above figure:
- Type: ```/bin/bash```
- Dependency: [Seismic Unix][SU]
- Data availability: Input data is preparing.

  

##### Subfunction (1): ```t04a_oneGather.scr```
```sh
#!/bin/bash
#
# shot gathre and its dispersion image (with automatic labelling!)
# 28-09-2020, J.Liu

# sample colormap:  red, green, blue
cmap="whls=0.666666,.5,1 ghls=.3333,.5,1 bhls=0,.5,1"
clip="perc=99"

tmax=0.3

Xmid=$1
# FK based FWI, test on synthetic case
rawData=MASW/file.dat/${Xmid}.sum.su
dspData=MASW/file.dat/${Xmid}.sum.dsp
dispFile=MASW/file.disp/${Xmid}.M0.disp
calcDisp=MASW/e_text/Xmid${Xmid}_LN3_DC.par

./c0_makePAR.scr ${Xmid}
./c1_makePAR.scr ${Xmid}

filtering="sufilter f=5,10,70,80 amps=0,1,1,0"

WIDTH=7.0; HEIGHT1=7.5
geometry="xbox=0 ybox=0 wbox=$WIDTH hbox=$HEIGHT1"
# (1) raw data
< $rawData suchw key1=offset key2=gx key3=sx b=1 c=-1 |  
sushw key=tracf a=1 b=1 | $filtering | 
suwind tmax=$tmax | sunormalize norm=max |
supswigp $geometry $clip va= \
x1beg=0 x1end=$tmax f1=0 d1=0.00025 d1num=0.1 n1tic=5 \
f2=1 d2num=10 n2tic=1 \
labelsize=28 label2="Receiver number" label1="Time (s)" > temp/fig04_shot.eps 

# (2) MASW analysis
< $dspData sunan verbose=0 | sunormalize norm=max |
suflip flip=3 > temp/23.tmp

# (3) determine the number of picked points
npair=$(wc -l $dispFile | awk '{print $1}')
echo "Number of picked dispersion point is $npair"

WIDTH=7.0; HEIGHT2=7.5
geometry="xbox=0 ybox=0 width=$WIDTH height=$HEIGHT2"
# (4) dispersion image

< temp/23.tmp suwind key=tracl min=1 max=45 |
supsimage f1=300 d1=-1 d1num= n1tic=5 \
n2tic=5 d2num=20 $geometry \
legend=0 lstyle=vertright \
curve=$calcDisp,$dispFile npair=61,$npair \
curvecolor=black,white curvewidth=3,4 curvedash=0,1 \
lheight=$LHEIGHT lwidth=$LWIDTH units="Normalized amplitude" \
label1="Rayleigh-wave phase velocity (m/s)" label2="Frequency (Hz)" labelsize=28 \
$cmap $size $clip > temp/fig04_disp.eps

# (5) labeling all the subfigures
dx=0.5; dy=0.2; labelsize=36
xlabel=$(echo 0.0 $dx | awk '{print $1 - $2}')
y1label=$(echo $HEIGHT1 $dy | awk '{print $1 + $2}')
y2label=$(echo $HEIGHT2 $dy | awk '{print $1 + $2}')

pslabel t="(a)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_a.eps
pslabel t="(d)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_b.eps

psmerge translate=0,0 scale=1,1 in=temp/fig04_shot.eps \
    translate=$xlabel,$y1label scale=1,1 in=temp/label_a.eps > temp/fig04_shot_label.eps

psmerge translate=0,0 scale=1,1 in=temp/fig04_disp.eps \
    translate=$xlabel,$y2label scale=1,1 in=temp/label_b.eps > temp/fig04_disp_label.eps


# (6) calculate (x,y) positions of each subfigs
scale=0.18; dX=0.8; dY=0.25
# 1st row
x1=0; y1=0
y2=$(echo $HEIGHT2 $scale $dY| awk '{print $1 * $2 + $3}'); x2=$x1

# merge into one file
psmerge translate=$x1,$y1 scale=$scale,$scale in=temp/fig04_disp_label.eps \
translate=$x2,$y2 scale=$scale,$scale in=temp/fig04_shot_label.eps > figs/fig04_Xmid${Xmid}.eps

#open figs/fig04_Xmid${Xmid}.eps &
```

<br>

##### Subfunction (2): ```c0_makePAR.scr```

```sh
#!/bin/bash
#
# This script is designed to convert picked dispersion curve to PAR file format
# 28-09-2020, J.Liu

Xmid=$1
pvcFile=MASW/file.pick/${Xmid}.M0.pvc
dispFile=MASW/file.disp/${Xmid}.M0.disp

# number of line
num=$(wc -l $pvcFile | awk '{print $1}')

fstart=1; fend=$num
std=0.0 # output wavelength instead 

rm -f $dispFile

echo "Dispersion curve is from line $fstart to $fend"
 
# print frequency & phase velocity info
for ((ifreq=$fstart; ifreq<=$fend; ifreq++)) do
    Freq=$(head -$ifreq $pvcFile | tail -1 | awk '{print $1}')
    Vel=$(head -$ifreq $pvcFile | tail -1 | awk '{print $2}')
    Wavelength=$(echo $Freq $Vel | awk '{print $2 / $1}')

    echo "Frequency is at $Freq Hz, Velocity is $Vel m/s, Wavelength is $Wavelength m"

    printf "%.3f  %.3f \n" $Vel $Freq >> $dispFile
    
done

```

<br>

##### Subfunction (3): ```c1_makePAR.scr```

```sh
#!/bin/bash
#
# This script is designed to convert theorital dispersion curve to PAR file format
# 28-09-2020, J.Liu

Xmid=$1
pvcFile=MASW/e_text/Xmid${Xmid}_LN3_DC.txt
dispFile=MASW/e_text/Xmid${Xmid}_LN3_DC.par

# number of line
#num=$(wc -l $pvcFile | awk '{print $1}')

# plot only the best curve
fstart=6; fend=66
std=0.0 # output wavelength instead 

rm -f $dispFile

echo "Dispersion curve is from line $fstart to $fend"
 
# print frequency & phase velocity info
for ((ifreq=$fstart; ifreq<=$fend; ifreq++)) do
    Freq=$(head -$ifreq $pvcFile | tail -1 | awk '{print $1}')
    Vel=$(head -$ifreq $pvcFile | tail -1 | awk '{print 1.0/$2}')
    Wavelength=$(echo $Freq $Vel | awk '{print $2 / $1}')

    echo "Frequency is at $Freq Hz, Velocity is $Vel m/s, Wavelength is $Wavelength m"

    printf "%.3f  %.3f \n" $Vel $Freq >> $dispFile
    
done

```

<br>

##### Main function: ```t04_combine.scr```


```sh
#!/bin/bash
#
#
Xmid1=5.0000; Xmid2=23.0000; Xmid3=30.0000
./t04a_oneGather.scr $Xmid1
./t04a_oneGather.scr $Xmid2
./t04a_oneGather.scr $Xmid3

WIDTH=1.4
scale=1.2; dX=0.25

# calculate (x,y) positions of each subfigs
x1=0; y1=0
x2=$(echo $WIDTH $scale $dX| awk '{print $1 * $2 + $3}'); y2=$y1
x3=$(echo $WIDTH $scale $dX $x2| awk '{print $1 * $2 + $3 +$4}'); y3=$y1

# merge into one file
psmerge translate=$x1,$y1 scale=$scale,$scale in=figs/fig04_Xmid${Xmid1}.eps \
translate=$x2,$y2 scale=$scale,$scale in=figs/fig04_Xmid${Xmid2}.eps \
translate=$x3,$y3 scale=$scale,$scale in=figs/fig04_Xmid${Xmid3}.eps > figs/fig04_merge.eps

open figs/fig04_merge.eps &

```

---

<a href="#top">Back to top</a>
