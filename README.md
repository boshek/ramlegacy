Kshitiz Gupta
2018-11-09

<!-- README.md is generated from README.Rmd. Please edit that file -->
\# ramlegacy
============

[![lifecycle](https://img.shields.io/badge/lifecycle-experimental-orange.svg)](https://www.tidyverse.org/lifecycle/#experimental)

[![Build Status](https://travis-ci.com/kshtzgupta1/ramlegacy.svg?branch=master)](https://travis-ci.com/kshtzgupta1/ramlegacy)

[![Coverage status](https://codecov.io/gh/kshtzgupta1/ramlegacy/branch/master/graph/badge.svg)](https://codecov.io/github/kshtzgupta1/ramlegacy?branch=master)

[![AppVeyor Build Status](https://ci.appveyor.com/api/projects/status/github/kshtzgupta1/ramlegacy?branch=master&svg=true)](https://ci.appveyor.com/project/kshtzgupta1/ramlegacy)

-   **Authors**: Kshitiz Gupta, [Carl Boettiger](http://www.carlboettiger.info/)
-   **License**: [MIT](http://opensource.org/licenses/MIT)
-   [Package source code on Github](https://github.com/kshtzgupta1/ramlegacy)
-   [**Submit Bugs and feature requests**](https://github.com/kshtzgupta1/ramlegacy/issues)

`ramlegacy` is an R package that supports caching and reading in different versions of the RAM Legacy Stock Assessment Data Base, an online compilation of stock assessment results for commercially exploited marine populations from around the world. More information about the database can be found [here.](www.ramlegacy.org)

What does `ramlegacy` do?
-------------------------

-   Provides a function `download_ramlegacy`, to download all the available
    versions of the RAM Legacy Stock Assessment Excel Database as RDS objects. This way once a version has been downloaded it doesn't need to be re-downloaded for subsequent analysis.
-   Supports reading in the cached versions of the database through loading the package i.e. calling `library(ramlegacy)` and also by providing a function `load_ramlegacy` to load any specified version.
-   Provides a function `ram_dir()` to view the path where the downloaded database was saved.

Installation
------------

You can install the development version from [GitHub](https://github.com/) with:

``` r
install.packages("devtools")
#> Installing package into '/home/kshitiz/R/x86_64-pc-linux-gnu-library/3.4'
#> (as 'lib' is unspecified)
library(devtools)
install_github("kshtzgupta1/ramlegacy", message = F, warning = F)
#> Downloading GitHub repo kshtzgupta1/ramlegacy@master
#> 
#>   
   checking for file ‘/tmp/RtmprmcCUA/remotes3b813d6a5414/kshtzgupta1-ramlegacy-550e45c/DESCRIPTION’ ...
  
✔  checking for file ‘/tmp/RtmprmcCUA/remotes3b813d6a5414/kshtzgupta1-ramlegacy-550e45c/DESCRIPTION’
#> ─  preparing ‘ramlegacy’:
#> ✔  checking DESCRIPTION meta-information
#> 
  
─  checking for LF line-endings in source and make files and shell scripts
#> ─  checking for empty or unneeded directories
#> ─  building ‘ramlegacy_0.1.0.tar.gz’
#> 
  
   
#> 
#> Warning in readLines(f): incomplete final line found on '/home/
#> kshitiz/.Rprofile'
#> Installing package into '/home/kshitiz/R/x86_64-pc-linux-gnu-library/3.4'
#> (as 'lib' is unspecified)
#> Warning in i.p(...): installation of package '/tmp/RtmprmcCUA/
#> file3b81676beb12/ramlegacy_0.1.0.tar.gz' had non-zero exit status
```

Usage
-----

Please see the ramlegacy vignette for more detailed examples and additional package functionality.

Start by loading the package using `library`.

``` r
library(ramlegacy)
```

When `ramlegacy` is loaded for the first time after installation of the package calling `library(ramlegacy)` will prompt the user to download a version of the database using `download_ramlegacy()`. After downloading a version or multiple versions of the database the subsequent behavior of `library(ramlegacy)` will depend on which version/versions were downloaded and are present on disk as well as whether `library(ramlegacy)` is called in an interactive vs non-interactive session. For more details about this behavior please see the ramlegacy vignette.

### download\_ramlegacy

`download_ramlegacy()` downloads the specified version of **RAM Legacy Stock Assessment Excel Database** and then saves it as an RDS object in user’s application data directory as detected by the package. This location is also where `load_ramlegacy` will look for the downloaded database.

``` r
# downloads version 3.0
download_ramlegacy(version = "3.0")
```

If version is not specified then download\_ramlegacy defaults to downloading current latest version (4.3) :

``` r
# downloads current latest version 4.3
download_ramlegacy()
```

To ensure that the user is able to download the data in case www.ramlegacy.org is down, the function also supports downloading all the different versions of the database from a [backup location](www.github.com/kshtzgupta1/ramlegacy-assets/) :

``` r
# downloads version 1.0 from backup location if www.ramlegacy.org is down
download_ramlegacy(version = "4.3")
```

### load\_ramlegacy

After the specified version of the database has been downloaded through `download_ramlegacy`, in addition to calling `library(ramlegacy)` to read in the database we can call `load_ramlegacy()` to do the same thing. That is, calling `load_ramlegacy` makes all the dataframes present in the database become available in the user's global environment. Note that `load_ramlegacy()` does not support vectorization and can only load and read in one version at a time. If version is not specified then `load_ramlegacy` defaults to loading the latest version (currently 4.3) :

``` r
# load version 3.0
load_ramlegacy(version = "3.0")

# loads current latest version 4.3
load_ramlegacy()
```

### ram\_dir

To view the exact path where the database was downloaded and cached by `download_ramlegacy` you can run `ram_dir()` and specify the version inside it:

``` r
# downloads version 2.5
download_ramlegacy(version = "2.5")

# view the location where version 2.5 of the database was downloaded
ram_dir(vers = "2.5")
```
