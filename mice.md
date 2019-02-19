Mice
================

The purpose of this problem is to build intuition for the bootstrap
procedure. With that in mind, consider the very small data set of the
weights of three mice that came from the same litter. The weights are
82, 107 and 93 grams.

``` r
weights <- c(82, 107, 93)
```

  - What is the mean weight of the three mice?
  - How many possible bootstrap samples are there from this sample of
    three mice?
  - List all possible bootstrap samples and compute the mean of each.
  - Compute the mean of the bootstrap means. How does this compare with
    the mean from part (a)?
  - Calculate a percentile-based bootstrap confidence interval with
    level of confidence at least 95%. What information does this
    interval provide? How confident are you in reporting this interval?
    Explain.

<!-- end list -->

``` r
mean(weights)
```

    ## [1] 94

The mean weight of the three mice is 94.

``` r
samps <- expand.grid(weights, weights, weights)

nrow(samps)
```

    ## [1] 27

There are 27 possible bootstrap samples.

``` r
samps$Mean <- rowMeans(samps)

samps
```

    ##    Var1 Var2 Var3      Mean
    ## 1    82   82   82  82.00000
    ## 2   107   82   82  90.33333
    ## 3    93   82   82  85.66667
    ## 4    82  107   82  90.33333
    ## 5   107  107   82  98.66667
    ## 6    93  107   82  94.00000
    ## 7    82   93   82  85.66667
    ## 8   107   93   82  94.00000
    ## 9    93   93   82  89.33333
    ## 10   82   82  107  90.33333
    ## 11  107   82  107  98.66667
    ## 12   93   82  107  94.00000
    ## 13   82  107  107  98.66667
    ## 14  107  107  107 107.00000
    ## 15   93  107  107 102.33333
    ## 16   82   93  107  94.00000
    ## 17  107   93  107 102.33333
    ## 18   93   93  107  97.66667
    ## 19   82   82   93  85.66667
    ## 20  107   82   93  94.00000
    ## 21   93   82   93  89.33333
    ## 22   82  107   93  94.00000
    ## 23  107  107   93 102.33333
    ## 24   93  107   93  97.66667
    ## 25   82   93   93  89.33333
    ## 26  107   93   93  97.66667
    ## 27   93   93   93  93.00000

``` r
mean(samps$Mean)
```

    ## [1] 94

The mean of all the possible bootstrap samples is the same as the mean
for the three mice (94).

``` r
quantile(samps$Mean, probs = c(0.025, 0.975))
```

    ##      2.5%     97.5% 
    ##  84.38333 103.96667

This interval provides a 95% confidence interval on the average weight
of the mice population that these mice were taken from (assuming it is a
representative sample). However, since the sample size is so small, I’m
not very confident in reporting this interval.
