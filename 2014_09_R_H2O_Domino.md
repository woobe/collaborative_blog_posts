Using R, H2O and Domino for Real, Practical and Scalable Data Analysis
===============

*version 0.7*

<br>


### Introduction

This blog post is the sequel to [TTTAR1 a.k.a. an introduction to H2O Deep Learning](http://bit.ly/bib_TTTAR1). If the previous blog post was a brief intro to H2O, this post is a proper machine learning case study based on a recent [Kaggle competition](https://www.kaggle.com/c/afsis-soil-properties). In short, I have (finally, yes, finally!) managed to achieve good performance for a real-world data mining contest by leveraging the power of R, H2O and Domino. 

(screenshot here)

Note that the public score is only based on a small subset (17%) of test data. My position on the final leaderboard might change dramatically, I'm trying my best to avoid the drop. In my opinion, climbing up the public leaderboard is just the baby step, making sure the models are generalised enough to stay up is the real challenge. Anyway, that is another topic for a future blog post. 

The main purpose of this post is not about Kaggle competitions. It is more about finding a generic, robust, practical and scalable data analysis solution. A solution that I can rely on and apply to many of my machine learning problems in life. My experience with this R + H2O + Domino combination in the last couple weeks has been very promising. So I would like to use this opportunity to share with you my experience. Hopefully, this post will encourage more data geeks out there to give R, H2O and Domino a try if they haven't done so.

I always believe that learning-by-doing is the best way to learn. So here is a starter code pack for the Kaggle competition. So be prepared to get your hands dirty and craft your own Kaggle submission :) I will break the code down and explain each key steps in the following sections.

<br><br>

#### What are H2O, Domino and Kaggle?

Brief intro here ...

<br><br>


**************

### Quick Start - Running the Starter Code on Domino Cloud

Intro ...

<br><br>

#### Step 1 - Sign up for a free Domino account

URL here 
(screenshot here)

<br><br>

#### Step 2 - Install Domino Client for your OS

Install Client
(screenshot here)

<br><br>> domino.run("Kaggle_AfSIS_with_H2O.R")
  Determining which files are out of date...

No changes to upload to server, because you're up to date.
Run for project woobe/quick-start started. You can view progress here: https://app.dominoup.com/woobe/quick-start#r/5419a889e4b062b695d962a9


#### Step 3 - Go through the tutorial (Optional)

(screenshot here)

<br><br>


#### Step 4 - Install and Load Domino's R Package

```
install.packages("domino")
library(domino)
```

<br><br>

#### Step 5 - Login 

```
domino.login("your_username", "your_password")
```

<br><br>


#### Step 6 - Set working diectory to a folder of your choice

```
setwd("your_working_dir") 
```

<br><br>

#### Step 7 - Download the "quick-start" Project

```
domino.get("quick-start")
```

After that, you should have the following files

- results/
- main.m
- main.py
- main.r

<br><br>

#### Step 8 - Upload the Kaggle AfSIS data and my R script

Copy the data files and my R script to the folder

- **data/train.zip**
- **data/test.zip**
- **data/sample_submission.csv**
- results/
- **Kaggle_AfSIS_with_H2O.R**
- main.m
- main.py
- main.r

```
domino.upload()
```

<br><br>

#### Step 9 - Check the files using Web UI

(screenshot here)

<br><br>

#### Step 10 - Run the R Script (Two Options)

Option 1 - Web UI

(screenshot here)

Option 2 - R

```
domino.run("Kaggle_AfSIS_with_H2O.R")
```

<br><br>


#### Step 11 - Monitor the Process

(screenshot here)

<br><br>



#### Step 12 - Download the Results

Email notification

(screenshot here)

Option 1 - Web UI

(screenshot here)

Option 2 - R

<br><br>


#### Step 13 - Submit it to Kaggle


(screenshot here)

<br><br>

#### Share your project folder

(screenshot here)

<br><br>

#### Other Cool Stuff

(screenshot here)

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
train_hex_split <- h2o.splitFrame(train_hex, ratios = c(0.8, 0.199), shuffle = TRUE)

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

### Conclusions

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
