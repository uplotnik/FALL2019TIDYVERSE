

    Assignment

    Part I

    Part II

TidyVerse Assignment
Uliana Plotnikova
November 23, 2019
Assignment
Part I

Using one or more TidyVerse packages, and any dataset from fivethirtyeight.com or Kaggle, create a programming sample “vignette” that demonstrates how to use one or more of the capabilities of the selected TidyVerse package with your selected dataset. (25 points)
What is ‘tidyverse’

The ‘tidyverse’ is a set of packages that work in harmony because they share common data representations and ‘API’ design. This package is designed to make it easy to install and load multiple ‘tidyverse’ packages in a single step. Learn more about the ‘tidyverse’ at https://tidyverse.org.

Library(tidyverse) will load the core tidyverse packages:

- ggplot2, for data visualisation.

- dplyr, for data manipulation.

- tidyr, for data tidying.

- readr, for data import.

- purrr, for functional programming.

- tibble, for tibbles, a modern re-imagining of data frames.
Preparation

suppressWarnings({library(tidyverse)})

## -- Attaching packages ---------------------------------------------------------------------------------------------------------------- tidyverse 1.2.1 --

## v ggplot2 3.1.0     v purrr   0.3.2
## v tibble  2.1.3     v dplyr   0.8.3
## v tidyr   1.0.0     v stringr 1.3.1
## v readr   1.3.1     v forcats 0.4.0

## -- Conflicts ------------------------------------------------------------------------------------------------------------------- tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()

Dataset was downloaded and saved on github from Kaggle.com https://www.kaggle.com/russellyates88/suicide-rates-overview-1985-to-2016

url<- "https://raw.githubusercontent.com/uplotnik/Data607/master/Suicide.csv"
dataset <- read.csv(url)

Package “dplyr”

For this assignment I will use package “dplyr”

“dplyr” is a grammar of data manipulation, providing a consistent set of verbs that help you solve the most common data manipulation challenges:

- filter() to select cases based on their values.

- arrange() to reorder the cases.

- select() and rename() to select variables based on their names.

- mutate() and transmute() to add new variables that are functions of existing variables.

- summarise() to condense multiple values to a single value.

- sample_n() and sample_frac() to take random samples.

head(dataset)

##   country year    sex         age suicides_no population suicides.100k.pop
## 1 Albania 1987   male 15-24 years          21     312900              6.71
## 2 Albania 1987   male 35-54 years          16     308000              5.19
## 3 Albania 1987 female 15-24 years          14     289700              4.83
## 4 Albania 1987   male   75+ years           1      21800              4.59
## 5 Albania 1987   male 25-34 years           9     274300              3.28
## 6 Albania 1987 female   75+ years           1      35600              2.81
##   country.year HDI.for.year gdp_for_year.... gdp_per_capita....
## 1  Albania1987           NA    2,156,624,900                796
## 2  Albania1987           NA    2,156,624,900                796
## 3  Albania1987           NA    2,156,624,900                796
## 4  Albania1987           NA    2,156,624,900                796
## 5  Albania1987           NA    2,156,624,900                796
## 6  Albania1987           NA    2,156,624,900                796
##        generation
## 1    Generation X
## 2          Silent
## 3    Generation X
## 4 G.I. Generation
## 5         Boomers
## 6 G.I. Generation

tail(dataset)

##          country year    sex         age suicides_no population
## 27815 Uzbekistan 2014 female 25-34 years         162    2735238
## 27816 Uzbekistan 2014 female 35-54 years         107    3620833
## 27817 Uzbekistan 2014 female   75+ years           9     348465
## 27818 Uzbekistan 2014   male  5-14 years          60    2762158
## 27819 Uzbekistan 2014 female  5-14 years          44    2631600
## 27820 Uzbekistan 2014 female 55-74 years          21    1438935
##       suicides.100k.pop   country.year HDI.for.year gdp_for_year....
## 27815              5.92 Uzbekistan2014        0.675   63,067,077,179
## 27816              2.96 Uzbekistan2014        0.675   63,067,077,179
## 27817              2.58 Uzbekistan2014        0.675   63,067,077,179
## 27818              2.17 Uzbekistan2014        0.675   63,067,077,179
## 27819              1.67 Uzbekistan2014        0.675   63,067,077,179
## 27820              1.46 Uzbekistan2014        0.675   63,067,077,179
##       gdp_per_capita....   generation
## 27815               2309   Millenials
## 27816               2309 Generation X
## 27817               2309       Silent
## 27818               2309 Generation Z
## 27819               2309 Generation Z
## 27820               2309      Boomers

summary(dataset)

##         country           year          sex                 age      
##  Austria    :  382   Min.   :1985   female:13910   15-24 years:4642  
##  Iceland    :  382   1st Qu.:1995   male  :13910   25-34 years:4642  
##  Mauritius  :  382   Median :2002                  35-54 years:4642  
##  Netherlands:  382   Mean   :2001                  5-14 years :4610  
##  Argentina  :  372   3rd Qu.:2008                  55-74 years:4642  
##  Belgium    :  372   Max.   :2016                  75+ years  :4642  
##  (Other)    :25548                                                   
##   suicides_no        population       suicides.100k.pop
##  Min.   :    0.0   Min.   :     278   Min.   :  0.00   
##  1st Qu.:    3.0   1st Qu.:   97498   1st Qu.:  0.92   
##  Median :   25.0   Median :  430150   Median :  5.99   
##  Mean   :  242.6   Mean   : 1844794   Mean   : 12.82   
##  3rd Qu.:  131.0   3rd Qu.: 1486143   3rd Qu.: 16.62   
##  Max.   :22338.0   Max.   :43805214   Max.   :224.97   
##                                                        
##       country.year    HDI.for.year            gdp_for_year....
##  Albania1987:   12   Min.   :0.483   1,002,219,052,968:   12  
##  Albania1988:   12   1st Qu.:0.713   1,011,797,457,139:   12  
##  Albania1989:   12   Median :0.779   1,016,418,229    :   12  
##  Albania1992:   12   Mean   :0.777   1,018,847,043,277:   12  
##  Albania1993:   12   3rd Qu.:0.855   1,022,191,296    :   12  
##  Albania1994:   12   Max.   :0.944   1,023,196,003,075:   12  
##  (Other)    :27748   NA's   :19456   (Other)          :27748  
##  gdp_per_capita....           generation  
##  Min.   :   251     Boomers        :4990  
##  1st Qu.:  3447     G.I. Generation:2744  
##  Median :  9372     Generation X   :6408  
##  Mean   : 16866     Generation Z   :1470  
##  3rd Qu.: 24874     Millenials     :5844  
##  Max.   :126352     Silent         :6364  
## 

Filter rows with filter()

filter() allows you to select a subset of rows in a data frame. Like all single verbs, the first argument is the tibble (or data frame). The second and subsequent arguments refer to variables within that data frame, selecting rows where the expression is TRUE.

head(filter(dataset,country== "Russian Federation"))

##              country year    sex         age suicides_no population
## 1 Russian Federation 1989   male   75+ years        1393    1349100
## 2 Russian Federation 1989   male 35-54 years       12030   18058500
## 3 Russian Federation 1989   male 55-74 years        6250    9383700
## 4 Russian Federation 1989   male 25-34 years        6856   12748800
## 5 Russian Federation 1989 female   75+ years        1677    4738100
## 6 Russian Federation 1989   male 15-24 years        2581   10073900
##   suicides.100k.pop           country.year HDI.for.year gdp_for_year....
## 1            103.25 Russian Federation1989           NA  506,500,173,960
## 2             66.62 Russian Federation1989           NA  506,500,173,960
## 3             66.60 Russian Federation1989           NA  506,500,173,960
## 4             53.78 Russian Federation1989           NA  506,500,173,960
## 5             35.39 Russian Federation1989           NA  506,500,173,960
## 6             25.62 Russian Federation1989           NA  506,500,173,960
##   gdp_per_capita....      generation
## 1               3740 G.I. Generation
## 2               3740          Silent
## 3               3740 G.I. Generation
## 4               3740         Boomers
## 5               3740 G.I. Generation
## 6               3740    Generation X

Arrange rows with arrange()

arrange() works similarly to filter() except that instead of filtering or selecting rows, it reorders them. It takes a data frame, and a set of column names (or more complicated expressions) to order by. If you provide more than one column name, each additional column will be used to break ties in the values of preceding columns:

head(dataset%>%arrange(desc(suicides_no)))

##              country year  sex         age suicides_no population
## 1 Russian Federation 1994 male 35-54 years       22338   19044200
## 2 Russian Federation 1995 male 35-54 years       21706   19249600
## 3 Russian Federation 2001 male 35-54 years       21262   21476420
## 4 Russian Federation 2000 male 35-54 years       21063   21378098
## 5 Russian Federation 1999 male 35-54 years       20705   21016400
## 6 Russian Federation 1996 male 35-54 years       20562   19507100
##   suicides.100k.pop           country.year HDI.for.year gdp_for_year....
## 1            117.30 Russian Federation1994           NA  395,077,301,248
## 2            112.76 Russian Federation1995           NA  395,531,066,563
## 3             99.00 Russian Federation2001           NA  306,602,673,980
## 4             98.53 Russian Federation2000           NA  259,708,496,267
## 5             98.52 Russian Federation1999           NA  195,905,767,669
## 6            105.41 Russian Federation1996           NA  391,719,993,757
##   gdp_per_capita.... generation
## 1               2853    Boomers
## 2               2844    Boomers
## 3               2229    Boomers
## 4               1879    Boomers
## 5               1412    Boomers
## 6               2813    Boomers

head(dataset%>%arrange(suicides_no))

##   country year    sex         age suicides_no population suicides.100k.pop
## 1 Albania 1987 female  5-14 years           0     311000                 0
## 2 Albania 1987 female 55-74 years           0     144600                 0
## 3 Albania 1987   male  5-14 years           0     338200                 0
## 4 Albania 1988 female  5-14 years           0     317200                 0
## 5 Albania 1988   male  5-14 years           0     345000                 0
## 6 Albania 1989 female  5-14 years           0     321900                 0
##   country.year HDI.for.year gdp_for_year.... gdp_per_capita....
## 1  Albania1987           NA    2,156,624,900                796
## 2  Albania1987           NA    2,156,624,900                796
## 3  Albania1987           NA    2,156,624,900                796
## 4  Albania1988           NA    2,126,000,000                769
## 5  Albania1988           NA    2,126,000,000                769
## 6  Albania1989           NA    2,335,124,988                833
##        generation
## 1    Generation X
## 2 G.I. Generation
## 3    Generation X
## 4    Generation X
## 5    Generation X
## 6    Generation X

Select columns with select()

Often you work with large datasets with many columns but only a few are actually of interest to you. select() allows you to rapidly zoom in on a useful subset using operations that usually only work on numeric variable positions:

head(dataset%>%select(country, year,sex,age,suicides_no))

##   country year    sex         age suicides_no
## 1 Albania 1987   male 15-24 years          21
## 2 Albania 1987   male 35-54 years          16
## 3 Albania 1987 female 15-24 years          14
## 4 Albania 1987   male   75+ years           1
## 5 Albania 1987   male 25-34 years           9
## 6 Albania 1987 female   75+ years           1

head(dataset%>%select(population:country.year))

##   population suicides.100k.pop country.year
## 1     312900              6.71  Albania1987
## 2     308000              5.19  Albania1987
## 3     289700              4.83  Albania1987
## 4      21800              4.59  Albania1987
## 5     274300              3.28  Albania1987
## 6      35600              2.81  Albania1987

head(dataset%>% select(-(year:HDI.for.year)))

##   country gdp_for_year.... gdp_per_capita....      generation
## 1 Albania    2,156,624,900                796    Generation X
## 2 Albania    2,156,624,900                796          Silent
## 3 Albania    2,156,624,900                796    Generation X
## 4 Albania    2,156,624,900                796 G.I. Generation
## 5 Albania    2,156,624,900                796         Boomers
## 6 Albania    2,156,624,900                796 G.I. Generation

Rename column with Rename() function

head(rename(dataset, gender = sex))

##   country year gender         age suicides_no population suicides.100k.pop
## 1 Albania 1987   male 15-24 years          21     312900              6.71
## 2 Albania 1987   male 35-54 years          16     308000              5.19
## 3 Albania 1987 female 15-24 years          14     289700              4.83
## 4 Albania 1987   male   75+ years           1      21800              4.59
## 5 Albania 1987   male 25-34 years           9     274300              3.28
## 6 Albania 1987 female   75+ years           1      35600              2.81
##   country.year HDI.for.year gdp_for_year.... gdp_per_capita....
## 1  Albania1987           NA    2,156,624,900                796
## 2  Albania1987           NA    2,156,624,900                796
## 3  Albania1987           NA    2,156,624,900                796
## 4  Albania1987           NA    2,156,624,900                796
## 5  Albania1987           NA    2,156,624,900                796
## 6  Albania1987           NA    2,156,624,900                796
##        generation
## 1    Generation X
## 2          Silent
## 3    Generation X
## 4 G.I. Generation
## 5         Boomers
## 6 G.I. Generation

Summarise() collapses a data frame to a single row.

filter(dataset,country== "Russian Federation")%>%summarise(suicide_min=min(suicides_no), suicide_mean=mean(suicides_no),suicide_max=max(suicides_no))

##   suicide_min suicide_mean suicide_max
## 1          44     3733.772       22338

Randomly sample rows with sample_n() and sample_frac()

head(sample_n(dataset, 10))

##         country year    sex         age suicides_no population
## 1         Chile 2013 female  5-14 years           8    1238965
## 2        France 2012   male  5-14 years          22    3995444
## 3 United States 2005 female 35-54 years        3209   43509335
## 4     Guatemala 2005 female 15-24 years          40    1358448
## 5     Australia 1985 female 35-54 years         143    1832700
## 6        Serbia 2008   male 35-54 years         296    1009044
##   suicides.100k.pop      country.year HDI.for.year   gdp_for_year....
## 1              0.65         Chile2013        0.830    278,384,332,694
## 2              0.55        France2012        0.886  2,683,825,225,093
## 3              7.38 United States2005        0.897 13,093,726,000,000
## 4              2.94     Guatemala2005        0.576     27,211,377,225
## 5              7.80     Australia1985           NA    180,190,994,861
## 6             29.33        Serbia2008           NA     49,259,526,053
##   gdp_per_capita....   generation
## 1              17140 Generation Z
## 2              45002 Generation Z
## 3              47423      Boomers
## 4               2450   Millenials
## 5              12374       Silent
## 6               7049      Boomers

head(sample_frac(dataset, 0.01))

##             country year    sex         age suicides_no population
## 1          Suriname 1985 female   75+ years           2       4200
## 2         Mauritius 2012 female  5-14 years           2      89061
## 3 Republic of Korea 2005 female 55-74 years         986    3815878
## 4        Costa Rica 1999   male 55-74 years          27     175883
## 5             Qatar 2015 female  5-14 years           0     104727
## 6           Finland 1988 female  5-14 years           1     314400
##   suicides.100k.pop          country.year HDI.for.year gdp_for_year....
## 1             47.62          Suriname1985           NA      873,250,000
## 2              2.25         Mauritius2012        0.772   11,668,685,524
## 3             25.84 Republic of Korea2005           NA  898,137,194,716
## 4             15.35        Costa Rica1999           NA   14,195,623,425
## 5              0.00             Qatar2015           NA  164,641,483,516
## 6              0.32           Finland1988           NA  109,103,056,148
##   gdp_per_capita....      generation
## 1               2706 G.I. Generation
## 2               9884    Generation Z
## 3              19460          Silent
## 4               4115          Silent
## 5              69937    Generation Z
## 6              23546    Generation X

Group_by ()

In the following example, we split the complete dataset into individual countries and then summarise each country by counting the number of suicides (count = n()) and computing the mean of suicides in each country suicides_mean = mean(suicides_no, na.rm = TRUE))

by_country <- group_by(dataset, country)
sui <- summarise(by_country,
  count = n(),
  suicides_mean = mean(suicides_no, na.rm = TRUE))
head(sui %>% arrange(desc(suicides_mean)))

## # A tibble: 6 x 3
##   country            count suicides_mean
##   <fct>              <int>         <dbl>
## 1 Russian Federation   324         3734.
## 2 United States        372         2780.
## 3 Japan                372         2169.
## 4 Ukraine              336          952.
## 5 Germany              312          934.
## 6 France               360          914.

Mutate ()

Will use mutate to round decimals

my_data<-head(sui %>% arrange(desc(suicides_mean)) %>%  mutate(suicides_mean = round(suicides_mean, 2)),50)
my_data

## # A tibble: 50 x 3
##    country            count suicides_mean
##    <fct>              <int>         <dbl>
##  1 Russian Federation   324         3734.
##  2 United States        372         2780.
##  3 Japan                372         2169.
##  4 Ukraine              336          952.
##  5 Germany              312          934.
##  6 France               360          914.
##  7 Republic of Korea    372          704.
##  8 Brazil               372          609.
##  9 Poland               288          483.
## 10 Sri Lanka            132          422.
## # ... with 40 more rows

Visualize with ggplot()

my_data%>%ggplot(aes(x=country, y=suicides_mean, fill=country))+
  geom_bar(stat = "identity", position = "dodge") + 
  guides(fill = FALSE) +
  ggtitle("Suicides mean 1985-2016")+ 
  theme(axis.text.x = element_text(angle = 60, hjust = 1))

Part II

Extend an Existing Example. Using one of your classmate’s examples (as created above), extend his or her example with additional annotated code. (15 points)

For this part of the assignment I will extend Lin Li’s example.

weather <- read.csv("https://raw.githubusercontent.com/fivethirtyeight/data/master/us-weather-history/KCLT.csv")
head(weather)

##       date actual_mean_temp actual_min_temp actual_max_temp
## 1 2014-7-1               81              70              91
## 2 2014-7-2               85              74              95
## 3 2014-7-3               82              71              93
## 4 2014-7-4               75              64              86
## 5 2014-7-5               72              60              84
## 6 2014-7-6               74              61              87
##   average_min_temp average_max_temp record_min_temp record_max_temp
## 1               67               89              56             104
## 2               68               89              56             101
## 3               68               89              56              99
## 4               68               89              55              99
## 5               68               89              57             100
## 6               68               89              57              99
##   record_min_temp_year record_max_temp_year actual_precipitation
## 1                 1919                 2012                 0.00
## 2                 2008                 1931                 0.00
## 3                 2010                 1931                 0.14
## 4                 1933                 1955                 0.00
## 5                 1967                 1954                 0.00
## 6                 1964                 1948                 0.00
##   average_precipitation record_precipitation
## 1                  0.10                 5.91
## 2                  0.10                 1.53
## 3                  0.11                 2.50
## 4                  0.10                 2.63
## 5                  0.10                 1.65
## 6                  0.10                 1.95

Existing code

    tidyr separate function:

weather2 <- weather %>% separate(date, c("year", "month", "day"), sep = "-")
head(weather2)

##   year month day actual_mean_temp actual_min_temp actual_max_temp
## 1 2014     7   1               81              70              91
## 2 2014     7   2               85              74              95
## 3 2014     7   3               82              71              93
## 4 2014     7   4               75              64              86
## 5 2014     7   5               72              60              84
## 6 2014     7   6               74              61              87
##   average_min_temp average_max_temp record_min_temp record_max_temp
## 1               67               89              56             104
## 2               68               89              56             101
## 3               68               89              56              99
## 4               68               89              55              99
## 5               68               89              57             100
## 6               68               89              57              99
##   record_min_temp_year record_max_temp_year actual_precipitation
## 1                 1919                 2012                 0.00
## 2                 2008                 1931                 0.00
## 3                 2010                 1931                 0.14
## 4                 1933                 1955                 0.00
## 5                 1967                 1954                 0.00
## 6                 1964                 1948                 0.00
##   average_precipitation record_precipitation
## 1                  0.10                 5.91
## 2                  0.10                 1.53
## 3                  0.11                 2.50
## 4                  0.10                 2.63
## 5                  0.10                 1.65
## 6                  0.10                 1.95

Extend existing code

head(weather2%>%arrange(desc(year)))

##   year month day actual_mean_temp actual_min_temp actual_max_temp
## 1 2015     1   1               40              26              53
## 2 2015     1   2               47              42              52
## 3 2015     1   3               50              47              52
## 4 2015     1   4               56              47              65
## 5 2015     1   5               45              36              54
## 6 2015     1   6               41              24              57
##   average_min_temp average_max_temp record_min_temp record_max_temp
## 1               30               50              10              74
## 2               30               50               6              78
## 3               30               50               8              74
## 4               30               50               8              75
## 5               30               50              10              72
## 6               30               50               5              73
##   record_min_temp_year record_max_temp_year actual_precipitation
## 1                 1928                 1985                 0.00
## 2                 1928                 1952                 0.12
## 3                 1887                 2004                 0.25
## 4                 1887                 1950                 0.26
## 5                 1920                 1950                 0.00
## 6                 1884                 1950                 0.00
##   average_precipitation record_precipitation
## 1                  0.11                 1.54
## 2                  0.10                 2.10
## 3                  0.11                 1.93
## 4                  0.11                 1.32
## 5                  0.12                 1.77
## 6                  0.11                 3.45

Existing code

    dplyr filter (subsetting dataset)

head(filter(weather2, year == "2014"))

##   year month day actual_mean_temp actual_min_temp actual_max_temp
## 1 2014     7   1               81              70              91
## 2 2014     7   2               85              74              95
## 3 2014     7   3               82              71              93
## 4 2014     7   4               75              64              86
## 5 2014     7   5               72              60              84
## 6 2014     7   6               74              61              87
##   average_min_temp average_max_temp record_min_temp record_max_temp
## 1               67               89              56             104
## 2               68               89              56             101
## 3               68               89              56              99
## 4               68               89              55              99
## 5               68               89              57             100
## 6               68               89              57              99
##   record_min_temp_year record_max_temp_year actual_precipitation
## 1                 1919                 2012                 0.00
## 2                 2008                 1931                 0.00
## 3                 2010                 1931                 0.14
## 4                 1933                 1955                 0.00
## 5                 1967                 1954                 0.00
## 6                 1964                 1948                 0.00
##   average_precipitation record_precipitation
## 1                  0.10                 5.91
## 2                  0.10                 1.53
## 3                  0.11                 2.50
## 4                  0.10                 2.63
## 5                  0.10                 1.65
## 6                  0.10                 1.95

Extend existing code

filter(weather2, year == "2014")%>%
  summarise(actual_min_temp=min(actual_min_temp), actual_mean_temp=mean(actual_mean_temp),actual_max_temp=max(actual_max_temp))

##   actual_min_temp actual_mean_temp actual_max_temp
## 1              14         63.97283              96

