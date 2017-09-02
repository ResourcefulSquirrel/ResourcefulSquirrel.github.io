---
title: File names, directories, R, and switching OSes
author: Katie
date: 2017-09-02
categories: R data
---

One of the key ways that I use R to make sure I can trace back my data to the original file or files which created an analysis. Most of the work I do in R is the immensely important but fiddly data-cleaning and data-wrangling work that quietly drives scientists crazy. At the very least, it leaves us sitting alone mumbling to ourselves in coffee shops and other fine drinking establisments.

One of the problems that I have recently encountered is due to switching from my old computer (Mac) to a Windows PC. This switch is because of some other software requirements, but I can't take a 4-month break from data analysis while I spend time doing fieldwork collecting new data! 

This means that I'm spending plenty of time finding out which of my previously-written scripts have a call to grab data from somewhere that relies on the file path system on my Mac, because they break when run on the PC. It is also a good reminder to me to clean up old R scripts that worked but had the organization of a Jackson Pollock painting.

So, to that end, I decided to upgrade my previous method of dealing with this problem:

```r
#mac
setwd("~/CloudFolder/Project/ProjectCode")

#windows
setwd("C:/Users/Squirrel/CloudFolder/Project/ProjectCode")
```

To a slightly better solution where RStudio checks which OS is running and then uses the correct filepath. Yes, this is still hard-coding the location into my script, and blah blah blah bad form, but these are scripts that might be used by one other person to process data used by a total of 3 people. I do not need a general-purpose solution here, I just want to be able to run my entire script without error.

So I took my question to [Twitter](https://twitter.com/ResourcefulSqrl/status/900263030612774912), as one does, and got some advice.

And this is my revised code to deal with switching between operating systems and computers for my project:

```r
if(Sys.info()['sysname'] == "Darwin"){
  setwd("~/CloudFolder/Project/ProjectCode")
  print("set working directory for Mac machine")
  } else {
    if(Sys.info()['sysname'] == "Windows"){
  setwd("C:/Users/Squirrel/CloudFolder/Project/ProjectCode")
  print("set working directory for windows machine")
    }
  }
```

And along this journey I learned about the ```file.path``` function to construct filepaths, which I did not use here, but think will be useful in the future.

I also learned that Mac reports the system name as "Darwin" to RStudio or R, which would be a frustrating problem to troubleshoot if I hadn't run across information which included that little nugget. So I am repeating it here :-)


