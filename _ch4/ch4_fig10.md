---
layout: post
title: Figure 10
description: Measured and computed data (Line A)
img: /assets/ch4/thumbnail/ch4_fig10.png
importance: 10
comments: true
---

{% include _mylinks_library.md %}

<script type="text/javascript">
 function showhide(id) {
    var e = document.getElementById(id);
    e.style.display = (e.style.display == 'block') ? 'none' : 'block';
 }
</script>


<img src="{{ '/assets/ch4/ch4_fig10.png' | prepend: site.baseurl | prepend: site.url }}" alt="Figure 10" style="zoom:80%;" />

_Figure 10:_ Comparison between measured and computed data.
    
---
#### Source code used to reproduce the above figure:
- Type: ```/bin/bash```
- Dependency: [Seismic Unix][SU]
- Data availability: Input data is preparing.

##### Subfunction (1): ```t10a_compareGathers.scr```
```sh
#!/bin/bash
#
# Comparison between measured and computed data(with automatic labelling!)
# 20-11-2020, J. Liu

WIDTH=4.0; HEIGHT=4
size="width=$WIDTH height=$HEIGHT"
LHEIGHT=$(echo $HEIGHT | awk '{print $1 * 0.85}')
LWIDTH=0.15

psize="wbox=$WIDTH; hbox=$HEIGHT"

# sx=16.5
fldr=15

clip="perc=99"

tmax=0.3

windows="min=10 max=110 j=4"
gain="sugain agc=0 wagc=0.1"

dir=Paper4_ostia_NEW/shortLine/par_masw_q15_till5st

rawData=$dir/ZfieldProcessed/PSV_processed_y.su.shot$fldr
synData=$dir/ZsynFD/computed_y.su.shot${fldr}

< $synData sushw key=tracf a=1 b=1 |
suchw key1=offset key2=gx key3=sx b=1 c=-1 | 
suwind key=offset min=-1000 max=1000 |surange 

filtering="sufilter f=5,10,30,40 amps=0,1,1,0"

# correct for time delay used during preprocessing step
tmin=0.01
< $synData sushw key=tracf a=1 b=1 |
sushift tmin=$tmin | sushw key=delrt a=0 |
suresamp rf=0.1 |
sukill key=tracf a=82 | 
sukill key=tracf a=93 | 
sukill key=tracf a=96 | 
sukill key=tracf a=109 | 
sukill key=tracf a=116 | 
sukill key=tracf min=31 count=9 | 
suwind key=tracf $windows | $filtering |
suwind tmax=$tmax | sunormalize norm=max > temp/inv.su

# (1) Computed data
< temp/inv.su \
supswigb xbox=0.0 ybox=0.0 wbox=$WIDTH hbox=$HEIGHT $clip  \
x1beg=0 x1end=$tmax f1=0 d1=0.0005 d1num=0.1 n1tic=5 \
f2=1 d2num=10 n2tic=1 title= va=0 \
labelsize=24 label2="Receiver number" label1= > temp/fig10_inv.eps 

< $rawData sushw key=tracf a=1 b=1 |
suresamp rf=0.1 |
suwind key=tracf $windows | $filtering |
suwind tmax=$tmax | sunormalize norm=max > temp/raw.su

# (2) Measured data
< temp/raw.su \
supswigb xbox=0.0 ybox=0.0 wbox=$WIDTH hbox=$HEIGHT $clip  \
x1beg=0 x1end=$tmax f1=0 d1=0.0005 d1num=0.1 n1tic=5 \
f2=1 d2num=10 n2tic=1 title= va=0 \
labelsize=24 label2="Receiver number" label1="Time (s)" > temp/fig10_raw.eps 

# display overlay gathers
ns=$(<temp/raw.su surange | grep ns | awk '{print $2}')
ntr=$(<temp/raw.su surange | grep traces | awk '{print $1 }')
dt=$(<temp/raw.su surange | grep dt | awk '{print $2/1000000}')
((ntrp=$ntr+1))
((npairs=$ntr+$ntr))

echo "Ns=$ns; Ntr=$ntr; Dt=$dt; ntrp=$ntrp"

./c09_print_p2.scr
source paras.txt

# conver su to rsf
sfsuread endian=0 < temp/raw.su \
tfile=temp/tfile > temp/raw.rsf

sfsuread endian=0 < temp/inv.su \
tfile=temp/tfile > temp/inv.rsf

rm -f temp/rawinv.bin
< temp/raw.rsf \
sf2graph x2beg=1 clip=1.5 |
sfrsf2bin >> temp/rawinv.bin

< temp/inv.rsf \
sf2graph x2beg=1 clip=1.5 |
sfrsf2bin >> temp/rawinv.bin

# (3) Measured (black) and computed data
< temp/rawinv.bin psgraph pairs=$npairs d1=$dt \
x2beg=0 x2end=$ntrp labelsize=24 \
$lineWidth $lineColors $Narry \
xbox=0 ybox=0 $psize n1tic=5 d1num=0.1 n2tic=1 d2num=10 \
label1= label2="Receiver number" \
style=seismic title= > temp/fig10_rawinv.eps

# (4) labeling all the subfigures
dx=0.4; dy=0.15; labelsize=32
xlabel=$(echo 0.0 $dx | awk '{print $1 - $2}')
ylabel=$(echo $HEIGHT $dy | awk '{print $1 + $2}')

pslabel t="(a)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_a.eps
pslabel t="(b)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_b.eps
pslabel t="(c)" f="Times-Bold" nsub=1 size=$labelsize > temp/label_c.eps

psmerge translate=0,0 scale=1,1 in=temp/fig10_raw.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_a.eps > temp/fig10_raw_label.eps

psmerge translate=0,0 scale=1,1 in=temp/fig10_inv.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_b.eps > temp/fig10_inv_label.eps

psmerge translate=0,0 scale=1,1 in=temp/fig10_rawinv.eps \
    translate=$xlabel,$ylabel scale=1,1 in=temp/label_c.eps > temp/fig10_rawinv_label.eps

# (5) calculate (x,y) positions of each subfigs
scale=0.5; dX=0.4; dY=0.35
# 1st row
x1=0; y1=0
x2=$(echo $WIDTH $scale $dX| awk '{print $1 * $2 + $3}'); y2=$y1
x3=$(echo $WIDTH $scale $x2 $dX| awk '{print $1 * $2 + $3 + $4}'); y3=$y1


# merge into one file
psmerge translate=$x1,$y1 scale=$scale,$scale in=temp/fig10_raw_label.eps \
translate=$x2,$y2 scale=$scale,$scale in=temp/fig10_inv_label.eps \
translate=$x3,$y3 scale=$scale,$scale in=temp/fig10_rawinv_label.eps > figs/fig10_fldr${fldr}.eps

#open figs/fig10_fldr${fldr}.eps &

```



<br>

##### Subfunction (2): ```c09_print_p2.scr```

```sh
#!/bin/bash
# print parameters for `psgraph` input, two data version
# 11-03-2020, J. Liu

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

width=2
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
color=red
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

color=black
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
ns=601
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



<br>

##### Main function: ```t09_combine.scr```


```sh
#!/bin/bash
#
# combine subfigures for (fldr=15,30)
./t10a_compareGathers.scr
./t10a_compareGathers.scr

HEIGHT=2.0
scale=1.0; dY=0.5

# calculate (x,y) positions of each subfigs
x1=0; y1=0
y2=$(echo $HEIGHT $scale $dY| awk '{print $1 * $2 + $3}'); x2=$x1

# merge into one file
psmerge translate=$x1,$y1 scale=$scale,$scale in=figs/fig10_fldr30.eps \
translate=$x2,$y2 scale=$scale,$scale in=figs/fig10_fldr15.eps > figs/fig10_merge.eps

open figs/fig10_merge.eps &

```

---

<a href="#top">Back to top</a>
