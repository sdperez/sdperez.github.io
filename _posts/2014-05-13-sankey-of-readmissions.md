---
layout: post
title: "Sankey Diagram of Complications and Readmissions"
---
======================================

Sankey Diagrams (credited to Matthew Henry Phineas Riall Sankey 1898) are a type of flow diagram that shows how entities change from one "state" to another. Mathew Sakey used them to track how energy is lost in a mechanical system but perhaps one of the best known (and coolest)use of a Sankey Diagram is [Charles Minard's diagram](http://en.wikipedia.org/wiki/File:Minard.png) of Napoleon's army in 1812 . 

In our case, we thought the diagrams could help us show how patients "flow" from having a complication to being readmitted to the hospital in the 30 days following surgery.
In surgical research, it is known that patient outcomes are not independent from each other; patients who have complications have a higher risk of post-operative readmissions. A Sankey Diagram can help visualize that relationship and see which complications are related to which kinds of readmissions. 



<iframe src="/images/unnamed-chunk-1.html" width=1000 height=700></iframe>


The colored blocks on the left of the diagram represent the quantities of patients who had certain types of complications after surgery (size is proportional to the number of complications). The blocks on the right represent the different reasons for a patient being readmitted (once again size is proportional to the count). The thickness of the lines joining these blocks represent the number of patients that 'flowed' from one state to the other. 

Not surprising, the majority of patients with any of the complications flowed into the 'not readmitted' bucket because, overall, most patients do not come back to the hospital. Among those readmitted, however, some pattern can be discerned. Surgical site infections ('Organ Space SSI, 'Deep Incisional SSI', and 'Superficial SSI') tend to lead to readmissions for infections, based on the relative thickness of those links. These are relationships that need to be studied further.

##Data
The data presented here comes from the 2012 American College of Surgeons National Quality Improvement Project (ACS-NSQIP) public use file. We looked at Vascular surgery cases (N=29,056) but the diagram shows only the 10,170 patients with a complication. 


##Code
The Sankey Diagram was constructed using the rCharts package in R software. The rCharts package actually creates javascript plots from R code. This particular javascript chart is a [D3](http://d3js.org/) visualization created by Mike Bostock . [rCharts](http://rcharts.io/) was created by Ramnath Vaidyanathan  and the template that maps to this particular visualization was created by [TimelyPortfolio](http://timelyportfolio.github.io/rCharts_d3_sankey/example_build_network_sankey.html).
Below is the R code used.

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
  
)

sankeyPlot
```

