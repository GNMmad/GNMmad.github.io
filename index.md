---
title       : Developing Data Products
subtitle    : Project on shiny and slidify
author      : G. Nevado
framework   : io2012   # {io2012, html5slides, shower, dzslides, ...}
highlighter : prettify  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides

--- &twocol

## Project goals

*** =left
### Shiny application
Write a shiny application with supporting documentation and deploy (and share) it on Rstudio's shiny server. 
Submit code server.R and ui.R to github.
The application must have:
* Some form of input (textbox, radio button, checkbox, ...)
* Some operation on the ui input in sever.R
* Some reactive output displayed as a result of server calculations
* Enough user documentation

*** =right
### Reproducible Pitch Presentation
To pitch the idea, write a presentation that must satisfy the following:
* Done in Slidify or Rstudio Presenter
* 5 pages length
* Hosted on github or Rpubs
* Contains some embedded R code that gets run when slidifying the document


--- .class #id

## Application layout 

This application predicts the specie of an iris plant from the values of Sepal length (4.3 to 7.9 cm), Sepal width (2.0 to 4.4 cm), Petal length (1.0 to 6.9 cm), Petal width (0.1 to 2.5 cm).
The prediction model was trained using the Iris dataset and saved to an RDS file that is read by application.

Side panel: Values for the variables can be set using sliders, with minimum, maximum and default values. After setting values, submit button must be pressed to predict specie based on input values.

Main panel: Has 3 tabs to display results, trained model and documentation.

Tab 1: Result of prediction. Input values and the result of prediction are displayed and updated after submit button is pushed.   
Tab 2: Train model. The train model is displayed. The model was trained using a CART algorithm with default control values, and saved to an RDS file that is read when application starts.   
Tab 3: Train model. Support documentation (this text) is displayed.   

--- 

## Application layout (II)


<img src="app.jpg" />

--- 



## Prediction Model  

The model used for prediction was trained with a CART algorithm, with default control settings.


```r
library(caret)
iris_modelRPART <- readRDS("iris-dataset.RDS")
iris_modelRPART$finalModel
```

n= 120 

node), split, n, loss, yval, (yprob)
      * denotes terminal node

1) root 120 80 setosa (0.33333333 0.33333333 0.33333333)  
  2) Petal.Length< 2.45 40  0 setosa (1.00000000 0.00000000 0.00000000) *
  3) Petal.Length>=2.45 80 40 versicolor (0.00000000 0.50000000 0.50000000)  
    6) Petal.Length< 4.95 41  3 versicolor (0.00000000 0.92682927 0.07317073) *
    7) Petal.Length>=4.95 39  2 virginica (0.00000000 0.05128205 0.94871795) *

