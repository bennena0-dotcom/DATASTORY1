# DATASTORY1
Carbon/Energy
---
title: "Data Story1"
author: "Nicky Bennett"
date: "`r Sys.Date()`"
output: html_document
---

library (ggplot2)
library(readr)

url <- "https://ourworldindata.org/grapher/levelized-cost-of-energy.csv"

energy <- read_csv(url)

head(energy)

# Graph 1 will look into developed countries Co2 emmisions such as the United States, Japan, and Russia. Co2 emmisions greatly effect SDG goals (good health and well-being and clean water and Sanatation). 


read_cvs <- ('https://ourworldindata.org/grapher/levelized-cost-of-energy.metadata.json?v=1&csvType=full&useColumnShortNames=true') 

library(dplyr)
library(readr)

library(readr)
library(dplyr)
library(ggplot2)
url <- 'https://nyc3.digitaloceanspaces.com/owid-public/data/co2/owid-co2-data.csv'
carbon <- read_csv(url) 
carbon %>% head



countries <- c("United States", "Russia", "Japan")

carbon_ <- carbon %>%
  filter(country %in% countries)
ggplot(carbon_, aes(x = year, y = co2, color = country)) +
  geom_line(size = 1.2) +
  labs(
    title = "Co2 Emissions Over Time",
    x = "Year",
    y = "Co2 Emissions (million tonnes)"
  ) +
  theme_minimal()


# Graph 2 will look at the same countries to see if population has any effect on the amount of Co2 emmissions emmitted. 
  
 ggplot(carbon_, aes(x = year)) +
  geom_line(aes(y = co2, color = "Co2")) +
  geom_line(aes(y = population / 1e6, color = "Population")) +
  facet_wrap(~country, scales = "free_y") +
  labs(
    title = "Co2 vs Population by Country",
    y = "Values (Population in millions)",
    color = "Metric") +
  theme_minimal()
  
  
# Graph 3 will look into Co2 emissions from 1990-2010 for developing countries (Algeria, Greece, and Cuba)

read_cvs <- ('https://ourworldindata.org/grapher/levelized-cost-of-energy.metadata.json?v=1&csvType=full&useColumnShortNames=true') 

library(dplyr)
library(readr)

library(readr)
library(dplyr)
library(ggplot2)

library(dplyr)
library(ggplot2)

countries <- c("Algeria", "Greece", "Cuba")

co2_developing <- carbon %>%
  filter(country %in% countries) %>%
  filter(!is.na(co2))

ggplot(co2_developing, aes(x = year, y = co2, color = country)) +
  geom_line(size = 1.2) +
  labs(
    title = "Co2 Emissions Over Time",
    subtitle = "Algeria vs Greece vs Cuba",
    x = "Year",
    y = "Co2 Emissions (million tonnes)",
    color = "Country"
  ) +
  theme_minimal()
  
# Graph 4 will compare the United States to a developing country (Algeria) 

read_cvs <- ('https://ourworldindata.org/grapher/levelized-cost-of-energy.metadata.json?v=1&csvType=full&useColumnShortNames=true') 

library(dplyr)
library(ggplot2)

co2_comparing <- carbon %>%
  filter(country %in% countries) %>%
  filter(!is.na(co2))
countries <- c("Algeria","United States")

ggplot(co2_comparing, aes(x = year, y = co2, color = country)) +
  geom_line(size = 1.2) +
  labs(
    title = "CO2 Emissions: Algeria vs United States",
    x = "Year",
    y = "CO2 Emissions (million tonnes)",
    color = "Country"
  ) +
  theme_minimal()

# Final Bargraph comparing co2 emissions with United States, Algeria, Japan, and Greece

library(dplyr)
library(ggplot2)

read_cvs <- ('https://ourworldindata.org/grapher/levelized-cost-of-energy.metadata.json?v=1&csvType=full&useColumnShortNames=true') 

countries <- c("United States", "Algeria", "Japan", "Greece")

co2_bar <- carbon %>%
  filter(country %in% countries) %>%
  filter(!is.na(co2)) %>%
  group_by(country) %>%
  filter(year == max(year)) %>%   

ggplot(co2_bar, aes(x = reorder(country, co2), y = co2, fill = country)) +
  geom_col(width = 0.7) +
  labs(
    title = "Co2 Emissions Comparison (Most Recent Year)",
    x = "Country",
    y = "co2 Emissions (million tonnes)"
  ) +
  theme_minimal() +
  theme(legend.position = "none")


# Overall the developed countries produce alot more Co2 emmisions than developing countries. These emissions greatly effect peoples health
