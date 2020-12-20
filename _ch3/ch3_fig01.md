---
layout: post
title: Figure 1
description: Flowchart for diffraction imaging proposed in this paper.
img: /assets/ch3/thumbnail/ch3_fig01.png
importance: 1
comments: true
---

{% include _mylinks_library.md %}

<script type="text/javascript">
 function showhide(id) {
    var e = document.getElementById(id);
    e.style.display = (e.style.display == 'block') ? 'none' : 'block';
 }
</script>


<img src="{{ '/assets/ch3/ch3_fig01.png' | prepend: site.baseurl | prepend: site.url }}" alt="Figure 01" style="zoom:100%;" />

_Figure 1:_ Flowchart for raw-data processing for diffraction imaging. To reveal weak diffractions, a combination of seismic interferometry (SI) and adaptive subtraction (AS) is firstly used to suppress dominating surface waves (SW). A crosscoherence-based super-virtual interferometry (SVI) is then applied to further enhance the diffractions.

---
#### Source code used to reproduce the above figure:
- Type: ```.tex```
- Dependency: [Tikz][Tikz]
- Data availability: NO input data is needed.  


```tex
% Workflow
% Based on Tikz examples by Pavel Seda
% Author: Jianhuan Liu
% 20-01-2020


\documentclass[border=10pt]{standalone}
\usepackage{tikz}
\usetikzlibrary{arrows.meta}
\tikzset{
  >={Latex[width=2mm,length=2mm]},
  % Specifications for style of nodes:
            base/.style = {rectangle, rounded corners, draw=black,
                           minimum width=4cm, minimum height=1cm,
                           text centered, font=\sffamily},
  activityStarts/.style = {base, fill=blue!30},
       startstop/.style = {base, fill=red!30},
    activityRuns/.style = {base, fill=green!30},
         process/.style = {base, minimum width=2.5cm, fill=orange!15,
                           font=\ttfamily},
}
\begin{document}    
% Drawing part, node distance is 1.5 cm and every node
% is prefilled with white background
\begin{tikzpicture}[node distance=1.5cm,
    every node/.style={fill=white, font=\sffamily}, align=center]
  % Specification of nodes (position, etc.)
  \node (start)             [activityStarts]              {Raw data};
  \node (onCreateBlock)     [process, below of=start,yshift=-1cm]          {Data after trace editing, static correction, \\ geometrical-spreading correction, etc.};
  \node (onStartBlock)      [process, below of=onCreateBlock, yshift=-1cm]   {Data after SW suppression,  which is \\ done with a conbination of  seismic \\ interferometry (SI) and adaptive subtraction (AS).};
  \node (onResumeBlock)     [process, below of=onStartBlock, yshift=-1cm]   {Data after diffraction enhencement, using \\ crosscoherence-based super-virtual interferometry (SVI).};
  \node (activityRuns)      [activityRuns, below of=onResumeBlock, yshift=-1cm]
                                                      {Diffraction section};
    
  % Specification of lines between nodes specified above
  % with aditional nodes for description 
  \draw[->]             (start) -- node[text width=3cm]{Pre-processing} (onCreateBlock);
  \draw[->]     (onCreateBlock) -- node[text width=3cm]{SI+AS} (onStartBlock);
  \draw[->]      (onStartBlock) -- node[text width=3cm]{SVI} (onResumeBlock);
  \draw[->]     (onResumeBlock) -- node[text width=3cm]{Diffraction imaging} (activityRuns);
  
  \end{tikzpicture}
\end{document}

```
---

<a href="#top">Back to top</a>
