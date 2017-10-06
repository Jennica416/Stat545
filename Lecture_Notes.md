# Stat 545 Lecture Notes
By Jennica Nichols  
September 24, 2017  


# Stat545
These are my personal notes from Stat 545 to help with my.

## Lecture 1 
### Add text to README file
Go to Github and get link to clone. Open using in RStudio and pull to get the latest version. You can then make edits locally, where you then commit changes and then push back to the repository.

## Lecture 2
No notes to add

## Lecture 3
No notes to add

## Lecture 4
### Changing output format
The following YAML formatting at the top for a markdown file will make sure that I keep the md intermediate file.

output:
  html_document:
    keep_md: true  
    
[Here is information on YAML features for Markdown](http://rmarkdown.rstudio.com/html_document_format.html)

[Here is a Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

## Lecture 5

The first part of the lecture is to look at working with a dataframe

```r
##number of columns 
ncol(iris)
```

```
## [1] 5
```

```r
##column names
colnames(iris)
```

```
## [1] "Sepal.Length" "Sepal.Width"  "Petal.Length" "Petal.Width" 
## [5] "Species"
```

```r
##number of rows
nrow(iris)
```

```
## [1] 150
```

```r
##smallest values for each numeric variable
summary(iris)
```

```
##   Sepal.Length    Sepal.Width     Petal.Length    Petal.Width   
##  Min.   :4.300   Min.   :2.000   Min.   :1.000   Min.   :0.100  
##  1st Qu.:5.100   1st Qu.:2.800   1st Qu.:1.600   1st Qu.:0.300  
##  Median :5.800   Median :3.000   Median :4.350   Median :1.300  
##  Mean   :5.843   Mean   :3.057   Mean   :3.758   Mean   :1.199  
##  3rd Qu.:6.400   3rd Qu.:3.300   3rd Qu.:5.100   3rd Qu.:1.800  
##  Max.   :7.900   Max.   :4.400   Max.   :6.900   Max.   :2.500  
##        Species  
##  setosa    :50  
##  versicolor:50  
##  virginica :50  
##                 
##                 
## 
```

```r
##make a histogram of Petal.Width
hist(iris$Petal.Width)
```

![](Lecture_Notes_files/figure-html/unnamed-chunk-1-1.png)<!-- -->

The second part of the lecture is to learn the fundamentals of dplyr. The package's primary functions are:

* Pick observations by their values (filter()).
* Pick variables by their names (select()).
* Reorder the rows (arrange()).
* Create new variables with functions of existing variables (mutate()).
* Collapse many values down to a single summary (summarise()).
* Then there’s group_by(), which can be used in conjunction with all of these.


```r
#load libraries
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
library(gapminder)

#use filer
filter(gapminder, country=="Canada")
```

```
## # A tibble: 12 x 6
##    country continent  year lifeExp      pop gdpPercap
##     <fctr>    <fctr> <int>   <dbl>    <int>     <dbl>
##  1  Canada  Americas  1952  68.750 14785584  11367.16
##  2  Canada  Americas  1957  69.960 17010154  12489.95
##  3  Canada  Americas  1962  71.300 18985849  13462.49
##  4  Canada  Americas  1967  72.130 20819767  16076.59
##  5  Canada  Americas  1972  72.880 22284500  18970.57
##  6  Canada  Americas  1977  74.210 23796400  22090.88
##  7  Canada  Americas  1982  75.760 25201900  22898.79
##  8  Canada  Americas  1987  76.860 26549700  26626.52
##  9  Canada  Americas  1992  77.950 28523502  26342.88
## 10  Canada  Americas  1997  78.610 30305843  28954.93
## 11  Canada  Americas  2002  79.770 31902268  33328.97
## 12  Canada  Americas  2007  80.653 33390141  36319.24
```
Relational operators are logical expressions that will give you either a TRUE or FALSE output. 
* a == b means	a is equal to b
* a != b means 	a is not equal to b.
* a > b	means a is greater than b.
* a < b	means a is less than b.
* a >= b	means a is greater than or equal to b.
* a <= b	means a is less than or equal to b.
* a %in% b	means a is an element in b

* a | b means a or b
* a & b means a and b


```r
#testing these out
4 %in% c(1, 2, 3, 4, 5)
```

```
## [1] TRUE
```

```r
## Canada entries before 1970
filter(gapminder, country == "Canada", year <1970)
```

```
## # A tibble: 4 x 6
##   country continent  year lifeExp      pop gdpPercap
##    <fctr>    <fctr> <int>   <dbl>    <int>     <dbl>
## 1  Canada  Americas  1952   68.75 14785584  11367.16
## 2  Canada  Americas  1957   69.96 17010154  12489.95
## 3  Canada  Americas  1962   71.30 18985849  13462.49
## 4  Canada  Americas  1967   72.13 20819767  16076.59
```

```r
## Canada and Kenya entries after 1985
filter(gapminder, country %in% c("Canada", "Kenya"), year>1985)
```

```
## # A tibble: 10 x 6
##    country continent  year lifeExp      pop gdpPercap
##     <fctr>    <fctr> <int>   <dbl>    <int>     <dbl>
##  1  Canada  Americas  1987  76.860 26549700 26626.515
##  2  Canada  Americas  1992  77.950 28523502 26342.884
##  3  Canada  Americas  1997  78.610 30305843 28954.926
##  4  Canada  Americas  2002  79.770 31902268 33328.965
##  5  Canada  Americas  2007  80.653 33390141 36319.235
##  6   Kenya    Africa  1987  59.339 21198082  1361.937
##  7   Kenya    Africa  1992  59.285 25020539  1341.922
##  8   Kenya    Africa  1997  54.407 28263827  1360.485
##  9   Kenya    Africa  2002  50.992 31386842  1287.515
## 10   Kenya    Africa  2007  54.110 35610177  1463.249
```

```r
## Canada and Kenya entries from the 1960s
filter(gapminder, country %in% c("Canada", "Kenya"), year %in% 1960:1969)
```

```
## # A tibble: 4 x 6
##   country continent  year lifeExp      pop  gdpPercap
##    <fctr>    <fctr> <int>   <dbl>    <int>      <dbl>
## 1  Canada  Americas  1962  71.300 18985849 13462.4855
## 2  Canada  Americas  1967  72.130 20819767 16076.5880
## 3   Kenya    Africa  1962  47.949  8678557   896.9664
## 4   Kenya    Africa  1967  50.654 10191512  1056.7365
```

```r
## Select only continent and country rows
select(gapminder, continent, country)
```

```
## # A tibble: 1,704 x 2
##    continent     country
##       <fctr>      <fctr>
##  1      Asia Afghanistan
##  2      Asia Afghanistan
##  3      Asia Afghanistan
##  4      Asia Afghanistan
##  5      Asia Afghanistan
##  6      Asia Afghanistan
##  7      Asia Afghanistan
##  8      Asia Afghanistan
##  9      Asia Afghanistan
## 10      Asia Afghanistan
## # ... with 1,694 more rows
```
Next is testing piping, which is where you chain together functions to run code efficiently. 


```r
#Select country, year, and GDP per capita for Canada and Kenya entries in the 1960s
gapminder %>%
  filter(country %in% c("Canada", "Kenya"), year %in%
           1960:1969) %>%
  select(country, year, gdpPercap)
```

```
## # A tibble: 4 x 3
##   country  year  gdpPercap
##    <fctr> <int>      <dbl>
## 1  Canada  1962 13462.4855
## 2  Canada  1967 16076.5880
## 3   Kenya  1962   896.9664
## 4   Kenya  1967  1056.7365
```

```r
#Take all countries in Europe that have a GPD per capita greater than 10000, and select all variables except gdpPercap
gapminder %>%
  filter(continent=="Europe", gdpPercap>10000) %>%
  select(-gdpPercap)
```

```
## # A tibble: 214 x 5
##    country continent  year lifeExp     pop
##     <fctr>    <fctr> <int>   <dbl>   <int>
##  1 Austria    Europe  1962  69.540 7129864
##  2 Austria    Europe  1967  70.140 7376998
##  3 Austria    Europe  1972  70.630 7544201
##  4 Austria    Europe  1977  72.170 7568430
##  5 Austria    Europe  1982  73.180 7574613
##  6 Austria    Europe  1987  74.940 7578903
##  7 Austria    Europe  1992  76.040 7914969
##  8 Austria    Europe  1997  77.510 8069876
##  9 Austria    Europe  2002  78.980 8148312
## 10 Austria    Europe  2007  79.829 8199783
## # ... with 204 more rows
```

```r
#Order the data frame by year, then descending by life expectancy. Rearrange data frame so year comes first then life expectancy
gapminder %>%
  arrange(pop, desc(lifeExp)) %>%
  select(year, lifeExp, everything())
```

```
## # A tibble: 1,704 x 6
##     year lifeExp               country continent   pop gdpPercap
##    <int>   <dbl>                <fctr>    <fctr> <int>     <dbl>
##  1  1952  46.471 Sao Tome and Principe    Africa 60011  879.5836
##  2  1957  48.945 Sao Tome and Principe    Africa 61325  860.7369
##  3  1952  34.812              Djibouti    Africa 63149 2669.5295
##  4  1962  51.893 Sao Tome and Principe    Africa 65345 1071.5511
##  5  1967  54.425 Sao Tome and Principe    Africa 70787 1384.8406
##  6  1957  37.328              Djibouti    Africa 71851 2864.9691
##  7  1972  56.480 Sao Tome and Principe    Africa 76595 1532.9853
##  8  1977  58.550 Sao Tome and Principe    Africa 86796 1737.5617
##  9  1962  39.693              Djibouti    Africa 89898 3020.9893
## 10  1982  60.351 Sao Tome and Principe    Africa 98593 1890.2181
## # ... with 1,694 more rows
```

You can use mutate to create new variables that are calculated from other variables within the data frame. 

```r
mutate(gapminder, 
       gdp = gdpPercap * pop, 
       gdpBill = round(gdp/1000000000, 1))
```

```
## # A tibble: 1,704 x 8
##        country continent  year lifeExp      pop gdpPercap         gdp
##         <fctr>    <fctr> <int>   <dbl>    <int>     <dbl>       <dbl>
##  1 Afghanistan      Asia  1952  28.801  8425333  779.4453  6567086330
##  2 Afghanistan      Asia  1957  30.332  9240934  820.8530  7585448670
##  3 Afghanistan      Asia  1962  31.997 10267083  853.1007  8758855797
##  4 Afghanistan      Asia  1967  34.020 11537966  836.1971  9648014150
##  5 Afghanistan      Asia  1972  36.088 13079460  739.9811  9678553274
##  6 Afghanistan      Asia  1977  38.438 14880372  786.1134 11697659231
##  7 Afghanistan      Asia  1982  39.854 12881816  978.0114 12598563401
##  8 Afghanistan      Asia  1987  40.822 13867957  852.3959 11820990309
##  9 Afghanistan      Asia  1992  41.674 16317921  649.3414 10595901589
## 10 Afghanistan      Asia  1997  41.763 22227415  635.3414 14121995875
## # ... with 1,694 more rows, and 1 more variables: gdpBill <dbl>
```

Summarize reduces the tibble to summary statistics, which is very useful when used with group_by

```r
gapminder %>% 
    group_by(country) %>% 
    summarize(mean_pop=mean(pop), sd_pop=sd(pop))
```

```
## # A tibble: 142 x 3
##        country   mean_pop     sd_pop
##         <fctr>      <dbl>      <dbl>
##  1 Afghanistan 15823715.4  7114583.5
##  2     Albania  2580249.2   828585.5
##  3     Algeria 19875406.2  8613355.3
##  4      Angola  7309390.1  2672280.6
##  5   Argentina 28602239.9  7546609.0
##  6   Australia 14649312.5  3915203.0
##  7     Austria  7583298.4   437660.0
##  8     Bahrain   373913.2   210893.3
##  9  Bangladesh 90755395.3 34711660.7
## 10     Belgium  9725118.7   520635.9
## # ... with 132 more rows
```

```r
#Find the minimum GDP per capita experienced by each country
gapminder %>%
  group_by(country) %>%
  summarize(minGDP = min(gdpPercap))
```

```
## # A tibble: 142 x 2
##        country     minGDP
##         <fctr>      <dbl>
##  1 Afghanistan   635.3414
##  2     Albania  1601.0561
##  3     Algeria  2449.0082
##  4      Angola  2277.1409
##  5   Argentina  5911.3151
##  6   Australia 10039.5956
##  7     Austria  6137.0765
##  8     Bahrain  9867.0848
##  9  Bangladesh   630.2336
## 10     Belgium  8343.1051
## # ... with 132 more rows
```

```r
#Find how many years of records does each country have
gapminder %>%
  group_by(country) %>%
  summarize(n_distinct(year))
```

```
## # A tibble: 142 x 2
##        country `n_distinct(year)`
##         <fctr>              <int>
##  1 Afghanistan                 12
##  2     Albania                 12
##  3     Algeria                 12
##  4      Angola                 12
##  5   Argentina                 12
##  6   Australia                 12
##  7     Austria                 12
##  8     Bahrain                 12
##  9  Bangladesh                 12
## 10     Belgium                 12
## # ... with 132 more rows
```

```r
#Within Asia, what are the min and max life expectancies experienced in each year?
gapminder %>% 
    filter(continent=="Asia") %>% 
    group_by(year) %>% 
    summarize(minexp=min(lifeExp),
              maxexp=max(lifeExp))
```

```
## # A tibble: 12 x 3
##     year minexp maxexp
##    <int>  <dbl>  <dbl>
##  1  1952 28.801 65.390
##  2  1957 30.332 67.840
##  3  1962 31.997 69.390
##  4  1967 34.020 71.430
##  5  1972 36.088 73.420
##  6  1977 31.220 75.380
##  7  1982 39.854 77.110
##  8  1987 40.822 78.670
##  9  1992 41.674 79.360
## 10  1997 41.763 80.690
## 11  2002 42.129 82.000
## 12  2007 43.828 82.603
```
If want additional introduction to dplyr, 
*[Stats 545 Intro Part 1](http://stat545.com/block009_dplyr-intro.html)
*[Stats 545 Intro Part 2](http://stat545.com/block010_dplyr-end-single-table.html)

# Lecture 6
This lecture is about ggplot2. 


```r
#load library
library(ggplot2)
library(gapminder)

#create first layer that contains dataset and an indication of what variables will go to what scale
p <- ggplot(gapminder, aes(x=year, y=lifeExp))

#this is blank as you need to layer on points and asthetics which is done using a "+"
p + geom_point(alpha=0.25)
```

![](Lecture_Notes_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

```r
#make a scatterplot of GDP per capita and life expectancy
p2 <- ggplot(gapminder, aes(x=gdpPercap, y=lifeExp))
p2+ geom_point(aes(size=year, color=continent, alpha=1/20))
```

![](Lecture_Notes_files/figure-html/unnamed-chunk-7-2.png)<!-- -->

```r
#log transformation
p3 <- p2 + geom_point() + scale_x_log10()

#Colour log transformation by continent and set transparency and size
p4 <- p3 + geom_point(aes(color = continent), alpha=(1/3), size=3)

#Add a smooth line without standard error and using lm
p4 + geom_smooth(method=lm, se = FALSE)
```

![](Lecture_Notes_files/figure-html/unnamed-chunk-7-3.png)<!-- -->

```r
#Take advantage of facetting (factoring)
p4 + facet_wrap(~continent)
```

![](Lecture_Notes_files/figure-html/unnamed-chunk-7-4.png)<!-- -->

```r
##subsetting: looking at 4 countries
jCountries <- c("Canada", "Kenya", "France", "India")

ggplot(subset(gapminder, country %in% jCountries),
       aes(x = year, y = lifeExp, color= country)) + geom_line() +   geom_point()
```

![](Lecture_Notes_files/figure-html/unnamed-chunk-7-5.png)<!-- -->

```r
#Make a plot of year (x) vs lifeExp (y), with points coloured by continent. Then, fit a regression line to each continent, without the error bars. If you can, try piping the data frame into the ggplot function
q <- ggplot(gapminder, aes(x=year, y=lifeExp, color=continent))

q + geom_point()+ geom_smooth(method=lm, se = FALSE)
```

![](Lecture_Notes_files/figure-html/unnamed-chunk-7-6.png)<!-- -->

```r
##Make a plot of year (x) vs lifeExp (y), facetted by continent. Then, fit a smoother through the data for each continent, without the error bars. Choose a span that you feel is appropriate.
q + geom_point()+ geom_smooth(method=lm, se = FALSE) + facet_wrap(~continent)
```

![](Lecture_Notes_files/figure-html/unnamed-chunk-7-7.png)<!-- -->

```r
##Plot the population over time (year) using lines, so that each country has its own line. Add alpha transparency to your liking.Add points to the plot in Exercise 7.
r <- ggplot(gapminder, aes(x=year, y=pop, group=country))
r + geom_line(alpha=1/3) 
```

![](Lecture_Notes_files/figure-html/unnamed-chunk-7-8.png)<!-- -->

```r
r2 <-r + geom_line(alpha=1/3)
r2 + geom_point() 
```

![](Lecture_Notes_files/figure-html/unnamed-chunk-7-9.png)<!-- -->

#  Lecture 7

```r
# Regression curves
# Regression analysis fits some curve through the data, representing the mean of Y given the specified X value. Sometimes you assume a line (linear model) or can apply a general curve (i.e. a smoother)

vc1 <- ggplot(gapminder, aes(year, lifeExp)) +
    geom_point() 
vc1 + geom_smooth(se=FALSE)
```

```
## `geom_smooth()` using method = 'gam'
```

![](Lecture_Notes_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

```r
# Exercise 1: Make a plot of year (x) vs lifeExp (y), with points coloured by continent. Then, to that same plot, fit a straight regression line to each continent, without the error bars. If you can, try piping the data frame into the ggplot function

ggplot(gapminder, aes(year, lifeExp, colour=continent)) +
  geom_point() +  # need this to show points on graph
  geom_smooth(method= "lm", se=FALSE)
```

![](Lecture_Notes_files/figure-html/unnamed-chunk-8-2.png)<!-- -->

```r
# Facetting separates data from each group into its own “mini plot”, called a panel. These panels are arranged next to each otherfor easier comparison. There are two facetting functions in ggplot2: (1) facet_wrap: 1D facetting and (2) facet_grid: 2D facetting. Example of (1):

ggplot(gapminder, aes(gdpPercap, lifeExp)) +
    facet_wrap(~ continent) +
    geom_point()
```

![](Lecture_Notes_files/figure-html/unnamed-chunk-8-3.png)<!-- -->

```r
# Exercise 2: Make a plot of year (x) vs lifeExp (y), facetted by continent. Then, fit a smoother through the data for each continent, without the error bars. Choose a span that you feel is appropriate. NOTE: A small span results in a more jagged curve; a larger one results in a smoother curve. You have to find one that fits your data

ggplot(gapminder, aes(year, lifeExp)) +
  geom_point() +
  facet_wrap(~continent)+
  geom_smooth(method = "lm", se=FALSE, span=1)
```

![](Lecture_Notes_files/figure-html/unnamed-chunk-8-4.png)<!-- -->

```r
# Facet_grid allows you to add a third variable so each row corresponds to one grouping and each column corresponds to another grouping. facet_grid(var 1~ var 2) Example 3: Look at continent and population size by “small” (<=7,000,000 population) and “large” (>7,000,000 population) countries. 

vc2 <- gapminder %>% 
    mutate(size=ifelse(pop > 7000000, "large", "small")) %>%     ggplot(aes(gdpPercap, lifeExp)) +
    facet_grid(size ~ continent) 

vc2 + geom_point(aes(colour=year))
```

![](Lecture_Notes_files/figure-html/unnamed-chunk-8-5.png)<!-- -->

```r
# Connect the dots with geom_line (connect dots left-to-right) or geom_path (conects dots in the order they appear within the data frame). With these geoms, you must specify group=VARIABLE in your aesthetics (aes function), otherwise ggplot won’t distinguish between groups. Example:
ggplot(gapminder, aes(year, lifeExp, group=country)) +
    geom_line(alpha=0.2)
```

![](Lecture_Notes_files/figure-html/unnamed-chunk-8-6.png)<!-- -->

```r
# geom_path is typically used when a “time” variable is not shown on an axis. For example, let’s look at a scatterplot of pop vs. gdpPercap of Afghanistan, and let’s “connect the dots” in the order of time. Example:

gapminder %>%
    filter(country=="Afghanistan") %>% 
    arrange(year) %>% 
    ggplot(aes(pop, gdpPercap)) +
    geom_point() +
    geom_path()
```

![](Lecture_Notes_files/figure-html/unnamed-chunk-8-7.png)<!-- -->

```r
# Example 4:  Plot the population over time (year) using lines, so that each country has its own line. Colour by  gdpPercap. Add alpha transparency to your liking. Fit it to a log 10 scale.

##remember group is essential for this!

ggplot(gapminder, aes(year, pop, group=country)) + 
  geom_line(aes(colour=gdpPercap), alpha=0.2) +
  geom_point() +
  scale_y_log10()
```

![](Lecture_Notes_files/figure-html/unnamed-chunk-8-8.png)<!-- -->

# Lecture 8
## Modeling
First we will look at linear regression using the **lm()** function.

```r
# create a linear model
fit1 <- lm(lifeExp ~ log(gdpPercap), data=gapminder)
fit1
```

```
## 
## Call:
## lm(formula = lifeExp ~ log(gdpPercap), data = gapminder)
## 
## Coefficients:
##    (Intercept)  log(gdpPercap)  
##         -9.101           8.405
```

```r
# can make predictions using the model. Remember if you don’t specify new data, it will make predictions using the existing X values.
predict(fit1) %>% head
```

```
##        1        2        3        4        5        6 
## 46.86506 47.30012 47.62400 47.45579 46.42835 46.93666
```

```r
# can plot again the original x values
qplot(log(gapminder$gdpPercap), predict(fit1))
```

![](Lecture_Notes_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

```r
# can predict with new data as long as the data frame has the same column names as the x values.
(my_newdata <- data.frame(gdpPercap=c(100, 547, 289)))
```

```
##   gdpPercap
## 1       100
## 2       547
## 3       289
```

```r
predict(fit1, newdata=my_newdata)
```

```
##        1        2        3 
## 29.60596 43.88854 38.52591
```

```r
predict(fit1, newdata=filter(gapminder, country=="Canada"))
```

```
##        1        2        3        4        5        6        7        8 
## 69.38986 70.18158 70.81182 72.30336 73.69461 74.97451 75.27641 76.54409 
##        9       10       11       12 
## 76.45408 77.24871 78.43120 79.15337
```

```r
# can extract model characteristics
  #model coefficients
  coef(fit1)
```

```
##    (Intercept) log(gdpPercap) 
##      -9.100889       8.405085
```

```r
  #residuals (looking at the first 6 and then plotting all)
  resid(fit1) %>% head
```

```
##          1          2          3          4          5          6 
## -18.064063 -16.968123 -15.627000 -13.435788 -10.340352  -8.498661
```

```r
  qplot(log(gapminder$gdpPercap), resid(fit1)) +
    geom_hline(yintercept=0, linetype="dashed", colour="red")
```

![](Lecture_Notes_files/figure-html/unnamed-chunk-9-2.png)<!-- -->

```r
  #lots of information can be determined using summary, such as p-values and standard errors
  summary(fit1)
```

```
## 
## Call:
## lm(formula = lifeExp ~ log(gdpPercap), data = gapminder)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -32.778  -4.204   1.212   4.658  19.285 
## 
## Coefficients:
##                Estimate Std. Error t value Pr(>|t|)    
## (Intercept)     -9.1009     1.2277  -7.413 1.93e-13 ***
## log(gdpPercap)   8.4051     0.1488  56.500  < 2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 7.62 on 1702 degrees of freedom
## Multiple R-squared:  0.6522,	Adjusted R-squared:  0.652 
## F-statistic:  3192 on 1 and 1702 DF,  p-value: < 2.2e-16
```

```r
  #can extract specifics from the summary
  sum1 <- summary(fit1)
  
    #r-squared and r-square adjusted
    sum1$r.square
```

```
## [1] 0.6522466
```

```r
    sum1$adj.r.squared
```

```
## [1] 0.6520423
```

```r
    #estimated standard deviation of the random error term
    sum1$sigma
```

```
## [1] 7.619535
```

###Other Models:
1.  generalized linear models (such as logistic regression). For this, you use the **glm()** function. It is quite similar to lm, except you need to specify what model to run using the family argument. Syntax includes:

    * Poisson regression:
glm(y ~ x1 + x2 + ... + xp, family=poisson, data=your_data_frame)

    * Logistic (aka Binomial) regression:
glm(y ~ x1 + x2 + ... + xp, family=binomial, data=your_data_frame)

2. Generalized) Mixed Effects Models:
Two R packages are available: lme4 and nlme.
Check out [this](https://stats.stackexchange.com/questions/5344/how-to-choose-nlme-or-lme4-r-library-for-mixed-effects-models) discussion for a comparison of the two packages.

3. Kernel smoothing (i.e. fitting a “smoother”):
Check out the loess function.

4. Generalized Additive Models:
The gam function in either the gam package or mgcv package.

5. Robust linear regression: 
The rlm function in the MASS package is your friend

## More dplyr
One of the most powerful functions is using **mutate()** with grouped tibble. 

```r
# Exercise 1: Calculate the growth in population since the first year on record for each country
gapminder %>%
  group_by(country) %>%
  mutate(pop_growth = pop-pop[1])
```

```
## # A tibble: 1,704 x 7
## # Groups:   country [142]
##        country continent  year lifeExp      pop gdpPercap pop_growth
##         <fctr>    <fctr> <int>   <dbl>    <int>     <dbl>      <int>
##  1 Afghanistan      Asia  1952  28.801  8425333  779.4453          0
##  2 Afghanistan      Asia  1957  30.332  9240934  820.8530     815601
##  3 Afghanistan      Asia  1962  31.997 10267083  853.1007    1841750
##  4 Afghanistan      Asia  1967  34.020 11537966  836.1971    3112633
##  5 Afghanistan      Asia  1972  36.088 13079460  739.9811    4654127
##  6 Afghanistan      Asia  1977  38.438 14880372  786.1134    6455039
##  7 Afghanistan      Asia  1982  39.854 12881816  978.0114    4456483
##  8 Afghanistan      Asia  1987  40.822 13867957  852.3959    5442624
##  9 Afghanistan      Asia  1992  41.674 16317921  649.3414    7892588
## 10 Afghanistan      Asia  1997  41.763 22227415  635.3414   13802082
## # ... with 1,694 more rows
```

```r
# What about growth compared to 1972?
gapminder %>%
  group_by(country) %>%
  mutate(pop_growth = pop-pop[year==1972])
```

```
## # A tibble: 1,704 x 7
## # Groups:   country [142]
##        country continent  year lifeExp      pop gdpPercap pop_growth
##         <fctr>    <fctr> <int>   <dbl>    <int>     <dbl>      <int>
##  1 Afghanistan      Asia  1952  28.801  8425333  779.4453   -4654127
##  2 Afghanistan      Asia  1957  30.332  9240934  820.8530   -3838526
##  3 Afghanistan      Asia  1962  31.997 10267083  853.1007   -2812377
##  4 Afghanistan      Asia  1967  34.020 11537966  836.1971   -1541494
##  5 Afghanistan      Asia  1972  36.088 13079460  739.9811          0
##  6 Afghanistan      Asia  1977  38.438 14880372  786.1134    1800912
##  7 Afghanistan      Asia  1982  39.854 12881816  978.0114    -197644
##  8 Afghanistan      Asia  1987  40.822 13867957  852.3959     788497
##  9 Afghanistan      Asia  1992  41.674 16317921  649.3414    3238461
## 10 Afghanistan      Asia  1997  41.763 22227415  635.3414    9147955
## # ... with 1,694 more rows
```

* Vectorized Functions: These take a vector, and operate on each component independently to return a vector of the same length. In other words, they work element-wise.
    * Examples are cos, sin, log, exp, round.
    * We don’t need to group_by in order to mutate with these.

*Aggregate Functions: These take a vector, and return a vector of length 1 – as if “aggregating” the values in the vector into a single value.
    * Examples are mean, sd, length, typeof.
    * We use these in dplyr’s summarise function.

* Window Functions: these take a vector, and return a vector of the same length that depends on other values in the vector.
  * Examples are lag, rank, cumsum.
  * See the window-functions vignette for the dplyr package.



* [ggplot2 cheatsheet](https://www.rstudio.com/wp-content/uploads/2015/03/ggplot2-cheatsheet.pdf)
* The broom package makes the output from statistical models in R less cryptic. Check out its vignette.
dplyr has a window-functions vignette that explains about window functions. Useful for grouped mutate.
* There are “complete themes” that come with ggplot2.
* For scales in ggplot, check out this tutorial by Hadley Wickham.
