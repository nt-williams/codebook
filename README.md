
<!-- README.md is generated from README.Rmd. Please edit that file -->

# codebook

<!-- badges: start -->

[![Lifecycle:
experimental](https://img.shields.io/badge/lifecycle-experimental-orange.svg)](https://lifecycle.r-lib.org/articles/stages.html#experimental)
[![R-CMD-check](https://github.com/nt-williams/dictionary/workflows/R-CMD-check/badge.svg)](https://github.com/nt-williams/dictionary/actions)
[![codecov](https://codecov.io/gh/nt-williams/codebook/branch/main/graph/badge.svg?token=QGGA7OE5UY)](https://codecov.io/gh/nt-williams/codebook)
<!-- badges: end -->

Quickly and easily label your data using code books saved as YAML.

## Installation

``` r
remotes::install_github("nt-williams/codebook")
```

or

``` r
# Install 'codebook' from 'nt-williams' universe
install.packages('codebook', repos = 'https://nt-williams.r-universe.dev')
```

## A basic example

``` r
some_data <- data.frame(
     x = c(1, 2, 5, 3, 4),
     y = c(0, 1, 1, 0, 1), 
     z = c(5.2, 3.1, 5.6, 8.9, 9.0), 
     w = c(1, 1, 0, 1, 1)
)
```

Your codebook as YAML, saved in your project directory (or somewhere
else) as `codebook.yml`.

``` yaml
x:
  label: Variable X
  cb:
    1: These
    2: Are
    3: Random
    4: Factor
    5: Labels

"y":
  label: Variable Y
  cb: &binary
    0: "No"
    1: "Yes"
    
z:
  label: Variable Z

w:
  label: Variable W
  cb: *binary
```

Apply the code book to the data:

``` r
codebook(some_data)
#>        x   y   z   w
#> 1  These  No 5.2 Yes
#> 2    Are Yes 3.1 Yes
#> 3 Labels Yes 5.6  No
#> 4 Random  No 8.9 Yes
#> 5 Factor Yes 9.0 Yes
```

Rename columns based on the codebook labels:

``` r
label(some_data)
#>   Variable X Variable Y Variable Z Variable W
#> 1          1          0        5.2          1
#> 2          2          1        3.1          1
#> 3          5          1        5.6          0
#> 4          3          0        8.9          1
#> 5          4          1        9.0          1
```
