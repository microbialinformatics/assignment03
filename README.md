# Assignment 3
Marian L Schmidt  
September 26, 2014  

Complete the exercises listed below and submit as a pull request to the [Assignment 3 repository](http://www.github.com/microbialinformatics/assignment03).  Format this document approapriately using R markdown and knitr. For those cases where there are multiple outputs, make it clear in how you format the text and interweave the solution, what the solution is.

Your pull request should only include your *.Rmd and *.md files. You may work with a partner, but you must submit your own assignment and give credit to anyone that worked with you on the assignment and to any websites that you used along your way. You should not use any packages beyond the base R system and knitr.

This assignment is due on October 10th.

------

1.  Generate a plot that contains the different pch symbols. Investigate the knitr code chunk options to see whether you can have a pdf version of the image produced so you can print it off for yoru reference. It should look like this:

    <img src="pch.png", style="margin:0px auto;display:block" width="500">



```r
symbol <- c(1:25)
y <- rep(1, 25)
plot(symbol, y, type = "n", xlab = "PCH value", xlim=c(0,25), frame = F, yaxt = "n", xaxt="n", ylab="", main="PCH Symbols")
axis(side=1, at=1:25)# abs=c(seq(1, 25, 2))side = 1, 1:25
     #lab=c("1", "", "3", "", "5", "", "7", "", "9", "", "11", "", "13", "", "15", "", "17", "", "19", "", "21", "", "23", "", "25")) 
abline(v=seq(1:25), b=0, col = "gray")
points(symbol,y, pch = c(1:25), cex=2)
```

<img src="./README_files/figure-html/unnamed-chunk-1.png" title="plot of chunk unnamed-chunk-1" alt="plot of chunk unnamed-chunk-1" style="display: block; margin: auto;" />

For frame = F:  http://stackoverflow.com/questions/4946491/removing-the-frame-from-the-boxplot-function-in-r
Axes: http://www.statmethods.net/advgraphs/axes.html




2.  Using the `germfree.nmds.axes` data file available in this respositry, generate a plot that looks like this. The points are connected in the order they were sampled with the circle representing the beginning ad the square the end of the time course:

    <img src="beta.png", style="margin:0px auto;display:block" width="700">


<img src="./README_files/figure-html/unnamed-chunk-2.png" title="plot of chunk unnamed-chunk-2" alt="plot of chunk unnamed-chunk-2" style="display: block; margin: auto;" />



3.  On pg. 57 there is a formula for the probability of making x observations after n trials when there is a probability p of the observation.  For this exercise, assume x=2, n=10, and p=0.5.  Using R, calculate the probability of x using this formula and the appropriate built in function. Compare it to the results we obtained in class when discussing the sex ratios of mice.




```r
n_trials <- 10
prob <- 0.5
x_observ <- 2
woot <- dbinom(x = x_observ, size = n_trials, prob = prob)
hist(woot, breaks = seq(-0.5, 10.5, 1))
```

![plot of chunk unnamed-chunk-3](./README_files/figure-html/unnamed-chunk-3.png) 

```r
percent <- woot*100
```

***Here, we performed 10 breedings of mice but only observed 2 of the breedings.  The probability of getting a male mouse versus a female mouse was 50/50.  This calculation was the same as what we did in class, with a point probability of 0.0439.  This means that 4.3945% of the time we will get either 2 females or 2 males from our 2 observations.***


4.  On pg. 59 there is a formula for the probability of observing a value, x, when there is a mean, mu, and standard deviation, sigma.  For this exercise, assume x=10.3, mu=5, and sigma=3.  Using R, calculate the probability of x using this formula and the appropriate built in function



```r
#woot <- rnorm(x=2, n=10, p = 0.5)
```


5.  One of my previous students, Joe Zackular, obtained stool samples from 89 people that underwent colonoscopies.  30 of these individuals had no signs of disease, 30 had non-cancerous ademonas, and 29 had cancer.  It was previously suggested that the bacterium *Fusobacterium nucleatum* was associated with cancer.  In these three pools of subjects, Joe determined that 4, 1, and 14 individuals harbored *F. nucleatum*, respectively. Create a matrix table to represent the number of individuals with and without _F. nucleatum_ as a function of disease state.  Then do the following:

    * Run the three tests of proportions you learned about in class using built in R  functions to the 2x2 study design where normals and adenomas are pooled and compared to carcinomas.
    * Without using the built in chi-squared test function, replicate the 2x2 study design in the last problem for the Chi-Squared Test...
      * Calculate the expected count matrix and calculate the Chi-Squared test statistics. Figure out how to get your test statistic to match Rs default statistic.
      *	Generate a Chi-Squared distributions with approporiate degrees of freedom by the method that was discussed in class (hint: you may consider using the `replicate` command)
      * Compare your Chi-Squared distributions to what you might get from the appropriate built in R functions
      * Based on your distribution calculate p-values
      * How does your p-value compare to what you saw using the built in functions? Explain your observations.


6\.  Get a bag of Skittles or M&Ms.  Are the candies evenly distributed amongst the different colors?  Justify your conclusion.

