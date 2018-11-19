# Smart Odisha Hackathon - 2018

Link- https://www.hackerearth.com/sprints/smart-odisha-hackathon/

Problem Statement - Data Analysis and Development of Environmental Information System for Mining Areas in Odisha

## Seismic-Data-Analysis

### Introduction

The dangers associated with coal mining are myriad; black lung, flammable gas pockets,
rock-bursts, and tunnel collapses are all very real dangers that mining companies must consider
when attempting to provide safe working conditions for miners. One class of mining hazard,
commonly called 'seismic hazards', are notoriously difficult to protect against and even more
difficult to predict with certainty. Therefore, predicting these hazards has become a well-known
problem for machine learning and predictive analytics. The UCI Machine Learning Repository
(https://archive.ics.uci.edu) provides a 'seismic bumps' data set that contains many records of
combined categorical and numeric variables that could be used to predict seismic hazards. This
'seismic bumps' data set can be found at
https://archive.ics.uci.edu/ml/datasets/seismic-bumps .

### Problem Statement

Our analysis attempts to use logistic regression techniques to predict whether a seismic
'bump' is predictive of a notable seismic hazard. We attempt to characterize our prediction
accuracy and compare the results against the state of the art results from other statistical and
machine learning techniques, that are included within the data set.

### Data Set Description

The data were taken from instruments in the Zabrze-Bielszowice coal mine, in Poland.
There are 2,584 records, with only 170 class = 1 variables, so the data are significantly skewed
towards non-hazardous training data. Field descriptions are below, but essentially energy
readings and bump counts during one work shift are used to predict a 'hazardous' bump during
the next shift. From the data description, a 'hazardous bump' is a seismic event with > 10,000
Joules, and a 'shift' is a period of 8 hours. For the sake of reference, a practical example of
10,000 Joules would be the approximate energy required to lift 10,000 tomatoes 1m above the
ground. A class = 1 variable result signifies that a hazardous bump did, indeed, occur in the
following shift to the measured data. 

![Description ]("img/att.jpg")
