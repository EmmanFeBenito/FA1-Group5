FA1_Lecture3
================
Emmanuel Fe Benito
2026-02-01

# 1.

``` r
diamonds %>%
  summarize(min_price = min(price))
```

    ## # A tibble: 1 × 1
    ##   min_price
    ##       <int>
    ## 1       326

``` r
diamonds %>%
  slice_min(price, n = 1) %>%
  select(price)
```

    ## # A tibble: 2 × 1
    ##   price
    ##   <int>
    ## 1   326
    ## 2   326

# 2.

``` r
diamonds %>%
  filter(x >= 1.5 * y) %>%
  count()
```

    ## # A tibble: 1 × 1
    ##       n
    ##   <int>
    ## 1    10

# 3.

``` r
diamonds %>%
  filter(color %in% c("D", "E", "F", "G")) %>%
  group_by(cut) %>%
  summarize(median_carat = median(carat))
```

    ## # A tibble: 5 × 2
    ##   cut       median_carat
    ##   <ord>            <dbl>
    ## 1 Fair              0.91
    ## 2 Good              0.72
    ## 3 Very Good         0.7 
    ## 4 Premium           0.71
    ## 5 Ideal             0.52
