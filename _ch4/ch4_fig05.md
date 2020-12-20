---
layout: post
title: Figure 5
description: Dispersion curve inversion by NA algorithm.
img: /assets/ch4/thumbnail/ch4_fig05.png
importance: 5
comments: true
---

{% include _mylinks_library.md %}

<script type="text/javascript">
 function showhide(id) {
    var e = document.getElementById(id);
    e.style.display = (e.style.display == 'block') ? 'none' : 'block';
 }
</script>


<img src="{{ '/assets/ch4/ch4_fig05.png' | prepend: site.baseurl | prepend: site.url }}" alt="Figure 05" style="zoom:70%;" />

_Figure 5:_ Results for 1D Neighborhood Algorithm (NA) inversion of picked dispersion data (blacked line in Figure 5c) at different lateral positions. (a) Comparison between picked dispersion curve of fundamental mode and the calculated dispersion curves from accepted models within misfit less than 1.0 (e) Invered S-wave velocity structure. Theoretical dispersion and corresponging S-wave velocity models are represented with misfit-based colors. (b), (f), (c), (g), (d), (h) are the same as (a)-(e), but for lateral locations at 5 m, 10 m, 15 m. The tumulus is located near lateral location of 23 m.
    
---
#### Source code used to reproduce the above figure:
- Type: ```/bin/bash```
- Dependency: [Dinver][Dinver]
- Data availability: Input data is preparing.

---

<a href="#top">Back to top</a>
