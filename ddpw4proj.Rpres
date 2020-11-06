Developing Data Products Week 4 Peer Graded 
========================================================
author: Jayesh Kumar Rout
date: 6/11/2020
autosize: true

First Slide
========================================================

Github repo link of the project
<https://github.com/jayesh265/ddpw4proj>.

Files in the repo
- server.r
- ui.r
- ddpw4proj.rpres

Server.ui code
========================================================


mpgData <- mtcars
mpgData$am <- factor(mpgData$am, labels = c("Automatic", "Manual"))

shinyServer(function(input, output) {
    
    formulaText <- reactive({
        paste("mpg ~", input$variable)
    })
    
    formulaTextPoint <- reactive({
        paste("mpg ~", "as.integer(", input$variable, ")")
    })
    
    fit <- reactive({
        lm(as.formula(formulaTextPoint()), data=mpgData)
    })
    
    output$caption <- renderText({
        formulaText()
    })
    
    output$mpgBoxPlot <- renderPlot({
        boxplot(as.formula(formulaText()), 
                data = mpgData,
                outline = input$outliers)
    })
    
    output$fit <- renderPrint({
        summary(fit())
    })
    
    output$mpgPlot <- renderPlot({
        with(mpgData, {
            plot(as.formula(formulaTextPoint()))
            abline(fit(), col=2)
        })
    })
    
})


ui.r code
========================================================

```{r)
shinyUI(
    navbarPage("Shiny Application",
               tabPanel("Analysis",
                        fluidPage(
                            titlePanel("The relationship between variables"),
                            sidebarLayout(
                                sidebarPanel(
                                    selectInput("variable", "Variable:",
                                                c("No of cyl" = "cyl",
                                                  "Disp" = "disp",
                                                  "total hpr" = "hp",
                                                  "Rear ratio of the axle" = "drat",
                                                  "Wght" = "wt",
                                                  "mile time" = "qsec",
                                                  "v by s" = "vs",
                                                  "Transmission" = "am",
                                                  "no of fwd gears" = "gear",
                                                  "No of carb" = "carb"
                                                )),
                                    
                                    checkboxInput("outliers", "Show BoxPlot's outliers", FALSE)
                                ),
                                
                                mainPanel(
                                    h3(textOutput("caption")),
                                    
                                    tabsetPanel(type = "tabs", 
                                                tabPanel("BoxPlot", plotOutput("mpgBoxPlot")),
                                                tabPanel("Regression model", 
                                                         plotOutput("mpgPlot"),
                                                         verbatimTextOutput("fit")
                                                )
                                    )
                                )
                            )
                        )
               ),
               tabPanel("info abt data",
                        
                        h3("DDP WEEK 4 PROJ BY JAYESH KUMAR ROUT"),
                        helpText("You work for Motor Trend, a magazine about the car business Looking at an informational index of an assortment of vehicles, they are keen on investigating the relationship",
                                 "between a bunch of factors and miles per gallon (MPG) (result). They are especially keen on the accompanying two inquiries: Is a programmed or manual transmission better for MPG. Measure the MPG contrast among programmed and manual transmissions"),
                        h3("Imp"),
                        p("A data frame with few observations and multiple variables"),
                        
                       
               ),
               tabPanel("More Details Regarding data",
                        h2("Motor Trend of the tests of the car on road"),
                        hr(),
                        h3("Descp"),
                        helpText("The data was extracted from a motor magazine published in the states in the year of 1974,",
                                 " and has data about multiple other factors",
                                 " for 32 automobiles"),
                        h3("Format"),
                        p("A data frame with 32 obs on 11 vars."),
                        
                  
                        
                        h3("Source"),
                        
                        p("Henderson and Velleman (1981), Building multiple regression models interactively. Biometrics, 37, 391-411.")
               ),
               tabPanel("Go back to my Github repo",
                        a("https://github.com/jayesh265/ddpw4proj"),
                        hr(),
                        h4("I hope you find this interesting"),
                        h4("The name of the repo is DDPW4PROJ")
               )
    )
)
```
