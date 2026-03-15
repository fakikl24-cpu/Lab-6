Lab 06 - La Quinta is Spanish for next to Denny’s, Pt. 2
================
Kryschelle Fakir 
3/2/2026

### Load packages and data

``` r
library(tidyverse) 
library(dsbox) 
```
install.packages("devtools")
devtools::install_github("tidyverse/dsbox")
``` r
states <- read_csv("data/states.csv")

dn <- read_csv("data/dennys.csv")

lq <- read_csv("data/laquinta.csv")
```

### Exercise 1

``` r
dn_ak <- dn %>%
filter(state == "AK")
nrow(dn_ak)
```
There are 3 Denny's locations in Alaska.

``` r
lq_ak <- lq %>%
filter(state == "AK")
nrow(lq_ak)
```
There are 2 La Quinta locations in Alaska. 

### Exercise 2

``` r

```

### Exercise 3

…

### Exercise 4

…

### Exercise 5

…

### Exercise 6

…

Add exercise headings as needed.
