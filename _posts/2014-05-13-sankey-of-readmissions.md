---
layout: post
title: "Sankey Diagram of Complications and Readmissions"
---
======================================
In surgical research you often study patients outcomes such as mortality, complications or readmissions after surgery. These outcomes are not independent, however. Patients who have complications have a higher risk of post-operative readmissions. Below we use a Sankey Diagram (a type of flow diagram)to show the quantities of patients with certain complications who subsequently get readmitted for various reasons.



<iframe src="/images/unnamed-chunk-1.html" width=1000 height=700></iframe>



Because you have so many categories in complications and readmission reasons this would make for a very big table. It's much simpler to understand as a plot.


##Code is below

```r
setwd('C:/Users/sdperez.EMORYUNIVAD/Desktop/My Documents/CurrentStudies/ShipraReadmit')
library(xlsx)
library(rCharts)

###Import Data##########;
data1<-read.xlsx2('Tables/TableforSankey.xlsx',1,stringsAsFactors=F)
#Clean
##Add not readmitted category and relabel readmission categories
data1$ReadmReason<-ifelse(data1$ReadmReason=='.',
                          'Not Readmitted',
                          paste('Readmitted',data1$ReadmReason,sep=':')
                          )
##Relabel complications

colnames(data1) <- c("source","target","value") 
sankeyPlot <- rCharts$new()
#you need the template file to create sankey diagrams.
sankeyPlot$setLib('http://timelyportfolio.github.io/rCharts_d3_sankey') 

sankeyPlot$set(
  data = data1,
  nodeWidth = 15,
  nodePadding = 10,
  layout = 32,
  width = 750,
  height = 600
  #labelFormat = ".1%"
)

sankeyPlot
```

