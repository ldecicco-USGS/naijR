
<!-- README.md is generated from README.Rmd. Please edit that file -->

# naijR <img src="man/figures/logo.png" width=120px align="right" />

An R package on Nigeria and for Nigeria

<!-- badges: start -->

[![CRAN
status](https://www.r-pkg.org/badges/version/naijR)](https://cran.r-project.org/package=naijR)
[![Codecov test
coverage](https://codecov.io/gh/BroVic/naijR/branch/master/graph/badge.svg)](https://app.codecov.io/gh/BroVic/naijR?branch=master)
[![R build
status](https://github.com/BroVic/naijR/workflows/R-CMD-check/badge.svg)](https://github.com/BroVic/naijR/actions)
[![Lifecycle:
stable](https://img.shields.io/badge/lifecycle-stable-brightgreen.svg)](https://lifecycle.r-lib.org/articles/stages.html#stable)
<!-- badges: end -->

The goal of **naijR** is to make it easier for R users to work with data
related to Nigeria.

## Usage

### Some simple operations

#### Maps

One of the useful aspects of this package is enabling users to plot
country and sub-national geo-spatial maps. Currently, only vector-type
graphics are supported. To find out more, read the vignette–accessible
from within R as follows:

``` r
vignette('nigeria-maps', 'naijR')
```

### Administrative Regions

#### States

To create a list of all the States of the Nigerian Federation, simply
call `states()`.

``` r
library(naijR, quietly = TRUE)
ss <- states()
head(ss)
Abia

Adamawa

Akwa Ibom

Anambra

Bauchi

Bayelsa
cat(sprintf("\n...but Nigeria has %i States.", length(ss)))

...but Nigeria has 37 States.
```

States from a given geo-political zone can also be selected:

``` r
states(gpz = "ne")  # i.e. North-East
Adamawa

Bauchi

Borno

Gombe

Taraba

Yobe
```

For other capabilities of this function, see `?states()`.

#### Local Government Areas

This is a basic example that shows how to very quickly fetch the names
of Local Government Areas within a given State:

``` r
lgas("Imo")
Aboh Mbaise

Ahiazu Mbaise

Ehime Mbano

Ezinihitte

Ideato North

Ideato South

Ihitte/Uboma

Ikeduru

Isiala Mbano

Isu

Mbaitoli

Ngor Okpala

Njaba

Nkwerre

Nwangele

Obowo

Oguta

Ohaji/Egbema

Okigwe

Orlu

Orsu

Oru East

Oru West

Owerri Municipal

Owerri North

Owerri West

Unuimo
```

To list all the LGAs in Nigeria, call the same function without any
parameters:

``` r
n <- length(lgas())
sprintf("Nigeria has a total of %i Local Government Areas", n)
[1] "Nigeria has a total of 774 Local Government Areas"
```

Want to create a function to check how many LGAs a particular State has?

``` r
how_many_lgas <- function(state) {
  n <- length(lgas(state))
  cat(state, "State has", n, "LGAs\n")
}

how_many_lgas("Sokoto")
Sokoto State has 23 LGAs
```

### Working with phone numbers

It is common to come across datasets where phone numbers are wrongly
entered or misinterpreted by software like MS Excel. The function
`fix_mobile()` helps with this.

``` r
fix_mobile("8032000000")
[1] "08032000000"
```

The function works on vectors; thus an entire column of a table with
phone numbers can be quickly processed. Illegible or irreparable numbers
are turned into missing values, e.g.

``` r
(dat <- data.frame(
  serialno = 1:8,
  phone = c(
    "123456789",
    "0123456789",
    "8000000001",
    "9012345678",
    "07098765432",
    "08123456789",
    "09064321987",
    "O8055577889"
  )
))
  serialno       phone
1        1   123456789
2        2  0123456789
3        3  8000000001
4        4  9012345678
5        5 07098765432
6        6 08123456789
7        7 09064321987
8        8 O8055577889
```

``` r
fix_mobile(dat$phone)
[1] NA            NA            "08000000001" "09012345678" "07098765432"
[6] "08123456789" "09064321987" "08055577889"
```

## Installation

To download and install the current stable version of this package from
CRAN:

``` r
install.packages("naijR")
```

The development version can be obtained from
[GitHub](https://github.com/BroVic/naijR) with:

``` r
# install.packages("pak")  # if necessary
pak::pkg_install("BroVic/naijR")
```

## Feedback/Contribution

Contributions are welcome and pull requests for R code or documentation
will be gladly entertained. For bug reports or feature requests, kindly
submit an [issue](https://github.com/BroVic/naijR/issues/new).
