
<!-- README.md is generated from README.Rmd. Please edit that file -->

# polycor

<!-- badges: start -->

<!-- badges: end -->

The polycor package computes polychoric and polyserial correlations by
quick “two-step” methods or ML, optionally with standard errors;
tetrachoric and biserial correlations are special cases.

It was originally written by Prof. John Fox, who passed away in
November, 2025. I (Duncan Murdoch) have taken over as maintainer in
order to keep the package available as R evolves.

Please submit bug reports as Github issues at
<https://github.com/dmurdoch/polycor/issues>.

## Installation

You can install polycor from CRAN using:

``` r
install.packages("polycor")
```

You can install the development version of polycor from
[GitHub](https://github.com/) with:

``` r
# install.packages("pak")
pak::pak("dmurdoch/polycor")
```

## Example

``` r
library(mvtnorm)
library(polycor)

set.seed(12345)
data <- rmvnorm(1000, c(0, 0), matrix(c(1, .5, .5, 1), 2, 2))
x <- data[,1]
y <- data[,2]
cor(x, y)  # sample correlation
#> [1] 0.5263698

x <- cut(x, c(-Inf, .75, Inf))
y <- cut(y, c(-Inf, -1, .5, 1.5, Inf))
polychor(x, y)  # 2-step estimate
#> [1] 0.5230474
polychor(x, y, ML=TRUE, std.err=TRUE)  # ML estimate
#> 
#> Polychoric Correlation, ML est. = 0.5231 (0.03819)
#> Test of bivariate normality: Chisquare = 2.739, df = 2, p = 0.2543
#> 
#>   Row Threshold
#>   Threshold Std.Err.
#>      0.7537  0.04403
#> 
#> 
#>   Column Thresholds
#>   Threshold Std.Err.
#> 1   -0.9842  0.04746
#> 2    0.4841  0.04127
#> 3    1.5010  0.06118
```
