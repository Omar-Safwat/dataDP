---
title       : "Week 4 Assignment"
subtitle    : Slidify
author      : Omar Safwat
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
--- 

## What does the app do ?

- The purpose of this app is to visually demonstrate the overfitting of data when applying regression models. 

- The user is prompted with a slider input bar to choose an order polynomial for the model to 
fit the data.

--- .class #id

## Outline of UI file


```r
library(shiny)
shinyUI(fluidPage(
    sidebarLayout(
    #Include slider input in side bar panel with a submit button
    ),
    mainPanel(
        #Text output for MSE of training and Validation datasets
        #Plot the fitted model
        #Add a documentation tab to briefly explain the program
    )
))
```

--- .class #id

## Outline of server.r file




```r
#Load the necessary packages and data 
shinyServer(function(input, output) {
    #mdl is fit reactively as the user input changes
    mdl <- reactive({i
        #slider input is assumed to be "2" for this presentation
        deg = 2
        lm(Temp ~ poly(Ozone, deg), data = training)
    })
    #output training and validation sets error (output$pred1 $ output$pred2, 
    #respectively)
    output$pred1 = renderText({
        mean((training$Temp - predict(mdl(), newdata = training))^2)})
    output$pred2 = renderText({mean((y_cv - predict(mdl(), newdata = cv))^2)})
    #plot the data....
})
```

```
##   Training set error Validation set error 
##             36.16538             32.00387
```

--- .class #id

## Thank you!




