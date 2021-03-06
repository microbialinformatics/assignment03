# Assignment 3
Patrick D. Schloss  
September 26, 2014  

Complete the exercises listed below and submit as a pull request to the [Assignment 3 repository](http://www.github.com/microbialinformatics/assignment03).  Format this document approapriately using R markdown and knitr. For those cases where there are multiple outputs, make it clear in how you format the text and interweave the solution, what the solution is.

Your pull request should only include your *.Rmd and *.md files. You may work with a partner, but you must submit your own assignment and give credit to anyone that worked with you on the assignment and to any websites that you used along your way. You should not use any packages beyond the base R system and knitr.

This assignment is due on October 10th.

------

1.  Generate a plot that contains the different pch symbols. Investigate the knitr code chunk options to see whether you can have a pdf version of the image produced so you can print it off for yoru reference. It should look like this:

    <img src="pch.png", style="margin:0px auto;display:block" width="500">


```r
x<-1:25
y<-rep(1, 25)
plot(c(1,25), c(0,2), type="n", main="PCH Symbols", xlab="PCH value", ylab="", axes=F)
abline(v=x, col="gray")
points(x,y, pch=x, cex=2)
axis(1, label=1:25, at=1:25)
```

<img src="./figures/pch.diagram-1.png" title="" alt="" style="display: block; margin: auto;" />

2.  Using the `germfree.nmds.axes` data file available in this respositry, generate a plot that looks like this. The points are connected in the order they were sampled with the circle representing the beginning ad the square the end of the time course:

    <img src="beta.png", style="margin:0px auto;display:block" width="700">


```r
a<-read.table(file="germfree.nmds.axes", header=T)
animal <- factor(a$mouse)
day <- a$day
clr <- c("337" = "black", "343" = "blue", "361" = "red", "387" = "green", "389" = "brown")

par(mar=c(5, 4, 1, 1))
plot(c(min(a$axis1), max(a$axis1)), c(min(a$axis2), max(a$axis2)), type="n", xlab="NMDS Axis 1", ylab="NMDS Axis 2")
for(i in levels(animal)){
	z <- animal == i
	points(a[z,"axis2"]~a[z,"axis1"], type="l", col=clr[i], lwd=3)
}
z <- day == 1
points(a[z,"axis2"]~a[z,"axis1"], col=clr, pch=19, cex=2)
z <- day == 21 | (animal=="337" & day == 20)
points(a[z,"axis2"]~a[z,"axis1"], col=clr, pch=15, cex=2)

legend(x=0, y=-0.2, legend=paste("Mouse", levels(animal)), col=clr[levels(animal)], lwd=4)
```

<img src="./figures/beta.diversity-1.png" title="" alt="" style="display: block; margin: auto;" />

3.  On pg. 57 there is a formula for the probability of making x observations after n trials when there is a probability p of the observation.  For this exercise, assume x=2, n=10, and p=0.5.  Using R, calculate the probability of x using this formula and the appropriate built in function. Compare it to the results we obtained in class when discussing the sex ratios of mice.


```r
n <- 10
x <- 2
p <- 0.5

prob.formula <- choose(k=x, n=n) * p^x * (1-p)^(n-x)
prob.function <- dbinom(x=x, size=n, prob=p)
```

When we use the forumla the probability of getting 2 males out of 10 total pups assuming a 1:1 sex ratio is 0.0439453. This is identical to what we see using the built-in `dbinom` R function: 0.0439453.


4.  On pg. 59 there is a formula for the probability of observing a value, x, when there is a mean, mu, and standard deviation, sigma.  For this exercise, assume x=10.3, mu=5, and sigma=3.  Using R, calculate the probability of x using this formula and the appropriate built in function


```r
sigma <- 3
mu <- 5
x <- 10.3

prob.formula <- (1/(sqrt(2*pi)*sigma)) * exp(-(x-mu)^2/(2*sigma*sigma))
prob.function <- dnorm(x=x, mean=mu, sd=sigma)
```
When we use the forumla the probability of getting a value of 10.3 assuming it came from a distribution with a mean of 5 and a standard deviation of 3 is 0.0279285. This is identical to what we see using the built-in `dnorm` R function: 0.0279285.



5.  One of my previous students, Joe Zackular, obtained stool samples from 89 people that underwent colonoscopies.  30 of these individuals had no signs of disease, 30 had non-cancerous ademonas, and 29 had cancer.  It was previously suggested that the bacterium *Fusobacterium nucleatum* was associated with cancer.  In these three pools of subjects, Joe determined that 4, 1, and 14 individuals harbored *F. nucleatum*, respectively. Create a matrix table to represent the number of individuals with and without _F. nucleatum_ as a function of disease state. 


```r
data <- matrix(c(4, 1, 14, 25, 29, 15), nrow=2, byrow=T)
rownames(data) <- c("positive", "negative")
colnames(data) <- c("normal", "adenoma", "carcinoma")
```


Then do the following:

* Run the three tests of proportions you learned about in class using built in R  functions to the 2x2 study design where normals and adenomas are pooled and compared to carcinomas.
    

```r
not.cancer <- data[,"normal"] + data[,"adenoma"]
cancer <- data[,"carcinoma"]

prop.test.result <- prop.test(not.cancer, not.cancer+cancer)
chisq.test.result <- chisq.test(rbind(not.cancer, cancer))
fisher.test.result <- fisher.test(rbind(not.cancer, cancer))
```

The P-values for the test of proportion, Chi-Squared test, and Fisher exact test were 6.6120601\times 10^{-5}, 6.6120601\times 10^{-5}, and 4.7795921\times 10^{-5}, respectively.



* Without using the built in chi-squared test function, replicate the 2x2 study design in the last problem for the Chi-Squared Test...
  * Calculate the expected count matrix and calculate the Chi-Squared test statistics. Figure out how to get your test statistic to match Rs default statistic.
 

```r
observed <- rbind(not.cancer, cancer)
n.total <- sum(observed)
r.sum <- apply(observed, 1, sum)/n.total
c.sum <- apply(observed, 2, sum)/n.total
expected <- (r.sum %*% t(c.sum)) * n.total

chi.sq.formula <- sum( (observed - expected)^2 / expected)
chi.sq.function <- chisq.test(rbind(not.cancer, cancer))$statistic
chi.sq.function.nocor <-  chisq.test(rbind(not.cancer, cancer), correct=F)$statistic
```

Using the function we get 18.1938326 while we get 15.9187454 when we use the built in chisq.test funciton. If we use `correct=F` then we get 18.1938326 with the built in function.


  *	Generate a Chi-Squared distributions with approporiate degrees of freedom by the method that was discussed in class (hint: you may consider using the `replicate` command)
  

```r
iterations <- 1e7
dist <- rnorm(iterations, 0, 1)^2
```
  
  * Compare your Chi-Squared distributions to what you might get from the appropriate built in R functions
  

```r
h <- hist(dist, breaks=500, plot=F)
plot(h$density~h$mids, type="l", col="red", xlab="Statistic value", ylab="Density")
points(dchisq(h$breaks, df=1)~h$breaks, type="l", col="blue")
legend(x=15, y=3.0, legend=c("Empirical", "Formula"), lty=1, lwd=2, col=c("red", "blue"))
```

<img src="./figures/distributions-1.png" title="" alt="" style="display: block; margin: auto;" />

They look very close!


  * Based on your distribution calculate p-values


```r
p.empirical <- sum(dist > chi.sq.formula)/iterations
```
My P-value was 1.93\times 10^{-5}.

* How does your p-value compare to what you saw using the built in functions? Explain your observations.

Very close!


6\.  Get a bag of Skittles or M&Ms.  Are the candies evenly distributed amongst the different colors?  Justify your conclusion.


```r
my.bag <- c("red" = 9, "purple"=8, "green"=6, "yellow"=5, "orange"=3)
n.candies <- sum(my.bag)
n.colors <- length(my.bag)
even.distro <- rep(n.candies / n.colors, n.colors)
skittle.test <- chisq.test(rbind(my.bag, even.distro))
```

```
## Warning in chisq.test(rbind(my.bag, even.distro)): Chi-squared
## approximation may be incorrect
```

The distribution of colors I observed was not significantly different from what you'd expect if they were evenly distributed (P=0.74)
