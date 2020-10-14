Feschotte lab diversity
================

Read csv and load libraries
===========================

``` r
suppressPackageStartupMessages(library(tidyverse))
suppressPackageStartupMessages(library(knitr))
lab <- read_csv("Lab_members_stats_Feschotte.csv")
lab
```

Create a world map
==================

``` r
library("rnaturalearth") # install.packages("rnaturalearth")
library("rnaturalearthdata") # install.packages("rnaturalearthdata")
library("rgeos") #install.packages("rgeos")
```

``` r
world <- ne_countries(scale = "medium", returnclass = "sf")
```

``` r
lab %>% 
  group_by(Country,lat,long) %>% 
  summarize(n=n()) %>% 
  ggplot() +
  geom_sf(data = world, color = "lightgrey", fill = "grey") +
  geom_point(aes(x=long, y=lat, size=n,color=6*n), color="red", fill="red", alpha=0.8, shape=21) +
  scale_size(range=c(1,10),breaks=c(1,5,10,20,50)) +
  labs(title= "Feschotte Lab Diversity", subtitle="From 2014-2020") +
  theme(panel.grid = element_blank()) +
  theme(axis.title.y = element_blank(), axis.title.x = element_blank())
```

![](world_map_files/figure-markdown_github/unnamed-chunk-5-1.png)
