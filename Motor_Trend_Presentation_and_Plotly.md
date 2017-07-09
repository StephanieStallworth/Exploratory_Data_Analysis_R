# R Markdown Presentation & Plotly
Stephanie Stallworth  
April 13, 2017  



## R Markdown

This is an R Markdown presentation created using **Knit**, which allows the capability to include content as well as output of embedded R code chunks within a document.  

In this presentation, I will also demonstrate how a `ggplot` object can be turned into an interactive web graphic using the `plotly` package.  

##Plotly Code

```r
#Load packages
library(plotly);library(dplyr);library("datasets")

#Read dataset
data(mtcars)

#Create plot
p <-ggplot(mtcars, aes(x = mpg, y = wt, col = factor(cyl))) + 
        geom_point() + 
        labs(title = "Weight vs Mpg", x = "Mpg",y= "Weight") +
        theme(legend.title = element_blank())

#Pass ggplot object to plotly function and format
ggplotly(p) %>%  add_annotations( text="Cylinder", 
                  xref="paper", yref="paper",
                  x=1.02, xanchor="left",
                  y=0.8, yanchor="bottom",   
                  legendtitle=TRUE, showarrow=FALSE ) %>%
                  layout( legend=list(y=0.8, yanchor="top" ) )
```




##mtcars Interactive Plotly Scatter
<!--html_preserve--><div id="htmlwidget-b387c6bff5b8f3ca6a4a" style="width:720px;height:432px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-b387c6bff5b8f3ca6a4a">{"x":{"data":[{"x":[22.8,24.4,22.8,32.4,30.4,33.9,21.5,27.3,26,30.4,21.4],"y":[2.32,3.19,3.15,2.2,1.615,1.835,2.465,1.935,2.14,1.513,2.78],"text":["mpg: 22.8<br>wt: 2.32<br>factor(cyl): 4","mpg: 24.4<br>wt: 3.19<br>factor(cyl): 4","mpg: 22.8<br>wt: 3.15<br>factor(cyl): 4","mpg: 32.4<br>wt: 2.2<br>factor(cyl): 4","mpg: 30.4<br>wt: 1.62<br>factor(cyl): 4","mpg: 33.9<br>wt: 1.84<br>factor(cyl): 4","mpg: 21.5<br>wt: 2.46<br>factor(cyl): 4","mpg: 27.3<br>wt: 1.94<br>factor(cyl): 4","mpg: 26<br>wt: 2.14<br>factor(cyl): 4","mpg: 30.4<br>wt: 1.51<br>factor(cyl): 4","mpg: 21.4<br>wt: 2.78<br>factor(cyl): 4"],"key":null,"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(248,118,109,1)","opacity":1,"size":5.66929133858268,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(248,118,109,1)"}},"hoveron":"points","name":"4","legendgroup":"4","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text"},{"x":[21,21,21.4,18.1,19.2,17.8,19.7],"y":[2.62,2.875,3.215,3.46,3.44,3.44,2.77],"text":["mpg: 21<br>wt: 2.62<br>factor(cyl): 6","mpg: 21<br>wt: 2.88<br>factor(cyl): 6","mpg: 21.4<br>wt: 3.21<br>factor(cyl): 6","mpg: 18.1<br>wt: 3.46<br>factor(cyl): 6","mpg: 19.2<br>wt: 3.44<br>factor(cyl): 6","mpg: 17.8<br>wt: 3.44<br>factor(cyl): 6","mpg: 19.7<br>wt: 2.77<br>factor(cyl): 6"],"key":null,"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(0,186,56,1)","opacity":1,"size":5.66929133858268,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(0,186,56,1)"}},"hoveron":"points","name":"6","legendgroup":"6","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text"},{"x":[18.7,14.3,16.4,17.3,15.2,10.4,10.4,14.7,15.5,15.2,13.3,19.2,15.8,15],"y":[3.44,3.57,4.07,3.73,3.78,5.25,5.424,5.345,3.52,3.435,3.84,3.845,3.17,3.57],"text":["mpg: 18.7<br>wt: 3.44<br>factor(cyl): 8","mpg: 14.3<br>wt: 3.57<br>factor(cyl): 8","mpg: 16.4<br>wt: 4.07<br>factor(cyl): 8","mpg: 17.3<br>wt: 3.73<br>factor(cyl): 8","mpg: 15.2<br>wt: 3.78<br>factor(cyl): 8","mpg: 10.4<br>wt: 5.25<br>factor(cyl): 8","mpg: 10.4<br>wt: 5.42<br>factor(cyl): 8","mpg: 14.7<br>wt: 5.34<br>factor(cyl): 8","mpg: 15.5<br>wt: 3.52<br>factor(cyl): 8","mpg: 15.2<br>wt: 3.44<br>factor(cyl): 8","mpg: 13.3<br>wt: 3.84<br>factor(cyl): 8","mpg: 19.2<br>wt: 3.85<br>factor(cyl): 8","mpg: 15.8<br>wt: 3.17<br>factor(cyl): 8","mpg: 15<br>wt: 3.57<br>factor(cyl): 8"],"key":null,"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(97,156,255,1)","opacity":1,"size":5.66929133858268,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(97,156,255,1)"}},"hoveron":"points","name":"8","legendgroup":"8","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text"}],"layout":{"margin":{"t":45.7108066971081,"r":7.30593607305936,"b":42.130898021309,"l":31.4155251141553},"plot_bgcolor":"rgba(235,235,235,1)","paper_bgcolor":"rgba(255,255,255,1)","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":"Weight vs Mpg","titlefont":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"xaxis":{"domain":[0,1],"type":"linear","autorange":false,"tickmode":"array","range":[9.225,35.075],"ticktext":["10","15","20","25","30","35"],"tickvals":[10,15,20,25,30,35],"ticks":"outside","tickcolor":"rgba(51,51,51,1)","ticklen":3.65296803652968,"tickwidth":0.66417600664176,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(255,255,255,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":"Mpg","titlefont":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"type":"linear","autorange":false,"tickmode":"array","range":[1.31745,5.61955],"ticktext":["2","3","4","5"],"tickvals":[2,3,4,5],"ticks":"outside","tickcolor":"rgba(51,51,51,1)","ticklen":3.65296803652968,"tickwidth":0.66417600664176,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(255,255,255,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":"Weight","titlefont":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":true,"legend":{"bgcolor":"rgba(255,255,255,1)","bordercolor":"transparent","borderwidth":1.88976377952756,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895},"y":0.8,"yanchor":"top"},"hovermode":"closest","annotations":[{"text":"Cylinder","xref":"paper","yref":"paper","x":1.02,"xanchor":"left","y":0.8,"yanchor":"bottom","legendtitle":true,"showarrow":false}]},"source":"A","config":{"modeBarButtonsToAdd":[{"name":"Collaborate","icon":{"width":1000,"ascent":500,"descent":-50,"path":"M487 375c7-10 9-23 5-36l-79-259c-3-12-11-23-22-31-11-8-22-12-35-12l-263 0c-15 0-29 5-43 15-13 10-23 23-28 37-5 13-5 25-1 37 0 0 0 3 1 7 1 5 1 8 1 11 0 2 0 4-1 6 0 3-1 5-1 6 1 2 2 4 3 6 1 2 2 4 4 6 2 3 4 5 5 7 5 7 9 16 13 26 4 10 7 19 9 26 0 2 0 5 0 9-1 4-1 6 0 8 0 2 2 5 4 8 3 3 5 5 5 7 4 6 8 15 12 26 4 11 7 19 7 26 1 1 0 4 0 9-1 4-1 7 0 8 1 2 3 5 6 8 4 4 6 6 6 7 4 5 8 13 13 24 4 11 7 20 7 28 1 1 0 4 0 7-1 3-1 6-1 7 0 2 1 4 3 6 1 1 3 4 5 6 2 3 3 5 5 6 1 2 3 5 4 9 2 3 3 7 5 10 1 3 2 6 4 10 2 4 4 7 6 9 2 3 4 5 7 7 3 2 7 3 11 3 3 0 8 0 13-1l0-1c7 2 12 2 14 2l218 0c14 0 25-5 32-16 8-10 10-23 6-37l-79-259c-7-22-13-37-20-43-7-7-19-10-37-10l-248 0c-5 0-9-2-11-5-2-3-2-7 0-12 4-13 18-20 41-20l264 0c5 0 10 2 16 5 5 3 8 6 10 11l85 282c2 5 2 10 2 17 7-3 13-7 17-13z m-304 0c-1-3-1-5 0-7 1-1 3-2 6-2l174 0c2 0 4 1 7 2 2 2 4 4 5 7l6 18c0 3 0 5-1 7-1 1-3 2-6 2l-173 0c-3 0-5-1-8-2-2-2-4-4-4-7z m-24-73c-1-3-1-5 0-7 2-2 3-2 6-2l174 0c2 0 5 0 7 2 3 2 4 4 5 7l6 18c1 2 0 5-1 6-1 2-3 3-5 3l-174 0c-3 0-5-1-7-3-3-1-4-4-5-6z"},"click":"function(gd) { \n        // is this being viewed in RStudio?\n        if (location.search == '?viewer_pane=1') {\n          alert('To learn about plotly for collaboration, visit:\\n https://cpsievert.github.io/plotly_book/plot-ly-for-collaboration.html');\n        } else {\n          window.open('https://cpsievert.github.io/plotly_book/plot-ly-for-collaboration.html', '_blank');\n        }\n      }"}],"modeBarButtonsToRemove":["sendDataToCloud"]},"base_url":"https://plot.ly"},"evals":["config.modeBarButtonsToAdd.0.click"],"jsHooks":[]}</script><!--/html_preserve-->

***








###Thank You!

