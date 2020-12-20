---
layout: post
title: Figure 3
description: Windowing technology used for surface analysis.
img: /assets/ch4/thumbnail/ch4_fig03.png
importance: 3
comments: true
---

{% include _mylinks_library.md %}

<script type="text/javascript">
 function showhide(id) {
    var e = document.getElementById(id);
    e.style.display = (e.style.display == 'block') ? 'none' : 'block';
 }
</script>


<img src="{{ '/assets/ch4/ch4_fig03.png' | prepend: site.baseurl | prepend: site.url }}" alt="Figure 03" style="zoom:120%;" />

_Figure 3:_ Windowing technology used for surface analysis.
    
---
#### Source code used to reproduce the above figure:
- Type: ```.tex```
- Dependency: [Tikz][Tikz]
- Data availability: Input data is preparing.


```tex
% Schemes for windowing technology for SW analysis
% Author: Jianhuan Liu
% 20-01-2020

\documentclass[tikz,border=10pt]{standalone}
\usepackage{amssymb}
\usepackage{verbatim}
\usepackage{xcolor}
\usepackage{stix}

\usepackage{tikz}
\usetikzlibrary{arrows,shapes,positioning}
\usetikzlibrary{decorations.markings}
\tikzstyle arrowstyle=[scale=1]
\usetikzlibrary{patterns,arrows,calc,decorations.pathmorphing}
\tikzstyle directed=[postaction={decorate,decoration={markings,
    mark=at position .65 with {\arrow[arrowstyle]{stealth}}}}]
\tikzstyle reverse directed=[postaction={decorate,decoration={markings,
    mark=at position .65 with {\arrowreversed[arrowstyle]{stealth};}}}]
    
% Modified \textcircled macro
\renewcommand*\textcircled[1]{\tikz[baseline=(char.base)]{
  \node [shape=circle,draw,inner sep=1pt] (char) {#1};}}

\begin{document}
\begin{tikzpicture}[scale=2.0]
    % variables for pn-junction diagram:
    % all parameters are in tikz scale
    % p-side of the junction is here on the right
%\draw[step=1cm,gray,ultra thin] (0,0) grid (5,5);

\def\Ax{0.5}, \def\Ay{2.0} % start point
\def\StepX{0.3}

% ----> Step (1) <----
% define cooridinates
\coordinate (A) at (\Ax,\Ay);
 
% 1st receiver array
\foreach \i in {0,...,16}
    \draw (\Ax+\i*0.25, \Ay+0.75) node {\color{black}$\blacktriangledown$};

\foreach \i in {6,...,10}
    \draw (\Ax+\i*0.25, \Ay+0.75) node {\color{red}$\blacktriangledown$};
    
\foreach \i in {5}
    \draw (\Ax+\i*0.75-0.1, \Ay+0.75) node {\color{red} $\bigstar$};

\draw (\Ax+16*0.25+0.5, \Ay+0.75) node{\textcolor{blue}{Image $2$}};

\draw (\Ax+16*0.25+0.5, \Ay+0.25) node{\textbf{Stacked image}};

% from here, 2st receivery array     
\foreach \i in {0,...,16}
    \draw (\Ax+\i*0.25, \Ay+1.0) node {\color{black}$\blacktriangledown$};

\foreach \i in {6,...,10}
    \draw (\Ax+\i*0.25, \Ay+1.0) node {\color{red}$\blacktriangledown$};
    
\foreach \i in {1}
    \draw (\Ax+\i*0.75-0.1, \Ay+1.0) node {\color{red} $\bigstar$};

\draw (\Ax+16*0.25+0.5, \Ay+1.0) node{\textcolor{blue}{Image $1$}};

% make the receiver line
\draw [black,thick] (\Ax, \Ay+1.25) -- (\Ax+16*0.25, \Ay+1.25);

\draw (\Ax+6*0.25+0.5, \Ay+1.6) node{\textcolor{blue}{$X_0$}};

% draw selected areas
\draw [fill=gray,draw=none,opacity=0.5] (0.75,2.65) rectangle (1.5,3.25);

\draw [fill=gray,draw=none,opacity=0.5] (0.75+2.75,2.65) rectangle (1.5+2.75,3.25);

\draw [fill=none] (2.0,2.65) rectangle (3.0,3.25);

% 3st receiver array
\foreach \i in {0,...,16}
    \draw (\Ax+\i*0.25, \Ay+2.0) node {\color{black}$\blacktriangledown$};

\foreach \i in {0,...,5}
    \draw (\Ax+\i*0.75-0.1, \Ay+2.0) node {\color{red} $\bigstar$};

\draw (\Ax+2.0, \Ay+2.25) node {Multishot acquisition geometry};

% make the legends
\draw (\Ax+0.2, \Ay) node{\color{red}$\bigstar$ \color{black} Active shot};

\draw (\Ax+0.3, \Ay-0.25) node{\color{black}$\blacktriangledown$ Recorded trace};

\draw (\Ax+0.75, \Ay-0.5) node{\color{red}$\blacktriangledown$ \color{black} Selected trace within range};

\draw (\Ax+2.5, \Ay) node{$\hrectangle$ Selected trace within range};

\draw (\Ax+2.5, \Ay-0.25) node{\color{gray} $\hrectangleblack$ \color{black} Selected shot within range};

\end{tikzpicture}
\end{document}

```
---

<a href="#top">Back to top</a>
