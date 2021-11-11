# Multivariate Statistics

-----------

## Table of Contents

[Preparing Our Data](#preparing-our-data) 

[Creating A Baseline Model For Hapto.Log](#creating-a-baseline-model-for-hapto-log)

[Creating A Linear Regression Model for Hapto.Log By Removing One Variable At A Time](#creating-a-linear-regression-model-for-hapto-log-by-removing-one-variable-at-a-time)

[Creating A Baseline Model For Hapto0.35](#creating-a-baseline-model-for-hapto-035)

[Creating A Logistic Regression Model For Hapto0.35 By Removing One Variable At A Time](#creating-a-logistic-regression-model-for-hapto-035-by-removing-one-variable-at-a-time)


# Preparing Our Data
First we have to set our working directory and load in our dataset
```r
setwd("/Users/MoniekSmink/Desktop/R/Hapto")

load(file="MS_hp9_Log.RData")
```

Then let's access any packages we will be needing for the Multivariate Statistics
```r
library(car)
library(lme4)
library(lmerTest)
```

Now we are ready to begin creating our models.


# Creating A Baseline Model For Hapto Log

First we want to create a baseline model with no additional variables besides the variables that can counter-act the nesting effects, in this case CowID and Farm.No
``` r
baselineLM <- lmer(Hapto.Log ~ 1 + (1|CowID:Farm.No), data = hp9)

plot(baselineLM)
```

<img src="https://user-images.githubusercontent.com/52465712/62807608-5ccb7880-babb-11e9-998e-eb729681624e.png" width="300">


# Creating a Linear Regression Model For Hapto Log By Removing One Variable At A Time

Now we take our baseline model for Hapto.Log and add all the variables that had a p-value below 0.1 in the bi-variate analysis and didn't have a correlation above 0.7.

```r
Hapto.Log_10 <- lmer(Hapto.Log ~ Milk.Yield + MS.Milk.Yield + MS.BHBA.Log + MS.DIM + MS.Fat +
                    MS.Protein + MS.Lactose + MS.Urea + MS.S.Cell.Count.Log +
                    MS.pH + CE.Environ.Temp + Cow.Breed + Hfr.or.Cow + BS.Month + CE.Skin.Dehydration +
                    CE.Stom.Tension + CE.Stom.Layering + CE.Stom.Fluid.Movement + CE.Stom.Fullness + CE.Stom.Noise.Freq +
                    CE.Waste.Consistency + CE.Lame + BS.NEFA.0.7 + (1|CowID:Farm.No), data = hp9)
```

Now we run a test to see which variable is the least significant
```r
Anova(Hapto.Log_10, type = "III")


#Response: Hapto.Log
#                         Chisq Df Pr(>Chisq)    
#(Intercept)             0.1657  1  0.6840049    
#Milk.Yield              5.7103  1  0.0168657 *  
#MS.Milk.Yield           0.0417  1  0.8382250    
#MS.BHBA.Log             0.4005  1  0.5268273    
#MS.Fat                  1.5982  1  0.2061635    
#MS.DIM                  0.0023  1  0.9617691       <- This is the least significant
#MS.Protein              4.2585  1  0.0390553 *  
#MS.Lactose              0.9252  1  0.3361020    
#MS.Urea                 2.4385  1  0.1183888    
#MS.S.Cell.Count.Log    13.3541  1  0.0002579 ***
#MS.pH                   0.0426  1  0.8364866    
#CE.Environ.Temp         1.4139  1  0.2344120    
#Cow.Breed               0.0561  1  0.8127500    
#Hfr.or.Cow              0.0033  1  0.9545145    
#BS.Month               10.6533  6  0.0997018 .  
#CE.Skin.Dehydration     0.0287  1  0.8654327    
#CE.Stom.Tension         5.5084  1  0.0189252 *  
#CE.Stom.Layering        0.9888  1  0.3200249    
#CE.Stom.Fluid.Movement  0.1558  1  0.6930227    
#CE.Stom.Fullness        3.4332  1  0.0638996 .  
#CE.Stom.Noise.Freq      1.5860  2  0.4524781    
#CE.Waste.Consistency    5.5175  3  0.1375946    
#CE.Lame                 1.2741  1  0.2590070    
#BS.NEFA.0.7             1.8861  1  0.1696417    
#---
#Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
```
MS.DIM has the highest p-value of 0.9619, now we remove this variable and repeat until we have only statistically significant values (p-value below 0.05)

We take the improved model and run another test
```r
Hapto.Log_11 <- lmer(Hapto.Log ~ Milk.Yield + MS.Milk.Yield + MS.BHBA.Log + MS.Fat +
                       MS.Protein + MS.Lactose + MS.Urea + MS.S.Cell.Count.Log +
                       MS.pH + CE.Environ.Temp + Cow.Breed + Hfr.or.Cow + BS.Month + CE.Skin.Dehydration +
                       CE.Stom.Tension + CE.Stom.Layering + CE.Stom.Fluid.Movement + CE.Stom.Fullness + CE.Stom.Noise.Freq +
                       CE.Waste.Consistency + CE.Lame + BS.NEFA.0.7 + (1|CowID:Farm.No), data = hp9)

Anova(Hapto.Log_11, type = "III")


#Response: Hapto.Log
#                         Chisq Df Pr(>Chisq)    
#(Intercept)             0.1699  1  0.6801687    
#Milk.Yield              5.8545  1  0.0155370 *  
#MS.Milk.Yield           0.0514  1  0.8206632    
#MS.BHBA.Log             0.4065  1  0.5237429    
#MS.Fat                  1.6364  1  0.2008250    
#MS.Protein              4.8440  1  0.0277423 *  
#MS.Lactose              0.9464  1  0.3306436    
#MS.Urea                 2.6160  1  0.1057925    
#MS.S.Cell.Count.Log    13.6875  1  0.0002159 ***
#MS.pH                   0.0414  1  0.8387557    
#CE.Environ.Temp         1.4862  1  0.2228027    
#Cow.Breed               0.0537  1  0.8167428    
#Hfr.or.Cow              0.0049  1  0.9443313       <- Now this is the least significant  
#BS.Month               10.8686  6  0.0925244 .  
#CE.Skin.Dehydration     0.0310  1  0.8603417    
#CE.Stom.Tension         5.5974  1  0.0179867 *  
#CE.Stom.Layering        1.0149  1  0.3137341    
#CE.Stom.Fluid.Movement  0.1584  1  0.6906744    
#CE.Stom.Fullness        3.6157  1  0.0572378 .  
#CE.Stom.Noise.Freq      1.6334  2  0.4418779    
#CE.Waste.Consistency    5.6054  3  0.1324679    
#CE.Lame                 1.4193  1  0.2335116    
#BS.NEFA.0.7             2.1854  1  0.1393209    
#---
#Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
```
Now we see that Hfr.or.Cow has the highest p-value (0.9443) and is the least statistically significant, so we take this variable out and repeat again.

After doing this 14 times we have a final model where all of our p-values are significant:
```r
Hapto.Log_24 <- lmer(Hapto.Log ~ Milk.Yield +
                       MS.Protein + MS.Urea + MS.S.Cell.Count.Log +
                       CE.Environ.Temp + BS.Month + 
                       CE.Stom.Tension + CE.Stom.Fullness +
                       CE.Lame + BS.NEFA.0.7 + (1|CowID:Farm.No), data = hp9)

Anova(Hapto.Log_24, type = "III")

#Response: Hapto.Log
#                      Chisq Df Pr(>Chisq)    
#(Intercept)         21.5707  1  3.410e-06 ***
#Milk.Yield          20.5155  1  5.915e-06 ***
#MS.Protein           9.0160  1   0.002676 ** 
#MS.Urea              4.9891  1   0.025507 *  
#MS.S.Cell.Count.Log 35.8007  1  2.186e-09 ***
#CE.Environ.Temp      5.8084  1   0.015950 *             All the variables are significant
#BS.Month            11.7329  6   0.068199 .  
#CE.Stom.Tension      8.1664  1   0.004267 ** 
#CE.Stom.Fullness     6.5862  1   0.010277 *  
#CE.Lame              8.7208  1   0.003146 ** 
#BS.NEFA.0.7         15.4171  1  8.621e-05 ***
#---
#Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
```
So the variables in our final model are: Milk.Yield, MS.Protein, MS.Urea, MS.S.Cell.Count.Log, CE.Environ.Temp, BS.Month, CE.Stom.Tension, CE.Stom.Fullness, CE.Lame, and BS.NEFA.0.7

And here is our model plotted
```r
plot(Hapto.Log_24)
```

<img src="https://user-images.githubusercontent.com/52465712/62807606-5b01b500-babb-11e9-9acc-095169cec723.png" width="300">


--------
# Creating a Baseline Model for Hapto 035


First we want to create a baseline model with no additional variables besides the variables that can counter-act the nesting effects, in this case CowID and Farm.No
``` r
baselineLM2 <- glmer(Hapto0.35 ~ 1 + (1|CowID:Farm.No), data = hp9, family = binomial(link=logit))

plot(baselineLM2)
```

<img src="https://user-images.githubusercontent.com/52465712/63232326-702dc080-c1ec-11e9-880d-ab18d6c9835d.png" width="300">


-----------
# Creating a Logistic Regression Model For Hapto 035 By Removing One Variable At A Time

Now we take our baseline model for Hapto.Log and add all the variables that had a p-value below 0.1 in the bi-variate analysis and didn't have a correlation above 0.7.

```r
Hapto0.35_1 <- glmer(data = hp9, Hapto0.35 ~ Milk.Yield + MS.Milk.Yield + MS.BHBA.Log + MS.DIM + MS.Fat + MS.Protein + MS.Lactose + MS.Acetone.Log
                    + MS.S.Cell.Count.Log + MS.pH + CE.Environ.Temp + Cow.Breed + Hfr.or.Cow + BS.Month + CE.Skin.Dehydration +
                    CE.Stom.Fullness + CE.Stom.Noise.Freq + CE.Lame + BS.NEFA.0.7 + (1|CowID:Farm.No), family = binomial(link = logit))
```

Now we run a test to see which variable is the least significant
```r
Anova(Hapto0.35_1, type = "III")

#Response: Hapto0.35
                     Chisq Df Pr(>Chisq)   
#(Intercept)         0.0000  1   0.994417   
#Milk.Yield          6.2881  1   0.012155 * 
#MS.Milk.Yield       1.5813  1   0.208577   
#MS.BHBA.Log         3.1756  1   0.074744 . 
#MS.DIM              0.0133  1   0.908286   
#MS.Fat              0.8008  1   0.370853   
#MS.Protein          1.0508  1   0.305323   
#MS.Lactose          1.0766  1   0.299460   
#MS.Acetone.Log      1.2894  1   0.256163   
#MS.S.Cell.Count.Log 7.9418  1   0.004831 **
#MS.pH               0.4699  1   0.493047   
#CE.Environ.Temp     2.3858  1   0.122442   
#Cow.Breed           2.8248  1   0.092818 . 
#Hfr.or.Cow          2.1591  1   0.141730   
#BS.Month            4.0903  6   0.664452   
#CE.Skin.Dehydration 2.1744  1   0.140322   
#CE.Stom.Fullness    0.2190  1   0.639792   
#CE.Stom.Noise.Freq  4.1724  2   0.124157   
#CE.Lame             0.0114  1   0.915021       <- This is the least significant
#BS.NEFA.0.7         2.5347  1   0.111370   
#---
#Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
```
CE.Lame has the highest p-value of 0.9150, now we remove this variable and repeat until we have only statistically significant values (p-value below 0.05)

We take the improved model and run another test
```r
Hapto0.35_2 <- glmer(data = hp9, Hapto0.35 ~ Milk.Yield + MS.Milk.Yield + MS.BHBA.Log + MS.DIM + MS.Fat + MS.Protein + MS.Lactose + MS.Acetone.Log
                     + MS.S.Cell.Count.Log + MS.pH + CE.Environ.Temp + Cow.Breed + Hfr.or.Cow + BS.Month + CE.Skin.Dehydration +
                       CE.Stom.Fullness + CE.Stom.Noise.Freq + BS.NEFA.0.7 + (1|CowID:Farm.No), family = binomial(link = logit))

Anova(Hapto0.35_2, type = "III")

#Response: Hapto0.35
                     Chisq Df Pr(>Chisq)   
#(Intercept)         0.0000  1   0.999566   
#Milk.Yield          7.6076  1   0.005812 **
#MS.Milk.Yield       1.6815  1   0.194719   
#MS.BHBA.Log         3.1536  1   0.075760 . 
#MS.DIM              0.0084  1   0.927143       <- Now this is the least significant variable 
#MS.Fat              0.8172  1   0.365987   
#MS.Protein          1.0610  1   0.302976   
#MS.Lactose          1.3563  1   0.244182   
#MS.Acetone.Log      1.4366  1   0.230690   
#MS.S.Cell.Count.Log 8.5487  1   0.003458 **
#MS.pH               0.6645  1   0.414964   
#CE.Environ.Temp     2.4667  1   0.116285   
#Cow.Breed           2.9559  1   0.085565 . 
#Hfr.or.Cow          4.0556  1   0.044026 * 
#BS.Month            4.0987  6   0.663327   
#CE.Skin.Dehydration 2.2890  1   0.130292   
#CE.Stom.Fullness    0.3703  1   0.542815   
#CE.Stom.Noise.Freq  5.1032  2   0.077956 . 
#BS.NEFA.0.7         3.4946  1   0.061569 . 
#---
#Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
```
Now we see that MS.DIM has the highest p-value (0.9271) and is the least statistically significant, so we take this variable out and repeat again.

After doing this 15 times we have a final model where all of our p-values are significant:
```r
Hapto0.35_15 <- glmer(data = hp9, Hapto0.35 ~ Milk.Yield + MS.Protein
                      + MS.S.Cell.Count.Log + CE.Environ.Temp +
                        BS.NEFA.0.7 + (1|CowID:Farm.No), family = binomial(link = logit))

Anova(Hapto0.35_15, type = "III")

#Response: Hapto0.35
#                      Chisq Df Pr(>Chisq)    
#(Intercept)          1.3414  1    0.24679    
#Milk.Yield          16.8923  1  3.956e-05 ***
#MS.Protein           5.8666  1    0.01543 *  
#MS.S.Cell.Count.Log 15.7557  1  7.207e-05 ***       All Variables Significant
#CE.Environ.Temp      5.4085  1    0.02004 *  
#BS.NEFA.0.7         18.0150  1  2.192e-05 ***
#---
#Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
```
So the variables in our final model are: Milk.Yield, MS.Protein, MS.S.Cell.Count.Log, CE.Environ.Temp and BS.NEFA.0.7.

And here is our model plotted
```r
plot(Hapto0.35_15)
```

<img src="https://user-images.githubusercontent.com/52465712/63232283-06151b80-c1ec-11e9-9ff1-a1cb374b11d2.png" width="300">
