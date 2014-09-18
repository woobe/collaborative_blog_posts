Using R, H2O and Domino for Practical and Scalable Data Analysis
===============

*version 0.10*

<br>


### Introduction

This blog post is the sequel to [TTTAR1 a.k.a. an introduction to H2O Deep Learning](http://bit.ly/bib_TTTAR1). If the previous blog post was a brief intro to H2O, this post is a proper machine learning case study based on a recent [Kaggle competition](https://www.kaggle.com/c/afsis-soil-properties). In short, I am leveraging the power of R, H2O and Domino to compete in a real-world data mining contest.

(screenshot here ... update later)

Note that the public score is only based on a small subset (17%) of test data. My position on the final leaderboard might change dramatically. In my opinion, climbing up the public leaderboard is just the first step, making sure the models are generalised enough to stay up is the real challenge. Anyway, that is another topic for a future blog post. 

<br>

#### Learning-by-Doing

I always believe that learning-by-doing is the best way to learn. So I have prepared two short tutorials with code below to get you started with Domino and H2O. Hopefully, by going through the tutorials, you will be able to master the basics and to try your own data analysis with the new tools. Moreover, if you follow the steps and run the code, you will get a CSV file that is ready for the Kaggle competition. 

The purpose of this post is not only about Kaggle competitions. It is more about finding a generic, robust, practical and scalable data analysis solution. A solution that I can rely on and apply to many of my machine learning problems in life. My experience with this R + H2O + Domino combination in the last couple weeks has been very promising. So I would like to use this opportunity to share with you my experience. Hopefully, this post will encourage more data geeks out there to give R, H2O and Domino a try if they haven't done so.

<br>

#### What are H2O, Domino and Kaggle?

T.B.C.

<br><br>


**************

### Tutorial One - Quick Start with Domino

In the first tutorial, I will only focus on the basic Domino operations via 
Web UI and R interface. Although the R code is based on a Kaggle example using 
H2O, it is hard to learn two new things at the same time. So I will leave the 
H2O machine learning discussion for the next section. 

Ready? Let's go!

<br><br>

#### Step 1 - Get Up and Running with Domino

If you haven't done so, [sign up](update link) for a free account on the site, 
download and install the [client](update link). If you aren’t sure how to do this, 
you can follow their [quick-start guide](update link).

<br>

<center><img src="http://i.imgur.com/HAQkggc.png" alt="domino_website" style="width:640px"></center>

<br><br>


#### Step 2 - R Interface for Domino

Domino has its own [R package](update link) on CRAN. After installing the package, 
you can log into your Domino account and manage your projects directly from R. 
The Domino team has done a great job streamlining the whole process. Personally, 
I think this is yet another excellent example of using R as an interface.


```
install.packages("domino")
library(domino)
domino.login("your_username", "your_password")
```

<br><br>


#### Step 3 - Download Data and Code

This tutorial is based on the Kaggle competition. In order to run the analysis,
you will need to [download the original datasets](https://www.kaggle.com/c/afsis-soil-properties/data) 
from Kaggle and this R script ("Kaggle_AfSIS_with_H2O.R")

<br>

<center><img src="http://i.imgur.com/g7Bk82B.png" alt="kaggle_data" style="width:640px"></center>

<br><br>


#### Step 4 - Upload Data and Code to Domino

You will need to upload the files to a specific project folder on Domino.
To keep things simple, I will use the "quick-start" folder here because most of 
you should have this folder somewhere on your local drive after going through 
Domino's [quick start guide](update link).

On your machine, copy the datasets and R script to the 'quick-start' folder. The 
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

After that, you are ready to upload the files via R. 

```
## Set Working Directory to the 'quick-start' folder
setwd("quick_start_dir_on_your_local_drive") 
```

```
## Upload new files to the 'quick-start' folder on Domino cloud
domino.upload()
```

<br><br>


#### Step 5 - Check the Files

Before running the analysis, check and make sure the files are on the cloud. 
You can log into Domino's web UI and browse your files in the 'quick-start' folder.

<br>

<center><img src="http://i.imgur.com/PRpk7ws.png" alt="kaggle_files" style="width:640px"></center>

<br><br>



#### Step 10 - Start a Run

Great, you now are ready to run the analysis on the cloud! 
There are two ways to do this.

You can use the Web UI to start a run (Runs -> Run -> Enter of the File Name-> Start Run).

<br>

<center><img src="http://i.imgur.com/s5V8XBr.png" alt="kaggle_startrun" style="width:640px"></center>

<br>

Alternatively, you can send the command directly from R.

```
domino.run("Kaggle_AfSIS_with_H2O.R")
```

<br><br>


#### Step 11 - Monitor the Process

Domino has a neat Web UI for monitoring your runs online. 
You can access to all your files and project settings panel on the left.
When you click on any of your runs, it will display the native console 
(R in this case) with a summary below showing CPU, memory usage and other stats.

<br>

<center><img src="http://i.imgur.com/sHyFswF.png" alt="kaggle_monitor" style="width:640px"></center>

<br><br>



#### Step 12 - Download the Results

By default, you will receive an email notification once the run has finished. 
There are more ways to customize notifcation but I will leave that for a future
discussion (read more [here](update link) if you are interested).

<br>

<center><img src="http://i.imgur.com/gpHK8TK.png" alt="kaggle_monitor" style="width:640px"></center>

<br>

After that, you can download the results (CSV for Kaggle submission) from the
Web UI or via R.

<br>

<center><img src="http://i.imgur.com/BYdgulM.png" alt="kaggle_monitor" style="width:640px"></center>

<br>


```
## Download the results to your local drive
domino.download()
```

<br><br>


#### Step 13 - Submit it to Kaggle (Optional)

You can now go to the [submission page](https://www.kaggle.com/c/afsis-soil-properties/submissions/attach) 
and upload the CSV file. Good luck :)

<br><br>

#### More about Domino

Other features ...

<br><br>



**************

### Dig Deeper - Using H2O Deep Learning for Soil Property Predictions

Intro ....

<br><br>

#### Step 1 - Install H2O

CRAN Version
```
install.packages("h2o")
```


Bleeding Edge Version
```
## Specify H2O version here
h2o_ver <- "1510"

## Install H2O
local({r <- getOption("repos"); r["CRAN"] <- "http://cran.us.r-project.org"; options(repos = r)})
txt_repo <- (c(paste0(paste0("http://s3.amazonaws.com/h2o-release/h2o/master/",
                             h2o_ver),"/R"),
               getOption("repos")))
install.packages("h2o", repos = txt_repo, quiet = TRUE)
```

<br><br>


#### Step 2 - Initiate and Connect to a Local H2O Cluster on Domino

```
library(h2o)
localH2O <- h2o.init(max_mem_size = '1g')

```

<br><br>

#### Step 3 - Import Data

```
## Get the local path on Domino
path_cloud <- getwd()

## Define other paths
path_train <- paste0(path_cloud, "/data/train.zip")
path_test <- paste0(path_cloud, "/data/test.zip")
path_submission <- paste0(path_cloud, "/data/sample_submission.csv")
path_output <- paste0(path_cloud, "/results/my_Kaggle_submission.csv")

## Import Data to H2O Cluster
train_hex <- h2o.importFile(localH2O, path = path_train)
test_hex <- h2o.importFile(localH2O, path = path_test)
raw_sub <- read.csv(path_submission)

```

<br><br>

#### Step 4 - Train a Deep Neural Networks model for each variable
```
## Split the dataset into 80:20 for training and validation
train_hex_split <- h2o.splitFrame(train_hex, ratios = 0.8, shuffle = TRUE)

## One Variable at at Time
ls_label <- c("Ca", "P", "pH", "SOC", "Sand")

for (n_label in 1:5) {

  ## Display
  cat("\n\nNow training a DNN model for", ls_label[n_label], "...\n")

  ## Train a DNN
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

<br><br>

#### Step 5 - Save Results as a  CSV
```
write.csv(raw_sub, file = path_output, row.names = FALSE)
```
<br><br>


#### H2O Machine Learning Algorithms

NB, RF, GBM, GLM ... 

<br><br>


#### Other Key H2O Functions


<br><br>


**************

### Scaling it up! 

Run your analysis faster with Domino

- from 1 core to 32 cores
- from 1GB Ram to 60GB Ram

##### Step 1 - Change the Hardware Tier

(screenshot here)


##### Step 2 - Modify the R script slightly


Allocate more memory for the H2O cluster
```
localH2O <- h2o.init(max_mem_size = '55g')
```

Go deeper with DNN
```
model <- h2o.deeplearning(...,
                          hidden = c(1000, 1000, 1000),
                          epochs = 1000,
                          ...)
```

##### Multiple Instances!

Try different settings at the same time

(screenshot here)

<br><br>

**************

### Conclusions


I think Domino is very user-friendly and flexible as you can use the web UI or write your own scripts to manage your Domino projects. Although the tutorials here are very R-centric, please remember that Domino also supports other programming langauges like Python and Matlab.

Transferring files is free on Domino. The storage limit is about 30GB per project.



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
