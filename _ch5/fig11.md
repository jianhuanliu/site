---
layout: post
title: Figure 11
description: Comparison between measured and computed data.
img: /assets/ch5/thumbnail/ch5_fig11.png
comments: true
---

{% include _mylinks_library.md %}

<script type="text/javascript">
 function showhide(id) {
    var e = document.getElementById(id);
    e.style.display = (e.style.display == 'block') ? 'none' : 'block';
 }
</script>


<img src="{{ '/assets/ch5/ch5_fig11.png' | prepend: site.baseurl | prepend: site.url }}" alt="Figure 11" style="zoom:50%;" />

_Figure 11:_ Comparison between measured data and computed data.
    
---
#### Source code used to reproduce the above figure:
- Type: ```/bin/bash```
- Dependency: [Seismic Unix][SU]
- Data availability: Input data is preparing.   



Subfunction (1): ```t11a_compareGathers.scr```


```sh
#/bin/bash
#
# plot measured & computed data
# 20-11-2020, J. Liu

WIDTH=4.0; HEIGHT=4
size="width=$WIDTH height=$HEIGHT"
LHEIGHT=$(echo $HEIGHT | awk '{print $1 * 0.85}')
LWIDTH=0.15

psize="wbox=$WIDTH; hbox=$HEIGHT"

# sx=11.5
fldr=25

clip="perc=99"
tmax=0.2

windows="min=10 max=110 j=4"
gain="sugain agc=0 wagc=0.1"

dir=firstLine/par_masw_vs_sig3

rawData=$dir/Zfield_SYN/SH_processed_y.shot${fldr}
synData=$dir/Zfield_SYN/SH_computed_y.shot${fldr}

< $synData sushw key=tracf a=1 b=1 |
suchw key1=offset key2=gx key3=sx b=1 c=-1 | 
suwind key=offset min=-1000 max=1000 |surange 

filtering="sufilter f=5,10,50,60 amps=0,1,1,0"

# correct delayed time used during the procedure source wavelet inversion
tmin=0.01
< $synData sushw key=tracf a=1 b=1 |
sushift tmin=$tmin | sushw key=delrt a=0 |
suresamp rf=0.1 |
sukill key=tracf a=26 | 
sukill key=tracf a=38 | 
sukill key=tracf a=41 | 
sukill key=tracf a=44 | 
sukill key=tracf a=56 | 
sukill key=tracf a=56 | 
sukill key=tracf a=63 | 
sukill key=tracf a=72 | 
sukill key=tracf a=94 | 
sukill key=tracf min=17 count=9 | 
suwind key=tracf $windows | $filtering |
suwind tmax=$tmax | sunormalize norm=max > temp/inv.su

# (1) Computed data
< temp/inv.su \
supswigb xbox=0.0 ybox=0.0 wbox=$WIDTH hbox=$HEIGHT $clip  \
x1beg=0 x1end=$tmax f1=0 d1=0.00025 d1num=0.05 n1tic=5 \
f2=1 d2num=10 n2tic=1 title= va=0 \
labelsize=24 label2="Receiver number" label1= > temp/fig11_inv.eps 

< $rawData sushw key=tracf a=1 b=1 |
suresamp rf=0.1 |
suwind key=tracf $windows | $filtering |
suwind tmax=$tmax | sunormalize norm=max > temp/raw.su

# (2) Measured data
< temp/raw.su \
supswigb xbox=0.0 ybox=0.0 wbox=$WIDTH hbox=$HEIGHT $clip  \
x1beg=0 x1end=$tmax f1=0 d1=0.00025 d1num=0.05 n1tic=5 \
f2=1 d2num=10 n2tic=1 title= va=0 \
labelsize=24 label2="Receiver number" label1="Time (s)" > temp/fig11_raw.eps 

# display overlay gathers
ns=$(<temp/raw.su surange | grep ns | awk '{print $2}')
ntr=$(<temp/raw.su surange | grep traces | awk '{print $1 }')
dt=$(<temp/raw.su surange | grep dt | awk '{print $2/1000000}')
((ntrp=$ntr+1))
((npairs=$ntr+$ntr))

echo "Ns=$ns; Ntr=$ntr; Dt=$dt; ntrp=$ntrp"

./c11_print_p2.scr
source paras.txt

# conver su to rsf
sfsuread endian=0 < temp/raw.su \
tfile=temp/tfile > temp/raw.rsf

sfsuread endian=0 < temp/inv.su \
tfile=temp/tfile > temp/inv.rsf

rm -f temp/rawinv.bin
< temp/raw.rsf \
sf2graph x2beg=1 clip=1.2 |
sfrsf2bin >> temp/rawinv.bin

< temp/inv.rsf \
sf2graph x2beg=1 clip=1.2 |
sfrsf2bin >> temp/rawinv.bin

# (3) Measured (black) and computed data
< temp/rawinv.bin psgraph pairs=$npairs d1=$dt \
x2beg=0 x2end=$ntrp labelsize=24 \
$lineWidth $lineColors $Narry \
xbox=0 ybox=0 $psize n1tic=5 d1num=0.05 n2tic=1 d2num=10 \
label1= label2="Receiver number" \
style=seismic title= > temp/fig11_rawinv.eps

# (4) labeling all the subfigures
dx=0.4; dy=0.15; labelsize=32
xlabel=$(echo 0.0 $dx | awk '{print $1 - $2}')
ylabel=$(echo $HEIGHT $dy | awk '{print $1 + $2}')

pslabel t="(a)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_a.eps
pslabel t="(b)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_b.eps
pslabel t="(c)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_c.eps

psmerge translate=0,0 scale=1,1 in=temp/fig11_raw.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_a.eps > temp/fig11_raw_label.eps

psmerge translate=0,0 scale=1,1 in=temp/fig11_inv.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_b.eps > temp/fig11_inv_label.eps

psmerge translate=0,0 scale=1,1 in=temp/fig11_rawinv.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_c.eps > temp/fig11_rawinv_label.eps

# (5) calculate (x,y) positions of each subfigs
scale=0.5; dX=0.5; dY=0.35
# 1st row
x1=0; y1=0
x2=$(echo $WIDTH $scale $dX| awk '{print $1 * $2 + $3}'); y2=$y1
x3=$(echo $WIDTH $scale $x2 $dX| awk '{print $1 * $2 + $3 + $4}'); y3=$y1

# merge into one file
psmerge translate=$x1,$y1 scale=$scale,$scale in=temp/fig11_raw_label.eps \
translate=$x2,$y2 scale=$scale,$scale in=temp/fig11_inv_label.eps \
translate=$x3,$y3 scale=$scale,$scale in=temp/fig11_rawinv_label.eps > figs/fig11_fldr${fldr}.eps

```



Subfunction (2): ```t11b_compareGathers.scr```

```sh
#!/bin/bash
#
# plot measured & computed data
# 20-11-2020, J. Liu

WIDTH=4.0; HEIGHT=4
size="width=$WIDTH height=$HEIGHT"
LHEIGHT=$(echo $HEIGHT | awk '{print $1 * 0.85}')
LWIDTH=0.15

psize="wbox=$WIDTH; hbox=$HEIGHT"

fldr=50

clip="perc=99"
tmax=0.2

windows="min=10 max=110 j=4"
gain="sugain agc=0 wagc=0.1"

dir=firstLine/par_masw_vs_sig3

rawData=$dir/Zfield_SYN/SH_processed_y.shot${fldr}
synData=$dir/Zfield_SYN/SH_computed_y.shot${fldr}

< $synData sushw key=tracf a=1 b=1 |
suchw key1=offset key2=gx key3=sx b=1 c=-1 | 
suwind key=offset min=-1000 max=1000 |surange 

filtering="sufilter f=5,10,50,60 amps=0,1,1,0"

# delayed time during source wavelet inversion
tmin=0.01
< $synData sushw key=tracf a=1 b=1 |
sushift tmin=$tmin | sushw key=delrt a=0 |
suresamp rf=0.1 |
sukill key=tracf a=15 | 
sukill key=tracf a=24 | 
sukill key=tracf a=46 | 
sukill key=tracf min=19 count=9 | 
suwind key=tracf $windows | $filtering |
suwind tmax=$tmax | sunormalize norm=max > temp/inv.su

# (1) Computed data
< temp/inv.su \
supswigb xbox=0.0 ybox=0.0 wbox=$WIDTH hbox=$HEIGHT $clip  \
x1beg=0 x1end=$tmax f1=0 d1=0.00025 d1num=0.05 n1tic=5 \
f2=1 d2num=10 n2tic=1 title= va=0 \
labelsize=24 label2= label1= > temp/fig11_inv.eps 

< $rawData sushw key=tracf a=1 b=1 |
suresamp rf=0.1 |
suwind key=tracf $windows | $filtering |
suwind tmax=$tmax | sunormalize norm=max > temp/raw.su

# (2) Measured data
< temp/raw.su \
supswigb xbox=0.0 ybox=0.0 wbox=$WIDTH hbox=$HEIGHT $clip  \
x1beg=0 x1end=$tmax f1=0 d1=0.00025 d1num=0.05 n1tic=5 \
f2=1 d2num=10 n2tic=1 title= va=0 \
labelsize=24 label2= label1="Time (s)" > temp/fig11_raw.eps 

# display overlay gathers
ns=$(<temp/raw.su surange | grep ns | awk '{print $2}')
ntr=$(<temp/raw.su surange | grep traces | awk '{print $1 }')
dt=$(<temp/raw.su surange | grep dt | awk '{print $2/1000000}')
((ntrp=$ntr+1))
((npairs=$ntr+$ntr))

echo "Ns=$ns; Ntr=$ntr; Dt=$dt; ntrp=$ntrp"

./c11_print_p2.scr
source paras.txt

# conver su to rsf
sfsuread endian=0 < temp/raw.su \
tfile=temp/tfile > temp/raw.rsf

sfsuread endian=0 < temp/inv.su \
tfile=temp/tfile > temp/inv.rsf

rm -f temp/rawinv.bin
< temp/raw.rsf \
sf2graph x2beg=1 clip=1.2 |
sfrsf2bin >> temp/rawinv.bin

< temp/inv.rsf \
sf2graph x2beg=1 clip=1.2 |
sfrsf2bin >> temp/rawinv.bin

# (3) Measured (black) and computed data
< temp/rawinv.bin psgraph pairs=$npairs d1=$dt \
x2beg=0 x2end=$ntrp labelsize=24 \
$lineWidth $lineColors $Narry \
xbox=0 ybox=0 $psize n1tic=5 d1num=0.05 n2tic=1 d2num=10 \
label1= label2= \
style=seismic title= > temp/fig11_rawinv.eps

# (4) labeling all the subfigures
dx=0.4; dy=0.15; labelsize=32
xlabel=$(echo 0.0 $dx | awk '{print $1 - $2}')
ylabel=$(echo $HEIGHT $dy | awk '{print $1 + $2}')

pslabel t="(d)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_d.eps
pslabel t="(e)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_e.eps
pslabel t="(f)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_f.eps

psmerge translate=0,0 scale=1,1 in=temp/fig11_raw.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_d.eps > temp/fig11_raw_label.eps

psmerge translate=0,0 scale=1,1 in=temp/fig11_inv.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_e.eps > temp/fig11_inv_label.eps

psmerge translate=0,0 scale=1,1 in=temp/fig11_rawinv.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_f.eps > temp/fig11_rawinv_label.eps

# (5) calculate (x,y) positions of each subfigs
scale=0.5; dX=0.5; dY=0.35
# 1st row
x1=0; y1=0
x2=$(echo $WIDTH $scale $dX| awk '{print $1 * $2 + $3}'); y2=$y1
x3=$(echo $WIDTH $scale $x2 $dX| awk '{print $1 * $2 + $3 + $4}'); y3=$y1

# merge into one file
psmerge translate=$x1,$y1 scale=$scale,$scale in=temp/fig11_raw_label.eps \
translate=$x2,$y2 scale=$scale,$scale in=temp/fig11_inv_label.eps \
translate=$x3,$y3 scale=$scale,$scale in=temp/fig11_rawinv_label.eps > figs/fig11_fldr${fldr}.eps

```



Subfunction (3): ```c11_print_p2.scr```

```sh
#!/bin/bash
#
# print input parameters for `psgraph`, two data version
# 11-03-2020, J.Liu-4@tudelft.nl

nparas=25

rm -f paras.txt

# print linewidth info
width=2
printf "lineWidth=\"linewidth=" >> paras.txt 
for ((i=1; i<=nparas; i++)) do
    if [ $i -lt $nparas ] 
    then
        printf "$width,"  >> paras.txt
    fi 
   
    if [ $i -eq $nparas ] 
    then
        printf "$width," >> paras.txt
    fi 
done

width=1
for ((i=1; i<=nparas; i++)) do
    if [ $i -lt $nparas ] 
    then
        printf "$width,"  >> paras.txt
    fi 
   
    if [ $i -eq $nparas ] 
    then
        printf "$width\"" >> paras.txt
    fi 
done
printf "\n" >> paras.txt

# print linecolor info
color=black
printf "lineColors=\"linecolor=" >> paras.txt 
for ((i=1; i<=nparas; i++)) do
    if [ $i -lt $nparas ] 
    then
        printf "$color," >> paras.txt
    fi 
   
    if [ $i -eq $nparas ] 
    then
        printf "$color,"  >> paras.txt
    fi 
done

color=red
for ((i=1; i<=nparas; i++)) do
    if [ $i -lt $nparas ] 
    then
        printf "$color," >> paras.txt
    fi 
   
    if [ $i -eq $nparas ] 
    then
        printf "$color\""  >> paras.txt
    fi 
done
printf "\n" >> paras.txt

# print Number of samples  info
ns=801
printf "Narry=\"n=" >> paras.txt
for ((i=1; i<=nparas; i++)) do
    if [ $i -lt $nparas ] 
    then
        printf "$ns," >> paras.txt
    fi 
   
    if [ $i -eq $nparas ] 
    then
        printf "$ns,"  >> paras.txt
    fi 
done

for ((i=1; i<=nparas; i++)) do
    if [ $i -lt $nparas ] 
    then
        printf "$ns," >> paras.txt
    fi 
   
    if [ $i -eq $nparas ] 
    then
        printf "$ns\""  >> paras.txt
    fi 
done
printf "\n" >> paras.txt

```



Main function: ```t11_combine.scr```

```sh
#!/bin/bash
#
# combine subfigures for (fldr=25,50)
./t11a_compareGathers.scr
./t11b_compareGathers.scr

HEIGHT=2.0
scale=1.0; dY=0.4

# calculate (x,y) positions of each subfigs
x1=0; y1=0
y2=$(echo $HEIGHT $scale $dY| awk '{print $1 * $2 + $3}'); x2=$x1

# merge into one file
psmerge translate=$x1,$y1 scale=$scale,$scale in=figs/fig11_fldr50.eps \
translate=$x2,$y2 scale=$scale,$scale in=figs/fig11_fldr25.eps > figs/fig11_merge.eps

open figs/fig11_merge.eps &

```
---

<a href="#top">Back to top</a>

