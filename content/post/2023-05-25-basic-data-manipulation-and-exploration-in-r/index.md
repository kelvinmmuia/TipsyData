---
title: Basic Data Manipulation and Exploration in R
author: Kelvin M. Muia
date: "2023-05-25"
slug: []
categories:
- R
- packages
tags:
- data analytics
- data science
- rstats
- tidyverse
- r
- ggplot2
- data processing
- data manipulation
- data transformation
- data exploration using r
description: In this article , we'll explore the basics of data manipulation and exploration
  in R. These skills are essential for any data scientist or analyst working with
  R.
lead: Explore the basics of data manipulation and exploration in R.
thumbnail:
  src: img/data_manipulation.png
  visibility: list
---

<!--more-->

**Importing Data.**

Before we can start manipulating and exploring data, we need to import it into R. R provides various functions to read data from different file formats such as CSV, Excel, or databases. 
Here's an example of importing a CSV file:


```r
#read a CSV file from your working directory into a data frame
data <- read.csv("data.csv")
```


**Filtering Data.**

Filtering allows us to select specific rows or columns from a dataset based on certain conditions. It helps us focus on the relevant data for our analysis.  

Below is an example of filtering data based on a condition:  


```r
#filter data based on a condition
filtered_data <- subset(data, column_name > 10)
```


**Sorting Data.**   

Sorting data allows us to arrange the rows of a dataset in a particular order based on one or more columns. It helps us organize the data for better analysis and visualization.    

Below is an example of sorting data:  


```r
# Sort data by a column in ascending order
sorted_data <- data[order(data$column_name), ]
```

    
**Transforming Data.** 

Data transformation involves modifying the structure or values of the data to derive new variables or enhance the existing ones. It enables us to perform calculations, create new features, or prepare data for specific analyses.   

Below is an example of transforming data by creating a new variable:  


```r
#create a new variable based on existing variables
data$new_variable <- data$variable1 + data$variable2
```


**Summary Statistics**   

Summary statistics provide a high-level overview of the dataset by calculating measures such as mean, median, standard deviation, and more. They help us understand the central tendencies and variability in the data. 

In R, descriptive statistics are easily computed using in-built functions such as `mean()`, `median()` as shown below:


```r
# Calculate summary statistics
mean_value <- mean(data$column_name)
median_value <- median(data$column_name)
sd_value <- sd(data$column_name)
```


**Basic Visualizations**   

Visualizations help us explore and communicate insights from the data effectively. R provides powerful libraries like ggplot2 for creating a wide range of plots, including histograms, scatter plots, and bar charts. 

Below is an example of creating a histogram:

```r
# Create a histogram
ggplot(data, aes(x = column_name)) +
  geom_histogram()
```


Feel free to copy and work with the code examples provided here, and even try working with a real data set!

If the code pieces provided do not work for one reason or another, don't freak out! Comment to ask any questions regarding this content or to share your experience with us below!
