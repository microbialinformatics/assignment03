# Assignment 3
Patrick D. Schloss  
September 26, 2014  

Complete the exercises listed below and submit as a pull request to the [Assignment 3 repository](http://www.github.com/microbialinformatics/assignment03).  Format this document appropriately using R markdown and knitr. For those cases where there are multiple outputs, make it clear in how you format the text and interweave the solution, what the solution is.

Your pull request should only include your *.Rmd and *.md files. You may work with a partner, but you must submit your own assignment and give credit to anyone that worked with you on the assignment and to any websites that you used along your way. You should not use any packages beyond the base R system and knitr.

This assignment is due on October 10th.

------

1.  Generate a plot that contains the different pch symbols. Investigate the knitr code chunk options to see whether you can have a pdf version of the image produced so you can print it off for your reference. It should look like this:

    <img src="pch.png", style="margin:0px auto;display:block" width="500">

```r
pchvalues <- 1:25
pdf('rplot1.pdf')
plot1 <- plot(x=1, y=1, pch= pchvalues[1], xlim = c(1,25), xlab = "PCH Values", main = "PCH Symbols", yaxt='n', ylab="")
i = 1
repeat
{
i = i +1 
points(x=i, y=1, pch= pchvalues[i])
if (i > 25)
break;
}
```

2.  Using the `germfree.nmds.axes` data file available in this repository, generate a plot that looks like this. The points are connected in the order they were sampled with the circle representing the beginning and the square the end of the time course:

    <img src="beta.png", style="margin:0px auto;display:block" width="700">
    

```r
germfree <- read.table(file="germfree.nmds.axes", header=T)
plot(x=germfree$axis1[1:20], y=germfree$axis2[1:20], type = "l", xlim = c(-0.2, 0.6), ylim = c(-0.4, 0.4), lwd = 2)
points(x=germfree$axis1[21:42], y=germfree$axis2[21:42], type = "l", col = "blue", lwd = 2)
points(x=germfree$axis1[42:63], y=germfree$axis2[42:63], type = "l", col = "red", lwd = 2)
points(x=germfree$axis1[63:84], y=germfree$axis2[63:84], type = "l", col = "green", lwd = 2)
points(x=germfree$axis1[84:105], y=germfree$axis2[84:105], type = "l", col = "brown", lwd = 2)
legend(x = 0.0, y = -0.2, legend = c("Mouse 337", "Mouse 343", "Mouse 361", "Mouse 387", "Mouse 389"), col = c("black","blue", "red", "green", "brown"), lty = 1, lwd = 2)
```

![plot of chunk unnamed-chunk-2](./README_files/figure-html/unnamed-chunk-2.png) 


3.  On pg. 57 there is a formula for the probability of making x observations after n trials when there is a probability p of the observation.  For this exercise, assume x=2, n=10, and p=0.5.  Using R, calculate the probability of x using this formula and the appropriate built in function. Compare it to the results we obtained in class when discussing the sex ratios of mice.


4.  On pg. 59 there is a formula for the probability of observing a value, x, when there is a mean, mu, and standard deviation, sigma.  For this exercise, assume x=10.3, mu=5, and sigma=3.  Using R, calculate the probability of x using this formula and the appropriate built in function


5.  One of my previous students, Joe Zackular, obtained stool samples from 89 people that underwent colonoscopies.  30 of these individuals had no signs of disease, 30 had non-cancerous ademonas, and 29 had cancer.  It was previously suggested that the bacterium *Fusobacterium nucleatum* was associated with cancer.  In these three pools of subjects, Joe determined that 4, 1, and 14 individuals harbored *F. nucleatum*, respectively. Create a matrix table to represent the number of individuals with and without _F. nucleatum_ as a function of disease state.  Then do the following:

    * Run the three tests of proportions you learned about in class using built in R  functions to the 2x2 study design where normals and adenomas are pooled and compared to carcinomas.
    * Without using the built in chi-squared test function, replicate the 2x2 study design in the last problem for the Chi-Squared Test...
      * Calculate the expected count matrix and calculate the Chi-Squared test statistics. Figure out how to get your test statistic to match Rs default statistic.
      *	Generate a Chi-Squared distributions with approporiate degrees of freedom by the method that was discussed in class (hint: you may consider using the `replicate` command)
      * Compare your Chi-Squared distributions to what you might get from the appropriate built in R functions
      * Based on your distribution calculate p-values
      * How does your p-value compare to what you saw using the built in functions? Explain your observations.


6\.  Get a bag of Skittles or M&Ms.  Are the candies evenly distributed amongst the different colors?  Justify your conclusion.

