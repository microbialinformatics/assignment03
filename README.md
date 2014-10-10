---
output: html_document
---
# Assignment 3
Edna Chiang

October 1, 2014  

Complete the exercises listed below and submit as a pull request to the [Assignment 3 repository](http://www.github.com/microbialinformatics/assignment03).  Format this document approapriately using R markdown and knitr. For those cases where there are multiple outputs, make it clear in how you format the text and interweave the solution, what the solution is.

Your pull request should only include your *.Rmd and *.md files. You may work with a partner, but you must submit your own assignment and give credit to anyone that worked with you on the assignment and to any websites that you used along your way. You should not use any packages beyond the base R system and knitr.

This assignment is due on October 10th.

------

1.  Generate a plot that contains the different pch symbols. Investigate the knitr code chunk options to see whether you can have a pdf version of the image produced so you can print it off for yoru reference. It should look like this:

    <img src="pch.png", style="margin:0px auto;display:block" width="500">
    

```r
x <- 1:25
y <- rep(1,25)
plot(x,y,pch=1:25, main="PCH Symbols", xlab="PCH Value", ylab="", axes=F)

#Add x-axis
axis(side=1,at=1:25)

#Add y-axis
axis(side=1, at=1:25, col="grey", label=F, tck=1)

#To save plot as pdf, click "Export" and "Save plot as PDF"


```


2.  Using the `germfree.nmds.axes` data file available in this respositry, generate a plot that looks like this. The points are connected in the order they were sampled with the circle representing the beginning and the square the end of the time course:

    <img src="beta.png", style="margin:0px auto;display:block" width="700">
    
    
    ```r
    germfree <- read.table(file="germfree.nmds.axes", header=T)
    plot(x=germfree$axis1, y=germfree$axis2, xlab="NMDS Axis 1", ylab="NMDS Axis 2", type="n")
    mousenum <- as.factor(germfree$mouse)
    germfree$mousenum <- mousenum
    
    #Plot mouse337
    mouse337 <- as.matrix(germfree[germfree$mousenum==337,])
    lines(x=mouse337[,3], y=mouse337[,4], col="black")
    points(x=mouse337[1,3], y=mouse337[1,4], col="black", pch=16)
    points(x=mouse337[20,3], y=mouse337[20,4], col="black", pch=15)
    
    #Plot mouse343
    mouse343 <- as.matrix(germfree[germfree$mousenum==343,])
    lines(x=mouse343[,3], y=mouse343[,4], col="blue")
    points(x=mouse343[1,3], y=mouse343[1,4], col="blue", pch=16)
    points(x=mouse343[20,3], y=mouse343[20,4], col="blue", pch=15)
    
    #Plot mouse361
    mouse361 <- as.matrix(germfree[germfree$mousenum==361,])
    lines(x=mouse361[,3], y=mouse361[,4], col="red")
    points(x=mouse361[1,3], y=mouse361[1,4], col="red", pch=16)
    points(x=mouse361[20,3], y=mouse361[20,4], col="red", pch=15)
    
    #Plot mouse387
    mouse387 <- as.matrix(germfree[germfree$mousenum==387,])
    lines(x=mouse387[,3], y=mouse387[,4], col="green")
    points(x=mouse387[1,3], y=mouse387[1,4], col="green", pch=16)
    points(x=mouse387[20,3], y=mouse387[20,4], col="green", pch=15)
    
    #Plot mouse389
    mouse389 <- as.matrix(germfree[germfree$mousenum==389,])
    lines(x=mouse389[,3], y=mouse389[,4], col="brown")
    points(x=mouse389[1,3], y=mouse389[1,4], col="brown", pch=16)
    points(x=mouse389[20,3], y=mouse389[20,4], col="brown", pch=15)
    
    #Add legend
    legend(x=c(0,0.2), y=c(-0.2,0), legend=c("Mouse 337", "Mouse 343", "Mouse 361", "Mouse 387", "Mouse 389"), col=c("black", "blue", "red", "green", "brown"), lwd=3)
    ```


3.  On pg. 57 there is a formula for the probability of making x observations after n trials when there is a probability p of the observation.  For this exercise, assume x=2, n=10, and p=0.5.  Using R, calculate the probability of x using this formula and the appropriate built in function. Compare it to the results we obtained in class when discussing the sex ratios of mice.pc


```r
x <- 2
n <- 10
p <- 0.5

choose(n,x) * p^x * (1-p)^(n-x)

#OR

dbinom(2,10,0.5)
```


**Answer:** The probability is 0.0439




4.  On pg. 59 there is a formula for the probability of observing a value, x, when there is a mean, mu, and standard deviation, sigma.  For this exercise, assume x=10.3, mu=5, and sigma=3.  Using R, calculate the probability of x using this formula and the appropriate built in function


```r
x <- 10.3
m <- 5
sd <- 3

(1/((sqrt(2*3.14159))*sd)) * exp(-((x-m)^2)/(2*(sd^2)))

#OR

dnorm(x,m,sd)
```


**Answer:** The probability is 0.0279


5.  One of my previous students, Joe Zackular, obtained stool samples from 89 people that underwent colonoscopies.  30 of these individuals had no signs of disease, 30 had non-cancerous ademonas, and 29 had cancer.  It was previously suggested that the bacterium *Fusobacterium nucleatum* was associated with cancer.  In these three pools of subjects, Joe determined that 4, 1, and 14 individuals harbored *F. nucleatum*, respectively. Create a matrix table to represent the number of individuals with and without _F. nucleatum_ as a function of disease state.  Then do the following:

**Answer:**

```r
Fnuc <- matrix(c(26,29,15,4,1,14), nrow=2, ncol=3,byrow=T)
colnames(Fnuc)<-c("Healthy", "Benign", "Cancer")
rownames(Fnuc)<-c("No F. nucleatum", "F.nucleatum")
```


```r
                Healthy Benign Cancer
No F. nucleatum      26     29     15
F.nucleatum           4      1     14
```


    * Run the three tests of proportions you learned about in class using built in R  functions to the 2x2 study design where normals and adenomas are pooled and compared to carcinomas.
    
```r
    #Make pooled matrix
    pooled.Fnuc <- matrix(c(55, 15, 5, 14), nrow=2,ncol=2)
    colnames(pooled.Fnuc)<-c("No Cancer", "Cancer")
    rownames(pooled.Fnuc) <- c("No F. nucleatum", "F. nucleatum")
```
    
    
```r
                    No Cancer Cancer
No F. nucleatum        55      5
F. nucleatum           15     14
```


**Answer: Test of Proportions**

```r
prop.test.pooled.Fnuc <- prop.test(pooled.Fnuc)
prop.test.pooled.Fnuc
  
  2-sample test for equality of proportions with continuity
	correction

data:  pooled.Fnuc
X-squared = 16.2736, df = 1, p-value = 5.482e-05
alternative hypothesis: two.sided
95 percent confidence interval:
 0.1789983 0.6198522
sample estimates:
   prop 1    prop 2 
0.9166667 0.5172414 
```
    
    
**Answer: Fisher's Test**
```r
fisher.test.pooled.Fnuc <- fisher.test(pooled.Fnuc)
fisher.test.pooled.Fnuc
    
    Fisher's Exact Test for Count Data

data:  pooled.Fnuc
p-value = 4.094e-05
alternative hypothesis: true odds ratio is not equal to 1
95 percent confidence interval:
  2.831846 41.154868
sample estimates:
odds ratio 
  9.926223 
```
  
  
**Answer:  χ² Test**
```r
chi.test.pooled.Fnuc <- chisq.test(pooled.Fnuc)
chi.test.pooled.Fnuc

  Pearson's Chi-squared test with Yates' continuity correction

data:  pooled.Fnuc
X-squared = 16.2736, df = 1, p-value = 5.482e-05
```
   
   
    * Without using the built in chi-squared test function, replicate the 2x2 study design in the last problem for the Chi-Squared Test...
      * Calculate the expected count matrix and calculate the Chi-Squared test statistics. Figure out how to get your test statistic to match Rs default statistic.
      
      
**Answer:**
```r
      #Fnuc or No Fnuc
      sum.pooled.Fnuc <- margin.table(pooled.Fnuc,1)
      sum.pooled.Fnuc
      No F. nucleatum    F. nucleatum 
             60              29 
       
       #Calculate proportion of Fnuc/NoFnuc
      frac.Fnuc <- sum.pooled.Fnuc["F. nucleatum"]/sum(sum.pooled.Fnuc)
      frac.noFnuc <- 1 - frac.Fnuc
      frac.bac <- c(No=frac.noFnuc, Yes=frac.Fnuc)
       frac.bac
 No.F. nucleatum Yes.F. nucleatum 
       0.6741573        0.3258427 
       
       #Cancer or no cancer
       cancer.sums <- margin.table(pooled.Fnuc,2)
       cancer.sums
       No Cancer    Cancer 
       70        19 
       
       #Calculate proportion of Cancer/NoCancer
       frac.cancer <- cancer.sums["Cancer"]/sum(cancer.sums)
       frac.nocancer<-1-frac.cancer
       frac.can <- c(N = frac.nocancer, Y=frac.cancer)
       frac.can
       N.Cancer  Y.Cancer 
      0.7865169 0.2134831
      
      #Calculate Expected
      expected <- frac.bac %*% t(frac.can)
      expected <- expected * sum(pooled.Fnuc)
      expected
           N.Cancer  Y.Cancer
      [1,] 47.19101 12.808989
      [2,] 22.80899  6.191011
      
      #Generate Chi-squared statistics
      chi.sq <- sum((expected - pooled.Fnuc)^2/expected)
      chi.sq
      [1] 18.57628
      #Does not match with Chi-squared statistics generated by R function, which is 16.2736.
      
      #The Chi-squared R function includes Yates' continuity correction
      
      #Calculate Chi-squared, including Yates' continuity correction
      chisq<- sum((((abs(expected-pooled.Fnuc))-0.5)^2)/expected)
      chisq
      [1] 16.2736
      #This matches the R-generated Chi-squared statistic generated.
```
      
      
      *	Generate a Chi-Squared distributions with approporiate degrees of freedom by the method that was discussed in class (hint: you may consider using the `replicate` command)
      
      
**Answer:**
```r
      #Calculate df
      df <- (nrow(pooled.Fnuc) - 1) * (ncol(pooled.Fnuc) - 1)
      df
      [1] 1
      #df = k
      
      #Draw k variables from a normal distribution
      dist <- replicate(1000, sum((rnorm(1,0,1))^2))
      
      #Calculate proportion of distribution > Chi-squared
      dist.Xsq <- (dist > 16.2736)
      sum(dist.Xsq==TRUE)
      [1] 0
      #0 of the distribution is larger than Chi-squared (16.2736)
      
      hist(dist,breaks=500)
```
      
      
      * Compare your Chi-Squared distributions to what you might get from the appropriate built in R functions
      
**Answer:**
```r
      plot(seq(0, 20, 0.05), dchisq(seq(0, 20, 0.05), df = df), type = "l", xlab = "ChiSquared Statistic", ylab = "Probability with 1 degree of freedom")
      arrows(x0 = chisq, x1 = chisq, y0 = 0.4, y1 = 0.05, lwd = 2, col = "red")
```
My  χ² distribution looks quite similar to the R-generated distribution. Both exponentially decrease as the x-axis value increases. My distribution begins to level out when X = 2, whereas the R-generated distribution begins to level out when X = 4. However, whereas my distribution is discrete, the R-generated distribution is continuous.
      
      
      * Based on your distribution calculate p-values
      
**Answer:** p-value=0. The p-value is the probability that the  χ² distribution is larger than my  χ² Statistic. In regards to my distribution, the p-value is equivalent to the integral of the graph when dist > X, or dist > 16.2736. Because my distribution has 0 values which are larger than my  χ² Statistic, my p-value is 0.
      
      
      * How does your p-value compare to what you saw using the built in functions? Explain your observations.
      
      
**Answer:** My p-value (0) is smaller than the R-generated p-value (5.482e-05). The two are not equal because my  χ² distribution is not equivalent to the R-generated distribution. My distribution is created from 1000 replicates & is discrete, whereas the R-generated  χ² distribution is continuous.


6.  Get a bag of Skittles or M&Ms.  Are the candies evenly distributed amongst the different colors?  Justify your conclusion.


```r
#Make matrix of M&M colors
mm <- matrix(c(2,7,5,1,3,2), nrow=1)
colnames(mm) <- c("Red", "Orange", "Yellow", "Green", "Blue", "Brown")

#Proportion of colors
prop.mm <- prop.table(mm)
prop.mm

     Red Orange Yellow Green Blue Brown
[1,] 0.1   0.35   0.25  0.05 0.15   0.1

#Expected proportion if evenly distributed
2+7+5+1+3+2
[1] 20
a <- 20/6
a
[1] 3.333333
a/20
[1] 0.1666667

#Prepare for prop.test
count <- c(2,7,5,1,3,2)
trials <- rep(20,6)
exp <- rep(0.1666667,6)

#What is the probability that the proportion of M&M colors is the same?
#H0 = M&M colors are evenly distributed
prop.test(count, trials, exp)

  6-sample test for given proportions without continuity
	correction

data:  count out of trials, null probabilities exp
X-squared = 9.12, df = 6, p-value = 0.1669
alternative hypothesis: two.sided
null values:
   prop 1    prop 2    prop 3    prop 4    prop 5    prop 6 
0.1666667 0.1666667 0.1666667 0.1666667 0.1666667 0.1666667 
sample estimates:
prop 1 prop 2 prop 3 prop 4 prop 5 prop 6 
  0.10   0.35   0.25   0.05   0.15   0.10 

Warning message:
In prop.test(count, trials, exp) :
  Chi-squared approximation may be incorrect
```

**Answer:** The p-value is 0.1669, so I fail to reject the statement that M&M's colors are evenly distributed. The results are not statistically significant at the level 0.05.
