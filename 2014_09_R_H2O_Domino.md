Using R, H2O and Domino for Fast, Practical and Big Data Analysis
===============

*version 0.1 - draft document structure only*


## Introduction

- Why
- Things I experimented with H2O and Domino since TTTAR1 blog post
- What I like about these tools
- Using R + H2O + Domino together for real (Kaggle, Big Data)
- Encourage readers to try H2O and Domino with code snippets and two case studies


## R + H2O

- Awesome R integration. Do it within R environment.
- Parallelised machine learning algorithms
- Ability to handling big data with limited memory
- Links to Arno's slides/videos about H2O deep learning


## R + Domimo

- Awesome R integration. Do it all within R environment.
- no hassle elastic cloud computing (only pay for analysis runtime, about 30GB storage per project)
- multiple instants
- easy scheduled / recurring runs
- Collaborative / open projects
- Turning your awesome R models into API (links to Nick's post)


## R + H2O + Domino

- Question one: does it work? Yes.
- Analysing and building predictive models on huge datasets
- Quick turnaround with multiple instants
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


## Case Study 2: Scaling it up! The Higgs Data

short paragraphs and code snippets:

- importing and inspecting the full 11M-row Higgs data
- building predictive models in realistic timescale
- memory usage for each algorithm


## What's Next?

- Domino for recurring daily stock market analysis 
- Deep learning for football (soccer) analysis
- Comparing different model blending apporaches: the original motivation of the blenditbayes blog.
- RUGSMAPS2 - My first crowd-sourcing experiment to improve the original RUGSMAPS with inputs from R users worldwide.
- Based on RUGSMAPS2, how can we use crowd-sourcing to improve documentation for H2O, rCharts and other open-source tools in future.
- Some upcoming conferences / meetups related to H2O and Domino.


## Acknowledgement

**Note**: I don't want to miss any of you here. If you gonna check one thing, check this section :)




