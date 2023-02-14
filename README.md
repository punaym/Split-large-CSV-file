# Split-larg-CSV-file
R-code to split large CSV files into multiple CSV file. Number of rows per file can be selected
---
title: "Split CSV to multiple files"
author: "Punay Mehra"
date: "1/6/2022"
output: html_document
---

```{r setup, include=FALSE}
if( ! require("dplyr")) {install.packages("dplyr")} + library(dplyr)

if( ! require("svDialogs")) {install.packages("svDialogs")} + library(svDialogs)

data<-read.csv(choose.files())


#data<-data[order(data$MSR_TPR_ID), ]
data<-distinct(data)


r=as.integer(dlg_input(message = "Enter number of rows per sheet..Not more then 9lac")$res)
if (r>900000)
  {
  dlg_message(message = "Rows can not be more then 9Lac")

  } else 
    {
x=1
f=1
while (x<nrow(data)) {
  data1<-data[x:(x+r),]
  #write.xlsx2(data1, file="output.xlsx", sheetName=paste0("sheet-",f), row.names=FALSE)
  write.csv(data1,file=paste0("sheet_",f,".csv"), row.names = F)
  x<-x+r
  f<-f+1
}
}
```
