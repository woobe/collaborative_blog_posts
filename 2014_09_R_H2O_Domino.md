Using R, H2O and Domino for Fast, Practical and Scalable Data Analysis
===============

*version 0.2*

## Introduction

This blog post is the sequel to [TTTAR1 a.k.a. an introduction to H2O Deep Learning](update link here). It is quite a lengthy post so let me explain why you should read this. If the previous post was a brief intro, this post is a proper machine learning case study based on two real-world datasets: Soil data from the Africa Soil Property Prediction Challenge on Kaggle and the Higgs data provided by Prof. Whiteson.

In short, I will use bitesize code examples to show you how to ...
- use R as the main user interface for H2O and Domino
- train predictive models using H2O
- scale up the machine learning process using Domino

I hope that this post will encourage more data geeks to give H2O, Domino as well as Kaggle a try. Although the post is quite R-oriented, the underlying processes should be easily transferrable to other programming langagues supported by H2O and Domino. So, if you're interested in general predictive analytics, read on :)


## R as the Main User Interface for H2O and Domino
## (previously three seperate sections)

This is not the way I used to use R. But it is certainly a very interesting way to use R.

- Question one: does it work? Yes.
- Awesome R integration. Do it within R environment.
- Parallelised machine learning algorithms
- Ability to handling big data with limited memory
- Links to Arno's slides/videos about H2O deep learning
- no hassle elastic cloud computing (only pay for analysis runtime, about 30GB storage per project)
- multiple instances
- easy scheduled / recurring runs
- Collaborative / open projects
- Turning your awesome R models into API (links to Nick's post)
- Analysing and building predictive models on huge datasets
- Quick turnaround with multiple instances
- Turn your big data analysis into products


## Case Study 1: AfSIS Kaggle Competition

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


## Case Study 2: Scaling it up! The Higgs Data

short paragraphs and code snippets:

- importing and inspecting the full 11M-row Higgs data
- building predictive models in realistic timescale (RF, GBM and DNN only)
- discssuion on memory usage for each algorithm


## What's Next?

- Domino for recurring daily stock market analysis 
- Deep learning for football (soccer) analysis
- Comparing different model blending apporaches: the original motivation of the blenditbayes blog.
- RUGSMAPS2 - My first crowd-sourcing experiment to improve the original RUGSMAPS with inputs from R users worldwide.
- Based on RUGSMAPS2, how can we use crowd-sourcing to improve documentation for H2O, rCharts and other open-source tools in future.
- Some upcoming conferences / meetups related to H2O and Domino.


## Acknowledgement

**Note**: I don't want to miss any of you here. If you gonna check one thing, check this section :)




