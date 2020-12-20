---
layout: post
title: Figure 5
description: Inversion of dispersion curve by NA algorithm.
img: /assets/ch5/thumbnail/ch5_fig05.png
comments: true
---

{% include _mylinks_library.md %}

<script type="text/javascript">
 function showhide(id) {
    var e = document.getElementById(id);
    e.style.display = (e.style.display == 'block') ? 'none' : 'block';
 }
</script>


<img src="{{ '/assets/ch5/ch5_fig05.png' | prepend: site.baseurl | prepend: site.url }}" alt="Figure 05" style="zoom:100%;" />


_Figure 5:_  Results for 1D Neighborhood Algorithm (NA) inversion of picked dispersion data (blacked line in Figure 5c). (a) Comparison between picked dispersion curve of fundamental mode and the calculated dispersion curves from accepted models within misfit less than 1.0 (b) Invered S-wave velocity structure. Theoretical dispersion and corresponging S-wave velocity models are represented with misfit-based colors.
    
---
#### Source code used to reproduce the above figure:
- Type: ```/bin/bash```
- Dependency: [Dinver][Dinver]
- Data availability: Input data is preparing.   

---
<a href="#top">Back to top</a>

