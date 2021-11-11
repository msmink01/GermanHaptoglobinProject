# Descriptive Statistics

--------------------------
## Table of Contents  

[Descriptive Statistics - Factor Variables](#descriptive-statistics---factor-variables)

[Descriptive Statistics - Numerical Variables](#descriptive-statistics---numerical-variables)  

[Descriptive Statistics - Log Transformations of Skewed Numerical Variables](#descriptive-statistics---log-transformations-of-skewed-numerical-variables)  


---------
## Descriptive Statistics - Factor Variables


#### Cow.Breed - Breed of the cow, represented by numbers, 1 = Simmental  & 2 = Braunvieh
```r
#Frequency table
table(hp6$Cow.Breed)
# 1   2 
# 437 275 

#61.4% of the cows are Simmental, 38.6% are Braunveih
```
Bar Graph:
<img src="https://user-images.githubusercontent.com/52465712/60673106-48221200-9e77-11e9-9ec9-8c341ec6e536.png" width="300">

#### CE.Skin.Dehydration - Elasticity of the skin of the cow to measure the dehydration, "phy" = normal, "red" = abnormal
```r
#Frequency table
table(hp6$CE.Skin.Dehydration)
#phy red 
#674  26 

#94.6% are normal, 5.4% are abnormal

```
Bar Graph:
<img src="https://user-images.githubusercontent.com/52465712/60673001-0b561b00-9e77-11e9-808e-c5a64614b62f.png" width="300">

#### CE.Stom.Tension - Measurement of abdominal tension aka stomach aches, "phy" = normal, "erh" = abnormal
```r
#Frequency table
table(hp6$CE.Stom.Tension)
#erh phy 
#50 649 

#7.0% are abnormal, 93% are normal
```
Bar Graph:
<img src="https://user-images.githubusercontent.com/52465712/60672811-a1d60c80-9e76-11e9-8121-f19e41dd6d19.png" width="300">

#### CE.Stom.Fluid.Movement - Movement of fluids in the stomach, "obb" = normal, "re" = abnormal
```r
#Frequency table
table(hp6$CE.Stom.Fluid.Movement)
#obb  re 
#672  26 

#94.4% are normal, 5.6% are abnormal
```
Bar Graph:
<img src="https://user-images.githubusercontent.com/52465712/60673029-232d9f00-9e77-11e9-9edf-37447dd3f69b.png" width="300">

#### CE.Stom.Ping - Ping of the stomach, "obb" = normal, "re" = abnormal
```r
#Frequency table
table(hp6$CE.Stom.Ping)
#obb  re 
#696   4  

#97.8% are normal, 2.2% are abnormal
```
Bar Graph:
<img src="https://user-images.githubusercontent.com/52465712/60672991-0002ef80-9e77-11e9-81df-e19bd3f44c45.png" width="300">

#### CE.Waste.Consistency - Waste Consistency, "thick", "normal", "thin"
```r
#Frequency table
table(hp6$CE.Waste.Consistency)
# 0  norm thick  thin 
# 0   524    53   115 

#75.7% are normal, 7.7% are thick, 16.6% are thin
```
Bar Graph:
<img src="https://user-images.githubusercontent.com/52465712/68156000-7d676b00-ff10-11e9-8d12-18be57d6c463.png" width="300">

#### CE.Waste.Digestion - How well food has been digested by the cow, "gut" = good, "maess" = less than good, "schl" = bad
```r
#Frequency table
table(hp6$CE.Waste.Digestion)
#gut maess  schl 
#522   164     4

#73.3% are well-digested, 23.0% are mildly-digested, 0.6% are terribly-digested
```
Bar Graph:
<img src="https://user-images.githubusercontent.com/52465712/60672787-8b2fb580-9e76-11e9-9fe5-abdcbbe4e7e9.png" width="300">

#### CE.Stom.Noise.Freq - Frequency of Rumen Rumbles, "phy" = normal (3 per minute), "bis_2" = under-active (less than 3 per minute), "groe_3" = over-active (more than 3 per minute)
```r
#Frequency table
table(hp6$CE.Stom.Noise.Freq)
#bis_2 groe_3    phy 
#52     26    146

#23.2% are under-active, 11.6% are over-active, 65.2% are normal
```
Bar Graph:
<img src="https://user-images.githubusercontent.com/52465712/60673012-16a94680-9e77-11e9-8f41-b34875d35128.png" width="300">

#### CE.Stom.Layering - Layering of the rumen, 0 = abnormal layering, 1 = normal layering
```r
#Frequency table
table(hp6$CE.Stom.Layering)
#  0   1 
# 20 678 

#2.9% are abnormally layered, 97.1% are normally layered
```
Bar Graph:
<img src="https://user-images.githubusercontent.com/52465712/60672867-c03c0800-9e76-11e9-8f3f-84da012d672a.png" width="300">

#### CE.Stom.Fullness - Measure of how full the stomach is, "norm" = normal, "abnorm" = abnormal
```r
#Frequency table
table(hp6$CE.Stom.Fullness)
#  0   high    low normal 
# 13      4     24    671 

#96% are normal, 0.6% are high, 3.4% are low
```
Bar Graph:
<img src="https://user-images.githubusercontent.com/52465712/68156003-7e000180-ff10-11e9-9b67-3a7f1b6b4dcb.png" width="300">

#### CE.Locomotion.Score - Locomotion Score, 1 & 2 = okay, 3, 4, & 5 = lame
```r
#Frequency table
table(hp6$CE.Locomotion.Score)
#1   2   3   4   5 
#375 230  59  22   2 

#87.9% are okay, 12.1% are lame
```
Bar Graph:
<img src="https://user-images.githubusercontent.com/52465712/60673083-3f314080-9e77-11e9-8404-f5a7b8260cd1.png" width="300">


#### Hfr.or.Cow - Is it a heifer or a cow?
```r
#Frequency table
table(hp6$Hfr.or.Cow)
# cow hfr 
#505 207

#70.9 are cows, 29.1% are heifers
```
Bar Graph:
<img src="https://user-images.githubusercontent.com/52465712/60673067-36d90580-9e77-11e9-9416-68869788c1fd.png" width="300">

#### Lame - is the cow lame, 1 = yes, 0 = no
```r
#Frequency table
table(hp6$CE.CE.Lame)
#0   1 
#605  83 

#87.9% were not lame, 12.1% were lame
```
Bar Graph:
<img src="https://user-images.githubusercontent.com/52465712/60672775-7f43f380-9e76-11e9-8874-39363a6ff349.png" width="300">

#### BS.Month - Month the blood sample was taken
```r
#Frequency table
table(hp6$BS.Month)
#06-2018 07-2018 08-2018 09-2018 10-2018 11-2018 12-2018 
#63      93     131      87     137     135      66

#8.8% were taken in June, 13.1% were taken in July, 18.3% were taken in August, 12.2% were taken in September, 19.2% were taken in October, 19.0% were taken in November, 9.2% were taken in December
```
Bar Graph:
<img src="https://user-images.githubusercontent.com/52465712/60672203-0db77580-9e75-11e9-9701-1b250ff4da12.png" width="300">


#### Hapto.0.1 - is this cow's haptoglobin level above 0.1? 1 = yes (>0.1), 0 = no (<0.1)
```r
#Frequency table
table(hp6$Hapto.0.1)
#  0   1 
#448 264 

#62.9% are below 0.1, 37.1% are above 0.1
```
Bar Graph:
<img src="https://user-images.githubusercontent.com/52465712/61126293-5b9f2f80-a4ac-11e9-83a8-85eead1818a9.png" width="300">

#### Hapto.0.35 - is this cow's haptoglobin level above 0.35? 1 = yes (>0.35) 0 = no (<0.35)
```r
#Frequency table
table(hp6$Hapto.0.35)
#  0   1 
#529 183

#74.3% are below 0.35, 25.7% are above 0.35
```
Bar Graph:
<img src="https://user-images.githubusercontent.com/52465712/61126294-5cd05c80-a4ac-11e9-9411-b2b319ce9566.png" width="300">

#### Hapto.HML - states whether this cow has low, medium, or high hapto levels according to a model, 0 = low (<0.4), 1 = medium (1.599>x>0.4), 2 = high (>1.6
```r
#Frequency table
table(hp6$Hapto.HML)
#  0   1   2 
#537  42 133 

#75.4% have low hapto levels, 5.9% have medium hapto levels, 18.7% have high hapto levels
```
Bar Graph:
<img src="https://user-images.githubusercontent.com/52465712/60672958-e82b6b80-9e76-11e9-82fa-7b54ef43ef92.png" width="300">

#### Hapto.HL - states whether this cow has high or low hapto levels according to a model, medium taken out, 1 = low, 3 = high
```r
#Frequency table
table(hp6$Hapto.HL)
#  1   3 
#537 133 

#80.1% have low hapto levels, 19.9% have high hapto levels
```
Bar Graph:
<img src="https://user-images.githubusercontent.com/52465712/60672983-f7aab480-9e76-11e9-88dc-98f1670d78c9.png" width="300">

#### BS.NEFA.0.7 - States whether the cow had a high or low blood NEFA level, 1 = >=0.7, 0 = <0.7
```r
#Frequency table
table(hp9$BS.NEFA.0.7)
#  0   1 
#572 140 
#80.3% had low NEFA levels, 19.7% had high NEFA levels
```
Bar Graph:
<img src="https://user-images.githubusercontent.com/52465712/60884932-88560b80-a24e-11e9-8cf9-d54fbbc394e1.png" width="300">

#### BS.BHBA.1.2 - States whether the cow had a high or low blood BHBA level, 1 = >=1.2, 0 = <1.2
```r
#Frequency table
table(hp9$BS.BHBA.1.2)
#  0   1 
#576 136 
#80.9% had low BHBA levels, 19.1% had high BHBA levels
```
Bar Grpah:
<img src="https://user-images.githubusercontent.com/52465712/60884939-8ee48300-a24e-11e9-9fd5-e8394bb98c65.png" width="300">

--------------
## Descriptive Statistics - Numerical Variables

#### BS.NEFA - NEFA levels in the blood (ng/mL)
```r
#Summary
summary(hp6$BS.NEFA)
#Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
#0.0200  0.1800  0.3400  0.4494  0.6200  2.3700 
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60725989-b8de3280-9f3a-11e9-8f4f-77699b54a8bd.png" width="300">
 
#### BS.BHBA - BHBA levels in the blood (ng/ml)
```r
#Summary
summary(hp6$BS.BHBA)
#   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
#0.1700  0.5875  0.7450  0.9144  1.0300  5.7700 
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60725977-b24fbb00-9f3a-11e9-8ff0-a5275f01f1b5.png" width="300">


#### BS.DIM - number of days after calving that the blood sample took place (days)
```r
#Summary
summary(hp6$BS.DIM)
#   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
#5.00   14.00   19.00   19.53   25.00   35.00 
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60726054-e5924a00-9f3a-11e9-878e-36d0c40e6492.png" width="300">


#### BS.MS.Date.Difference - days difference between the milk sample and the blood sample (days)
```r
#Summary
summary(hp6$BS.MS.Date.Difference)
#   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
#-1.0000  0.0000  1.0000  0.5548  1.0000  2.0000 
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60725894-7f0d2c00-9f3a-11e9-8f73-9a4d6b1cfcae.png" width="300">


#### Calving.No - Number of calves this cow has had (calves)
```r
#Summary
summary(hp6$Calving.No)
#   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
#1.000   1.000   3.000   3.044   4.000  11.000 
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60725961-a5cb6280-9f3a-11e9-9e41-900b37dd6ca6.png" width="300">


#### MS.DIM - How many days after calving was the milk sampled (days)
```r
#Summary
summary(hp6$MS.DIM)
#Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
#3.00   14.00   19.00   18.97   24.00   35.00 
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60725967-abc14380-9f3a-11e9-919c-db598f34b0bc.png" width="300">


#### Milk.Yield - Milk per day (kg)
```r
#Summary
summary(hp6$Milk.Yield)
#Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
#   1.40   26.75   32.60   32.19   37.75   62.90     325 
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60726018-cf848980-9f3a-11e9-939d-d95b4c80aaba.png" width="300">


#### MS.Milk.Yield - Kg of milk of that milk sample (kg)
```r
#Summary
summary(hp6$MS.Milk.Yield)
#   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
#0.40   11.00   13.70   14.92   17.60   46.30 
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60726086-0064be80-9f3b-11e9-9d8c-c97c43dad357.png" width="300">

#### MS.Fat - % fat of the milk (%)
```r
#Summary
summary(hp6$MS.Fat)
#   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
#1.260   3.820   4.365   4.490   5.072   9.450 
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60726006-c5628b00-9f3a-11e9-9a28-e0aae88ddf28.png" width="300">


#### MS.Protein - % protein of the milk (%)
```r
#Summary
summary(hp6$MS.Protein)
#   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
#2.420   3.060   3.260   3.284   3.480   5.980 
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60725907-86ccd080-9f3a-11e9-96c3-2cef8205f337.png" width="300">


#### MS.Lactose - % lactose of the milk (%)
```r
#Summary
summary(hp6$MS.Lactose)
#   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
#2.840   4.730   4.840   4.828   4.950   5.270
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60725924-92b89280-9f3a-11e9-8cbc-75be71fecdd6.png" width="300">


#### MS.S.Cell.Count - amount of somatic cells in the milk (1000 cells/mL)
```r
#Summary
summary(hp6$MS.S.Cell.Count)
#   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
#10.0    24.0    50.0   194.3   147.5  6260.0 
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60802124-86217d80-a178-11e9-97d0-a089bb14cfba.png" width="300">


#### MS.Urea - % Urea measurement (%)
```r
#Summary
summary(hp6$MS.Urea)
# Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
#7.30   19.98   24.10   24.95   28.60   79.40 
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60726003-bf6caa00-9f3a-11e9-8489-a7bb9f45a7b6.png" width="300">


#### MS.pH - pH measurement of the milk
```r
#Summary
summary(hp6$MS.pH)
#   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
#6.060   6.590   6.650   6.636   6.690   6.840 
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60726038-da3f1e80-9f3a-11e9-90fe-98797d8ccafe.png" width="300">

#### MS.Acetone - Acetone in milk (UNIT?)
```r
#Summary
summary(hp6$MS.Acetone)
#   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
#10.0    50.0    90.0   137.8   160.0  1920.0     191
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60726047-e034ff80-9f3a-11e9-8576-c42c8cafd804.png" width="300">


#### MS.BHBA - amount of BHBA in milk (ng/mL)
```r
#Summary
summary(hp6$MS.BHBA)
#   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
#10.00   40.00   60.00   76.99  100.00  470.00     110
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60725937-99470a00-9f3a-11e9-9ace-d20458ea0ab7.png" width="300">


#### MS.NEFA - amount of NEFA in milk (ng/mL)
```r
#Summary
summary(hp6$MS.NEFA)
#   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
#0.100   2.035   4.900   4.864   7.600   9.900     173 
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60725948-9f3ceb00-9f3a-11e9-84bb-9612b451dcf2.png" width="300">


#### MS.NSFA - Amount of non-saturated fatty acids in the milk (Micro mole/L)
```r
#Summary
summary(hp6$BS.NEFA)
#Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
#0.0200  0.1800  0.3400  0.4494  0.6200  2.3700 
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60726028-d57a6a80-9f3a-11e9-9679-f6ab6ee6fd16.png" width="300">


#### MS.MFA - Amount of monounsaturated fatty acids in the milk (Micro mole/L)
```r
#Summary
summary(hp6$MS.MFA)
#   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
#0.359   1.044   1.258   1.373   1.607   3.282     290
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60726012-ca273f00-9f3a-11e9-8571-3766d8cafb39.png" width="300">

#### MS.PFA - Amount of polyunsaturated fatty acids in the milk (Micro Mole/L)
```r
#Summary
summary(hp6$MS.PFA)
#   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
#0.0190  0.1310  0.1510  0.1578  0.1820  0.3160     290 
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60725884-7583c400-9f3a-11e9-920a-074544c58a7f.png" width="300">


#### MS.SFA - Amount of short fatty acids in the milk (Micro mole/L)
```r
#Summary
summary(hp6$MS.SFA)
#   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
#0.831   2.245   2.562   2.631   3.003   5.865     290 
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60726064-ea56fe00-9f3a-11e9-9a03-3664b39a2f74.png" width="300">


- MS.Palmeic - Amount of palmeic fatty acid in the milk (Micro mole/L)
```r
#Summary
summary(hp6$MS.Palmeic)
#   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
#0.5070  0.9593  1.0830  1.1159  1.2448  2.5250     290  
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60726110-11adcb00-9f3b-11e9-97f8-574bba498c4e.png" width="300">


#### MS.Stearine - Amount of stearine fatty acid in the milk (Micro mole/L)
```r
#Summary
summary(hp6$Ms.Stearine)
#   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
#0.1570  0.4090  0.4870  0.5198  0.6145  1.0930     290 
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60725916-8cc2b180-9f3a-11e9-945b-6d319622bf64.png" width="300">

#### MS.Oleic - Amount of oleic acid in the milk (Micro mole/L)
```r
#Summary
summary(hp6$Ms.Oleic)
#   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
#0.2150  0.9483  1.1655  1.2731  1.5245  3.2270     290 
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60726094-08246300-9f3b-11e9-82b2-a48a15dc9064.png" width="300">


#### Hapto.Result/Hapto.Log - Amount of Haptoglobin (ng/mL)
```r
#Summary
summary(hp6$Hapto.Result)
#     Min.   1st Qu.    Median      Mean   3rd Qu.      Max. 
#   140.0     280.0     462.3   79256.4    3854.9 2561350.0 
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60726100-0c508080-9f3b-11e9-85dc-65a5f30496db.png" width="300">


#### CE.Temp - Inner body temperature of the cow (celsius)
```r
#Summary
summary(hp6$CE.Temp)
#   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
#  37.2    38.3    38.5    38.6    38.7    83.0      14 
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60726076-f478fc80-9f3a-11e9-81ec-57e9f16d8ef9.png" width="300">


#### CE.Environ.Temp - Environmental temperature during the clinical evaluation (celsius)
```r
#Summary
summary(hp6$CE.Environ.Temp)
#   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
#  1.00   11.10   17.00   16.63   21.60   32.40      39 
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60726071-ef1bb200-9f3a-11e9-8c7f-02a644109bac.png" width="300">


#### CE.Fat.Level - Fat level on the back of the cow (mm)
```r
#Summary
summary(hp6$CE.Fat.Level)
#   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
#  3.00   12.00   16.00   16.55   20.00   50.00      17 
```
Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60726082-f93db080-9f3a-11e9-80d3-4d0d2ad8c0f2.png" width="300">

-------------
## Descriptive Statistics - Log Transformations of Skewed Numerical Variables
      
```r
#Let's keep a copy of the dataset without the log variables, just in case
hp9 <- hp6
#Our new data set is called hp9
```


#### Hapto.Result --> Hapto.Log

Since this variable is skewed very far right, we need to log transform it. 
```r
#Creating the new log transformed variable
#We first check if there are any 0's in the original data because if a value in the data is 0, the log transformation will fail
hp9$Hapto.Result 
#Now that we know there are no 0's we can create the new log version variable
hp9$Hapto.Log <- log(hp9$Hapto.Result)
hp9$Hapto.Log
```
Log-Transformed Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60805270-e36cfd00-a17f-11e9-91c2-2bb309711f01.png" width="300">


#### BS.NEFA --> BS.NEFA.Log

Since this variable is skewed right, we need to log transform it.
```r
#Creating the new log transformed variable
#We first check if there are any 0's in the original data because if a value in the data is 0, the log transformation will fail
hp9$BS.NEFA
#Now that we know there are no 0's we can create the new log version variable
hp9$BS.NEFA.Log <- log(hp9$BS.NEFA)
hp9$BS.NEFA.Log
```
Log-Transformed Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60805246-d3551d80-a17f-11e9-9e30-1b8c8c43dd3c.png" width="300">


#### BS.BHBA --> BS.BHBA.Log

Since this variable is skewed right, we need to log transform it.
```r
#Creating the new log transformed variable
#We first check if there are any 0's in the original data because if a value in the data is 0, the log transformation will fail
hp9$BS.BHBA
#Now that we know there are no 0's we can create the new log version variable
hp9$BS.BHBA.Log <- log(hp9$BS.BHBA)
hp9$BS.BHBA.Log
```
Log-Transformed Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60805276-e9fb7480-a17f-11e9-97c2-bd1b78c09803.png" width="300">


#### MS.S.Cell.Count --> MS.S.Cell.Count.Log

Since this variable is skewed very very far right, we need to log transform it.
```r
#Creating the new log transformed variable
#We first check if there are any 0's in the original data because if a value in the data is 0, the log transformation will fail
hp9$MS.S.Cell.Count
#Now that we know there are no 0's we can create the new log version variable
hp9$MS.S.Cell.Count.Log <- log(hp9$MS.S.Cell.Count)
hp9$MS.S.Cell.Count.Log
```
Log-Transformed Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60805228-c9331f00-a17f-11e9-9165-884484524b90.png" width="300">


#### MS.BHBA --> MS.BHBA.Log

Since this variable is skewed right, we need to log transform it.
```r
#Creating the new log transformed variable
#We first check if there are any 0's in the original data because if a value in the data is 0, the log transformation will fail
hp9$MS.BHBA
#Now that we know there are no 0's we can create the new log version variable
hp9$MS.BHBA.Log <- log(hp9$MS.BHBA)
hp9$MS.BHBA.Log
```
Log-Transformed Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60805218-c20c1100-a17f-11e9-9b54-568de9ee0df6.png" width="300">


#### MS.Acetone --> MS.Acetone.Log

Since this variable is skewed far right, we need to log transform it.
```r
#Creating the new log transformed variable
#We first check if there are any 0's in the original data because if a value in the data is 0, the log transformation will fail
hp9$MS.Acetone
#Now that we know there are no 0's we can create the new log version variable
hp9$MS.Acetone.Log <- log(hp9$MS.Acetone)
hp9$MS.Acetone.Log
```
Log-Transformed Histogram:
 <img src="https://user-images.githubusercontent.com/52465712/60805263-dcde8580-a17f-11e9-8967-49702e26ef22.png" width="300">
