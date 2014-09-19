Using R, H2O and Domino for Practical and Scalable Data Analysis
===============

*version 1.00 - Joe passing the ball to Nick*

<br>

### Introduction

This blog post is the sequel to [TTTAR1 a.k.a. An Introduction to H2O Deep Learning](http://bit.ly/bib_TTTAR1). If the previous blog post was a brief intro, this post is a proper machine learning case study based on a recent [Kaggle competition](https://www.kaggle.com/c/afsis-soil-properties). In short, I am leveraging the power of [R](http://www.r-project.org/), [H2O](http://h2o.ai/) and [Domino](http://www.dominoup.com/) to compete in a real-world data mining contest.

<center><img src="http://i.imgur.com/S3x3d2O.png" alt="kaggle_topspot" style="width:700px"></center>

<br>

The competition got tougher since then but I am still very proud to say that at least I stayed top for a few days!
Note that the public score is only based on a small subset (13%) of test data. My position on the final leaderboard might change dramatically. In my opinion, climbing up the public leaderboard is just the first step, making sure the models are generalized enough to stay up is the real challenge. Anyway, that is another topic for a future blog post.

<br>

#### Accelerate Your Data Analysis with Domino

I think it is fair to say that Kaggle contests are very challenging. Even more 
so when you put the time constraint into the mix. Using [Domino](http://www.dominoup.com/), 
I can easily scale up my analysis, take advantages of the parallelized code and carry out many tests 
within a very short space of time. Competing in a data mining contest is all about 
understanding the problem better and identifying the best strategies sooner
than your opponents. Having the ability to ask the data many questions at the 
same time is very crucial. 

In practice, that means I can cut down days or even weeks of analysis to just a few hours.
Using Domino, I can quickly evaluate many different machine learning strategies 
for the Kaggle contest. On top of that, I don't have to waste any time on infrastructure 
setup and hardware maintenance. Domino simply takes care of the rest. This really 
helps me to focus on understanding the machine learning problem better and improving 
the model performance steadily over time.


<br>

#### Go Deeper with H2O

To say that I am very impressed with the predictive performance of the 
[H2O deep learning module](https://github.com/0xdata/h2o/tree/master/docs/deeplearning/) 
is an understatement. All data geeks know about the 
[“No Free Lunch” theorem](http://www.statsblogs.com/2014/01/25/machine-learning-lesson-of-the-day-the-no-free-lunch-theorem/). 
Yet, againist all odds and my past experience, I have managed to climb up the ladder 
using just the ```h2o.deeplearning``` algorithm and some simple model 
averaging strategies.

Performance is not the only thing, H2O's highly efficient memory management and 
parallelized algorithms are just as amazing. It got even better when I realized 
that I can use R, H2O and Domino altogether. At that moment, I knew I had found 
a very promising machine learning solution and hence the motivation of this blog post.

<br>

#### About this Blog Post

The purpose of this post is not only about Kaggle competitions, 
**it is more about finding a practical and scalable data analysis solution**. 
A generic and robust solution that I can rely on and apply to many of my machine 
learning problems in life (like [this one](https://github.com/woobe/wc2014)). 
My experience with this R + H2O + Domino combination in the last couple weeks has
been very promising. So I would like to use this opportunity to share with you my 
experience. I realy hope that this post will encourage more data geeks out there 
to give R, H2O and Domino a try if they haven't done so.

Using H2O alone is a huge topic. In order to keep things simple, 
I will just walk you through the starter code here. I promise you that there 
will be a more in-depth discussion on various machine learning algorithms and 
strategies after the contest. I also hope that these blog posts can eventually 
evolve into proper tutorials (as my tiny contribution to the data science communitiy).

<br>

#### Learning-by-Doing

I always believe that learning-by-doing is the best way to learn. So I have prepared 
**two short tutorials with R starter code** below to get you started with Domino and H2O. 
Hopefully, by going through the tutorials, you will be able to master the basics 
and to try H2O and Domino for your own data analysis very soon. Moreover, if you
follow all the steps, you will get a CSV file that is ready for the Kaggle 
competition. Finally, when you are ready to up your game, check out the **third tutorial** 
about scaling up your analysis in just a few easy steps. 

<br>

#### Wait ... H2O, Domino, Kaggle? Who Are They?

Just in case you haven't heard of them yet ...

- [H2O](http://h2o.ai/) is an open-source math and in-memory prediction engine for big data science developed by [0xdata](http://0xdata.com/).
- [Domino](http://www.dominoup.com/) is a platform for analysts and data scientists that handles all the “plumbing” required to run, scale, share, and deploy analytical models.
- [Kaggle](http://www.kaggle.com/) is a platform for predictive modeling and analytics competitions and consulting.

Source: [CrunchBase](http://www.crunchbase.com/)

<br>

#### Ready?

OK, that's quite enough for an intro. ***Let's dive into it!!!***

<br><br>

**************

### Tutorial One - Getting Started with Domino

In the first tutorial, I will only focus on the basic Domino operations via 
their web UI and R interface. Although the R script is all about H2O machine learning, 
it is hard to learn two new things at the same time. So I will keep this simple
and leave the H2O discussion for the next tutorial.

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
using [this R script](https://github.com/woobe/blenditbayes/tree/master/2014-09-r-h2o-domino) ```Kaggle_AfSIS_with_H2O.R```.

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

#### Try Your Own Code

I have shown you the basic steps to get my Kaggle starter code up and running on 
the Domino cloud. Now it is time to try your own code. Remember Domino also 
supports **Python**, **Matlab** and **Julia**!

<br>

#### Share Your Projects

It is very easy to share your Domino projects with others. You can enable public 
access to your project folder in the project settings so everyone can view your 
files and runs. For example, see my ```quick-start``` project [here](https://app.dominoup.com/woobe/quick-start).

<center><img src="http://i.imgur.com/FpqM9Nj.png" alt="kaggle_monitor" style="width:300px"></center>

<br>

#### Version Control

The version control on Domino is a well-thought process specially designed for
data scientists. Instead of versioning individual files one at a time, Domino
creates snapshots of your data, code and results altogether. That means it is very
easy to go back in time and make reference to a particular run with the exact data 
and code used.

<center><img src="http://i.imgur.com/hCUvJWR.png" alt="kaggle_monitor" style="width:300px"></center>

<br><br>

**************

### Tutorial Two: Using H2O to Predict Soil Properties

In this section, I will explain how I use R and H2O to train predictive models 
for the Kaggle competition. In short, we have to develop regression models based 
on 1158 rows of training data and then use the models to predict five soil properties
Ca, P, pH, SOC and Sand for each of the 728 test records. For more 
information, please go to the [description page](https://www.kaggle.com/c/afsis-soil-properties) on Kaggle.

<br>

#### Step 2.1 - Install R Interface for H2O

Again, R acts as an interface. Having R as the common interface, 
H2O and Domino can work together seamlessly. This is one of the key reasons why
I think this R + H2O + Domino solution is very promising.

Like Domino, H2O also has an excellent R package. To begin with, you can install
the CRAN Version of H2O:

```
install.packages("h2o")
```

<br>

If you want to take advantages of the new H2O features, you can install the 
bleeding edge version.

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

In order to find out the latest H2O version number, go to
[this page](http://s3.amazonaws.com/h2o-release/h2o/master/1511/index.html) and 
look for the last four digits as shown in screenshot below.

<center><img src="http://i.imgur.com/VCuFIHO.png" alt="h2o_version" style="width:700px"></center>

<br>

(Optional) I use H2O a lot these days so I wrote a wrapper function to make my 
life easier. With two lines of code, you can install or upgrade H2O to the 
latest bleeding edge version:

```
## Use the wrapper function in my package 'deepr'
devtools::install_github("woobe/deepr")
deepr::install_h2o()
```

<br>


#### Step 2.2 - Initiate and Connect to a Local H2O Cluster

Using the argument ```max_mem_size``` in function ```h2o.init(...)```, we can 
manually limit the physical memory usage. In this tutorial, 
we set a limit of 1GB of memory as it is the maximum allowance of the Domino free tier.

```
library(h2o)
localH2O <- h2o.init(max_mem_size = '1g')
```

<center><img src="http://i.imgur.com/xvJFVzA.png" alt="h2o_version" style="width:500px"></center>

<br>


#### Step 2.3 - Import Data

Importing data is one of the best things I like about H2O!!! You can load compressed 
files (```.zip```, ```.gz```) directly into the H2O cluster. This may not be significantly 
important for the small Kaggle dataset in this tutorial but it is certainly useful 
for bigger datasets.

```
## Import Data to H2O Cluster
train_hex <- h2o.importFile(localH2O, "./data/train.zip")
test_hex <- h2o.importFile(localH2O, "./data/test.zip")
```

<br>


#### Step 2.4 - Train Deep Neural Networks Models and Make Predictions

Without further ado, here is the starter code to train one deep neural networks model 
for each target variable and then use the models to make predictions. There are
quite a few variables to tweak in the ```h2o.deeplearning(...)``` function. To keep
things simple, I only provide the barebone code to get you started. For more information,
I strongly recommend going through the [vignette and demo code](https://github.com/0xdata/h2o/tree/master/docs/deeplearning/).

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

The final step is to save all predictions as a CSV file. This is the CSV file
in the correct Kaggle submission format. 
```
write.csv(raw_sub, file = "./results/my_Kaggle_submission.csv", row.names = FALSE)
```

<br>


#### Try Other Datasets

That's it! You have just trained some Deep Neural Networks models and used them
for prediction! Why don't you try the same thing on other datasets? For example,
the [Breast Cancer and MNIST datasets I used in the previous TTTAR blog post](http://bit.ly/bib_TTTAR1).

<br>

#### Try Other H2O Machine Learning Algorithms

```h2o.deeplearning``` is just one of the algorithms available in H2O. You
can also try ```h2o.gbm```, ```h2o.glm```, ```h2o.naiveBayes```, 
```h2o.randomForest``` and more. All these functions can be called directly from
R like the code example above. They have similar syntax so it
should be very straight forward. For more information, the 
[H2O tutorial](http://docs.0xdata.com/tutorial/top.html) is a great place to start with.

<br><br>


**************

### Tutorial Three - Scaling Up Your Data Analysis!

I have walked you through a simple H2O machine learning exercise for Kaggle on 
the Domino cloud. I hope the starter code and tutorials can help you better
understand the R + H2O + Domino mechanism. However, the simplicity of the model 
means you will not be able to achieve a very good score on the Kaggle leaderboard. 

When you are ready to gear up your effort (e.g. building more complex models) or
analyse much bigger datasets, you can easily scale up your data analysis on Domino 
in a just few steps. Ready? Read on!

<br>

#### Choose a Higher Hardware Tier

You can find the hardware tier drop down list in the project settings. All you
need to do is to choose a tier that suits your needs. Domino will sort out the 
rest for you.

```Nick, please update this screenshot ... everything is free for me at the moment```

<center><img src="http://i.imgur.com/EPTWkTS.png" alt="domino_hardware" style="width:400px"></center>

<br>


#### Modify Your Code

If you use the R + H2O + Domino combination, you can easily improve H2O's performance
by increasing the physical memory allowance. H2O will automatically parallelize
the machine learning algorithms and utilize all CPU cores. For general code 
parallelization, read this Domino blog post about [easy parallel loops](http://blog.dominoup.com/simple-parallelization/).

```
## Increase the H2O Cluster Memory Allowance (e.g. 25GB)
localH2O <- h2o.init(max_mem_size = '25g') 
```

<br>


#### Use Multiple Instances

To further increase productivity, you can start multiple runs at the same time.
Again, no complex set up is required. Just start your runs as usual. Domino will
take care of the rest.

<center><img src="http://i.imgur.com/AYIriLr.png" alt="domino_hardware" style="width:400px"></center>

<br><br>


**************

### Conclusions

If I have to summarize this experience, I would say that the discovery of this 
R + H2O + Domino combination has been very exciting and promising! 
I am now very confident to say that I have a practical and scalable solution to 
deal with not just Kaggle but many other machine learning problems I have in life.
I also know that this solution can get even better! I will continue to explore and
experiment with other tools.

<br><br>

**************

### All the Links

It's quite a lengthy post so let me summarize all the useful resources here:

#### Domino 

- [Sign Up](http://www.dominoup.com/)
- [Documentation & FAQ](http://help.dominoup.com/)
- [Quick Start](http://help.dominoup.com/quickStart)
- [Step-by-Step Tour](https://app.dominoup.com/tour)
- [Blog](http://blog.dominoup.com/)
- [Nick's Post about Integrating R with Production Systems using an HTTP API](http://blog.revolutionanalytics.com/2014/08/using-r-inside-the-enterprise-integration-with-existing-systems.html)
- [Easy Parallel Loop](http://blog.dominoup.com/simple-parallelization/)

<br>

#### H2O

- [Documentation](http://docs.0xdata.com/)
- [Quick-Start Videos](http://docs.0xdata.com/tutorial/videos.html)
- [R Package](http://docs.0xdata.com/Ruser/Rpackage.html)
- [R Tutorial](http://docs.0xdata.com/Ruser/rtutorial.html)
- [Oxdata Presentations](http://www.slideshare.net/0xdata)
- [Deep Learning through Examples Screencast](http://www.youtube.com/watch?v=fdbQreQacIQ&feature=youtu.be)
- [h2ostream Forum on Google](https://groups.google.com/forum/#!forum/h2ostream)
- [H2O Deep Learning Vignette and Demo Code](https://github.com/0xdata/h2o/tree/master/docs/deeplearning/)

<br><br>

**************

### It Isn't Just About the Tools. It Is More About the People!

I have told you how great these tools are. But I haven't mentioned the awesome 
people behind the scenes. 

First of all, I would like to thank [Nick Elprin](https://twitter.com/DominoDataLab) 
for his tremendous support since the early days of Domino. Not only has Nick given 
me unlimited cloud resources in the last couple weeks to experiment with this R + H2O + Domino combination (it all began with a quick email *"Hi Nick, can I use H2O on Domino?"*), he also continously 
helps me out with many technical issues and turns my requests into new features. 

Then, of course, is the [Oxdata team](http://0xdata.com/about/) ([Sri Ambati](https://twitter.com/srisatish), 
[Arno Candel](https://twitter.com/ArnoCandel), Viraj Parmar, Cliff Click, Kevin Normoyle, 
[Raymond Peck](https://twitter.com/raymondpeck3), Spencer Aiello and many others) 
behind the H2O engine. Since the early days when I began taking my baby steps to 
understand H2O, they have been emailing me tips and information about H2O as well 
as encouraging me to push the boundaries. Especially [Arno Candel](https://twitter.com/ArnoCandel) 
who gave me some very specific advice on fine-tuning ```h2o.deeplearning``` and other functions.

I hope you find this post useful. If you decide to give this R + H2O + Domino 
combination a try but have questions regarding the set up, feel free to 
[email](mailto:jofai.chow@gmail.com) / [tweet](https://twitter.com/matlabulous) me 
as well as the Domino and Oxdata team. I know your questions and feedback will 
help them evolve and shape even better products for data science. Unfortunately, 
I need to follow Kaggle competition rules and I can't tell you exactly 
what I do to climb up the leaderboard. Yet, you can pretty much guess it from the 
name of my blog "[Blend It Like a Bayesian!](http://bit.ly/blenditbayes)".

I afraid I can't cover everything in one post but I will continue to blog about 
other cool Domino and H2O features in the coming months.

Till next time.

Joe
