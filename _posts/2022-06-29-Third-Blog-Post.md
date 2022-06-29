220-06-29-Third-Blog-Post
================
Steph Camino
2022-06-29

# R is WAY cool!

Last semester in my Bayes class I was in a group project working on NFL
field goal data. One of my partners had experience and knew TidyVerse
pretty darn well. He helped us tremendously with data cleaning and
creating beautiful plots. I wanted to learn everything he knew so I was
very excited to see it was part of the material in the course. ggplot
has probably been the coolest thing I’ve learned thus far so let me hit
ya with the cool stuff. Kachow!!!

``` r
# Libraries
library(tidyverse)
library(hrbrthemes)
library(babynames)
library(viridis)
library(knitr)
knitr::opts_chunk$set(fig.path = "../images/")

# Load dataset from github
data <- read.table("https://raw.githubusercontent.com/holtzy/data_to_viz/master/Example_dataset/3_TwoNumOrdered.csv", header=T)
data$date <- as.Date(data$date)

# Filter dataset
femaleNames <- babynames %>% 
  filter(name %in% c("Sarah", "Jordan", "Stephanie", "Cassidy",   "Jessica", "Sophia", "Autumn", "Laura", "Lauren")) %>%
  filter(sex=="F")

# Create the plot
femaleNames %>%
  ggplot( aes(x=year, y=n, group=name, fill=name)) +
    geom_area() +
    scale_fill_viridis(discrete = TRUE) +
    theme(legend.position="none") +
    ggtitle("Frequency of Female names in the last 30 years") +
    theme_ipsum() +
    theme(
      legend.position="none",
      panel.spacing = unit(0, "lines"),
      strip.text.x = element_text(size = 8),
      plot.title = element_text(size=13)
    ) +
    facet_wrap(~name, scale="free_y") + 
    labs(x = "Year", y = "Count")
```

![](C:\Users\scami\OneDrive\Documents\Summer%202022\St558\Repos\smcamino.github.io_posts\2022-06-29-Third-Blog-Post_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->
