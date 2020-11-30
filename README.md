# Klasifikasi-Penyakit-Nefritis-dan-Radang-Kandung-Kemih-dengan-Logistik-Regression
# UTS DMKM 2020/2021

library(readxl)
datauts <-read_excel("E:/uts intan/datauts.xlsx")
View(datauts)
data<-as.data.frame(datauts)

library(psych)
## Warning: package 'psych' was built under R version 4.0.3
library(caret)
## Warning: package 'caret' was built under R version 4.0.3
## Loading required package: lattice
## Loading required package: ggplot2
## 
## Attaching package: 'ggplot2'
## The following objects are masked from 'package:psych':
## 
##     %+%, alpha

data$inflamation_of_urinary<-as.factor(data$inflamation_of_urinary)
data$nephritis<-as.factor(data$nephritis)
data$occurance_of_nausea<-factor(data$occurance_of_nausea, levels =c('no', 'yes'), labels=c(0,1))
data$lumbar_pain<-factor(data$lumbar_pain, levels =c('no', 'yes'), labels=c(0,1))
data$urine_pushing<-factor(data$urine_pushing, levels =c('no', 'yes'), labels=c(0,1))
data$micturition_pains<-factor(data$micturition_pains, levels =c('no', 'yes'), labels=c(0,1))
data$burning<-factor(data$burning, levels =c('no', 'yes'), labels=c(0,1))
str(data)

## 'data.frame':    120 obs. of  8 variables:
##  $ temperature           : num  35.5 35.9 35.9 36 36 36 36.2 36.2 36.3 36.6 ...
##  $ occurance_of_nausea   : Factor w/ 2 levels "0","1": 1 1 1 1 1 1 1 1 1 1 ...
##  $ lumbar_pain           : Factor w/ 2 levels "0","1": 2 1 2 1 2 2 1 2 1 1 ...
##  $ urine_pushing         : Factor w/ 2 levels "0","1": 1 2 1 2 1 1 2 1 2 2 ...
##  $ micturition_pains     : Factor w/ 2 levels "0","1": 1 2 1 2 1 1 2 1 2 2 ...
##  $ burning               : Factor w/ 2 levels "0","1": 1 2 1 2 1 1 2 1 2 2 ...
##  $ inflamation_of_urinary: Factor w/ 2 levels "no","yes": 1 2 1 2 1 1 2 1 2 2 ...
##  $ nephritis             : Factor w/ 2 levels "no","yes": 1 1 1 1 1 1 1 1 1 1 ...

## Melihat Korelasi antar variabel
pairs.panels(data)

## Membuat data Training dan Testing
set.seed(1234)
sampel <-sample(2, nrow(data), replace = T, prob =c(0.8,0.2))
trainingset <-data[sampel==1, ]
testingset <-data[sampel==2, ]

