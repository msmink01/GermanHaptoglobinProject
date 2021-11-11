---
title: "Haptoglobin multivariate model"
output: 
  github_document:
    toc: true
    toc_depth: 3
editor_options: 
  chunk_output_type: inline
---

This is an [R Markdown](http://rmarkdown.rstudio.com) Notebook. When you execute code within the notebook, the results appear beneath the code. 

Try executing this chunk by clicking the *Run* button within the chunk or by placing your cursor inside it and pressing *Ctrl+Shift+Enter*. 

# Needed packages

```{r}
#glmer
if (!require("lme4")){install.packages("lme4", dependencies = TRUE)
  library(lme4)
}
#lsmeans
if (!require("lsmeans")){install.packages("lsmeans", dependencies = TRUE)
  library(lsmeans)
}
#effects plot
if (!require("effects")) {
  install.packages("effects", dependencies = TRUE)
  library(effects)
}
#dplyr
if (!require("dplyr")) {
  install.packages("dplyr", dependencies = TRUE)
  library(dplyr)
}
```

# Data import

```{r}
load("./Data/MS_hp9_Log.RData")
modelData <- hp9 
```
# Data Exploration
```{r}
hist(log10(hp9$Hapto.Log))
hist(hp9$Hapto.Log)
hist(hp9$Hapto.Result)
```


# Model building


## Baseline Model
```{r}
baselineLM <- lmer(Hapto.Log ~ 1 + (1|CowID:Farm.No), data = hp9)
plot(baselineLM)
```


## Full Model
```{r}
fullmodel <- lmer(Hapto.Log ~ MS.S.Cell.Count.Log + CE.Stom.Tension + BS.Month +
            Milk.Yield + BS.NEFA.0.7 + MS.Protein + (1|CowID:Farm.No), data = hp9)
plot(fullmodel)
```


## Model Fit
```{r}
#drop1(fullmodel, test = "Chisq")
```


