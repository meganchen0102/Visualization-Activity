---
title: "ANA 515 Week 5 Discussion"
author: "Zhiying Chen"
date: "6/26/2022"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```


``` {r, echo = FALSE}
#install.packages("tidyverse") 
#install.packages("ggplot2")

library("tidyverse")
library("knitr")
library("ggplot2")
```

```{r, echo = FALSE}
#The include = FALSE function hides both the code and output in my output document

#You need to install these packages first to be able to use the functions within them. You can install them from the Tools tab or write a new code chunk: install.packages("package_name").

url <- "https://raw.githubusercontent.com/fivethirtyeight/data/master/airline-safety/airline-safety.csv"
air_safety <- read.csv(url)

#I loaded readr to use the read_csv function which reads the csv file data.

```

```{r, echo = FALSE}

se_accident <- air_safety

names(se_accident)[names(se_accident) == "airline"] <- "airline_name"
names(se_accident)[names(se_accident) == "avail_seat_km_per_week"] <- "avail_seat"
names(se_accident)[names(se_accident) == "fatalities_85_99"] <- "num_fatalities_85_99"
names(se_accident)[names(se_accident) == "fatalities_00_14"] <- "num_fatalities_00_14"

colnames(se_accident)
```

```{r}

se_accident %>% 
  select(airline_name, incidents_00_14) %>% 
  top_n(3, incidents_00_14)%>%  
  ggplot(aes(x=airline_name, y=incidents_00_14)) +
  geom_bar(stat="identity")
#This bar chart displays the top 5 airlines with most fatal accidents during 2000 - 2014 and the number of accidents in this period. 
```
  
```{r}
vec <- c("airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline","airline")
se_accident_new <- se_accident
se_accident_new$airline <- vec  
ggplot(se_accident_new, aes(airline, incidents_00_14)) + geom_boxplot(fill = "red")+
scale_y_continuous("incidents_00_14", breaks= seq(0,25, by=1))+
labs(title = "Airline Incidents", x = "Ariline")

#This box chart shows the spread of the number of incidents among the airlines and detect the outliers. 
```

