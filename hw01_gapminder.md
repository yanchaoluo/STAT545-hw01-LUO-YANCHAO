hw01\_gapminder
================
yanchao

Load packages"gapminder"
------------------------

``` r
library(gapminder)
##First time should install "gapminder" using R code: Install.pakages("gapminder")
```

Display the structure of "gapminder"
------------------------------------

``` r
str(gapminder)
```

    ## Classes 'tbl_df', 'tbl' and 'data.frame':    1704 obs. of  6 variables:
    ##  $ country  : Factor w/ 142 levels "Afghanistan",..: 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ continent: Factor w/ 5 levels "Africa","Americas",..: 3 3 3 3 3 3 3 3 3 3 ...
    ##  $ year     : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
    ##  $ lifeExp  : num  28.8 30.3 32 34 36.1 ...
    ##  $ pop      : int  8425333 9240934 10267083 11537966 13079460 14880372 12881816 13867957 16317921 22227415 ...
    ##  $ gdpPercap: num  779 821 853 836 740 ...

Print gapminder to screen
-------------------------

``` r
class(gapminder)
```

    ## [1] "tbl_df"     "tbl"        "data.frame"

Only see head or tail of the data
---------------------------------

``` r
head(gapminder)
```

    ##       country continent year lifeExp      pop gdpPercap
    ## 1 Afghanistan      Asia 1952  28.801  8425333  779.4453
    ## 2 Afghanistan      Asia 1957  30.332  9240934  820.8530
    ## 3 Afghanistan      Asia 1962  31.997 10267083  853.1007
    ## 4 Afghanistan      Asia 1967  34.020 11537966  836.1971
    ## 5 Afghanistan      Asia 1972  36.088 13079460  739.9811
    ## 6 Afghanistan      Asia 1977  38.438 14880372  786.1134

``` r
tail(gapminder)
```

    ##       country continent year lifeExp      pop gdpPercap
    ## 1699 Zimbabwe    Africa 1982  60.363  7636524  788.8550
    ## 1700 Zimbabwe    Africa 1987  62.351  9216418  706.1573
    ## 1701 Zimbabwe    Africa 1992  60.377 10704340  693.4208
    ## 1702 Zimbabwe    Africa 1997  46.809 11404948  792.4500
    ## 1703 Zimbabwe    Africa 2002  39.989 11926563  672.0386
    ## 1704 Zimbabwe    Africa 2007  43.487 12311143  469.7093

Query basic info on a data frame
--------------------------------

``` r
names(gapminder)
```

    ## [1] "country"   "continent" "year"      "lifeExp"   "pop"       "gdpPercap"

``` r
nrow(gapminder)
```

    ## [1] 1704

``` r
dim(gapminder)
```

    ## [1] 1704    6

``` r
length(gapminder)
```

    ## [1] 6

``` r
ncol(gapminder)
```

    ## [1] 6

Statistical overview
--------------------

``` r
summary(gapminder)
```

    ##         country        continent        year         lifeExp     
    ##  Afghanistan:  12   Africa  :624   Min.   :1952   Min.   :23.60  
    ##  Albania    :  12   Americas:300   1st Qu.:1966   1st Qu.:48.20  
    ##  Algeria    :  12   Asia    :396   Median :1980   Median :60.71  
    ##  Angola     :  12   Europe  :360   Mean   :1980   Mean   :59.47  
    ##  Argentina  :  12   Oceania : 24   3rd Qu.:1993   3rd Qu.:70.85  
    ##  Australia  :  12                  Max.   :2007   Max.   :82.60  
    ##  (Other)    :1632                                                
    ##       pop              gdpPercap       
    ##  Min.   :6.001e+04   Min.   :   241.2  
    ##  1st Qu.:2.794e+06   1st Qu.:  1202.1  
    ##  Median :7.024e+06   Median :  3531.8  
    ##  Mean   :2.960e+07   Mean   :  7215.3  
    ##  3rd Qu.:1.959e+07   3rd Qu.:  9325.5  
    ##  Max.   :1.319e+09   Max.   :113523.1  
    ## 

Plot interested data
--------------------

``` r
plot( lifeExp  ~ pop, gapminder)
```

![](hw01_gapminder_files/figure-markdown_github-ascii_identifiers/unnamed-chunk-7-1.png)

``` r
plot( lifeExp ~ gdpPercap, gapminder)
```

![](hw01_gapminder_files/figure-markdown_github-ascii_identifiers/unnamed-chunk-8-1.png) \#\# Transform variable

``` r
plot(lifeExp ~ log(gdpPercap), gapminder)
```

![](hw01_gapminder_files/figure-markdown_github-ascii_identifiers/unnamed-chunk-9-1.png)

``` r
## these two variables seem to be more liear
```

Look at the variables inside a data frame
-----------------------------------------

``` r
head(gapminder$pop)
```

    ## [1]  8425333  9240934 10267083 11537966 13079460 14880372

``` r
summary(gapminder$pop)
```

    ##      Min.   1st Qu.    Median      Mean   3rd Qu.      Max. 
    ## 6.001e+04 2.794e+06 7.024e+06 2.960e+07 1.959e+07 1.319e+09

``` r
hist(gapminder$pop)
```

![](hw01_gapminder_files/figure-markdown_github-ascii_identifiers/unnamed-chunk-10-1.png)

``` r
### If the variables are categorical
table(gapminder$continent)
```

    ## 
    ##   Africa Americas     Asia   Europe  Oceania 
    ##      624      300      396      360       24

``` r
barplot(table(gapminder$continent))
```

![](hw01_gapminder_files/figure-markdown_github-ascii_identifiers/unnamed-chunk-10-2.png)

``` r
levels(gapminder$continent)
```

    ## [1] "Africa"   "Americas" "Asia"     "Europe"   "Oceania"

``` r
nlevels(gapminder$continent)
```

    ## [1] 5

ggplot of the data
------------------

### Comparison of the relationship between gdp per cap and life expectation

``` r
library(tidyverse)
```

    ## Loading tidyverse: ggplot2
    ## Loading tidyverse: tibble
    ## Loading tidyverse: tidyr
    ## Loading tidyverse: readr
    ## Loading tidyverse: purrr
    ## Loading tidyverse: dplyr

    ## Conflicts with tidy packages ----------------------------------------------

    ## filter(): dplyr, stats
    ## lag():    dplyr, stats

``` r
p <- ggplot(filter(gapminder, continent != "Oceania"),
            aes(x = gdpPercap, y = lifeExp)) 
p <- p + scale_x_log10() 
p + geom_point() 
```

![](hw01_gapminder_files/figure-markdown_github-ascii_identifiers/unnamed-chunk-11-1.png)

``` r
p + geom_point(aes(color = continent)) 
```

![](hw01_gapminder_files/figure-markdown_github-ascii_identifiers/unnamed-chunk-11-2.png)

``` r
p + geom_point(alpha = (1/3), size = 3) + geom_smooth(lwd = 3, se = FALSE)
```

    ## `geom_smooth()` using method = 'gam'

![](hw01_gapminder_files/figure-markdown_github-ascii_identifiers/unnamed-chunk-11-3.png)

``` r
p + geom_point(alpha = (1/3), size = 3) + facet_wrap(~ continent) +
  geom_smooth(lwd = 1.5, se = FALSE)
```

    ## `geom_smooth()` using method = 'loess'

![](hw01_gapminder_files/figure-markdown_github-ascii_identifiers/unnamed-chunk-11-4.png)

### Comparison of the relationship between population and life expectation

``` r
p <- ggplot(filter(gapminder, continent != "Oceania"),
            aes(x = pop, y = lifeExp)) 
p <- p + scale_x_log10() 
p + geom_point() 
```

![](hw01_gapminder_files/figure-markdown_github-ascii_identifiers/unnamed-chunk-12-1.png)

``` r
p + geom_point(aes(color = continent)) 
```

![](hw01_gapminder_files/figure-markdown_github-ascii_identifiers/unnamed-chunk-12-2.png)

``` r
p + geom_point(alpha = (1/3), size = 3) + geom_smooth(lwd = 3, se = FALSE)
```

    ## `geom_smooth()` using method = 'gam'

![](hw01_gapminder_files/figure-markdown_github-ascii_identifiers/unnamed-chunk-12-3.png)

``` r
p + geom_point(alpha = (1/3), size = 3) + facet_wrap(~ continent) +
  geom_smooth(lwd = 1.5, se = FALSE)
```

    ## `geom_smooth()` using method = 'loess'

![](hw01_gapminder_files/figure-markdown_github-ascii_identifiers/unnamed-chunk-12-4.png)
