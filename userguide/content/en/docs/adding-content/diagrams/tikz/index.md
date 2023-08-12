---
title: "Tikz"
date: 2023-03-31T21:13:54+02:00
draft: false
---

```tikz { disabled=true }
% Author : Hugues Vermeiren
% Replicating triangles
\documentclass[border=10pt]{standalone}
%%%<
\usepackage{verbatim}
%%%>
\begin{comment}
:Title: Replicating triangles
:Tags: Coordinate calculations;Geometry;Foreach;Fun
:Author: Hugues Vermeiren
:Slug: triangles

Replicating triangles, using the 'calc' tikz library.
\end{comment}
\usepackage{tikz}
\usetikzlibrary{calc}

\newcommand{\construct}[3]{
  \foreach \n in {1,...,\nmax} {
    \coordinate (#3) at ($(#2)!0.5!(#3)$);
    \coordinate (D)  at (#2);
    \coordinate (#2) at ($(#2)!1.0!{-60}:(#3)$);
    \coordinate (#1) at (D);
    \fill [blue!10] (#1) -- (#2) -- (#3) -- cycle;
    \draw (#3) -- (#2) -- (#1);
  }
}

\newcommand{\basetriangle}{% equilateral triangle with side 1
  \def\h{0.866025}% sqrt(3)/2
  \coordinate (X) at (-1/2,{-1/3*\h});
  \coordinate (Y) at (1/2,{-1/3*\h});
  \coordinate (Z) at (0,{2/3*\h});
  \fill[blue!10, draw=black] (X) -- (Y) -- (Z) -- cycle;
  }

\def\nmax{8}% nb. of triangles on each branch

\newcommand{\Triangle}[1]{%
  \foreach \coord/\point in {#1} {
    \coordinate (\coord) at (\point);}
  \construct{A}{B}{C}
}

\begin{document}
  \begin{tikzpicture}[scale=7.0]
    \basetriangle
    \Triangle{A/X,B/Y,C/Z}
    \Triangle{C/X,A/Y,B/Z}
    \Triangle{B/X,C/Y,A/Z}
  \end{tikzpicture}
\end{document}
```