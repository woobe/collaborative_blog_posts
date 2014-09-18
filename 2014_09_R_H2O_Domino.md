Using R, H2O and Domino for Practical and Scalable Data Analysis
===============

*version 0.15*

<br>

### Introduction

This blog post is the sequel to [TTTAR1 a.k.a. an introduction to H2O Deep Learning](http://bit.ly/bib_TTTAR1). If the previous blog post was a brief intro to H2O, this post is a proper machine learning case study based on a recent [Kaggle competition](https://www.kaggle.com/c/afsis-soil-properties). In short, I am leveraging the power of [R](http://www.r-project.org/), [H2O](http://h2o.ai/) and [Domino](http://www.dominoup.com/) to compete in a real-world data mining contest.

<center><img src="http://i.imgur.com/S3x3d2O.png" alt="kaggle_topspot" style="width:700px"></center>

<br>

The competition got tougher since then but I am still very proud to say that at least I stayed top for a few days!
Note that the public score is only based on a small subset (17%) of test data. My position on the final leaderboard might change dramatically. In my opinion, climbing up the public leaderboard is just the first step, making sure the models are generalized enough to stay up is the real challenge. Anyway, that is another topic for a future blog post. 

The purpose of this post is not only about Kaggle competitions, **it is more about finding a generic, robust, practical and scalable data analysis solution**. A solution that I can rely on and apply to many of my machine learning problems in life. My experience with this R + H2O + Domino combination in the last couple weeks has been very promising. So I would like to use this opportunity to share with you my experience. I realy hope that this post will encourage more data geeks out there to give R, H2O and Domino a try if they haven't done so.

<br>

#### Learning-by-Doing

I always believe that learning-by-doing is the best way to learn. So I have prepared **two short tutorials with code** below to get you started with Domino and H2O. Hopefully, by going through the tutorials, you will be able to master the basics and to try your own data analysis with the new tools. Moreover, if you follow the steps and run the code, you will get a CSV file that is ready for the Kaggle competition.

<br>

#### H2O, Domino and Kaggle?

Just in case you haven't heard of them yet ...

- [H2O](http://h2o.ai/) is an open-source math and in-memory prediction engine for big data science.
- [Domino Data Lab](http://www.dominoup.com/) is a platform for analysts and data scientists that handles all the “plumbing” required to run, scale, share, and deploy analytical models.
- [Kaggle](http://www.kaggle.com/) is a platform for predictive modeling and analytics competitions and consulting.

Source: [CrunchBase](http://www.crunchbase.com/)

<br><br>

**************

### Tutorial One - Getting Started with Domino

In the first tutorial, I will only focus on the basic Domino operations via 
Web UI and R interface. Although the R script is all about H2O machine learning, 
it is hard to learn two new things at the same time. So I will keep this simple
and leave the machine learning discussion for the next tutorial.

<br>

#### Ready? Here we go!!

<br>

#### Step 1.1 - Get Up and Running with Domino

If you haven't done so, [sign up](http://www.dominoup.com/) for a free account on the site, 
download and install the [client](http://help.dominoup.com/client). If you aren’t sure how to do this, 
you can follow their [quick-start guide](http://help.dominoup.com/quickStart) or
the step-by-step [tour](https://app.dominoup.com/tour).

<center><img src="http://i.imgur.com/HAQkggc.png" alt="domino_website" style="width:700px"></center>

<br>


#### Step 1.2 - Install R Interface for Domino

Domino has its own [R package](http://cran.r-project.org/web/packages/domino/index.html) 
on CRAN. After installing the package, you can log into your Domino account and 
manage your projects directly from R. The Domino team has done a great job 
streamlining the whole process. Personally, I think this is yet another excellent 
example of using R as an interface.


```
install.packages("domino")
library(domino)
domino.login("your_username", "your_password")
```

<br>


#### Step 1.3 - Download Data and Code

This tutorial is based on the [Kaggle Africa Soil Property Prediction Challenge](https://www.kaggle.com/c/afsis-soil-properties). In order to carry out the data analysis, you will need to [download the original datasets](https://www.kaggle.com/c/afsis-soil-properties/data) from Kaggle first. Then you can run a simple analysis 
using [this R script](Update Link) ```Kaggle_AfSIS_with_H2O.R```.

<center><img src="http://i.imgur.com/cORfbVt.png" alt="kaggle_data" style="width:500px"></center>

<br>


#### Step 1.4 - Upload Data and Code to Domino

You will need to upload the files to a specific project folder on Domino.
To keep things simple, I will use the ```quick-start``` folder here because most of 
you should have this folder somewhere on your local drive after going through 
Domino's [quick start guide](http://help.dominoup.com/quickStart).

On your machine, copy the Kaggle datasets and R script to the ```quick-start``` folder. The 
file structure should look like this:

**Before**

- results /
- main.m
- main.py
- main.r

**After**

- **data / train.zip** (*note*: create a new 'data' folder)
- **data / test.zip**
- **data / sample_submission.csv**
- results /
- **Kaggle_AfSIS_with_H2O.R**
- main.m
- main.py
- main.r

<br>

Afer that, you can upload the files to your ```quick-start``` folder on Domino.

```
## Set Working Directory to the 'quick-start' folder
setwd("quick_start_dir_on_your_local_drive") 

## Upload new files to the 'quick-start' folder on Domino cloud
domino.upload()
```

<br>


#### Step 1.5 - Check the Files

Before running the analysis, check and make sure the files are on the cloud. 
You can log into your Domino account via the [web UI](https://app.dominoup.com/overview) 
and browse your files in the ```quick-start``` folder.

<center><img src="http://i.imgur.com/PRpk7ws.png" alt="kaggle_files" style="width:700px"></center>

<br>



#### Step 1.6 - Start a Run

Got all the files there? Great, you now are ready to run the analysis on the cloud!

You can use the [web UI](https://app.dominoup.com/overview) to start a run 
(```Runs``` -> ```Run``` -> ```Enter of the File Name``` -> ```Start Run```).

<center><img src="http://i.imgur.com/s5V8XBr.png" alt="kaggle_startrun" style="width:700px"></center>

<br>

Alternatively, you can do this directly from R.

```
domino.run("Kaggle_AfSIS_with_H2O.R")
```

<br>


#### Step 1.7 - Monitor the Process

Domino has a very neat web UI for monitoring your runs online. 
You can get access to all your files and project settings on the left panel.
When you click on any of your runs, it will display the native console 
(R in this case) on the right with a summary below showing CPU load, memory usage
and other information about the run.

<center><img src="http://i.imgur.com/sHyFswF.png" alt="kaggle_monitor" style="width:700px"></center>

<br>


#### Step 1.8 - Download the Results

The analysis takes about half an hour. After that, you can download the 
results ```my_Kaggle_submission.csv``` either from the web ...

<center><img src="http://i.imgur.com/BYdgulM.png" alt="kaggle_monitor" style="width:500px"></center>

<br>

or via R.

```
## Download the results to your local drive
domino.download()
```

<br>

By default, you will receive an email notification once the run has finished. 
There are more ways to customize notifcation but I will leave that for a future
discussion (read more [here](http://help.dominoup.com/Notifications) if you are interested).

<center><img src="http://i.imgur.com/gpHK8TK.png" alt="kaggle_monitor" style="width:400px"></center>

<br>


#### Step 1.9 - Submit it to Kaggle (Optional)

You can now go to the [submission page](https://www.kaggle.com/c/afsis-soil-properties/submissions/attach) 
and upload the CSV file. Good luck :)

<br>

#### Try Your Own R Code

I have shown you the basic steps to get my Kaggle starter code up and running on 
the Domino cloud. Now it is time to try your own code. Remember Domino also 
supports **Python**, **Matlab** and **Julia**!

<br><br>


**************

### Tutorial Two: Using H2O to Predict Soil Properties

In this section, I will walk you through the starter code and explain how I use
R and H2O to train predictive models for the Kaggle competition.

<br>

#### What is the Problem?

In short, we have to develop regression models based on 1158 rows of training data and then
use the models to predict five target variables Ca, P, pH, SOC and Sand for each 
of the 728 test records. For more information, please go to the [description page](https://www.kaggle.com/c/afsis-soil-properties) on Kaggle.

<br>

#### Step 2.1 - Install R Interface for H2O

Again, R acts as an interface. Having R as the common interface, 
H2O and Domino can work together seamlessly. This is one of the key reasons why
I find this R + H2O + Domino solution very promising.

<br>

You can install the CRAN Version of H2O:

```
install.packages("h2o")
```

<br>

If you want to take advantages of the new H2O features, you can install the bleeding edge version.

```
## Specify H2O version here
h2o_ver <- "1511"

## Install H2O
local({r <- getOption("repos"); r["CRAN"] <- "http://cran.us.r-project.org"; options(repos = r)})
txt_repo <- (c(paste0(paste0("http://s3.amazonaws.com/h2o-release/h2o/master/",
                             h2o_ver),"/R"),
               getOption("repos")))
install.packages("h2o", repos = txt_repo, quiet = TRUE)
```

<br>

In order to find out the latest H2O version number, go to [this page](http://s3.amazonaws.com/h2o-release/h2o/master/1511/index.html) and look for the last four digits as shown in screenshot below.

<center><img src="http://i.imgur.com/VCuFIHO.png" alt="h2o_version" style="width:700px"></center>

<br>

(Optional) I wrote a wrapper function to make your life easier. You only need two
lines of code to install or upgrade H2O to the latest bleeding edge version:

```
devtools::install_github("woobe/deepr")
deepr::install_h2o()
```

<br>


#### Step 2.2 - Initiate and Connect to a Local H2O Cluster

Using the argument ```max_mem_size``` in function ```h2o.init(...)```, we can 
control the physical memory usage for the local H2O cluster. In this tutorial, 
we set a limit of 1GB of memory as it is the maximum allowance of the Domino free tier.

```
library(h2o)
localH2O <- h2o.init(max_mem_size = '1g')
```

<center><img src="http://i.imgur.com/xvJFVzA.png" alt="h2o_version" style="width:500px"></center>

<br>


#### Step 2.3 - Import Data

Importing data is one of the best things I like about H2O!!! You can load compressed 
files (.zip, .gz) directly into the H2O cluster. This may not be significantly 
important for the small Kaggle dataset in this tutorial but it is certainly useful 
for bigger datasets.

```
## Import Data to H2O Cluster
train_hex <- h2o.importFile(localH2O, "./data/train.zip")
test_hex <- h2o.importFile(localH2O, "./data/test.zip")
```

<br>


#### Step 2.4 - Train Deep Neural Networks Models and Make Predictions

Without further ado, here is the code to train one deep neural networks model 
for each target variable and then use the models to make predictions. For more information 
about the ```h2o.deeplearning(...)``` function, I strongly recommend going through 
the [vignette and demo code](https://github.com/0xdata/h2o/tree/master/docs/deeplearning/).

```
## Split the dataset into 80:20 for training and validation
train_hex_split <- h2o.splitFrame(train_hex, ratios = 0.8, shuffle = TRUE)

## One Variable at at Time
ls_label <- c("Ca", "P", "pH", "SOC", "Sand")

for (n_label in 1:5) {

  ## Display
  cat("\n\nNow training a DNN model for", ls_label[n_label], "...\n")

  ## Train a 50-node, three-hidden-layer Deep Neural Networks for 100 epochs
  model <- h2o.deeplearning(x = 2:3595,
                            y = (3595 + n_label),
                            data = train_hex_split[[1]],
                            validation = train_hex_split[[2]],
                            activation = "Rectifier",
                            hidden = c(50, 50, 50),
                            epochs = 100,
                            classification = FALSE,
                            balance_classes = FALSE)

  ## Print the Model Summary
  print(model)

  ## Use the model for prediction and store the results in submission template
  raw_sub[, (n_label + 1)] <- as.matrix(h2o.predict(model, test_hex))

}
```

<br>


#### Step 2.5 - Save Results as a  CSV

The final step is to save the predictions as a CSV file.

```
write.csv(raw_sub, file = "./results/my_Kaggle_submission.csv", row.names = FALSE)
```

<br><br>


**************

### Scaling Up Your Data Analysis!

I have walked you through a simple H2O machine learning exercise for Kaggle on 
the Domino cloud. I hope the starter code and tutorials can help you better
understand the R + H2O + Domino mechanism. However, the simplicity of the model 
means you will not be able to achieve a very good score on the Kaggle leaderboard. 

When you are ready to gear up your effort (e.g. building more complex models), 
you can easily scaling up your data analysis on Domino in a few steps.

<br>

#### Choose a Higher Hardware Tier

```Nick, please update this screenshot ... all tiers are free in my account```

<center><img src="http://i.imgur.com/EPTWkTS.png" alt="domino_hardware" style="width:400px"></center>

<br>


#### Modify Your Code

If you use the R + H2O + Domino combination, you can easily improve performance
by increasing the physical memory allowance. H2O will automatically parallelize
the machine learning algorithms and utilize all CPU cores. For general code 
parallelization, read this Domino blog post about [easy parallel loops](http://blog.dominoup.com/simple-parallelization/).

```
## Increase the H2O Cluster Memory Allowance (e.g. 25GB)
localH2O <- h2o.init(max_mem_size = '25g') 
```

<br>


##### Multiple Instances!

Try different settings at the same time

(screenshot here)


<br><br>


**************

### More about Domino and H2O

H2O ....

Domino ....

<br>


#### Other Cool Domino Features

<br>


#### Other Machine Learning Algorithms in H2O

NB, RF, GBM, GLM ... 

<br>


#### Other Key H2O Functions


<br>




**************

### Conclusions


I think Domino is very user-friendly and flexible as you can use the web UI or write your own scripts to manage your Domino projects. Although the tutorials here are very R-centric, please remember that Domino also supports other programming langauges like Python and Matlab.

Transferring files is free on Domino. The storage limit is about 30GB per project.

Most of the (human processing) time in data analysis is about getting the data into the right format.
I like H2O a lot because it handles large number of categorical variables and missing values out of the box.

Of course, being a data scientist, you cannot only rely on automatic data pre-processing. 
Especially for Kaggle competition, a lot of work is needed to investigate the data
and to determine appropriate pre-processing tasks manually. Again, that will be a topic for future discussion.

(Having said that, without any manual data pre-processing, I have managed to achieve
very good performance using h2o.deeplearning(...) and simple models blending.)



1. Domino - On demand and scalable cloud service that is built for data scientists.
2. H2O - highly efficient memory management and parallelised machine learning algorithms
3. User-friendly - Both Domino and H2O have great Web UI.
4. Native R Support - Both Domino and H2O have their own R packages for seamless R integration.
5. R + H2O + Domino = World-Class Analytics Machine.
6. A truly practical and scalable machine learning solution for everyone.
7. Try it! Ask them questions. Give them feedback. Help them improve and evolve!

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

all the links here

<br><br>

**************

### Looking back 

Things are evolving quickly these days. It is very important to keep an open mind when new tools appear. Two years ago, if you told me that R, H2O and Domino could one day work together and analyse big data, I would simply laugh it off. All I could imagine was a pirate ordering drinks and pizzas. 

<br><br>
