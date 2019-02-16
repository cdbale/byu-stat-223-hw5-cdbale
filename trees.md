Trees
================

In the trees dataset found in R, there are three variables “Girth”
“Height” and “Volume”. There is interest in using “Girth” and “Height”
(two noninvasive measures) to predict “Volume”. Carrying out this
prediction can be done using a regression model with two explanatory
variables (“Height” and “Girth”).

Principal interest lies in estimating the regression coefficient of
“Height” divided by the regression coefficient for “Girth”. Obtaining
an estimate of the ratio is easy — just compute the ratio of the two
slope estimates — but assessing uncertainty associated with the point
estimate can be difficult theoretically (although methods do exist).

  - For this problem construct a 95% confidence interval using the
    bootstrap procedure. Use 5,000 bootstrap samples. Compute your
    estimate and confidence bounds.

-----

Let’s take a look at the trees dataset.

``` r
head(trees)
```

    ##   Girth Height Volume
    ## 1   8.3     70   10.3
    ## 2   8.6     65   10.3
    ## 3   8.8     63   10.2
    ## 4  10.5     72   16.4
    ## 5  10.7     81   18.8
    ## 6  10.8     83   19.7

Create a function ‘tree\_bs’ which calculates a bootstrap sample from
the ‘trees’ data, runs the regression of ‘Volume’ on ‘Girth’ and
‘Height’, and calculates the ratio of the ‘Height’ coefficient to
the ‘Girth’ coefficient.

``` r
tree_bs <- function() {
  
  bs_sample <- trees[sample(nrow(trees), nrow(trees), replace = TRUE),]

  mdl <- lm(Volume ~ Girth + Height, data = bs_sample)

  girth_coeff <- summary(mdl)$coefficients[2, 1]
  height_coeff <- summary(mdl)$coefficients[3, 1]

  return(height_coeff / girth_coeff)
  
}
```

Run the ‘tree\_bs’ function 5000 times to create 5000 estimates of the
ratio calculated using the bootstrap procedure. Calculate an estimate of
the mean ratios from the bootstrapped ratios and a 95% confidence
interval around that mean ratio.

``` r
bs_coeffs <- replicate(5000, tree_bs())

mean(bs_coeffs)
```

    ## [1] 0.07278684

``` r
quantile(bs_coeffs, probs = c(0.025, 0.975))
```

    ##       2.5%      97.5% 
    ## 0.01361093 0.13091813
