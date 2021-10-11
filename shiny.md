Shiny
================

## What is Shiny?

-   Shiny is a web application framework for R.
-   Shiny allows you to create a graphical interface so that users can
    interact with your visualizations, models, and algorithms without
    needing to know R themselves.
-   Using Shiny, the time to create simple, yet powerful, web-based
    interactive data products in R is minimized.
-   Shiny is made by R Studio.

## Some Mild Prerequisites

Shiny doesn’t really require it, but as with all web programming, a
little knowledge of HTML, CSS and Javascript is very helpful.

-   HTML gives a web page structure and sectioning as well as markup
    instructions
-   CSS gives the style
-   Javascript for interactivity

Shiny uses Bootstrap (not the statistical boostrap) style, which tends
to look nice and renders well on mobile platforms.

## Getting Started

-   Make sure you have the lastest release of R installed
-   If on Windows, make sure that you have Rtools installed
-   `install.packages("shiny")`
-   `library(shiny)`

## A Shiny Project

A shiny project is a directory containing at least two files:

-   `ui.R` (for user interface) controls how your app looks.
-   `server.R` that controls what your app does.

## HTML Tags in Shiny

Shiny provides serval wrapper functions for using standar HTML tags in
your `us.R`, including `h1()` through `h6()`, `p()`, `a()`, `div()` and
`span()`.

-   See `?builder` for more details