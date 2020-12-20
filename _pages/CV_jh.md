---
layout: cv
permalink: /CV_jh/
title: 简历
description: My cirriculum vitae

profile:
  align: right
  image: 
news: false
social: false
---

{% include _mylinks_library.md %}

<script type="text/javascript">
 function showhide(id) {
    var e = document.getElementById(id);
    e.style.display = (e.style.display == 'block') ? 'none' : 'block';
 }
</script>


下载本人更详细的简历，请点击：<a class="page-link" href="{{ '/CV_jh/CV_jianhuan.pdf' | prepend: site.baseurl | prepend: site.url }}">这里</a>  

------


#### 教育背景:

<ul style="list-style: none;">
<li markdown="1"> 
<i class="fa fa-graduation-cap" aria-hidden="true"></i>
**博士，地球物理**，[代尔夫特理工大学][TUD]，荷兰, (2016年9月 &ndash; 至今)
</li>  
<li markdown="1">
<i class="fa fa-graduation-cap" aria-hidden="true"></i>
**硕士，地球物理**, [中国科学院大学][UCAS]，(2013年9月 &ndash; 2016年6月)
</li>  
<li markdown="1"> 
<i class="fa fa-graduation-cap" aria-hidden="true"></i>
**学士，勘探地球物理**, [吉林大学][JLU], (2009年9月 &ndash; 2013年6月).
</li>  
</ul>


#### 研究兴趣:
- 近地表成像方法
- 全波形反演
- 高性能计算在地球物理成像中的应用等

#### 技术能力：
- 操作系统及软件： Linux, OSX, LaTeX, Vim, Git, Seismic Unix, Madagascar
- C, Python, Matlab, Markdown, Shell , OpenMPI

#### 博士阶段计算机课程及相关证书:
- [并行计算入门(OpenMPI)][MPI2], 2020年12月
- [深度学习入门及进阶][AI], 2020年3月
- [MPI 编程入门][MPI], 2019年5月 
- [高性能计算入门][HPC], 2018年4月

#### 科研经历：
- 意大利罗马[Ostia][Ostia]、荷兰Vassen, Dreumel等地考古遗址地下地球物理成像的研究 (2017年5月– 2020年3月)
  - 作为项目组成员，在考古遗址现场进行了三周的勘查以及地震数据采集的工作
  - 在导师的指导下，进行适合浅地表的地震成像方法的研究
  - 利用提出的方法，处理实际野外数据，获得了研究区域高精度的横波速度结构信息
  - 相关结果将以期刊论文的方式发表。数据、代码也将陆续在个人网站上以开源方式公开

- 共反射面(CRS)叠加成像的研究 (2019年1月 – 2019年9月)
  - 阅读文献，掌握了CRS方法的成像原理； 了解已有实现算法的不足
  - 独立编写了一套适用于高性能计算集群的CRS软件包，近期将于开源方式在个人网站发表

- 利用地震散射响应探测浅地表地下异常体的分布 (2018年5月 – 2019年9月)
  - 提出并实现了一种新的散射成像方法
  - 用于实际数据处理，成果发表在期刊论文上（第一作者）
  - 在2019年欧洲近地表地球物理年会上报告了相关的成果

- 一种基于地震干涉原理的面波压制方法的研究 （2017年6月 – 2018年5月）
  - 提出并实现了一种新的面波压制方法
  - 用于实际数据的处理，成果发表在期刊论文上（第一作者）
  - 在2018年美国勘探地球物理年会上报告了相关的成果

- 地震散射波分离算法的研究 （2017年5月 – 2017年8月）
  - 阅读相关文献，掌握了地震散射波场的特征以及对其进行分离的原理
  - 实现了相关的算法，并编写了相关报告

- 助教，[代尔夫特理工大学][TUD] (2017年4月 – 2019年10月)
  - 野外勘探实践（本科课程)
  - 地球物理成像的理论及上机实验（本科课程）

- 黑龙江省大庆石油公司实习 （2012年7月 – 2012年9月）
  - 参观公司油井开采现场，熟悉常用地球物理勘探软件
  - 处理实际测井数据并编写报告

#### 奖励荣誉:
- 国家留学基金委([CSC][CSC])奖学金 （2016年9月 – 2020年9月）
- [代尔夫特理工大学][TUD]外国留学生奖学金 （2016年9月 – 2018年9月）
- [中国科学院][UCAS]研究生二等学业奖学金 （2013年 – 2016年）
- [吉林大学][JLU]校二等奖学金 （2012年）
- [吉林大学][JLU]地探学院一等奖学金，东荣奖学金（2010年 – 2011年）


#### 已发表科研成果：
##### 期刊论文 

* <a class="page-link" href="{{ '/publication/05_seg_article.pdf' | prepend: site.baseurl | prepend: site.url }}">Near-surface diffractor detection at archaeological sites based on an interferometric workflow</a> <br>
_[Liu J.][Jianhuan], [Draganov D.][Deyan], [Bourgeois Q.][Quentin], [Ghose R.][Ranajit] (2020)_, accepted by **Geophysics**.

  <i class="fa fa-sticky-note" aria-hidden="true"></i> <a href="javascript:showhide('article03')">_Abstract_</a>

  <div id="article03" style="display:none;">
  <p>  <div style="font-size:0.85em; text-align: justify;"> Detecting small-size objects is a primary challenge at archaeological sites due to the high degree of heterogeneity present in the near surface. Although high-resolution reflection seismic imaging often delivers the target resolution of the subsurface in different near-surface settings, the standard processing for obtaining an image of the subsurface is not suitable to map local diffractors. This happens because shallow seismic-reflection data are often dominated by strong surface waves which might cover weaker diffractions, and because traditional common-midpoint moveout corrections are only optimal for reflection events. Here, we propose an approach for imaging subsurface objects using masked diffractions. These masked diffractions are firstly revealed by a combination of seismic interferometry and nonstationary adaptive subtraction, and then further enhanced through crosscoherence-based super-virtual interferometry. A diffraction image is then computed by a spatial summation of the revealed diffractions. We use phase-weighted stack to enhance the coherent summation of weak diffraction signals. Using synthetic data, we show that our scheme is robust in locating diffractors from data dominated by strong Love waves. We test our method on field data acquired at an archaeological site. The resulting distribution of shallow diffractors agrees with the location of anomalous objects identified in the $V_S$ model obtained by elastic SH/Love full-waveform inversion using the same field data. The anomalous objects correspond to the position of a suspected burial, also detected in an independent magnetic survey and corings.</div> </p>
  </div>

* <a class="page-link" href="{{ '/publication/04_fb_article.pdf' | prepend: site.baseurl | prepend: site.url }}">Detection of near-surface heterogeneities at archaeological sites using seismic diffractions</a> <br>
_[Liu J.][Jianhuan], [Bourgeois Q.][Quentin], [Ghose R.][Ranajit] and [Draganov D.][Deyan] (2019)_, **First Break**, 37(9): 93-97.

	<i class="fa fa-sticky-note" aria-hidden="true"></i> <a href="javascript:showhide('article02')">_Abstract_</a>
	<div id="article02" style="display:none;">
	<p>  <div style="font-size:0.85em; text-align: justify;"> We propose a diffraction-imaging method based on optimal summation of seismic diffractions from these objects. An amplitude-unbiased coherency method is used to suppress the incoherent summation
of noise, with the aim to enhance the weak and coherent diffracted signals. The stacking procedure results in a section where diffractions are emphasized and the remaining surface
waves are further suppressed. This diffraction section can be useful for a reliable identification of the local heterogeneities. We demonstrate the reliability of the proposed diffraction imaging method using synthetic and field data.</div> </p>
	</div>



* <a class="page-link" href="{{ '/publication/03_nsg_article.pdf' | prepend: site.baseurl | prepend: site.url }}">Seismic interferometry facilitating the imaging of shallow shear-wave reflections hidden beneath surface waves</a> <br>
_[Liu J.][Jianhuan], [Draganov D.][Deyan] and [Ghose R.][Ranajit] (2018)_, **Near Surface Geophysics**, 16(3): 372-382.

  <i class="fa fa-sticky-note" aria-hidden="true"></i> <a href="javascript:showhide('article01')">_Abstract_</a>
	<div id="article01" style="display:none;">
	<p>  <div style="font-size:0.85em; text-align: justify;"> High-resolution reflection seismics is a powerful tool that can provide the required resolution for subsurface imaging and monitoring in urban settings. Shallow seismic reflection data acquired in soil-covered sites are often contaminated by source-coherent surface waves and other linear moveout noises (LMON) that might be caused by, e.g., anthropogenic sources or harmonic distortion in vibroseis data. In the case of shear-wave seismic reflection data, such noises are particularly
problematic as they overlap the useful shallow reflections. We have developed new schemes for suppressing such surface-wave noise and LMON while still preserving shallow reflections, which are of great interest to high-resolution near-surface imaging. We do this by making use of two techniques. First, we make use of seismic interferometry to retrieve predominantly source-coherent surface waves and LMON. We then adaptively subtract these dominant source-coherent surface waves and LMON from the seismic data in a separate step. We illustrate our proposed method using synthetic and field data. We compare results from our method with results from frequency–wavenumber (f-k) filtering. Using synthetic data, we show that our schemes are robust in separating shallow reflections from source-coherent surface waves and LMON even when they share very similar velocity and frequency contents, whereas f-k filtering might cause undesirable artefacts. Using a field shear-wave reflection dataset characterised by overwhelming LMON, we show that the reflectors at a very shallow depth can be imaged because of significant suppression of the LMON due to the application of the scheme that we have developed. </div> </p>
	</div>


##### 论文集：
* <a class="page-link" href="{{ '/publication/07_book_seismic.pdf' | prepend: site.baseurl | prepend: site.url }}">Ultra-shallow shear-wave reflections locating near-surface buried structures in the unexcavated southern fringe of the ancient Ostia, Rome</a> <br>
_[Ghose R.][Ranajit], [Liu J.][Jianhuan], [Draganov D.][Deyan], [Ngan-Tillard D.][Dominique], Warnaar M., [Brackenhoff J.][Joeri] et al., (2020)_, **Leiden University Press**. 

  <i class="fa fa-sticky-note" aria-hidden="true"></i> <a href="javascript:showhide('book01')">_Abstract_</a>

	<div id="book01" style="display:none;">
  <p>  <div style="font-size:0.85em; text-align: justify;">The southern boundary of Region IV of ancient Ostia coincides with the southern limit of the excavated area of the ancient city. The perceived expanse of the city is influenced by the extent of the excavation. It is not known whether the unexcavated part lying south of Region IV also contains structures of antiquity which might have important historical significance. We have carried out high-resolution, shallow seismic reflection surveys along two profiles, using shear (transverse) waves. The goal of these pilot surveys was to see whether any indication of ultra-shallow scatterers, indicating the potential location of shallow-buried structures, can be found in the shear- wave data. The results show very distinct back- scattered shear-wave arrivals from a mysterious tumulus, whose location along Line A was known. It has been possible to interpret with reasonable confidence the location of several conspicuous, shallow scatterers in the two seismic profiles. Use of shear waves and a high-frequency, electromagnetic shear-wave vibrator was crucial to achieving seismic resolution of nearly 25 cm. The amplitude of the scattered energy is helpful to locate the relatively strong scatterers. Our results suggest that the unexcavated areas located south of Region IV most likely contain buried underground structures. 3-D shear-wave seismic reflections together with new seismic-imaging approaches will be promising to illuminate the unknown shallow subsurface of this important archaeological site in a non-invasive manner.</div> </p>
	</div>

* <a class="page-link" href="{{ '/publication/06_book_GPR.pdf' | prepend: site.baseurl | prepend: site.url }}">Exploring with GPR the frigidarium of the byzantine baths in Ostia Antica after excavation, backfilling and floor re-tiling</a> <br>
_[Ngan-Tillard D.][Dominique], [Draganov D.][Deyan], Warnaar M., [Liu J.][Jianhuan],  [Brackenhoff J.][Joeri] et al., (2020)_, **Leiden University Press**. 

  <i class="fa fa-sticky-note" aria-hidden="true"></i> <a href="javascript:showhide('book02')">_Abstract_</a>

	<div id="book02" style="display:none;">
  <p>  <div style="font-size:0.85em; text-align: justify;">A GPR survey was conducted in the frigidarium of the Byzantine baths in 2017 almost 50 years after the area had been excavated, backfilled and re-tiled using a black and white mosaic. GPR signals are interpreted using photographs of the excavation provided by courtesy of Archivio di disegno as well as drawings and texts produced by scholars to retrace the multiple functions that the site had until the Late Antiquity. It is shown that some ancient reticulated wall structures can be recognised in the GPR data, but not all! There are also prominent GPR features which cannot be identified. We conclude that the partial excavation of the site and the backfilling operation have further complicated the structure of the ground below the mosaic of the Byzantine baths.</div> </p>
	</div>


##### 会议论文：
* Detection of near-surface heterogeneities at archaeological sites using seismic diffractions <br>
_[Liu J.][Jianhuan], [Bourgeois Q.][Quentin], [Ghose R.][Ranajit] and [Draganov D.][Deyan] (2019)_, 25th European Meeting of Environmental and Engineering Geophysics,**EAGE, Den Haag, The Netherlands**.

	<i class="fa fa-sticky-note" aria-hidden="true"></i> <a href="javascript:showhide('abstract03')">_Abstract_</a>
	<div id="abstract03" style="display:none;">
	<p>  <div style="font-size:0.85em; text-align: justify;">We develop a new approach to locate very shallow subsurface objects using seismic diffractions of low signal-to-noise ratio. In our approach we use the diffraction arrivals recorded from the subsurface objects. To image the objects, we apply spatial instantaneous-phase-coherency summation along diffraction hyperbolae. We demonstrate the performance of our method using synthetic and field data.</div> </p>
	</div>


* <a class="page-link" href="{{ '/publication/02_seg_abstract.pdf' | prepend: site.baseurl | prepend: site.url }}">Seismic interferometry facilitating the imaging of shallow seismic reflectors hidden beneath surface waves</a> <br>
_[Liu J.][Jianhuan], [Ghose R.][Ranajit] and [Draganov D.][Deyan] (2018)_, 88th Annual International Meeting, **SEG, California, USA**.

	<i class="fa fa-sticky-note" aria-hidden="true"></i> <a href="javascript:showhide('abstract02')">_Abstract_</a>
	<div id="abstract02" style="display:none;">
  <p>  <div style="font-size:0.85em; text-align: justify;"> High-resolution reflection seismics can be very helpful in subsurface imaging and monitoring in urban environments and in archaeological sites. An obstacle that hinders the success of high-resolution reflection seismic imaging of the very shallow targets is the presence of source-generated surface waves at soil-covered sites and surface waves generated by other anthrogenic sources, e.g., traffic and construction activities in the vicinity of the seismic line. Both of these can hide the very shallow reflection events. We have developed new schemes involving seismic interferometry (SI) to retrieve both source-coherent (and/or source-incoherent) surface waves part of data. The retrieved surface waves are then adaptively subtracted from the raw data, thereby exposing hidden reflections. We illustrate results on both synthetic and field seismic data. We show that artefacts caused by stacking the surface-wave noise are greatly reduced, and that reflectors, especially at very shallow depth, can be much better imaged and interpreted. </div> </p>
	</div>

* <a class="page-link" href="{{ '/publication/01_eage_abstract.pdf' | prepend: site.baseurl | prepend: site.url }}">Revealing very shallow structures in a heterogeneous dyke through interferometric subtraction of surface waves</a> <br>
_[Liu J.][Jianhuan], [Ghose R.][Ranajit] and [Draganov D.][Deyan] (2017)_, 23th Europen Meeting of Environmental and Engineering Geophysics, **EAGE, Malmö, Sweden**.

	<i class="fa fa-sticky-note" aria-hidden="true"></i> <a href="javascript:showhide('abstract01')">_Abstract_</a>
	<div id="abstract01" style="display:none;">
	<p>  <div style="font-size:0.85em; text-align: justify;"> It is challenging to image the very shallow structures in a heterogeneous dyke using traditional geophysical methods. With the aim to reveal these structures, a low-budget seismic S-wave reflection survey was carried out
over a dyke with a fixed-receivers array. We applied seismic interferometry to this dataset in order to retrieve surface waves and then adaptively subtracted these surface waves from the original recordings. Combined interpretation of the stacked images obtained from the original data and that from the data after adaptive subtraction reveals more complete shallow structures inside the dyke.</div> </p>
	</div>


#### 待发表的论文
两篇论文在准备中 ...

***
