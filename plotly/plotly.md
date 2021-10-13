plotly
================

## What is plotly?

Plotly is a web application for creating and sharing data
visualizations. Plotly can work with several programming languages and
applications (inlcluding R).

## Basic Scatterplot

A basic scatterplot is easy to make, with the added benefit of tooltips
that appear when your mouse hovers over each point. Specify
`mode = "markers"` and `type = "scatter`in the `plot_ly()` function to
create a scatterplot. Note that plotly will choose these values if none
are specified.

``` r
library(plotly)
plot_ly(mtcars, x = ~wt, y = ~mpg, mode = "markers", type = "scatter")
```

Note that in order to access variables from a data frame (here `mtcars`)
the variables have a tilde `~` in front of them.

## Scatterplot Color

Specifying the `color` argument in `plot_ly()` will add color to the
points. Here we are coloring the points based on how many cylinders are
present in each car.

``` r
plot_ly(mtcars, x = ~wt, y = ~mpg,  mode = "markers", type = "scatter", color = ~as.factor(cyl))
```

If instead we wanted a scale of continuous colors we can just pass a
numeric vector instead.

``` r
plot_ly(mtcars, x = ~wt, y = ~mpg,  mode = "markers", type = "scatter", color = ~disp)
```

## Scatterplot Sizing

The `size` argument controls the size of the points.

``` r
plot_ly(mtcars, x = ~wt, y = ~mpg,  mode = "markers", 
        type = "scatter", 
        color = ~as.factor(cyl), 
        size = ~hp)
```

## 3D Scatterplot

To create a 3D scatterplot we just pass an additional variable to the
`z` argument and specify `type = "scatter3d`.

``` r
set.seed(2016-07-21)
temp <- rnorm(100, mean = 30, sd = 5)
pressue <- rnorm(100)
dtime <- 1:100
plot_ly(x = ~temp, y = ~pressue, z = ~dtime,
        type = "scatter3d", color = ~temp)
```

## Line Graphs

In order to create a line graph, change `mode = "lines"`.

``` r
data("airmiles")
plot_ly(x = ~time(airmiles), y = ~airmiles, type = "scatter", mode = "lines")
```

## Multi Line Graph

You can show multiple lines by specifying the column in the data frame
that groups the lines and pass it to `color`:

``` r
library(plotly)
library(tidyr)
library(dplyr)
data("EuStockMarkets")
stocks <- as.data.frame(EuStockMarkets) %>%
  gather(index, price) %>%
  mutate(time = rep(time(EuStockMarkets), 4))
plot_ly(stocks, x = ~time, y = ~price, color = ~index, type = "scatter", mode = "lines")
```

## Histogram

A histogram is great for showing how counts of data are distributed. Use
the `type = "histogram"` argument.

``` r
plot_ly(x = ~precip, type = "histogram")
```

## Boxplot

Boxplots are wonderful for comparing how different datasets are
distributed. Specify `type = "box"` to create a boxplot.

``` r
plot_ly(iris, y = ~Petal.Length, color = ~Species, type = "box")
```
