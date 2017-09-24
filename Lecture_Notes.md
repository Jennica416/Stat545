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
