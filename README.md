
<!-- README.md is generated from README.Rmd. Please edit that file -->

# conflicted

[![Travis build
status](https://travis-ci.org/r-lib/conflicted.svg?branch=master)](https://travis-ci.org/r-lib/conflicted)
[![Coverage
status](https://codecov.io/gh/r-lib/conflicted/branch/master/graph/badge.svg)](https://codecov.io/github/r-lib/conflicted?branch=master)

The goal of conflicted is to provide an alternative conflict resolution
strategy. R’s default conflict resolution system gives precedence to the
most recently loaded package. This can make it hard to detect conflicts,
particularly when introduced by an update to an existing package.
conflicted takes a different approach, making every conflict an error
and forcing you to choose which function to use.

Thanks to [@krlmlr](https://github.com/krlmlr) for this neat idea\!

## Installation

``` r
# install.packages("devtools")
devtools::install_github("r-lib/conflicted")
```

## Usage

conflicted does not export any functions. To use it, all you need to do
is load it:

``` r
library(conflicted)
library(dplyr)

filter
#> Error: Multiple definitions found for filter. Please pick one:
#>  * dplyr::filter
#>  * stats::filter
```

Loading conflicted creates a new “conflicted” environment that is
attached just after the global environment. This environment contains an
active binding for any object that is exported by multiple packages; the
active binding will throw an error message describing how to
disambiguate the name. The conflicted environment also contains bindings
for `library()` and `require()` that suppress conflict reporting and
update the conflicted environment with any new conflicts.
