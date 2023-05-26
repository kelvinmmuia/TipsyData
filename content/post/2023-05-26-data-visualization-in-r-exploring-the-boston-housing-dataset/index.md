---
title: Data Visualization in R, exploring the Boston Housing Dataset
author: Kelvin M. Muia
date: '2023-05-26'
output: html_document
slug: []
categories:
  - R
  - packages
tags:
  - data exploration using r
  - data visualization using r
  - ggplot2
  - ggplot2 in r
  - data analytics
  - data science
  - data transformation
  - data processing
  - boxplot in r
description: Visually exploring the Boston Housing Dataset with R.
lead: Gain valuable insights through data visualization using the famous Boston Housing dataset.
thumbnail:
    src: img/chas_medv_boxplot.png
    visibility: list
---

<!--more-->



**The Boston Housing Dataset**   

The Boston Housing dataset is a classic dataset widely used for regression analysis and predictive modeling tasks. It consists of various attributes of houses in Boston, such as crime rate, average number of rooms, and proximity to employment centers. In this article, we will leverage this dataset to create informative and visually appealing plots.   

**Loading and Exploring the Dataset**   

Fortunately, the dataset is already availed in R through a number of publicly available packages including the `MASS`, `ISLR`, `mlbench` packages among others. To access it, one would only need to install one of these packages, and load the dataset.

Below we load the data set from the `MASS` package, and we view its structure using the `str()` function of R.  


```r
library(MASS) #required library
data(Boston) #load data
str(Boston)#internal structure of the dataset
## 'data.frame':	506 obs. of  14 variables:
##  $ crim   : num  0.00632 0.02731 0.02729 0.03237 0.06905 ...
##  $ zn     : num  18 0 0 0 0 0 12.5 12.5 12.5 12.5 ...
##  $ indus  : num  2.31 7.07 7.07 2.18 2.18 2.18 7.87 7.87 7.87 7.87 ...
##  $ chas   : int  0 0 0 0 0 0 0 0 0 0 ...
##  $ nox    : num  0.538 0.469 0.469 0.458 0.458 0.458 0.524 0.524 0.524 0.524 ...
##  $ rm     : num  6.58 6.42 7.18 7 7.15 ...
##  $ age    : num  65.2 78.9 61.1 45.8 54.2 58.7 66.6 96.1 100 85.9 ...
##  $ dis    : num  4.09 4.97 4.97 6.06 6.06 ...
##  $ rad    : int  1 2 2 3 3 3 5 5 5 5 ...
##  $ tax    : num  296 242 242 222 222 222 311 311 311 311 ...
##  $ ptratio: num  15.3 17.8 17.8 18.7 18.7 18.7 15.2 15.2 15.2 15.2 ...
##  $ black  : num  397 397 393 395 397 ...
##  $ lstat  : num  4.98 9.14 4.03 2.94 5.33 ...
##  $ medv   : num  24 21.6 34.7 33.4 36.2 28.7 22.9 27.1 16.5 18.9 ...
```

The Boston dataset as explored above consists of 506 observations across 14 variables. All its variables are either of `numeric` or `integer` data types.  
See [here](https://tipsydata.netlify.app/post/2023-05-23-introduction-to-data-types-in-r) for more details about data types in R.

To get a further overview of the data, we can use the summary function as below;


```r
summary(Boston) #descriptive statistics
##       crim                zn             indus            chas        
##  Min.   : 0.00632   Min.   :  0.00   Min.   : 0.46   Min.   :0.00000  
##  1st Qu.: 0.08205   1st Qu.:  0.00   1st Qu.: 5.19   1st Qu.:0.00000  
##  Median : 0.25651   Median :  0.00   Median : 9.69   Median :0.00000  
##  Mean   : 3.61352   Mean   : 11.36   Mean   :11.14   Mean   :0.06917  
##  3rd Qu.: 3.67708   3rd Qu.: 12.50   3rd Qu.:18.10   3rd Qu.:0.00000  
##  Max.   :88.97620   Max.   :100.00   Max.   :27.74   Max.   :1.00000  
##       nox               rm             age              dis        
##  Min.   :0.3850   Min.   :3.561   Min.   :  2.90   Min.   : 1.130  
##  1st Qu.:0.4490   1st Qu.:5.886   1st Qu.: 45.02   1st Qu.: 2.100  
##  Median :0.5380   Median :6.208   Median : 77.50   Median : 3.207  
##  Mean   :0.5547   Mean   :6.285   Mean   : 68.57   Mean   : 3.795  
##  3rd Qu.:0.6240   3rd Qu.:6.623   3rd Qu.: 94.08   3rd Qu.: 5.188  
##  Max.   :0.8710   Max.   :8.780   Max.   :100.00   Max.   :12.127  
##       rad              tax           ptratio          black       
##  Min.   : 1.000   Min.   :187.0   Min.   :12.60   Min.   :  0.32  
##  1st Qu.: 4.000   1st Qu.:279.0   1st Qu.:17.40   1st Qu.:375.38  
##  Median : 5.000   Median :330.0   Median :19.05   Median :391.44  
##  Mean   : 9.549   Mean   :408.2   Mean   :18.46   Mean   :356.67  
##  3rd Qu.:24.000   3rd Qu.:666.0   3rd Qu.:20.20   3rd Qu.:396.23  
##  Max.   :24.000   Max.   :711.0   Max.   :22.00   Max.   :396.90  
##      lstat            medv      
##  Min.   : 1.73   Min.   : 5.00  
##  1st Qu.: 6.95   1st Qu.:17.02  
##  Median :11.36   Median :21.20  
##  Mean   :12.65   Mean   :22.53  
##  3rd Qu.:16.95   3rd Qu.:25.00  
##  Max.   :37.97   Max.   :50.00
```

**Creating Basic Plots in R**   

Let's start our data visualization journey by creating some basic plots. We will begin with a scatter plot of the average number of rooms (rm) versus the median value of owner-occupied homes (medv):


```r
library(ggplot2)#build plots in layers
library(ggpubr) #publication ready graphics

# Scatter plot
ggplot(Boston, aes(x = rm, y = medv)) +
  geom_point() +
  labs(x = "Average Number of Rooms",
       y = "Median Value of Owner-Occupied Homes",
       title = "Scatter Plot of Rooms vs. Median Value") +
  theme_pubr()
```

<img src="{{< blogdown/postref >}}index_files/figure-html/scatterplot-1.png" width="672" />


![A simple scatter plot](index_files/figure-html/scatterplot-1.png){width=50%}
     

In the scatter plot above, we can observe the relationship between the average number of rooms and the median value of owner-occupied homes. This plot gives us an initial understanding of how these variables are related. For instance, there appears to be a positive trend, where an increase in the number of rooms in a dwelling unit appears to result to an increase in the median value of owner occupied homes. This relationship could be explored using other methods such as `OLS` regression.    

**Advanced Data Visualization Techniques**

To further explore the Boston Housing dataset, we can employ advanced data visualization techniques. For instance, we can create a box plot of the housing prices (medv) grouped by the neighborhood (neighborhood):


```r
#box plot
ggplot(Boston, aes(x = factor(chas), y = medv, fill= factor(chas))) +
  geom_boxplot() +
  labs(x = "Charles River Dummy",
       y = "Median Value of Owner-Occupied Homes",
       title = "Box Plot of Housing Prices by the Charles River Dummy") +
  theme(plot.title = element_text(hjust = 0.5))+
  theme_pubr(legend = "none")
```

<img src="{{< blogdown/postref >}}index_files/figure-html/boxplot-1.png" width="672" />

     
![A simple scatter plot](index_files/figure-html/boxplot-1.png){width=50%} 
A boxplot is a powerful way of visualizing numerical data grouped by nominal or ordinal features. In this example, note the conversion of the otherwise `integer` data type of the `chas` variable to factor variable, which enables us to visualize the boxplot above. From the boxplot, it is easy to conclude that those census tracts bound to the Charles river were observed to have higher median values of owner occupied homes than those that weren't during the 1970 census. The boxplot also ndicates the presence of outliers (points that go beyond Tukey's fences) for those tracts that weren't bound to the river.   

**Conclusion**  

In this blog post, we have explored the Boston Housing dataset and demonstrated the power of data visualization in R. By creating visual representations of the data, we can easily identify patterns, relationships, and outliers.

Data visualization is an essential skill for any data scientist or analyst. It enables us to effectively communicate insights and make data-driven decisions.  

Leave a comment below and stay tuned for more exciting topics in our data science journey!
