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

### Agenda

Task of hazards prediction bases on the relationship between the energy of recorded tremors and seismoacoustic activity with the possibility of rockburst occurrence.  With the information about the possibility of hazardous situation occurrence, an appropriate supervision service can reduce a risk of rockburst .


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

![Description ](https://github.com/TheCaffeineDev/Seismic-Data-Analysis/blob/master/img/att.JPG) 

### Main Effects

The main effects for this study are considered to be the all numeric variables, plus
ghazard, seismoacoustic and shift. This stands to reason, since numerical energy readings and
shift activity type all seem like they would impact the number of hazardous seismic events in
the next shift. The nbumps class of variables are left out for more advanced models, since the
resonance and frequency ranges could have a multitude of confounding variables that we,
without significant mining expertise, would miss. To test that nbumps isn’t necessarily the
largest effect, we looked at a side-by-side histogram of nbump records for each of the two
output classes:

![Bumps ](https://github.com/TheCaffeineDev/Seismic-Data-Analysis/blob/master/img/bumps.JPG) 

The pattern of frequency distributions appears to be consistent, regardless of class. Therefore, we will
not be making ‘nbumps’ one of our main effects variables.

### Logistic Regression Assumptions

#### Output Variable
Logistic regression requires a categorical output variable. In this case, our output variable (class) is a
binary categorical variable.

#### Independence of Observations
We are making the assumption that each measurement is an independent measurement, taken at
different times, from the same mine. This is based on the data set description at the UCI Machine
Learning repository, and the fact that you can’t take multiple simultaneous readings from the same
instrument.

#### Multi-collinearity
We used the following chart to assess the correlation of variables with each other. The most highly
correlated variables are energy and maxenergy. It is also interesting that the gpuls:genergy and
gdpuls:gdenergy are somewhat correlated, but we would expect that an increase in the count of pulses
per shift would raise the calculated energy per shift. We would also expect the change in variance in the
number of pulses per shift (gdpuls) to correlate somewhat with the variance in the energy measured
(gdenergy). For this model, we decided to leave all the main effects variables intact and address any
multicollinearity issues after glmnet’s automatic feature selection, if necessary (spoiler: it wasn’t).

![multicollinearity ](https://github.com/TheCaffeineDev/Seismic-Data-Analysis/blob/master/img/CORplot.png) 

#### Problem with unbalanced class variable

The dependent variable in our model is quite unevenly balanced with a 14:1 ratio for
non-hazardous to hazardous. To illustrate the problem with having an unbalanced class
variable we compare accuracy of the logistic regression full model with the null model.

#### Full Model

We first built a logistic regression model taking all the observations and variables into account.
glm(class ~ . , data = sb, family = "binomial"). Next we predict using this full model and calculate
the probability of getting a hazardous bump. To convert these probabilities to classes, we
defined a threshold. A good value for threshold is the mean of the original response variable.
Probabilities greater than this threshold are categorized into hazardous bump class and
probabilities lesser than the threshold are categorized into non-hazardous bump class. Model
accuracy is then calculated by comparing with the actual class variable.
Our calculation show that the logistic regression model with all the observations and variables
made a correct prediction 59% of the time.

#### Accuracy using other ML Algorithms

* Decision Tree : 0.8897485493230 
* KNN: 0.9323017408123792,
* KernelSVC': 0.9264990328820116,
* LinearSVC': 0.9264990328820116,
* Naive Bayes: 0.11798839458413926,
* Random Forest': 0.9226305609284333
* ANN : 0.9129593810444874

#### Conclusion

This data set has been used in many, many papers and theories. This seismic bump problem is an
interesting problem, an important problem, and has a fascinating data set. However, it is challenging
due in no small part to the unbalanced data. Like the infamous Challenger O-Ring data set, the lack of a
hazardous result is not a ‘null’ case but instead informs the model about situations where nothing bad
happens… a class = 0 event. Unlike the Challenger data set, we have many more parameters to choose
from, and myriad ways of dealing with the imbalanced data. We chose to Randomly Under-Sample, but
we could also do Synthetic Minority Over-Sampling, Cluster-Based Over-Sampling, Random
Over-Sampling, Algorithmic Ensemble Sampling, Bagging, Boosting, and probably many other techniques
which aren’t covered in a graduate level statistics course. We chose a pretty straightforward solution,
which definitely impacts the performance of our model.

Our logistic regression model predicts the test set with around 60 to 70% accuracy, after
random under-sampling.

While the methods for calculating the results of these various methods aren’t clearly documented in the
data set, we can assume that we understand a few of them through inference. Accuracy (Acc.) is the
percentage of times our model correctly predicted the class in the test set.

#### Some different ideas on this dataset:

* Where are the geophones located? Is it possible to do TRM (time reverse modeling) of stress wave propagation? With this dataset we simply know that if a rock burst occurs in a longwall but not where.

* What to do with the results? We may end up knowing if a rock burst is likely to occur or not. Can we use the recorded data to estimate locations and therefore controll stress release before the burst?

* Can we extract another set of useful information from the raw data from the geophones (what we got here is heavily processed)?




#### References

* https://www.hindawi.com/journals/sv/2016/8740868/#B13


