# Assignment 3
Patrick D. Schloss  
September 26, 2014  

Complete the exercises listed below and submit as a pull request to the [Assignment 3 repository](http://www.github.com/microbialinformatics/assignment03).  Format this document approapriately using R markdown and knitr. For those cases where there are multiple outputs, make it clear in how you format the text and interweave the solution, what the solution is.

Your pull request should only include your *.Rmd and *.md files. You may work with a partner, but you must submit your own assignment and give credit to anyone that worked with you on the assignment and to any websites that you used along your way. You should not use any packages beyond the base R system and knitr.

This assignment is due on October 10th.

------

1.  Generate a plot that contains the different pch symbols. Investigate the knitr code chunk options to see whether you can have a pdf version of the image produced so you can print it off for yoru reference. It should look like this:

    <img src="pch.png", style="margin:0px auto;display:block" width="500">
    
Here is my plot!
    

```r
plot(y=seq(from=0.5, to=1.5, by = 1/24), x=1:25, type="n", xlab="PCH value", ylab="", main="PCH Symbols", frame.plot=F, yaxt="n", xaxt="n")
axis(1, tick=T, at=1:25)
segments(x0=1:25, x1=1:25, y0=0, y1=2, col="grey")
points(y=rep(1, 25), x=1:25, pch=1:25,cex=2)
```

![plot of chunk unnamed-chunk-1](./README_files/figure-html/unnamed-chunk-1.png) 


2.  Using the `germfree.nmds.axes` data file available in this respositry, generate a plot that looks like this. The points are connected in the order they were sampled with the circle representing the beginning ad the square the end of the time course:

    <img src="beta.png", style="margin:0px auto;display:block" width="700">
    
Another plot!


```r
germ.free <- read.table(file="germfree.nmds.axes", header=T)

plot(x=c(min(germ.free$axis1), max(germ.free$axis1)), y=c(min(germ.free$axis2), max(germ.free$axis2)), type="n", xlab = "NMDS Axis 1", ylab= "NMDS Axis 2")

#Mouse 337
points(x=germ.free[germ.free$mouse==337 & germ.free$day==1,][3], y=germ.free[germ.free$mouse==337 & germ.free$day==1,][4], pch=16, col="black")

points(x=germ.free[germ.free$mouse==337 & germ.free$day==20,][3], y=germ.free[germ.free$mouse==337 & germ.free$day==20,][4], pch=15, col="black")

mouse337 <- as.matrix(germ.free[germ.free$mouse==337,])
lines(x=mouse337[,3], y=mouse337[,4], col="black", lwd=2)

#Mouse 343
points(x=germ.free[germ.free$mouse==343 & germ.free$day==1,][3], y=germ.free[germ.free$mouse==343 & germ.free$day==1,][4], pch=16, col="blue")

points(x=germ.free[germ.free$mouse==343 & germ.free$day==20,][3], y=germ.free[germ.free$mouse==343 & germ.free$day==20,][4], pch=15, col="blue")

mouse343 <- as.matrix(germ.free[germ.free$mouse==343,])
lines(x=mouse343[,3], y=mouse343[,4], col="blue", lwd=2)

#Mouse 361
points(x=germ.free[germ.free$mouse==361 & germ.free$day==1,][3], y=germ.free[germ.free$mouse==361 & germ.free$day==1,][4], pch=16, col="red")

points(x=germ.free[germ.free$mouse==361 & germ.free$day==20,][3], y=germ.free[germ.free$mouse==361 & germ.free$day==20,][4], pch=15, col="red")

mouse361 <- as.matrix(germ.free[germ.free$mouse==361,])
lines(x=mouse361[,3], y=mouse361[,4], col="red", lwd=2)

#Mouse 387
points(x=germ.free[germ.free$mouse==387 & germ.free$day==1,][3], y=germ.free[germ.free$mouse==387 & germ.free$day==1,][4], pch=16, col="green")

points(x=germ.free[germ.free$mouse==387 & germ.free$day==20,][3], y=germ.free[germ.free$mouse==387 & germ.free$day==20,][4], pch=15, col="green")

mouse387 <- as.matrix(germ.free[germ.free$mouse==387,])
lines(x=mouse387[,3], y=mouse387[,4], col="green", lwd=2)

#Mouse 389
points(x=germ.free[germ.free$mouse==389 & germ.free$day==1,][3], y=germ.free[germ.free$mouse==389 & germ.free$day==1,][4], pch=16, col="dark red")

points(x=germ.free[germ.free$mouse==389 & germ.free$day==20,][3], y=germ.free[germ.free$mouse==389 & germ.free$day==20,][4], pch=15, col="dark red")

mouse389 <- as.matrix(germ.free[germ.free$mouse==389,])
lines(x=mouse389[,3], y=mouse389[,4], col="dark red", lwd=2)

legend(x=0, y=-0.2, legend=c("Mouse 337", "Mouse 343","Mouse 361", "Mouse 387", "Mouse 389"), col=c("black", "blue", "red", "green", "dark red"), lty=1, lwd=2)
```

![plot of chunk unnamed-chunk-2](./README_files/figure-html/unnamed-chunk-2.png) 



3.  On pg. 57 there is a formula for the probability of making x observations after n trials when there is a probability p of the observation.  For this exercise, assume x=2, n=10, and p=0.5.  Using R, calculate the probability of x using this formula and the appropriate built in function. Compare it to the results we obtained in class when discussing the sex ratios of mice.

```r
pval.binom.formula <- choose(10,2)*(0.5)^2*(1-0.5)^8

pval.binom.builtin <- dbinom(2, 10, 0.5)
```

This returns the same p value we got in class for the probability of getting 2 males out of a litter of 10 pups when the sex ratios are equal - as it should.

4.  On pg. 59 there is a formula for the probability of observing a value, x, when there is a mean, mu, and standard deviation, sigma.  For this exercise, assume x=10.3, mu=5, and sigma=3.  Using R, calculate the probability of x using this formula and the appropriate built in function.


```r
pval.normal.formula <- (1/(3*sqrt(2*pi)))*exp((-(10.3-5)^2)/(2*9))

pval.normal.builtin <- dnorm(10.3, 5, 3)
```

The probability is 0.0279 from the function I wrote, and 0.0279 for the built in formula.

5.  One of my previous students, Joe Zackular, obtained stool samples from 89 people that underwent colonoscopies.  30 of these individuals had no signs of disease, 30 had non-cancerous ademonas, and 29 had cancer.  It was previously suggested that the bacterium *Fusobacterium nucleatum* was associated with cancer.  In these three pools of subjects, Joe determined that 4, 1, and 14 individuals harbored *F. nucleatum*, respectively. Create a matrix table to represent the number of individuals with and without _F. nucleatum_ as a function of disease state.  Then do the following:


```r
fnuc <- matrix(c(26, 4, 29, 1, 15, 14), nrow=3, ncol=2, byrow=TRUE)

rownames(fnuc)=c("healthy", "adenoma", "cancer")
colnames(fnuc)=c("no F.nuc", "F.nuc")
```

I made a 3x2 matrix of disease state by F. nucleatum presence.

    * Run the three tests of proportions you learned about in class using built in R  functions to the 2x2 study design where normals and adenomas are pooled and compared to carcinomas.
    

```r
fnuc.pooled <- matrix(c(55, 5, 15, 14), nrow=2, ncol=2, byrow=TRUE)
rownames(fnuc.pooled)=c("healthy", "cancer")
colnames(fnuc.pooled)=c("no F.nuc", "F.nuc")

fnuc.chi1 <- chisq.test(fnuc.pooled)

fnuc.fisher <- fisher.test(fnuc.pooled)

infected <- fnuc.pooled[,2]
fnuc.sums <- colSums(fnuc.pooled)
fnuc.prop <- prop.test(infected, fnuc.sums)
```

```
## Warning: Chi-squared approximation may be incorrect
```
  
  I got a probability of 5.4822 &times; 10<sup>-5</sup> that cancer rates are proportionally equal between F. nucleatum-infected and non-infected individuals from the builtin chi-squared test. I got a probability of 4.0941 &times; 10<sup>-5</sup> for the same comparison from the built in Fisher test. I summed the columns of my pooled F. nucleatus x cancer matrix to get the total number of people infected with the bacterium and the number not infected. I then took the number of infected people that were healthy (5), and the number with cancer (14), and used a test of proportions to test the hypothesis that F. nucleatus infection is random with respect to cancer status. The test of proportions rejected the null hypothesis with p-value 2.494 &times; 10<sup>-9</sup>.
  
   * Without using the built in chi-squared test function, replicate the 2x2 study design in the last problem for the Chi-Squared Test...
    
      * Calculate the expected count matrix and calculate the Chi-Squared test statistics. Figure out how to get your test statistic to match Rs default statistic.
      

```r
cancer.sums <- rowSums(fnuc.pooled)

frac.infected <- fnuc.sums["F.nuc"]/sum(fnuc.sums)
frac.no.inf <- 1 - frac.infected
frac.inf <- c(frac.no.inf,frac.infected)
names(frac.inf) <- c("N", "I")

frac.cancer <- cancer.sums["cancer"]/sum(cancer.sums)
frac.no.cancer <- 1 - frac.cancer
frac.canc <- c(frac.no.cancer,frac.cancer)
names(frac.canc) <- c("No", "Yes")

expected <- frac.canc %*% t(frac.inf)
expected <- expected * sum(fnuc.pooled)

chi.sq <- sum((fnuc.pooled-expected)^2/expected)
```

I have not managed to get it matching. I keep getting 18.5763 rather than 5.4822 &times; 10<sup>-5</sup>.

      *	Generate a Chi-Squared distributions with approporiate degrees of freedom by the method that was discussed in class (hint: you may consider using the `replicate` command)
      

```r
chi.samp <- replicate(1000000, rnorm(1, 0, 1)^2)
chi.hist <- hist(chi.samp, breaks=2000)
```

![plot of chunk unnamed-chunk-8](./README_files/figure-html/unnamed-chunk-8.png) 

  
      * Compare your Chi-Squared distributions to what you might get from the appropriate built in R functions


```r
chi.sq <- sum((expected - fnuc.pooled)^2/expected)
df <- (nrow(fnuc.pooled) - 1) * (ncol(fnuc.pooled) - 1)
plot(seq(0, 20, 0.05), dchisq(seq(0, 20, 0.05), df = df), type = "l", xlab = "ChiSquared Statistic", 
    ylab = "Probability with 1 degree of freedom")
arrows(x0 = chi.sq, x1 = chi.sq, y0 = 0.4, y1 = 0.05, lwd = 2, col = "red")
lines(x=seq(from=0, to=20, by=20/(length(chi.hist$density)-1)), y=chi.hist$density, col="red")
```

![plot of chunk unnamed-chunk-9](./README_files/figure-html/unnamed-chunk-9.png) 

My chi-squared distribution does not quite match up, especially in the 2-5 chi-square statistic range. It is also not completely smooth, because it is sampled from a distribution and there is stochasticity in the sampling process.  

      * Based on your distribution calculate p-values
      

```r
chimat <- cbind(x=seq(from=0, to=20, by=20/(length(chi.hist$density)-1)), y=chi.hist$density)
chimat.p <- chimat[chimat[,1]>chi.sq,]
pval <- sum(chimat.p[,2])/sum(chimat)
```
      * How does your p-value compare to what you saw using the built in functions? Explain your observations.


```r
chisq.builtin <- chisq.test(fnuc.pooled)
```

My chi-square p-value is less than the p-value from the built in command. This is likely because I calculated my p-value by summing all of the observations from my chi-squared distribution that were greater than my chi-squared statistic, and dividing them by the sum of the entire distribution. My chi-squared statistic is larger than the one generated by the built in function, so my p-value should be less. Another possibility is that even though I constructed my chi-squared distribution from 1,000,000
samples, the chi-square statistic is still so extreme that the sampling in that area is sparse relative to the theoretical distribution.

6\.  Get a bag of Skittles or M&Ms.  Are the candies evenly distributed amongst the different colors?  Justify your conclusion.

```r
colors <- c("red","orange", "yellow", "green", "blue", "brown")
numbers <- c(13,17,23,17, 14, 13)
test <- rep(sum(numbers), length(numbers))

prop.test(numbers, test, rep(1/length(numbers), length(numbers)))
```

```
## 
## 	6-sample test for given proportions without continuity correction
## 
## data:  numbers out of test, null probabilities rep(1/length(numbers), length(numbers))
## X-squared = 5.406, df = 6, p-value = 0.4929
## alternative hypothesis: two.sided
## null values:
## prop 1 prop 2 prop 3 prop 4 prop 5 prop 6 
## 0.1667 0.1667 0.1667 0.1667 0.1667 0.1667 
## sample estimates:
## prop 1 prop 2 prop 3 prop 4 prop 5 prop 6 
## 0.1340 0.1753 0.2371 0.1753 0.1443 0.1340
```

The test of proportions does not reject the null hypothesis that the M&M's are drawn from a population with equal representation of each color.
