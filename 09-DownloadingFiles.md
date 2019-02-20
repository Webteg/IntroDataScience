Downloading Files
================

-   [First: File System](#first-file-system)
    -   [Files and directories](#files-and-directories)
-   [Downloading Files](#downloading-files)
    -   [Reproducible Research](#reproducible-research)

First: File System
------------------

Where am I?

``` r
getwd()
```

    ## [1] "/Users/rafaelsantos/SYNC/OneDrive/INPE/CAP-394 Data Science/R"

Change working directory

``` r
orig <- getwd()
setwd("..")
getwd()
```

    ## [1] "/Users/rafaelsantos/SYNC/OneDrive/INPE/CAP-394 Data Science"

``` r
setwd("/Users/rafaelsantos/SYNC/OneDrive/")
getwd()
```

    ## [1] "/Users/rafaelsantos/SYNC/OneDrive"

``` r
setwd(orig)
getwd()
```

    ## [1] "/Users/rafaelsantos/SYNC/OneDrive/INPE/CAP-394 Data Science/R"

<b>This may reduce portability and compromise reproducibility!</b>

### Files and directories

``` r
file.exists("Data/Taubate.csv")
```

    ## [1] TRUE

``` r
file.exists("Data/TruthOrConsequences.csv")
```

    ## [1] FALSE

``` r
list.files("Data")
```

    ## [1] "SomeMixedData.R"     "Taubate-Fixed.csv"   "Taubate-Fixed.R"    
    ## [4] "Taubate-Missing.csv" "Taubate.csv"

``` r
file.info("Data/Taubate.csv")
```

    ##                  size isdir mode               mtime               ctime
    ## Data/Taubate.csv  829 FALSE  755 2017-06-26 15:56:46 2019-02-19 22:27:56
    ##                                atime uid gid        uname grname
    ## Data/Taubate.csv 2019-02-19 22:37:05 501  20 rafaelsantos  staff

``` r
tam <- file.info("Data/Taubate.csv")$size
tam
```

    ## [1] 829

``` r
age <- Sys.time()-(file.info("Data/Taubate.csv")$ctime)
age
```

    ## Time difference of 25.82609 mins

``` r
if (age > 7)
  {
  "Older than a week!"
  }
```

    ## [1] "Older than a week!"

Conditional directory creation:

``` r
file.exists("../TempData")
```

    ## [1] TRUE

``` r
if (!file.exists("../TempData"))
  {
  dir.create("../TempData")  
  }
file.exists("../TempData")
```

    ## [1] TRUE

``` r
# Do something with directory...
aVector <- c(1,2,3)
dump("aVector", file = "../TempData/aVector.R")
# CAREFUL HERE
unlink("../TempData", recursive = TRUE, force = TRUE)
```

Downloading Files
-----------------

``` r
taubateURL <- "https://raw.githubusercontent.com/rafaeldcsantos/IntroDataScience/master/Data/Taubate.csv"
dir.create("../TempData")  
download.file(taubateURL,destfile = "../TempData/Taubate.csv",method="curl")
if (file.exists("../TempData/Taubate.csv"))
  {
  tam <- file.info("../TempData/Taubate.csv")$size
  paste("File downloaded, ",tam," bytes")
  } else
  {
  "Error downloading file!"
  }
```

    ## [1] "File downloaded,  829  bytes"

Nasty stuff about ways different OSs works, timeouts, etc. will not be covered.

### Reproducible Research

Remember to store the URL and the date you've downloaded the file.

Consider that results may be significantly different from what you'll provide!
