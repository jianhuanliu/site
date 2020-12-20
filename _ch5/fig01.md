---
layout: post
title: Figure 1
description: Scheme for retrieving dominant surface waves by SVI.
img: /assets/ch5/thumbnail/ch5_fig01.png
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


<img src="{{ '/assets/ch5/ch5_fig01.png' | prepend: site.baseurl | prepend: site.url }}" alt="Figure 01" style="zoom:100%;" />

_Figure 1:_ The step for retrieving dominant inline surface waves between by SVI.

---
#### Source code used to reproduce the above figure:
- Type: ```.tex```
- Dependency: [Tikz][Tikz]
- Data availability: NO input data is needed.    


```tex
% Schemes for retrieving SW by VI
% Author: Jianhuan Liu
% 20-01-2020

\documentclass[tikz,border=10pt]{standalone}
%%%<
\usepackage{amssymb}
\usepackage{verbatim}
\usepackage{xcolor}

%%%>

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
%\draw[step=1cm,gray,very thin] (0,0) grid (9,6);

\def\Ax{0.5}, \def\Ay{1.5}
\def\Bx{1.5}, \def\By{1.5}
\def\Cx{2}, \def\Cy{1.5}
\def\Dx{1}, \def\Dy{0.5}
\def\StepX{2.5}, \def\StepY{2}
\def\Shift{0.15}

% ----> Step (1) <----
% define cooridinates
\coordinate (A) at (\Ax,\Ay);
\coordinate (B) at (\Bx,\By);
\coordinate (C) at (\Cx,\Cy);
\coordinate (D) at (\Dx,\Dy);

% nodes at each point
\draw (A) node {$\bigstar$};
\draw (B) node {\color{red}$\blacktriangledown$};
\draw (C) node {\color{blue}$\blacktriangledown$};
%\draw (D) node {$\bullet$};

% add comments at each nodes, suggested by Deyan
\draw (\Ax, \Ay+\Shift) node{\small $X$};
\draw (\Bx, \By+\Shift) node{\small $A$};
\draw (\Cx, \Cy+\Shift) node{\small $B$};
%\draw (\Dx, \Dy-\Shift) node{\small $O$};

%\draw (\Ax,\Dy) node {$\sum_{\bigstar}$};
\draw (\Ax,0.5*\Ay+0.5*\Dy) node {$\sum_{\color{red}\blacktriangledown}$};

\draw (0.5+\Cx, 0.5*\Ay+0.5*\Dy) node {$\bigoplus$};
\draw (\Ax+3.98,\Ay+0.4) node {\large (b) Convolve and stack over $\color{red}\blacktriangledown$ to retrieve super-virtual surface wave at \color{blue}$\blacktriangledown$ \color{black} from $\bigstar$ with higher S/N.};

% connect each nodes
\def\Vy{-0.2}
\draw [black,decorate, decoration={snake,amplitude=1.0mm, segment length=5mm},->] (\Ax, \Vy+\Ay) -- (\Bx, \Vy+\By);
\draw [thick] (A) -- (C);

% ----> Step (2) <----
% new coordinates
\pgfmathsetmacro\Ax{\Ax+\StepX}
\pgfmathsetmacro\Bx{\Bx+\StepX}
\pgfmathsetmacro\Cx{\Cx+\StepX}
\pgfmathsetmacro\Dx{\Dx+\StepX}

% define cooridinates
\coordinate (A) at (\Ax,\Ay);
\coordinate (B) at (\Bx,\By);
\coordinate (C) at (\Cx,\Cy);
\coordinate (D) at (\Dx,\Dy);

% nodes at each point
\draw (A) node {$\bigstar$};
\draw (B) node {\color{red}$\blacktriangledown$};
\draw (C) node {\color{blue}$\blacktriangledown$};
%\draw (D) node {$\bullet$};

% add comments at each nodes, suggested by Deyan
\draw (\Ax, \Ay+\Shift) node{\small $X$};
\draw (\Bx, \By+\Shift) node{\small $A$};
\draw (\Cx, \Cy+\Shift) node{\small $B$};
%\draw (\Dx, \Dy-\Shift) node{\small $O$};

\draw (0.5+\Cx, 0.5*\Ay+0.5*\Dy) node {$\Longrightarrow$};

% connect each nodes
\draw [red,decorate, decoration={snake,amplitude=1.0mm, segment length=5mm},->] (\Bx, \Vy+\By) -- (\Cx, \Vy+\Cy);
\draw [thick] (A) -- (C);

% ----> Step (3) <----
% new coordinates
\pgfmathsetmacro\Ax{\Ax+\StepX}
\pgfmathsetmacro\Bx{\Bx+\StepX}
\pgfmathsetmacro\Cx{\Cx+\StepX}
\pgfmathsetmacro\Dx{\Dx+\StepX}

% define cooridinates
\coordinate (A) at (\Ax,\Ay);
\coordinate (B) at (\Bx,\By);
\coordinate (C) at (\Cx,\Cy);
\coordinate (D) at (\Dx,\Dy);

% nodes at each point
\draw (A) node {$\bigstar$};
\draw (B) node {\color{red}$\blacktriangledown$};
\draw (C) node {\color{blue}$\blacktriangledown$};
%\draw (D) node {$\bullet$};

% add comments at each nodes, suggested by Deyan
\draw (\Ax, \Ay+\Shift) node{\small $X$};
\draw (\Bx, \By+\Shift) node{\small $A$};
\draw (\Cx, \Cy+\Shift) node{\small $B$};
%\draw (\Dx, \Dy-\Shift) node{\small $O$};

% connect each nodes
\draw [black,decorate, decoration={snake,amplitude=1.0mm, segment length=5mm},->] (\Ax, \Vy+\Ay) -- (\Cx, \Vy+\Cy);
\draw [thick] (A) -- (C);

% ----> Step (4) <----
% reset coordinates
\def\Ax{0.5}, \def\Ay{1.5}
\def\Bx{1.5}, \def\By{1.5}
\def\Cx{2}, \def\Cy{1.5}
\def\Dx{1}, \def\Dy{0.5}
\def\StepX{2.5}, \def\StepY{1.8}

% new coordinates
\pgfmathsetmacro\Ay{\Ay+\StepY}
\pgfmathsetmacro\By{\By+\StepY}
\pgfmathsetmacro\Cy{\Cy+\StepY}
\pgfmathsetmacro\Dy{\Dy+\StepY}

% define cooridinates
\coordinate (A) at (\Ax,\Ay);
\coordinate (B) at (\Bx,\By);
\coordinate (C) at (\Cx,\Cy);
\coordinate (D) at (\Dx,\Dy);
% nodes at each point
\draw (A) node {$\bigstar$};
\draw (B) node {\color{red}$\blacktriangledown$};
\draw (C) node {\color{blue}$\blacktriangledown$};
%\draw (D) node {$\bullet$};

% add comments at each nodes, suggested by Deyan
\draw (\Ax, \Ay+\Shift) node{\small $X$};
\draw (\Bx, \By+\Shift) node{\small $A$};
\draw (\Cx, \Cy+\Shift) node{\small $B$};
%\draw (\Dx, \Dy-\Shift) node{\small $O$};

\draw (\Ax,0.5*\Ay+0.5*\Dy) node {$\sum_\bigstar$};
\draw (0.5+\Cx, 0.5*\Ay+0.5*\Dy) node {$\bigotimes$};
\draw (\Ax+3.3,\Ay+0.4) node {\large (a) Crosscorrelate and stack over $\bigstar$ to retrieve a virtual surface wave at \color{blue}$\blacktriangledown$ \color{black} from \color{red}$\blacktriangledown$};

% connect each nodes
\draw [black,decorate, decoration={snake,amplitude=1.0mm, segment length=5mm},->] (\Ax, \Vy+\Ay) -- (\Cx, \Vy+\Cy);
\draw [thick] (A) -- (C);

% ----> Step (5) <----
% reset coordinates
\pgfmathsetmacro\Ax{\Ax+\StepX}
\pgfmathsetmacro\Bx{\Bx+\StepX}
\pgfmathsetmacro\Cx{\Cx+\StepX}
\pgfmathsetmacro\Dx{\Dx+\StepX}

% define cooridinates
\coordinate (A) at (\Ax,\Ay);
\coordinate (B) at (\Bx,\By);
\coordinate (C) at (\Cx,\Cy);
\coordinate (D) at (\Dx,\Dy);
% nodes at each point
\draw (A) node {$\bigstar$};
\draw (B) node {\color{red}$\blacktriangledown$};
\draw (C) node {\color{blue}$\blacktriangledown$};
%\draw (D) node {$\bullet$};
\draw (0.5+\Cx, 0.5*\Ay+0.5*\Dy) node {$\Longrightarrow$};

% add comments at each nodes, suggested by Deyan
\draw (\Ax, \Ay+\Shift) node{\small $X$};
\draw (\Bx, \By+\Shift) node{\small $A$};
\draw (\Cx, \Cy+\Shift) node{\small $B$};

% connect each nodes
\draw [black,decorate, decoration={snake,amplitude=1.0mm, segment length=5mm},->] (\Ax, \Vy+\Ay) -- (\Bx, \Vy+\By);
\draw [thick] (A) -- (C);

% ----> Step (6) <----
% reset coordinates
\pgfmathsetmacro\Ax{\Ax+\StepX}
\pgfmathsetmacro\Bx{\Bx+\StepX}
\pgfmathsetmacro\Cx{\Cx+\StepX}
\pgfmathsetmacro\Dx{\Dx+\StepX}

% define cooridinates
\coordinate (A) at (\Ax,\Ay);
\coordinate (B) at (\Bx,\By);
\coordinate (C) at (\Cx,\Cy);
\coordinate (D) at (\Dx,\Dy);
% nodes at each point
\draw (A) node {$\bigstar$};
\draw (B) node {\color{red}$\blacktriangledown$};
\draw (C) node {\color{blue}$\blacktriangledown$};

% add comments at each nodes, suggested by Deyan
\draw (\Ax, \Ay+\Shift) node{\small $X$};
\draw (\Bx, \By+\Shift) node{\small $A$};
\draw (\Cx, \Cy+\Shift) node{\small $B$};

% connect each nodes
\draw [red,decorate, decoration={snake,amplitude=1.0mm, segment length=5mm},->] (\Bx, \Vy+\By) -- (\Cx, \Vy+\Cy);
\draw [thick] (A) -- (C);

\end{tikzpicture}
\end{document}

```
---

<a href="#top">Back to top</a>   
