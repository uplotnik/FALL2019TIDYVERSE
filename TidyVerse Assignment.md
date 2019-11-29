---
title: "TidyVerse Assignment"
author: "Uliana Plotnikova"
date: "November 23, 2019"
output: 
  html_document:
    toc: true
    toc_float: true
---
## Assignment

##Part I
**Using one or more TidyVerse packages, and any dataset from fivethirtyeight.com or Kaggle, create a programming sample "vignette" that demonstrates how to use one or more of the capabilities of the selected TidyVerse package with your selected dataset. (25 points)**
 
### What is 'tidyverse'

**The 'tidyverse' is a set of packages that work in harmony because they share common data representations and 'API' design. This package is designed to make it easy to install and load multiple 'tidyverse' packages in a single step. Learn more about the 'tidyverse' at <https://tidyverse.org>.**

**Library(tidyverse) will load the core tidyverse packages:**

**- ggplot2, for data visualisation.**

**- dplyr, for data manipulation.**

**- tidyr, for data tidying.**

**- readr, for data import.**

**- purrr, for functional programming.**

**- tibble, for tibbles, a modern re-imagining of data frames.**

### Preparation




```{r}
suppressWarnings({library(tidyverse)})
```

Dataset was downloaded and saved on github from Kaggle.com
https://www.kaggle.com/russellyates88/suicide-rates-overview-1985-to-2016

```{r}
url<- "https://raw.githubusercontent.com/uplotnik/Data607/master/Suicide.csv"
dataset <- read.csv(url)

```

### Package "dplyr"

**For this assignment I will use package "dplyr"** 

**"dplyr" is a grammar of data manipulation, providing a consistent set of verbs that help you solve the most common data manipulation challenges:**


**- filter() to select cases based on their values.**

**- arrange() to reorder the cases.**

**- select() and rename() to select variables based on their names.**

**- mutate() and transmute() to add new variables that are functions of existing variables.**

**- summarise() to condense multiple values to a single value.**

**- sample_n() and sample_frac() to take random samples.**


```{r}
head(dataset)
```

```{r}
tail(dataset)
```


```{r}
summary(dataset)
```



#### Filter rows with filter()

filter() allows you to select a subset of rows in a data frame. Like all single verbs, the first argument is the tibble (or data frame). The second and subsequent arguments refer to variables within that data frame, selecting rows where the expression is TRUE.

```{r}
head(filter(dataset,country== "Russian Federation"))
```

#### Arrange rows with arrange()

arrange() works similarly to filter() except that instead of filtering or selecting rows, it reorders them. It takes a data frame, and a set of column names (or more complicated expressions) to order by. If you provide more than one column name, each additional column will be used to break ties in the values of preceding columns:

```{r}
head(dataset%>%arrange(desc(suicides_no)))
```
```{r}
head(dataset%>%arrange(suicides_no))
```

#### Select columns with select()

Often you work with large datasets with many columns but only a few are actually of interest to you. select() allows you to rapidly zoom in on a useful subset using operations that usually only work on numeric variable positions:

```{r}
head(dataset%>%select(country, year,sex,age,suicides_no))
```


```{r}
head(dataset%>%select(population:country.year))
```

```{r}
head(dataset%>% select(-(year:HDI.for.year)))
```

#### Rename column with Rename() function

```{r}
head(rename(dataset, gender = sex))
```


#### Summarise() collapses a data frame to a single row.

```{r}
filter(dataset,country== "Russian Federation")%>%summarise(suicide_min=min(suicides_no), suicide_mean=mean(suicides_no),suicide_max=max(suicides_no))

```  
  
#### Randomly sample rows with sample_n() and sample_frac()

```{r}
head(sample_n(dataset, 10))
```


```{r}
head(sample_frac(dataset, 0.01))
```

#### Group_by () 

In the following example, we split the complete dataset into individual countries and then summarise each country by counting the number of suicides (count = n()) and computing the mean of suicides in each country suicides_mean = mean(suicides_no, na.rm = TRUE))


```{r}
by_country <- group_by(dataset, country)
sui <- summarise(by_country,
  count = n(),
  suicides_mean = mean(suicides_no, na.rm = TRUE))
head(sui %>% arrange(desc(suicides_mean)))
```
#### Mutate ()
Will use mutate to round decimals

```{r}
my_data<-head(sui %>% arrange(desc(suicides_mean)) %>%  mutate(suicides_mean = round(suicides_mean, 2)),50)
head(my_data)
```
#### Visualize with ggplot()

```{r}
my_data%>%ggplot(aes(x=country, y=suicides_mean, fill=country))+
  geom_bar(stat = "identity", position = "dodge") + 
  guides(fill = FALSE) +
  ggtitle("Suicides mean 1985-2016")+ 
  theme(axis.text.x = element_text(angle = 60, hjust = 1))
```

##Part II

**Extend an Existing Example.  Using one of your classmate's examples (as created above), extend his or her example with additional annotated code. (15 points)**

For this part of the assignment I will extend Lin Li's example.

```{r}
weather <- read.csv("https://raw.githubusercontent.com/fivethirtyeight/data/master/us-weather-history/KCLT.csv")
head(weather)
```

### Existing code


2. tidyr separate function:
```{r}
weather2 <- weather %>% separate(date, c("year", "month", "day"), sep = "-")
head(weather2)
```

### Extend existing code
```{r}
head(weather2%>%arrange(desc(year)))
```


### Existing code

4. dplyr filter (subsetting dataset)

```{r}
head(filter(weather2, year == "2014"))
```

### Extend existing code


```{r}
filter(weather2, year == "2014")%>%
  summarise(actual_min_temp=min(actual_min_temp), actual_mean_temp=mean(actual_mean_temp),actual_max_temp=max(actual_max_temp))
```



