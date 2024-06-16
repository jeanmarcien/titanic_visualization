# Data Visualization of Titanic Dataset

This project visualizes the Titanic dataset using R and RMarkdown. The visualizations include a count plot, bar plot, violin plot, correlation heatmap, and facet grid. 

## Install and load libraries

First, we'll install and load the necessary libraries.

```{r}
# Install necessary packages
install.packages("ggplot2")
install.packages("dplyr")
install.packages("corrplot")
install.packages("GGally")

# Load the libraries
library(ggplot2)
library(dplyr)
library(corrplot)
library(GGally)
```

## Load the Titanic dataset

We'll use the Titanic dataset available in the titanic package.

```{r pressure, echo=FALSE}
# Install and load the titanic package
install.packages("titanic")
library(titanic)

# Load the Titanic dataset
data("titanic_train")

# Display the first few rows of the dataset
head(titanic_train)
```

## Exploratory Data Analysis (EDA)

We'll perform some basic exploratory analysis to understand the structure of the dataset.

```{r}
# Display summary statistics
summary(titanic_train)

# Check for missing values
colSums(is.na(titanic_train))
```

## Data visualization

We'll build a count plot to visualize the count of survivors.

```{r}
# Count plot for survivors
ggplot(titanic_train, aes(x = factor(Survived))) +
  geom_bar() +
  labs(title = "Count of Survivors", x = "Survived", y = "Count") +
  scale_x_discrete(labels = c("0" = "No", "1" = "Yes"))
```

We'll build a bar plot to visualize the survival rate by class.

```{r}
# Bar plot for survival rate by class
ggplot(titanic_train, aes(x = factor(Pclass), y = Survived)) +
  stat_summary(fun = mean, geom = "bar") +
  labs(title = "Survival Rate by Class", x = "Passenger Class", y = "Survival Rate")
```


We'll build a violin plot to visualize the distribution of ages by survival status.

```{r}
# Violin plot for age distribution by survival status
ggplot(titanic_train, aes(x = factor(Survived), y = Age)) +
  geom_violin() +
  labs(title = "Age Distribution by Survival Status", x = "Survived", y = "Age")
```

We'll build a heatmap to visualize the correlation matrix of the features.

```{r}
# Select numerical columns for correlation matrix
numerical_cols <- titanic_train %>% select_if(is.numeric)

# Calculate the correlation matrix
correlation_matrix <- cor(numerical_cols, use = "complete.obs")

# Correlation heatmap
corrplot(correlation_matrix, method = "color", addCoef.col = "black",
         tl.col = "black", tl.srt = 45, title = "Correlation Heatmap of Titanic Features")
```

We'll build a facetgrid to visualize the survival rate by age and sex.

```{r}
# FacetGrid for survival rate by age and sex
ggplot(titanic_train, aes(x = Age)) +
  geom_histogram(bins = 20) +
  facet_grid(Sex ~ Survived) +
  labs(title = "Survival Rate by Age and Sex", x = "Age", y = "Count")
```
