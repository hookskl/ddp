Shiny Gadgets
================

Shiny Gadgets provide a way to use Shiny’s interactivity and user
interface tools as a part of a data analysis.

-   create functions that opens a small Shiny app within RStudio
-   use the `miniUI` package for creating user interfaces.

At its core a Shiny Gadget is a function that launches a small
(single-page) Shiny application. These gadgets are meant to be displayed
in the RStudio viewer pane.

## Advantages

-   Shiny gadgets are functions, and they can take values as arguments
    and return values
-   this means they are more simple to create (no separate `ui.R` and
    `server.R` files required)
