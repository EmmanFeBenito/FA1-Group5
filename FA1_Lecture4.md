FA1_Lecture4
================
Emmanuel Fe Benito
2026-02-01

### Exercise: Import heights2.csv

``` r
heights2 <- read_csv(file = "C:/Users/Emmanuel/Downloads/heights.csv")
```

    ## Rows: 1192 Columns: 6
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): sex, race
    ## dbl (4): earn, height, ed, age
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

### Exercise: Using prose, describe how the variables and observations are organised in each of the sample tables.

table1: This is a tidy dataset. Each row represents a unique observation
(a specific country in a specific year), and each variable has its own
dedicated column .

table2: Observations are scattered across multiple rows. A single
observation (country + year) is split into two rows: one for “cases” and
one for “population” .

table3: Two variables are combined into a single column. The rate column
contains both “cases” and “population” separated by a slash .

table4a: Some column names (1999 and 2000) are actually values of the
year variable rather than variable names themselves. It only shows
“cases” data.

table4b: Similar to table4a, the column names 1999 and 2000 are values
of the year variable, but this table specifically contains “population”
data

### Exercise: Use pivot_longer() to tidy table4b in a similar fashion. What is the difference between the code used to tidy table4a and table4b?

``` r
table4b %>% 
  pivot_longer(cols = c(`1999`, `2000`), names_to = "year", values_to = "population")
```

    ## # A tibble: 6 × 3
    ##   country     year  population
    ##   <chr>       <chr>      <dbl>
    ## 1 Afghanistan 1999    19987071
    ## 2 Afghanistan 2000    20595360
    ## 3 Brazil      1999   172006362
    ## 4 Brazil      2000   174504898
    ## 5 China       1999  1272915272
    ## 6 China       2000  1280428583

The only difference is the values_to argument. In table4a, the values
represent cases , whereas in table4b, the values represent population.

### Exercises: 1. Why does this code fail?

The code fails because the column names 1999 and 2000 start with
numbers. In R, these must be surrounded by backticks (`1999`) to be
recognized as column names. Without them, R looks for column objects
that do not exist.

### 2. Tidy the simple tibble below. Do you need to make it wider or longer? What are the variables?

``` r
tribble(
  ~pregnant, ~male, ~female,
  "yes",     NA,    10,
  "no",      20,    12
) %>%
  pivot_longer(cols = c(male, female), names_to = "sex", values_to = "count")
```

    ## # A tibble: 4 × 3
    ##   pregnant sex    count
    ##   <chr>    <chr>  <dbl>
    ## 1 yes      male      NA
    ## 2 yes      female    10
    ## 3 no       male      20
    ## 4 no       female    12

You need to make it longer because the values “male” and “female” are
currently column headers but should be values under a single sex
variable. The variables are pregnant, sex, and count.

### Exercise: Consider the two tibbles below. What is the key column? Without writing any code, can you predict how many rows and columns left_join(x,y) and left_join(y,x) will have?

Key Column: The key column is state.

left_join(x, y) Prediction: Rows: 3 (It keeps all rows from x: PA, TX,
NY). Columns: 3 (state, population, and capital).

      Note: PA will have an NA for capital because it isn't in table y.

left_join(y, x) Prediction: Rows: 4 (It keeps all rows from y: TX, CA,
NY, MI). Columns: 3 (state, capital, and population).

      Note: CA and MI will have NA for population because they aren't in table
