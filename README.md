
<!-- README.md is generated from README.Rmd. Please edit that file -->

# lbr

<!-- badges: start -->
<!-- badges: end -->

**My personal tools for data wrangling and analysis, a collection of
random stuff, mostly relies on `tidyverse package` .**

## Installation

You can install the development version from
[GitHub](https://github.com/Lightbridge-AI/lbr) with:

``` r
# install.packages("devtools")
devtools::install_github("Lightbridge-AI/lbr")
```

## Read multiple CSV files from a directory

I want to use `readr::read_csv()` for multiple CSV files. So, I combine
`read_csv()` with `purrr::map()` to read from a directory path with a
little help of `utils`, `tools`, and `stringr` for file pattern
matching.

``` r
  library(lbr)

# Read form current working directory by default

  read_dir_csv()
  
# And file names are set to names of each data frame in a list
  
# Give a directory path
  read_dir_csv(path/to/dir)
  
# Also, can read from every sub-directory of given directory 
  read_dir_csv(path/to/dir, recursive = T)
  
# Can specify regular expression of file names to read
  read_dir_csv(file_pattern = "[:digit:]+\\.csv$")  # file name contains numbers
  
# If set strict_csv_ext = F and remove regex which require file name ending with .csv
# it might read other file type as well (if you like)
  read_dir_csv(file_pattern = "[:digit:]+", strict_csv_ext = F)
  
# If you want file names in snake_case (require snakecase package)
  read_dir_csv(snake_case = T)
```

## Plot correlation from data frame

**A wrapper around `corrplot::corrplot()` which accept data frame as
input.**

-   Can set p-value to exclude non-significant correlation out from the
    plot.

-   Correlation calculation method: “pearson”, “spearman” or “kendall”
    can be specified in `method_cor` argument.

-   `...` pass to arguments of **`corrplot::corrplot()`**

``` r
library(lbr)

# Plot correlation of numeric column (automatically filter only numeric for plot)

corrplot_df(iris)
```

<img src="man/figures/README-corrplot_df-1.png" width="100%" />

``` r
mtcars %>% 
  corrplot_df(method_plot = "circle", # specify graphic method of correlation
                method_cor = "pearson", # method of calculation of correlation
                type = "lower",         # display lower half of correlation plot
                sig.level = 0.01,       # p-value = 0.01
                insig = "pch"           # insignificant will be crossed out 
                )
```

<img src="man/figures/README-unnamed-chunk-2-1.png" width="100%" />

``` r
mtcars %>% 
  corrplot_df(method_plot = "number",   # Show correlation as number
                method_cor = "spearman",# Calculate correlation by "spearman" method
                type = "upper",         # display upper half of correlation plot
                sig.level = 0.05,       # p-value = 0.05
                insig = "blank"         # insignificant will be blank (default)
                )
```

<img src="man/figures/README-unnamed-chunk-3-1.png" width="100%" />
