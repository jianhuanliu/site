---
layout: page
title: ch4
description: This page inclues source codes used for preparing the following paper.
permalink: /ch4/
---

**A complete workflow based on surface-wave analysis for characterizing archaeological site: from disperion-curve inversion to full-waveform inversion**


_[Liu J.][Jianhuan], [Draganov D.][Deyan], [Ghose R.][Ranajit] (2020)_, preparing

{% include _mylinks_library.md %}

<script type="text/javascript">
 function showhide(id) {
    var e = document.getElementById(id);
    e.style.display = (e.style.display == 'block') ? 'none' : 'block';
 }
</script>

 <i class="fa fa-sticky-note" aria-hidden="true"></i> <a href="javascript:showhide('article04')">_Abstract_</a>

  <div id="article04" style="display:none;">
  <p>  <div style="font-size:0.85em; text-align: justify;"> Surface-wave analysis is a promising tool for imaging near-surface structures. We develop a complete workflow that can determine subsurface $V_S$ models from shallow field-data. We apply the workflow to a field data recorded at an archaeological site located in Ostia. The goal of this survey is to map the remains of an unexcavated archaeological site in a highly heterogeneous subsurface. The seismic survey consists of two intercrossed seismic line, with one line cover an known tumulus. We make use of a state-of-art 2D MASW technology to invert 2D $V_S$ structures under these lines, which are then provided as the starting models for the sequential 2D elastic FWI inversion. The FWI approach utilize the global correlation norm as objective function, with the aim of reducing different coupling effects at receiver positions. We identified a known tumulus in similar positon in the MASW and FWI results. Compared with MASW sections, the FWI result show high-resolution imaging of the distribution of subsurface heterogenities. The results demonstrate that surface-wave analysis by a combination of MASW and FWI method can be a promising geophysical tool to image shallow small-scale objects in the near-surface field, such as archaeological site. </div> </p>
  </div>

---
#### Figures & scripts:

{% assign projects = site.ch4 %}
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
