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
nrow(dn_ak) * nrow(lq_ak)

```

We need to calculate 6 distances between the Dennys
and LaQuinta locations. 

### Exercise 3

```r full-join
dn_lq_ak <- full_join(dn_ak, lq_ak,
  by = "state"
)
dn_lq_ak
```
…

### Exercise 4

```r

nrow(dn_lq_ak)

```

There are 6 observations in the joined data frame and the name of the variables
are address, city, state, longtitude, latitude, and zip code for the Dennys (.x)
and LaQuintas (.y).


### Exercise 5

We use the mutate function to add new variables to an existing data frame.

```r

haversine <- function(long1, lat1, long2, lat2, round = 3) {
  long1 <- long1 * pi / 180 
  lat2 <- lat1 * pi /180
  long2 <- long2 * pi /180 
  lat2 <- lat2 * pi /180
  
  R <- 6371
  
  a <- sin((lat2 - lat1) / 2)^2 + cos(lat1) * cos(lat2) * sin((long2 - long1) /2)^2
  d <- R * 2 * asin(sqrt(a))
  
  return(round(d, round))
}

View(dn_lq_ak)



```

### Exercise 6

```r

dn_lq_ak <- dn_lq_ak %>%
  mutate(distance = haversine(longitude.x, latitude.x, longitude.y, latitude.y, round = 3
))

``

Add exercise headings as needed.
