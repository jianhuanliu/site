---
layout: page
title: ch3
description: This page inclues source codes used for preparing the following paper.
permalink: /ch3/
---

**Near-surface diffractor detection at archaeological sites based on an interferometric workflow**

_[Liu J.][Jianhuan], [Draganov D.][Deyan], [Bourgeois Q.][Quentin], [Ghose R.][Ranajit] (2020)_, accepted by **Geophysics**.

{% include _mylinks_library.md %}

<script type="text/javascript">
 function showhide(id) {
    var e = document.getElementById(id);
    e.style.display = (e.style.display == 'block') ? 'none' : 'block';
 }
</script>

 <i class="fa fa-sticky-note" aria-hidden="true"></i> <a href="javascript:showhide('article03')">_Abstract_</a>

  <div id="article03" style="display:none;">
  <p>  <div style="font-size:0.85em; text-align: justify;"> Detecting small-size objects is a primary challenge at archaeological sites due to the high degree of heterogeneity present in the near surface. Although high-resolution reflection seismic imaging often delivers the target resolution of the subsurface in different near-surface settings, the standard processing for obtaining an image of the subsurface is not suitable to map local diffractors. This happens because shallow seismic-reflection data are often dominated by strong surface waves which might cover weaker diffractions, and because traditional common-midpoint moveout corrections are only optimal for reflection events. Here, we propose an approach for imaging subsurface objects using masked diffractions. These masked diffractions are firstly revealed by a combination of seismic interferometry and nonstationary adaptive subtraction, and then further enhanced through crosscoherence-based super-virtual interferometry. A diffraction image is then computed by a spatial summation of the revealed diffractions. We use phase-weighted stack to enhance the coherent summation of weak diffraction signals. Using synthetic data, we show that our scheme is robust in locating diffractors from data dominated by strong Love waves. We test our method on field data acquired at an archaeological site. The resulting distribution of shallow diffractors agrees with the location of anomalous objects identified in the $V_S$ model obtained by elastic SH/Love full-waveform inversion using the same field data. The anomalous objects correspond to the position of a suspected burial, also detected in an independent magnetic survey and corings.</div> </p>
  </div>

---
#### Figures & scripts:

{% assign projects = site.ch3 %}
{% for project in projects  %}

{% if project.redirect %}
<div class="project">
    <div class="thumbnail">
        <a href="{{ project.redirect }}">
        {% if project.img %}
        <img class="thumbnail" src="{{ project.img | prepend: site.baseurl | prepend: site.url }}"/>
        {% else %}
        <div class="thumbnail blankbox"></div>
        {% endif %}    
        <span>
            <h1>{{ project.title }}</h1>
            <br/>
            <p>{{ project.description }}</p>
        </span>
        </a>
    </div>
</div>
{% else %}

<div class="project ">
    <div class="thumbnail">
        <a target="_blank" href="{{ project.url | prepend: site.baseurl | prepend: site.url }}">
        {% if project.img %}
        <img class="thumbnail" src="{{ project.img | prepend: site.baseurl | prepend: site.url }}"/>
        {% else %}
        <div class="thumbnail blankbox"></div>
        {% endif %}    
        <span>
            <h1>{{ project.title }}</h1>
            <br/>
            <p>{{ project.description }}</p>
        </span>
        </a>
    </div>
</div>

{% endif %}

{% endfor %}
