# Assignment 3
Kat Wiles  
September 26, 2014  

Complete the exercises listed below and submit as a pull request to the [Assignment 3 repository](http://www.github.com/microbialinformatics/assignment03).  Format this document approapriately using R markdown and knitr. For those cases where there are multiple outputs, make it clear in how you format the text and interweave the solution, what the solution is.

Your pull request should only include your *.Rmd and *.md files. You may work with a partner, but you must submit your own assignment and give credit to anyone that worked with you on the assignment and to any websites that you used along your way. You should not use any packages beyond the base R system and knitr.

This assignment is due on October 10th.

------

####1.  
**Generate a plot that contains the different pch symbols. Investigate the knitr code chunk options to see whether you can have a pdf version of the image produced so you can print it off for yoru reference.**

![plot of chunk unnamed-chunk-1](./README_files/figure-html/unnamed-chunk-1.png) 

   
    
####2.  
**Using the `germfree.nmds.axes` data file available in this respositry, generate a plot that looks like this. The points are connected in the order they were sampled with the circle representing the beginning ad the square the end of the time course:**

   Note:   
    Iris helped me figure out how to get mice points.
    
![plot of chunk unnamed-chunk-2](./README_files/figure-html/unnamed-chunk-2.png) 



####3.  
**On pg. 57 there is a formula for the probability of making x observations after n trials when there is a probability p of the observation.  For this exercise, assume x=2, n=10, and p=0.5.  Using R, calculate the probability of x using this formula and the appropriate built in function. Compare it to the results we obtained in class when discussing the sex ratios of mice.**


```r
prob.choose<-1/choose(10,2)
```

The probability of making 2 observations after 10 trials is 0.0222. 



####4.  
**On pg. 59 there is a formula for the probability of observing a value, x, when there is a mean, mu, and standard deviation, sigma.  For this exercise, assume x=10.3, mu=5, and sigma=3.  Using R, calculate the probability of x using this formula and the appropriate built in function**

The probability of observing 10.3 in a normal distribution is 0.0279.



####5.  
**One of my previous students, Joe Zackular, obtained stool samples from 89 people that underwent colonoscopies.  30 of these individuals had no signs of disease, 30 had non-cancerous ademonas, and 29 had cancer.  It was previously suggested that the bacterium *Fusobacterium nucleatum* was associated with cancer.  In these three pools of subjects, Joe determined that 4, 1, and 14 individuals harbored *F. nucleatum*, respectively. Create a matrix table to represent the number of individuals with and without _F. nucleatum_ as a function of disease state.**  



```
##                           N with Disease State     N with F. nucleatum
## No Disease Present                          30                       4
## Non-Cancerous Ademonas                      30                       1
## cancer                                      29                      14
```



**Then do the following:**
**Run the three tests of proportions you learned about in class using built in R  functions to the 2x2 study design where normals and adenomas are pooled and compared to carcinomas.**
    


```
##        Disease State F. nucleatum
## Normal            60            5
## Cancer            29           14
```
 
 
 
 The probability value for the prop.test is 0.0022.
 The probability value for the fisher test is 0.0015.
 The probability value for the chi-squared test is 0.0022.
     
    
    
**Without using the built in chi-squared test function, replicate the 2x2 study design in the last problem for the Chi-Squared Test...**
    

```
##        no.fn f.nucleatum
## normal    60           5
## cancer    29          14
```

```
## [1] 108
```

```
## normal cancer 
##     65     43
```

```
##       no.fn f.nucleatum 
##          89          19
```

```
##         no.fn f.nucleatum
## normal 0.5556      0.0463
## cancer 0.2685      0.1296
```

```
##          no.fn f.nucleatum
## normal 0.92308     0.07692
## cancer 0.67442     0.32558
```

```
##         no.fn f.nucleatum
## normal 0.6742      0.2632
## cancer 0.3258      0.7368
```

    
    
**Calculate the expected count matrix and calculate the Chi-Squared test statistics. Figure out how to get your test statistic to match Rs default statistic.**
      
      
**Generate a Chi-Squared distributions with approporiate degrees of freedom by the method that was discussed in class (hint: you may consider using the `replicate` command)**
      
      
**Compare your Chi-Squared distributions to what you might get from the appropriate built in R functions**
      
      
**Based on your distribution calculate p-values**
      
      
**How does your p-value compare to what you saw using the built in functions? Explain your observations.**





####6.
**Get a bag of Skittles or M&Ms.  Are the candies evenly distributed amongst the different colors?  Justify your conclusion.**

