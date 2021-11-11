# Creating the Correlograms
--------------
## Table of Contents

[Cleaning the Correlogram Dataset](#cleaning-the-correlogram-dataset)  

[Creating Our First Correlogram](#creating-our-first-correlogram)  

[Creating Our First Simple Pearson Correlation Matrix](#creating-our-first-simple-pearson-correlation-matrix)

[Creating the Fatty Acid Pearson Correlation Matrix](#creating-the-fatty-acid-pearson-correlation-matrix)

[Creating the Clinical Evaluation Pearson Correlation Matrix](#creating-the-clinical-evaluation-pearson-correlation-matrix)

[Creating the Milk Sample Pearson Correlation Matrix](#creating-the-milk-sample-pearson-correlation-matrix)

[Results From Our Correlograms](#results-from-our-correlograms)


------------
## Cleaning the Correlogram Dataset


Before we get into creating the actual correlograms, we first need to edit our dataset and get rid of any factor variables and substitute for dummy-numeric variables.

So let's make a copy of our data just for our correlograms:
```r
chp9 <- hp9
```
Let's get started converting each of the factor variables. For a few of them which are already bi-numerically leveled (0 and 1) we only need to rewrite them as a numeric variable. For others, we will need to group several levels together.


- Cow.Breed
```r
chp9$Cow.Breed
chp9$Cow.Breed<-as.numeric(chp9$Cow.Breed)
chp9$Cow.Breed[chp9$Cow.Breed==1]<-0
chp9$Cow.Breed[chp9$Cow.Breed==2]<-1
```


- Hfr.or.Cow
```r
levels(chp9$Hfr.or.Cow)
chp9$Hfr.or.Cow<-as.numeric(chp9$Hfr.or.Cow)
chp9$Hfr.or.Cow[chp9$Hfr.or.Cow =="1"]<-"0"
chp9$Hfr.or.Cow[chp9$Hfr.or.Cow=="2"]<-"1"
chp9$Hfr.or.Cow<-as.numeric(chp9$Hfr.or.Cow)
```

- BS.Month
```r
levels(chp9$BS.Month)
chp9$BS.Month<-as.numeric(chp9$BS.Month)
chp9$BS.Month[chp9$BS.Month =="1"]<-"0"
chp9$BS.Month[chp9$BS.Month=="2"]<-"1"
chp9$BS.Month[chp9$BS.Month=="3"]<-"1"
chp9$BS.Month[chp9$BS.Month=="4"]<-"1"
chp9$BS.Month[chp9$BS.Month =="5"]<-"0"
chp9$BS.Month[chp9$BS.Month =="6"]<-"0"
chp9$BS.Month[chp9$BS.Month =="7"]<-"0"
chp9$BS.Month<-as.numeric(chp9$BS.Month)
```


- CE.Skin.Dehydration
```r
levels(chp9$CE.Skin.Dehydration)
chp9$CE.Skin.Dehydration<-as.numeric(chp9$CE.Skin.Dehydration)
chp9$CE.Skin.Dehydration[chp9$CE.Skin.Dehydration =="phy"]<-"0"
chp9$CE.Skin.Dehydration[chp9$CE.Skin.Dehydration=="red"]<-"1"
chp9$CE.Skin.Dehydration<-as.numeric(chp9$CE.Skin.Dehydration)
```


- CE.Stom.Tension
```r
levels(chp9$CE.Stom.Tension)
chp9$CE.Stom.Tension<-as.numeric(chp9$CE.Stom.Tension)
chp9$CE.Stom.Tension[chp9$CE.Stom.Tension =="2"]<-"0"
chp9$CE.Stom.Tension[chp9$CE.Stom.Tension=="1"]<-"1"
chp9$CE.Stom.Tension<-as.numeric(chp9$CE.Stom.Tension)
```


- CE.Stom.Layering
```r
levels(chp9$CE.Stom.Layering)
chp9$CE.Stom.Layering<-as.numeric(chp9$CE.Stom.Layering)
chp9$CE.Stom.Layering[chp9$CE.Stom.Layering =="0"]<-"1"
chp9$CE.Stom.Layering[chp9$CE.Stom.Layering=="2"]<-"0"
chp9$CE.Stom.Layering<-as.numeric(chp9$CE.Stom.Layering)
```


- CE.Stom.Fluid.Movement
```r
levels(chp9$CE.Stom.Fluid.Movement)
chp9$CE.Stom.Fluid.Movement<-as.character(chp9$CE.Stom.Fluid.Movement)
chp9$CE.Stom.Fluid.Movement[chp9$CE.Stom.Fluid.Movement =="re"]<-"1"
chp9$CE.Stom.Fluid.Movement[chp9$CE.Stom.Fluid.Movement=="obb"]<-"0"
chp9$CE.Stom.Fluid.Movement<-as.numeric(chp9$CE.Stom.Fluid.Movement)
```


- CE.Stom.Ping 
```r
levels(chp9$CE.Stom.Ping)
chp9$CE.Stom.Ping<-as.character(chp9$CE.Stom.Ping)
chp9$CE.Stom.Ping[chp9$CE.Stom.Ping =="re"]<-"1"
chp9$CE.Stom.Ping[chp9$CE.Stom.Ping=="obb"]<-"0"
chp9$CE.Stom.Ping<-as.numeric(chp9$CE.Stom.Ping)
```


- CE.Stom.Fullness
```r
levels(chp9$CE.Stom.Fullness)
chp9$CE.Stom.Fullness<-as.character(chp9$CE.Stom.Fullness)
chp9$CE.Stom.Fullness[chp9$CE.Stom.Fullness =="abnorm"]<-"1"
chp9$CE.Stom.Fullness[chp9$CE.Stom.Fullness=="0"]<-NA
chp9$CE.Stom.Fullness[chp9$CE.Stom.Fullness=="norm"]<-"0"
chp9$CE.Stom.Fullness<-as.numeric(chp9$CE.Stom.Fullness)
```


- CE.Stom.Noise.Freq
```r
levels(chp9$CE.Stom.Noise.Freq)
chp9$CE.Stom.Noise.Freq<-as.character(chp9$CE.Stom.Noise.Freq)
chp9$CE.Stom.Noise.Freq[chp9$CE.Stom.Noise.Freq =="phy"]<-"0"
chp9$CE.Stom.Noise.Freq[chp9$CE.Stom.Noise.Freq=="groe_3"]<-"1"
chp9$CE.Stom.Noise.Freq[chp9$CE.Stom.Noise.Freq=="bis_2"]<-"1"
chp9$CE.Stom.Noise.Freq<-as.numeric(chp9$CE.Stom.Noise.Freq)
```


- CE.Waste.Consistency
```r
levels(chp9$CE.Waste.Consistency)
chp9$CE.Waste.Consistency<-as.character(chp9$CE.Waste.Consistency)
chp9$CE.Waste.Consistency[chp9$CE.Waste.Consistency =="0"]<-NA
chp9$CE.Waste.Consistency[chp9$CE.Waste.Consistency =="norm"]<-"0"
chp9$CE.Waste.Consistency[chp9$CE.Waste.Consistency=="thick"]<-"1"
chp9$CE.Waste.Consistency[chp9$CE.Waste.Consistency=="thin"]<-"1"
chp9$CE.Waste.Consistency<-as.numeric(chp9$CE.Waste.Consistency)
```


- CE.Waste.Digestion
```r
levels(chp9$CE.Waste.Digestion)
chp9$CE.Waste.Digestion<-as.character(chp9$CE.Waste.Digestion)
chp9$CE.Waste.Digestion[chp9$CE.Waste.Digestion =="gut"]<-"0"
chp9$CE.Waste.Digestion[chp9$CE.Waste.Digestion=="maess"]<-"1"
chp9$CE.Waste.Digestion[chp9$CE.Waste.Digestion=="schl"]<-"1"
chp9$CE.Waste.Digestion<-as.numeric(chp9$CE.Waste.Digestion)
table(chp9$CE.Waste.Digestion)
```


- CE.Lame
```r
levels(chp9$CE.Lame)
chp9$CE.Lame<-as.numeric(chp9$CE.Lame)
chp9$CE.Lame[chp9$CE.Lame=="1"]<-"0"
chp9$CE.Lame[chp9$CE.Lame=="2"]<-"1"
chp9$CE.Lame<-as.numeric(chp9$CE.Lame)
table(chp9$CE.Lame)
```


- BS.BHBA.1.2
```r
levels(chp9$BS.BHBA.1.2)
chp9$BS.BHBA.1.2<-as.numeric(chp9$BS.BHBA.1.2)
chp9$BS.BHBA.1.2[chp9$BS.BHBA.1.2=="1"]<-"0"
chp9$BS.BHBA.1.2[chp9$BS.BHBA.1.2=="2"]<-"1"
chp9$BS.BHBA.1.2<-as.numeric(chp9$BS.BHBA.1.2)
table(chp9$BS.BHBA.1.2)
```



- BS.NEFA.0.7
```r
levels(chp9$BS.NEFA.0.7)
chp9$BS.NEFA.0.7<-as.numeric(chp9$BS.NEFA.0.7)
chp9$BS.NEFA.0.7[chp9$BS.NEFA.0.7=="1"]<-"0"
chp9$BS.NEFA.0.7[chp9$BS.NEFA.0.7=="2"]<-"1"
chp9$BS.NEFA.0.7<-as.numeric(chp9$BS.NEFA.0.7)
table(chp9$BS.NEFA.0.7)
```



- Hapto0.35
```r
levels(chp9$Hapto0.35)
chp9$Hapto0.35<-as.numeric(chp9$Hapto0.35)
chp9$Hapto0.35[chp9$Hapto0.35=="1"]<-"0"
chp9$Hapto0.35[chp9$Hapto0.35=="2"]<-"1"
chp9$Hapto0.35<-as.numeric(chp9$Hapto0.35)
table(chp9$Hapto0.35)
```



Now let's get rid of the other uneccessary variables.

```r
chp9$CE.Locomotion.Score <- NULL #we have CE.Lame
chp9$CE.Date <- NULL
chp9$MS.Date.Analyzed <- NULL
chp9$Calving.Date <- NULL
chp9$MS.Time.Taken <- NULL
chp9$MS.Date.Taken <- NULL
chp9$Cow.Exit.Date <- NULL
chp9$BS.DATE <- NULL
chp9$Farm.Name <- NULL
chp9$Farm.No <- NULL
chp9$CowID <- NULL
chp9$Cow.Birth.Date <- NULL
chp9$Hapto0.35.2 <- NULL
chp9$Hapto.Result <- NULL
chp9$Hapto.0.1 <- NULL
chp9$Hapto.HML <- NULL
chp9$Hapto.HL <- NULL
chp9$MS.Acetone <- NULL
chp9$MS.BHBA <- NULL
chp9$MS.S.Cell.Count <- NULL
chp9$BS.BHBA <- NULL
chp9$BH.NEFA <- NULL

str(chp9)
```
Now when we look at the structure of our dataset, there are only numerical variables.


The next step is to get rid of all NA's since correlograms do not work with them.
```r
chp9 <- na.omit(chp9)
head(chp9)
```

Now our dataset is all cleaned up and ready for correlogramification. 



----------
# Creating Our First Correlogram


Now that we have our dataset as all numerics with no na's we can create our first simple correlogram.

This correlogram will contain all variables (not just the statistically significant ones). The goal is to see possible correlation clusters between our variables.

Here is the r code to create this correlogram:
```r
corrs <- cor(chp9)
corrs1 <- as.data.frame(corrs)
corrs1
```

Then we will export this correlogram into a csv so we can color code it in excel:
```r
#write out as a csv file
write.csv(corrs1,file = "corrs1matrix.csv")
```

After color coding here is what part of our correlogram looks like:

<img src="https://user-images.githubusercontent.com/52465712/61298169-0c276f00-a7de-11e9-8479-d3848ff73ba6.png" width="1000">

We can already begin to see some clusters of variables that are related such as NEFA levels, fat levels, and all the fatty acid levels which makes sense since they all measure kind of the same thing. 




--------------
# Creating Our First Simple Pearson Correlation Matrix

Now we want to create a correlogram with a bit more meaning. Let's create a correlogram where we can see not just the correlation coefficients but the correlation graphics as well. 

For this correlogram we only want to use statistically significant variables. In our case that includes 28 variables. 

Let's start out by making a smaller correlogram with only very 'important' variables.

First we need to make the dataframe with only those variables:
```r
#Create the dataframe
chp9.4 <- chp9.2

#Get rid of uneccessary variables
chp9.2$Cow.Breed <- NULL
chp9.2$BS.MS.Date.Difference <- NULL
chp9.2$BS.DIM <- NULL
chp9.2$Hapto0.35 <- NULL
chp9.2$BS.NEFA <- NULL
chp9.2$Calving.No <- NULL
chp9.2$MS.NSFA <- NULL
chp9.2$MS.MFA <- NULL
chp9.2$MS.PFA <- NULL
chp9.2$MS.SFA <- NULL
chp9.2$MS.Palmeic <- NULL
chp9.2$MS.Stearine <- NULL
chp9.2$MS.Oleic <- NULL
chp9.2$CE.Temp <- NULL
chp9.2$CE.Fat.Level <- NULL
chp9.2$CE.Stom.Layering <- NULL
chp9.2$CE.Stom.Fluid.Movement <- NULL
chp9.2$CE.Stom.Ping <- NULL
chp9.2$CE.Waste.Digestion <- NULL
chp9.2$BS.BHBA.Log <- NULL
chp9.2$MS.Acetone.Log <- NULL
chp9.2$BS.NEFA.0.7 <- NULL
chp9.2$CE.Skin.Dehydration <- NULL
chp9.2$CE.Stom.Tension <- NULL
chp9.2$CE.Stom.Fullness <- NULL
chp9.2$CE.Stom.Noise.Freq <- NULL
chp9.2$CE.Waste.Consistency <- NULL
chp9.2$MS.Urea  <- NULL
chp9.2$BS.BHBA.1.2 <- NULL
chp9.2$MS.Milk.Yield <- NULL
chp9.2$MS.pH <- NULL
chp9.2$MS.Lactose <- NULL
chp9.2$MS.Fat <- NULL
chp9.2$MS.Protein <- NULL
chp9.2$MS.S.Cell.Count.Log <- NULL
chp9.2$CE.Environ.Temp <- NULL
chp9.2$Hapto0.35 <- NULL

names(chp9.2)
```

Now that we have the formatted dataframe we can create the correlogram.
```r
op <- par(mfrow = c(1,1), pty = "s")
pairs(chp9.2, lower.panel = panel.smooth, upper.panel = panel.cor, diag.panel = panel.hist, main = "Pearson Correlation Matrix")
par(op)

```

Here it is:

<img src="https://user-images.githubusercontent.com/52465712/61363007-83fba500-a883-11e9-848c-b45ebe949a3a.png" width="1000">



From this matrix we can see the magnitude and direction of each correlation. 

We can see for instance that Milk.Yield is strongly and negatively correlated with Hapto.Log, meaning that the higher the cow's milk yield, the lower the cow's haptoglobin amount.



-------------
# Creating The Fatty Acid Pearson Correlation Matrix


One part that has always been interesting about this dataset was the impact of the different fatty acids on the cow's haptoglobin levels. So let's create a Pearson Correlation Matrix to explore these relationships.


First we need to create and format a new dataframe:
```r
#Copying the dataframe from before
chp9.5 <- chp9.2

#Getting rid of other variables
chp9.5$MS.DIM <- NULL

#Adding the fatty acid variables
chp9.5$MS.SFA <- chp9$MS.SFA
chp9.5$MS.MFA <- chp9$MS.MFA
chp9.5$MS.PFA <- chp9$MS.PFA
chp9.5$MS.Palmeic <- chp9$MS.Palmeic
chp9.5$MS.Stearine <- chp9$MS.Stearine
chp9.5$MS.Oleic <- chp9$MS.Oleic
```

Then we need to code the matrix:
```r
op <- par(mfrow = c(1,1), pty = "s")
pairs(chp9.5, lower.panel = panel.smooth, upper.panel = panel.cor, diag.panel = panel.hist, main = "Pearson Correlation Matrix - Fatty Acids")
par(op)
```


Then here is the matrix:

<img src="https://user-images.githubusercontent.com/52465712/61460161-7a9b3700-a96e-11e9-921d-8b40e4439734.png" width="1000">


From this matrix we can see that: 
- MS.SFA and MS.Palmeic have very less impact on a cow's haptoglobin levels than the other fatty acids. 
- MS.NEFA.Log is highly correlated with all fatty acids except MS.SFA and MS.Palmeic.
- MS.BHBA.Log is highly correlated with all the fatty acids with no exceptions. 
- BS.Month has some impact on some of the fatty acids including MS.Palmeic and MS.SFA.

Overall, the fatty acids seem to act similarly within two groups. One group contains MS.Palmeic and MS.SFA. The other group contains MS.NSFA, MS.PFA, MS.MFA, MS.Stearine, and MS.Oleic. 

As for the Haptoglobin levels, these variables are positively correlated with Hapto.Log: Amount of Non-Saturated Fatty Acids (MS.NSFA 0.25), Amount of Polysaturated Fatty Acids (MS.PFA 0.284), Amount of Monosaturated Fatty Acids (MS.MFA 0.265), Amount of Stearine Fatty Acids (MS.Stearine 0.254), and Amount of Oleic Fatty Acids (MS.Oleic 0.257)


-----------
# Creating the Clinical Evaluation Pearson Correlation Matrix

We now want to look into the variables recorded during the clinical evaluation of the cow. These are all the variables with CE in the front of it such as CE.Environ.Temp which is the environmental temperature during the clinial eval.

To create this matrix, we first need to create and format a dataset with all the statistically significant CE variables and other important variables.
```r
chp9.6 <- chp9.2

names(chp9.6)
chp9.6$MS.DIM <- NULL
chp9.6$Milk.Yield <- NULL
chp9.6$MS.Milk.Yield <- NULL
chp9.6$MS.Protein <- NULL
chp9.6$MS.Lactose <- NULL
chp9.6$MS.Urea <- NULL
chp9.6$MS.pH <- NULL
chp9.6$BS.NEFA.Log <- NULL
chp9.6$MS.S.Cell.Count.Log <- NULL
chp9.6$BS.BHBA.1.2 <- NULL
```

Now to code the creation of the matrix:
```r
pairs(chp9.6, lower.panel = panel.smooth, upper.panel = panel.cor, diag.panel = panel.hist, main = "Pearson Correlation Matrix - Milk Sample")
par(op)
```


And here is the correlation matrix:

<img src="https://user-images.githubusercontent.com/52465712/61453942-bd094780-a95f-11e9-9929-070e8f65ba24.png" width="1000">

Here are some things we can tell from this correlation:

- CE.Lame is highly positively correlated with a cow's haptoglobin level, if the cow is lame, it is very likely they have a higher haptoglobin level.
- CE.Stom.Fullness is negatively correlated with a cow's haptoglobin level. The more normal the stomach of the cow is filled the more likely it is that the cow has high haptoglobin levels.
- CE.Environ.Temp is postively correlated with a cow's haptoglobin level. The higher the surrounding temperatures during the clinical evaluation, the higher the cow's haptoglobin level is likely to be.
- CE.Stom.Fullness and CE.Environ.Temp are negatively correlated. The more normal a cow's stomach fill is the more likely that the temperature is higher.
- CE.Lame and CE.Environ.Temp are positively correlated. This means that if a cow is lame it is more likely that the environmental temperature is higher.
- CE.Skin.Dehydration and CE.Lame are positively correlated. If a cow is dehydrated it is more likely that it is also lame.
- CE.Stom.Tension and CE.Stom.Fullness are positively correlated. If the cow's stomach is abnormally filled it is more likely that there is abnormal tension. 
- CE.Stom.Fullness and CE.Lame are strongly negatively correlated. If the stomach is abnormally filled it is more likely that the cow is not lame.
- CE.Lame and CE.Stom.Noise.Freq are positively correlated. If a cow is lame it is more likely to have an abnormal stomach noise frequency. 


------------
# Creating the Milk Sample Pearson Correlation Matrix

We now want to look into the variables recorded through the analysis of the milk sample taken from the cow. These are all the variables with MS in the front of it such as MS.Protein which is the percentage of protein found in the milk sample.

To create this matrix, we first need to create and format a dataset with all the statistically significant MS variables and other important variables.
```r
chp9.7 <- chp9.2

names(chp9.7)
MS.Milk.Yield
chp9.7$CE.Skin.Dehydration <- NULL
chp9.7$CE.Stom.Fullness <- NULL
chp9.7$CE.Stom.Tension <- NULL
chp9.7$CE.Stom.Noise.Freq <- NULL
chp9.7$CE.Waste.Consistency <- NULL
chp9.7$CE.Lame <- NULL
chp9.7$BS.BHBA.1.2 <- NULL
chp9.7$BS.NEFA.Log <- NULL
```

Now to code the creation of the matrix:
```r
pairs(chp9.7, lower.panel = panel.smooth, upper.panel = panel.cor, diag.panel = panel.hist, main = "Pearson Correlation Matrix - Milk Sample")
par(op)
```

And here is the correlation matrix:

<img src="https://user-images.githubusercontent.com/52465712/61456948-9949ff80-a967-11e9-8085-39c21e9e6132.png" width="1000">

Here are some things we can tell from this matrix: 

- Milk.Yield is strongly negatively correlated with a cow's haptoglobin level. The higher the cow's milk yield the lower the haptoglobin level is likely to be. 
- MS.S.Cell.Count.Log is strongly positively correlated with a cow's haptoglobin level. The higher the cell count, the higher the haptoglobin level is likely to be.
- MS.Acetone.Log is positively correlated with Hapto.Log. The higher the acetone percentage of the milk sample it is more likely that the cow's haptoglobin level will be higher.
- Hfr.or.Cow is negatively correlated with both Milk.Yield and MS.Protein. If the cow is a heifer they are more likely to have a low milk yield and a low protein percentage. 
- Hfr.or.Cow is postively correlated with MS.Lactose. If the cow is a heifer they are more likely to have a high lactose percentage in their milk.
- MS.DIM is negatively associated with MS.Protein and positively associated with MS.Lactose. The higher the days in milk the lower the protein percentage and the higher the lactose percentage.
- Milk.Yield has a positive correlation with MS.Milk.Yield and a negative correlation with MS.S.Cell.Count.Log. If the cow's average milk yield is high, it is more likely for the cow's milk sample milk yield to be high, and more likely for the cow's somatic cell count to be low. 
- MS.Fat has a negative correlation with MS.Lactose and a strong positive correlation with MS.Urea, MS.S.Cell.Count.Log, MS.Acetone.Log, and MS.BHBA.Log. If the fat percentage of the milk sample is high it is likely that the lactose percentage is low, the urea percentage is high, the somatic cell count is high, the acetone percentage is high, and the BHBA level is high.
- MS.Protein has a strong negative correlation with MS.Lactose, MS.Urea, and CE.Environ.Temp. The higher the protein percentage in the milk sample it is likely that the lactose percentage will be lower, the urea percentage will be lower, and the environmental temperature will be lower.
- MS.Urea is positively associated with MS.BHBA.Log and MS.Acetone.Log. The higher the urea percentage of the milk sample the higher the BHBA level and the higher the acetone percentage was likely to be.
- MS.pH is negatively associated with both CE.Environ.Temp and MS.BHBA.Log. The higher the pH of the milk sample the lower the environmental temp and the lower the BHBA level is likely to be. 
- MS.S.Cell.Count.Log is negatively associated with MS.Lactose and positively associated with MS.BHBA.Log and MS.Acetone.Log. The higher the somatic cell count the lower the percent lactose, the higher the BHBA level, and the higher the acetone percentage was likely to be.
- MS.BHBA.Log and MS.Acetone.Log were strongly positively associated. The higher the BHBA level, the higher the acetone percentage of the milk sample is likely to be. 




---------------
# Results From Our Correlograms

From our correlograms we have found that the following variables impact a cow's haptoglobin levels:

- Positively Correlated: Lameness/Locomotion Score (CE.Lame 0.42), Environmental Temperature (CE.Environ.Temp 0.292), Somatic Cell Count in the Milk Sample (MS.S.Cell.Count.Log 0.376), Acetone Percentage in the Milk Sample (MS.Acetone.Log 0.249), Amount of Non-Saturated Fatty Acids (MS.NSFA 0.25), Amount of Polysaturated Fatty Acids (MS.PFA 0.284), Amount of Monosaturated Fatty Acids (MS.MFA 0.265), Amount of Stearine Fatty Acids (MS.Stearine 0.254), and Amount of Oleic Fatty Acids (MS.Oleic 0.257)
- Negatively Correlated: Average Milk Yield (Milk.Yield -0.397), and Fill of the Stomach (CE.Stom.Fullness -0.31)


