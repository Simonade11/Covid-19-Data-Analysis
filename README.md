---
title: "Covid Analysis"
author: "Simonade"
date: "2024-10-28"
output: html_document
---

``````{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
library(ggplot2)
library(dplyr)
library(scales)
``````

##  Introduction

This report investigates the COVID-19 trends, focusing on the top three countries that have had the highest number of positive cases against the number of tests carried out.

Data Preparation

The data used in this report is based on the top 3 countries: United Kingdom, United States, and Turkey, which have the highest positive-to-tested case ratio.
```{r , echo=FALSE}
# Create the vectors for each country
united_kingdom <- c(0.11, 1473672, 166909, 0, 0)
united_states  <- c(0.10, 17282363, 1877179, 0, 0)
turkey         <- c(0.08, 2031192, 163941, 2980960, 0)

# Create matrix for COVID-19 data
covid_mat <- rbind(united_kingdom, united_states, turkey)
colnames(covid_mat) <- c("Ratio", "tested", "positive", "active", "hospitalized")

# Display the matrix
covid_mat
```


##  Top Three Countries Positive to Tested Ratio

We identified the top 3 countries with the highest positive-to-tested case ratio: United Kingdom, United States, and Turkey.

```{r dataframe, echo=FALSE}
# Create the data frame for the top 3 countries
covid_top_3_df <- data.frame(
  Country = c("United Kingdom", "United States", "Turkey"),
  Ratio = c(0.11, 0.10, 0.08),
  Tested = c(1473672, 17282363, 2031192),
  Positive = c(166909, 1877179, 163941),
  Active = c(0, 0, 2980960),
  Hospitalized = c(0, 0, 0)
)
covid_top_3_df
```

##  Visualizations

1. Bar Plot for Total Tested Cases

The following plot shows the total number of tests conducted in the top 3 countries.
```{r barchart, echo=FALSE}
ggplot(covid_top_3_df, aes(x = Country, y = Tested, fill = Country)) +
  geom_bar(stat = "identity") +
  theme_minimal() +
  labs(title = "Total COVID-19 Tested Cases in Top 3 Countries", x = "Country", y = "Tested Cases") +
  scale_y_continuous(labels = scales::comma)
```

2. Positive to Tested Ratio

The ratio of positive cases to tested cases provides insights into how the virus has spread within the population.
```{r top 3 countries, echo=FALSE}
ggplot(covid_top_3_df, aes(x = Country, y = Ratio, fill = Country)) +
  geom_bar(stat = "identity") +
  theme_minimal() +
  labs(title = "COVID-19 Positive to Tested Ratio in Top 3 Countries", x = "Country", y = "Positive/Tested Ratio") +
  scale_y_continuous(labels = scales::percent)
```

3. Stacked Bar Plot for Positive, Active, and Hospitalized Cases

This plot breaks down the positive, active, and hospitalized cases for the top 3 countries.
```{r country, echo=FALSE}
covid_cases_df <- data.frame(
  Country = rep(c("United Kingdom", "United States", "Turkey"), each = 3),
  Case_Type = rep(c("Positive", "Active", "Hospitalized"), 3),
  Cases = c(166909, 0, 0, 1877179, 0, 0, 163941, 2980960, 0)
)

```

4. Pie Chart for Positive Cases

A pie chart to show the proportion of positive cases among the top 3 countries.
```{r proportion, echo=FALSE}
positive_cases <- c(166909, 1877179, 163941)
countries <- c("United Kingdom", "United States", "Turkey")

pie(positive_cases, labels = countries, main = "Proportion of Positive Cases in Top 3 Countries", col = rainbow(length(countries)))
```

##  Conclusion

From the analysis and visualizations, the United States had the largest number of tested and positive cases, while Turkey had a relatively high active case count. Despite the difference in population size and testing strategies, the positive-to-tested ratios for these three countries were found to be significant.
