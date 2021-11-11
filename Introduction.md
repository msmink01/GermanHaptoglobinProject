# Haptoglobin-Project
### Moniek Smink, August 2019
----------
## Table of Contents  
[Introduction](#introduction)  

[Importing and Organizing the Data](#importing-and-organizing-the-data)

[Making New Variables](#making-new-variables)  

[Getting To Know Our Variables](#getting-to-know-our-variables)



--------
## Introduction

Analyzing clinical parameters of dairy cattle to identify associations between serum haptoglobin and precursors for infection.

--------
## Importing and Organizing the Data

```r
#First always set your working directory

setwd("/Users/MoniekSmink/Desktop/R/Hapto")


####### Loading in the RDataset ########

load(file="DD3_hp5_single_CowID_per_BS.Date6_25_19.RData")


####### Making Edits to the data ########

#Let's make a copy of our dataset so we don't tamper with the original
hp6 <- hp5
head(hp6) 
#Our data is now called hp6

#Getting rid of uneccessary variables
hp6$MPR_UID <- NULL
hp6$GER_NR <- NULL
hp6$STAND_DATE <- NULL
hp6$CD_Halsband <- NULL
hp6$CD_Uhrzeit <- NULL
hp6$CD_Lfd_Nr <- NULL
hp6$CD_Dateiname <- NULL
hp6$CD_Betrieb_Nr <- NULL

#Translating some German column names to English
colnames(hp6)[colnames(hp6)=="CD_Umgebungstemp"] <- "CE.Environ.Temp"
colnames(hp6)[colnames(hp6)=="CD_HauTu"] <- "CE.Skin.Dehydration"
colnames(hp6)[colnames(hp6)=="CD_Datum"] <- "CE.Date"
```

--------
## Making New Variables
```r
#We want to create a factor variable that simply states if the cow is lame or not
hp6$CE.Lame<-0
hp6$CE.Lame<-as.numeric(hp6$CE.CE.Lame)
hp6$CE.Lame[hp6$CE.Locomotion.Score==1]<-"0"
hp6$CE.Lame[hp6$CE.Locomotion.Score==2]<-"0"
hp6$CE.Lame[hp6$CE.Locomotion.Score==3]<-"1"
hp6$CE.Lame[hp6$CE.Locomotion.Score==4]<-"1"
hp6$CE.Lame[hp6$CE.Locomotion.Score==5]<-"1"
hp6$CE.Lame<-as.factor(hp6$CE.Lame) #Now we have created a variable with a 1 for lame, and a 0 for not

#Also, when looking at CD_Pans_Sc, which is the Pansen Score of the cows, we notice that the data is spread very thinly among many different levels. Let's combine a few of them in a new variable
hp6$CE.Stom.Fullness<-0
hp6$CE.Stom.Fullness<-as.numeric(hp6$CE.Stom.Fullness)
hp6$CE.Stom.Fullness[hp6$CD_Pans_Sc==0]<-"norm"
hp6$CE.Stom.Fullness[hp6$CD_Pans_Sc==1]<-"norm"
hp6$CE.Stom.Fullness[hp6$CD_Pans_Sc==2]<-"norm"
hp6$CE.Stom.Fullness[hp6$CD_Pans_Sc==3]<-"norm"
hp6$CE.Stom.Fullness[hp6$CD_Pans_Sc==4]<-"abnorm"
hp6$CE.Stom.Fullness[hp6$CD_Pans_Sc==5]<-"abnorm"
hp6$CE.Stom.Fullness<-as.factor(hp6$CE.Stom.Fullness) 
#Now we have a replacement variable for CD_Pans_Sc, so we can get rid of the old one
hp6$CD_Pans_Sc <- NULL

#CD_Kot_K also has data spread thinly across many levels, let's combine a few in a new variable
hp6$CE.Waste.Consistency<-0
levels(hp6$CD_Kot_K)
hp6$CE.Waste.Consistency<-as.numeric(hp6$CE.Waste.Consistency)
hp6$CE.Waste.Consistency[hp6$CD_Kot_K=="db"]<-"thick"
hp6$CE.Waste.Consistency[hp6$CD_Kot_K=="dick"]<-"thick"
hp6$CE.Waste.Consistency[hp6$CD_Kot_K=="sup"]<-"thin"
hp6$CE.Waste.Consistency[hp6$CD_Kot_K=="wäs"]<-"thin"
hp6$CE.Waste.Consistency[hp6$CD_Kot_K=="mb"]<-"norm"
hp6$CE.Waste.Consistency<-as.factor(hp6$CE.Waste.Consistency) 
#Now we have a replacement variable for CD_Kot_K with less levels so we can get rid of the old one
hp6$CD_Kot_K <- NULL

#We want to create a factor variable which states whether the cow has a low or high NEFA level in their blood with a cutoff value of 0.7 ng/mL
hp9$BS.NEFA.0.7<-0
hp9$BS.NEFA.0.7<-as.numeric(hp9$BS.NEFA.0.7)
hp9$BS.NEFA.0.7[hp9$BS.NEFA>=0.7]<-"1"
hp9$BS.NEFA.0.7[hp9$BS.NEFA<0.7]<-"0"
hp9$BS.NEFA.0.7<-as.factor(hp9$BS.NEFA.0.7) #Now we have created a variable with a 1 for a NEFA level above 0.7, and a 0 for below 0.7

#We want to create a factor variable which states whether the cow has a low or high BHBA level in their blood with a cutoff value of 1.2 ng/mL
hp9$BS.BHBA.1.2<-0
hp9$BS.BHBA.1.2<-as.numeric(hp9$BS.BHBA.1.2)
hp9$BS.BHBA.1.2[hp9$BS.BHBA>=1.2]<-"1"
hp9$BS.BHBA.1.2[hp9$BS.BHBA<1.2]<-"0"
hp9$BS.BHBA.1.2<-as.factor(hp9$BS.BHBA.1.2) #Now we have created a variable with a 1 for a BHBA level above 1.2, and a 0 for below 1.2
```
Re-ordering our variables in our data table to make everything easier to read
```r

hp6<-hp6[,c(1,5,4,3,6,7,2,53,55,52,34,47,48:51,8:13,54, 14:23,25,26,33,24,27:32,35:43,57,46,58,44,45,56)]
```
Now we want to export this edited and organized data set to use in tableau later.
```r
####### Exporting hp6 to use in tableau ########
save(hp6,file="MS_hp6.RData")
write.csv(hp6,file="MS_hp6.csv")

```
-------
## Getting To Know Our Variables

hp6 is a data frame with 712 observations and 58 variables. 

These variables consist of:
- 29 Numerical Variables: 
      BS.NEFA, BS.BHBA, Calving.No, MS.DIM, Milk.Yield, MS.Milk.Yield, MS.Fat, MS.Protein, MS.Lactose, MS.S.Cell.Count, MS.Urea, MS.pH, MS.NSFA, MS.Acetone, MS.BHBA, MS.MFA, MS.PFA, MS.SFA, MS.Palmeic, MS.Stearine, MS.Oleic, MS.NEFA, Hapto.Result, CE.Temp, CE.Environ.Temp, CE.Fat.Level, BS.DIM, BS.MS.Date.Difference and Hapto.Log
      
- 23 Factor Variables: 
      CowID, Farm.No, Farm.Name, Cow.Breed, CE.Skin.Dehydration, CE.Stom.Tension, CE.Stom.Layering, CE.Stom.Fluid.Movement, CE.Stom.Ping, CE.Waste.Consistency, CE.Waste.Digestion, CE.Locomotion.Score, CE.Stom.Noise.Freq, Hfr.or.Cow, Hapto.0.1, Hapto.0.35, Hapto.HML, Hapto.HL, CE.Lame, BS.Month, BS.BHBA.1.2, BS.NEFA.0.7, and CE.Stom.Fullness
      
- 9 POSIX Variables: 
      BS.Date, Cow.Birth.Date, Exit.Date, MS.Date.Taken, Calving.Date, MS.Date.Analyzed, CD_DATE, and MS.Time.Taken   
      
-------
