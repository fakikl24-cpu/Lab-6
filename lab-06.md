Lab 06 - La Quinta is Spanish for next to Denny’s, Pt. 2
================
Kryschelle Fakir 
3/2/2026

### Load packages and data

``` r
library(tidyverse) 
library(dsbox) 

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



```

### Exercise 6

```r

dn_lq_ak <- dn_lq_ak %>%
  mutate(distance = haversine(longitude.x, latitude.x, longitude.y, latitude.y, round = 3
))

```

### Exercise 7 

```r

dn_lq_ak <- dn_lq_ak %>%
  group_by(address.x) %>%
  mutate(minimum_distance = min(distance))

```

### Exercise 8 

```r

ggplot(dn_lq_ak, aes(x = minimum_distance)) +
  geom_histogram(binwidth = 80, fill = "steelblue", color = "black") +
  labs(
    title = "Distance from Denny’s to Nearest La Quinta (Alaska)",
    x = "Distance",
    y = "Frequency"
  )
  
summary(dn_lq_ak$minimum_distance)
  
```
The distribution is positively skewed, with the mean distance being about 11214 km
or about 6900 miles apart. The locations are a minimum of 10453 km apart and, at max, 
12644 km apart. Given the low population of Alaska, these distances make sense. 


### Exercise 9 

```r

dn_nc <- dn %>%
filter(state == "NC")
nrow(dn_nc)

lq_nc <- lq %>%
filter(state == "NC")
nrow(lq_nc)

nrow(dn_nc) * nrow(lq_nc)

dn_lq_nc <- full_join(dn_nc, lq_nc,
  by = "state"
)

dn_lq_nc

nrow(dn_lq_nc)

dn_lq_nc <- dn_lq_nc %>%
  mutate(distance = haversine(longitude.x, latitude.x, longitude.y, latitude.y, round = 3
))


dn_lq_nc <- dn_lq_nc %>%
  group_by(address.x) %>%
  mutate(minimum_distance = min(distance))
  
ggplot(dn_lq_nc, aes(x = minimum_distance)) +
  geom_histogram(binwidth = 500, fill = "steelblue", color = "black") +
  labs(
    title = "Distance from Denny’s to Nearest La Quinta (NC)",
    x = "Distance",
    y = "Frequency"
  )
  
summary(dn_lq_nc$minimum_distance)

```

The distribution is about normally distributed, with the mean distance being about 14071 km
or about 8700 miles apart. The locations are a minimum of 8778 km apart and, at max, 
19530 km apart.  


### Exercise 10

```r

dn_tx <- dn %>%
filter(state == "TX")
nrow(dn_tx)

lq_tx <- lq %>%
filter(state == "TX")
nrow(lq_tx)

nrow(dn_tx) * nrow(lq_tx)

dn_lq_tx <- full_join(dn_tx, lq_tx,
  by = "state"
)

dn_lq_tx

nrow(dn_lq_tx)

dn_lq_tx <- dn_lq_tx %>%
  mutate(distance = haversine(longitude.x, latitude.x, longitude.y, latitude.y, round = 3
))


dn_lq_tx <- dn_lq_tx %>%
  group_by(address.x) %>%
  mutate(minimum_distance = min(distance))

ggplot(dn_lq_tx, aes(x = minimum_distance)) +
  geom_histogram(binwidth = 500, fill = "steelblue", color = "black") +
  labs(
    title = "Distance from Denny’s to Nearest La Quinta (Texas)",
    x = "Distance",
    y = "Frequency"
  )
  
summary(dn_lq_tx$minimum_distance)

```

The distribution is about normally distributed, being slightly negatively skewed, 
with the mean distance being about 8940.5 km or about 5555 miles apart. 
The locations are a minimum of 110 km apart and, at max, 
17123 km apart. Given the sheer size of Texas, a larger distribution of distances 
makes a lot of sense. 


### Exercise 11

```r

dn_fl <- dn %>%
filter(state == "FL")
nrow(dn_fl)

lq_fl <- lq %>%
filter(state == "FL")
nrow(lq_fl)

nrow(dn_fl) * nrow(lq_fl)

dn_lq_fl <- full_join(dn_fl, lq_fl,
  by = "state"
)

dn_lq_fl

nrow(dn_lq_fl)

dn_lq_fl <- dn_lq_fl %>%
  mutate(distance = haversine(longitude.x, latitude.x, longitude.y, latitude.y, round = 3
))

View(dn_lq_fl)

dn_lq_fl <- dn_lq_fl %>%
  group_by(address.x) %>%
  mutate(minimum_distance = min(distance))

ggplot(dn_lq_fl, aes(x = minimum_distance)) +
  geom_histogram(binwidth = 500, fill = "steelblue", color = "black") +
  labs(
    title = "Distance from Denny’s to Nearest La Quinta (Florida)",
    x = "Distance",
    y = "Frequency"
  )
  
summary(dn_lq_fl$minimum_distance)

```

The distribution is negatively skewed but also somewhat bimodal, 
with the mean distance being about 12093 km or about 7500 miles apart. 
The locations are a minimum of 410 km apart and, at max, 
19420 km apart. They love their Denny's and LaQuintas which tracks for Florida
(I visit often and will be on the lookout for more Dennys and LaQuintas).