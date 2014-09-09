Using R, H2O and Domino for Practical and Scalable Data Analysis
===============

*version 0.5*

<br><br>

### Introduction

This blog post is the sequel to [TTTAR1 a.k.a. an introduction to H2O Deep Learning](update link here). It is quite a lengthy post so let me explain why you should read this. If the previous post was a brief intro, this post is a proper machine learning case study based on two real-world datasets: Soil data from the AfSIS Kaggle competition and Higgs data from UCI repository. In short, I will use bitesize code examples to illustrate how to:

- use R as the main user interface for H2O and Domino.
- train predictive models in parallel fashion using H2O.
- scale up and accelerate the process using Domino.

<br><br>

#### H2O Again?

xxx

<br><br>

#### What is Domino?

xxx

<br><br>

**************


### R as the Main User Interface for H2O and Domino

In the past, I would import data, fire up 'caret' and then train some models. All data wraggling and calculations were done using R and R only. The following examples, however, are ...

R, in this case, acts as the main user interface. It sends commands and transfers data between H2O and Domino. H2O does memory management and number-crunching. Domino scales up and accelerates the process. R keeps track of everything and makes sure H2O and Domino are working together as a team.

To sum it up in very technical terms, R, H2O and Domino can happily talk to each other.

<br><br>

**************

### About the Case Studies

1. Soil data on local machine - get yourself familiar with the H2O machine learning process
2. Soil data on Domino - demonstrates how to perform the same analysis on Domino's free tier
3. Soil data on Domino - scale it up, run faster and test more models
4. Higgs data on Domino - big data analysis

<br><br>

#### AfSIS Kaggle Competition

(screenshot of leaderboard here)

short intro
training data 
test data
3595 features
5 labels
my experience of using H2O to achieve good results

<br><br>

#### Higgs Dataset

xxx

<br><br>

**************

### Case Study One: Analysing Soil Data Locally

short paragraphs and code snippets:

- installing specific version (scripts ... or a simple function from my "deepr" package)
- h2o.init() (do it in R or shell)
- h2o.importFile() and as.h2o() for importing data
- h2o.ls(), h2o.rm() for freeing up memory
- caret::createFolds or h2o.splitFrame() for data slicing
- h2o.deeplearning(), h2o.randomForest() and h2o.gbm() for machine learning
- h2o.performance() for evaluation ... (also use "caret" for more metrics)
- blending models (simple averging for now) 
- h2o.saveModel(), h2o.loadModel
- trying out all your crazy ideas at once, use multiple runs on Domino
- after all snippets, provide a complete R script that just beats the BART benchmark

<br><br>

#### Step 1.1 Install H2O Bleeding Edge Version

Why? Because it has new and very cool features that are not yet available on the CRAN version.
To make life easier, I wrote a wrapper function in my deepr package to streamline the process.
You can install or upgrade the 'h2o' package on your machine with 2 lines of code.

```
## Install the latest version
devtools::install_github("woobe/deepr")
deepr::install_h2o()

## Install a specific version
deepr::install_h2o(h2o_ver = "1500")
```

<br><br>

#### Step 1.2 Start and Connect to a H2O Cluster

After installing the bleeding edge version, you're ready for the rest of the script.
To do anything with H2O, we need to initialise the connection between R and a H2O cluster first.

```
## Start and connect to a local H2O cluster with 4GB of memory
## Note that this is slightly different to the example in TTTAR1 
## as the argument 'Xmx' is deprecated.
library(h2o)
localH2O <- h2o.init(max_mem_size = "4g")
```

<br><br>

#### Step 1.3 Import the training and test datasets

I think this is one of the very cool features in H2O. 
You can import the dataset directly from compressed files (e.g. zip, gz). 

```
## Assuming the zip files are in the 'data' sub-folder
train_hex <- h2o.importFile(localH2O, path = "/data/train.zip")
test_hex <- h2o.importFile(localH2O, path = "/data/test.zip")
```

<br><br>

#### Step 1.4 Some Simple Operations

```
dim(train_hex)
head(train_hex)
colnames(train_hex)
```

<br><br>

#### Step 1.5 Building Predictive Models

column 1 is ID
columns 2 to 3955 are predictors
columns 3956 to 3960 are targets ()

```
## Train a DNN for Ca
model_ca_dnn <- h2o.deeplearnin(...)
```

```
## Train a RF for Ca
model_ca_rf <- h2o.randomForest(...)
```

```
## Train a GBM for Ca
model_ca_gbm <- h2o.randomForest(...)
```

<br><br>


#### Step 1.6 Build Regularised DNN

xxxx

<br><br>


#### Step 1.7 Use the DNN Models for Predictions

xxx

<br><br>

#### Step 18 Create your own Kaggle entry

xxx

<br><br>

**************

### Case Study Two: Analysing Soil Data on Domino

Many Screenshots here

<br><br>

#### Step 2.1 Create your Domino account

xxx

<br><br>

#### Step 2.2 Go through the Quick Start tutorial

xxx

<br><br>

#### Step 2.3 Upload the files

xxx

<br><br>

#### Step 2.4 Run

xxx

<br><br>

#### Step 2.5 Notification

xxx

<br><br>

#### Step 2.6 Download Results

xxx

<br><br>

**************

### Case Study Three: Let's Scale it up!! Run faster with Domino

Use higher tiers for case study two. Make it run a lot faster.

Test more models.

<br><br>

#### Step 3.1 Using Higher Tiers

xxx

<br><br>

#### Step 3.2 Upload, Run, Download

xxx

<br><br>

#### Step 3.3 Monitoring Memory Usage

xxx

<br><br>

**************


### Case Study Four: Analysing Big Data on Domino

short paragraphs and code snippets:

- importing and inspecting the full 11M-row Higgs data
- building predictive models in realistic timescale (RF, GBM and DNN only)
- discssuion on memory usage for each algorithm

<br><br>


**************

### What's Next?

- Domino for recurring daily stock market analysis 
- Deep learning for football (soccer) analysis
- Comparing different model blending apporaches: the original motivation of the blenditbayes blog.
- RUGSMAPS2 - My first crowd-sourcing experiment to improve the original RUGSMAPS with inputs from R users worldwide.
- Based on RUGSMAPS2, how can we use crowd-sourcing to improve documentation for H2O, rCharts and other open-source tools in future.
- Some upcoming conferences / meetups related to H2O and Domino.
- More TTTAR: data.table, Rcpp, DataRobot, RHadoop ...

<br><br>

**************

### Acknowledgement

**Note**: I don't want to miss any of you here. If you gonna check one thing, check this section :)

<br><br>

**************

### Key Resources

[Domino Online Help](http://help.dominoup.com/)

<br><br>

**************

### Looking back 

Things are evolving quickly these days. It is very important to keep an open mind when new tools appear.
Two years ago, if you told me that R, H2O and Domino could one day work together and analyse big data, I would simply laugh it off. All I could imagine was a pirate ordering drinks and pizzas. 

<br><br>
