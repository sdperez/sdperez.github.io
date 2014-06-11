---
layout: post
title: "My First Shiny App"
---
====================================


I recently completed the first week of the Data Products MOOC on Coursera by Brian Caffo. I took the course primarily to see if they cover the R Shiny package and lo-and-behold the first topic covered was Shiny. I had looked into Shiny before and understood some of it but I didn't understand how to run the app or deploy it, so the class was useful.

Here, I put together a simple Shiny App as a test case. The app shows you a scaterplot of two variables (van Driver deaths and total driver deaths) that show a linear relationship and lets you "guess" the linear regression line by tinkering with the intercept and slope parameters. The app is hosted on the free shinyapps.io server and I embedded it here with an "iframe". Deployment to the shiny server is incredibly easy so hosting your apps there is very convenient.


<iframe src="https://sdperez.shinyapps.io/shinyApp/" width=1000 height=700></iframe> 


####Data
 
I used he 'Seatbelts' dataset that is included in R, which shows monthly driver deaths in England before and after a  seatbelt law was enacted.