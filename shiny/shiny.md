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

-   Make sure you have the latest release of R installed
-   If on Windows, make sure that you have Rtools installed
-   `install.packages("shiny")`
-   `library(shiny)`

## A Shiny Project

A shiny project is a directory containing at least two files:

-   `ui.R` (for user interface) controls how your app looks.
-   `server.R` that controls what your app does.

## HTML Tags in Shiny

Shiny provides several wrapper functions for using standard HTML tags in
your `us.R`, including `h1()` through `h6()`, `p()`, `a()`, `div()` and
`span()`.

-   See `?builder` for more details

## Apps with Inputs and Outputs

Shiny provides several types of inputs including buttons, check boxes,
text boxes, and calendars.

## Apps with Plots

Allowing users to manipulate data and to see the results of their
manipulations as a plot can be very useful. Shiny provides the
`plotOutput()` function for `ui.R` and the `renderPlot()` function for
`server.R` for taking user input and creating plots.

## Reactivity

A reactive expression is like a recipe that manipulates inputs from
Shiny and then returns a value. Reactivity provides a way for your app
to respond since inputs will change depending on how users interact with
your user interface. Expressions wrapped by `reactive()` should be
expressions that are subject to change.

Creating a reactive expression is just like creating a function:

``` r
calc_sum <-reactive({
        input$box1 + input$box2
})

# ...

calc_sum()
```

## Reactive Example

From `ui.R`

``` r
library(shiny)
shinyUI(fluidPage(
    titlePanel("Predict Horsepower from MPG"),
    sidebarLayout(
        sidebarPanel(
            sliderInput("sliderMPG", "What is the MPG of the car?", 10, 35, value = 20),
            checkboxInput("showModel1", "Show/Hide Model 1", value = TRUE),
            checkboxInput("showModel2", "Show/Hide Model 2", value = TRUE)
        ),
        mainPanel(
            plotOutput("plot1"),
            h3("Predicted Horsepower from Model 1:"),
            textOutput("pred1"),
            h3("Predicted Horsepower from Model 2:"),
            textOutput("pred2")
        )
    )
))
```

Notes on this code:

-   Contains a `sliderInput()` and two `checkboxInput()`s in the
    `sidebarPanel()`
-   The `mainPanel()` displays a plot with predictions make by two
    models.

From `server.R` (within the body of `shinyServer()`)

``` r
    mtcars$mpgsp <- ifelse(mtcars$mpg - 20 > 0, mtcars$mpg - 20, 0)
    model1 <- lm(hp ~ mpg, data = mtcars)
    model2 <- lm(hp ~ mpgsp + mpg, data = mtcars)
    
    model1pred <- reactive({
        mpgInput <- input$sliderMPG
        predict(model1, newdata = data.frame(mpg = mpgInput))
    })
    
    model2pred <- reactive({
        mpgInput <- input$sliderMPG
        predict(model2, newdata = 
                    data.frame(mpg = mpgInput,
                               mpgsp = ifelse(mpgInput - 20 > 0,
                                              mpgInput - 20, 0)))
    })
```

-   This block creates two models from the `mtcars` dataset
-   Then a user can generate a prediction from the models using the
    slider (`input$sliderMPG`) - Note that because this is dictated by
    the user we wrap this in `reactive()` - To pass the results of these
    reactive expressions we can just call them `model1pred()` or
    `model2pred()`

## Delayed Reactivity

Sometimes it is preferable for an app to not immediately react to
changes in user input (long-running calculations). You can add a submit
button that will confirm all inputs before running the reactive
expressions.

To update the previous example, we only need one change to `ur.R`:

``` r
library(shiny)
shinyUI(fluidPage(
    titlePanel("Predict Horsepower from MPG"),
    sidebarLayout(
        sidebarPanel(
            sliderInput("sliderMPG", "What is the MPG of the car?", 10, 35, value = 20),
            checkboxInput("showModel1", "Show/Hide Model 1", value = TRUE),
            checkboxInput("showModel2", "Show/Hide Model 2", value = TRUE),
            submitButton("Submit") # NEW
        ),
        mainPanel(
            plotOutput("plot1"),
            h3("Predicted Horsepower from Model 1:"),
            textOutput("pred1"),
            h3("Predicted Horsepower from Model 2:"),
            textOutput("pred2")
        )
    )
))
```

## Advanced UI

There are several other kinds of UI components that you can mix into a
Shiny app including:

-   tabs
-   navbars
-   sidebars

Tabs can be added via the `tabsetPanel()` function, which specifies a
group of tabs, and then the `tabPanel()` function that specifies the
contents of each tab.

## Custom HTML

For more customized UI elements, the `ui.R` file can be replaced with an
`index.html` file and instead of using the various UI functions from
Shiny the user can just write their own HTML instead.

## Interactive Graphics

Shiny also allows for the creation of interactive graphics. One method
for doing so is the `brush` argument of `plotOutput()` function in the
`ui.R` file and using `brushedPoints()` on the `server.R` side.
