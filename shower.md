Shower
================

You think that your roommate takes showers whose duration is different
from yours. Your roommate disagrees but, instead of arguing, you both
decide to keep track of the time it takes both of you to shower for
fourteen days and then to employ skills from an introductory statistics
class (e.g., STAT 121) to create a confidence interval on the population
mean showering time of your roommate minus the population mean showering
time of you. The data and code to compute a 90% confidence interval are
below.

``` r
rm <- c(6,6.25,5.75,6.5,6,15,35,20,4,5.25,5.75)

you <- c(3.5,5.5,4,4,4,6,11,12,3,4,4.25,7,3.25)

t.test(rm, you, conf.level = 0.9)
```

    ## 
    ##  Welch Two Sample t-test
    ## 
    ## data:  rm and you
    ## t = 1.6826, df = 11.582, p-value = 0.1192
    ## alternative hypothesis: true difference in means is not equal to 0
    ## 90 percent confidence interval:
    ##  -0.3122975 10.3122975
    ## sample estimates:
    ## mean of x mean of y 
    ##      10.5       5.5

Notice that the confidence interval contains 0 and, therefore, your
roommate concludes that there is no significant difference in the time
it takes you both to take a shower. But it might be inappropriate to use
this confidence interval on the difference in means because the data are
not normally distributed and the sample sizes are small.

  - Use the bootstrap procedure to compute a 90% confidence interval on
    the difference in these means. Based on this bootstrap confidence
    interval, what conclusion do you make at the 0.10 level of
    significance?

For 10,000 repititions, calculate the difference between the mean shower
length of your roommate and yourself from bootstrapped samples of shower
time.

``` r
diff_means <- replicate(10000, mean(sample(rm, replace = TRUE)) - mean(sample(you, replace = TRUE)))
```

Calculate the 90% confidence interval for the difference in means.

``` r
quantile(diff_means, probs = c(0.05, 0.95))
```

    ##         5%        95% 
    ##  0.8215035 10.0385490

At the 10% level of significance, I conclude that my roommate takes
longer showers than I do since the 90% confidence interval does not
contain zero and is positive.
