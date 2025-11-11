# Week 7 Problem Set


## Assignment Introduction

This week we’ve been discussing tidy datasets. Please create a Quarto
document that matches the style and formatting that you see here. Once
your code is finalized, hide messages and warnings throughout the
document.

**Throughout this assignment, you will be creating many data frames.
Please show the first 5 lines of these data frames where appropriate.**

Commit your final `week7_PS.qmd` and `week7_PS.md` to the `problem_sets`
folder in your GitHub repository.

**Deadline**: 11/19/25 10pm

## Tidy Data and Data Joins

Load all necessary packages.

``` r
## add your code here
```

### Exercise 1

This exercise brings us back to the `ratdat` dataset to highlight what
working with real data can be like! You will need to download the
following three datasets from the course website: `ratdat_plots.csv`,
`ratdat_species.csv`, and `ratdat_surveys.csv`.

#### 1.1 Load the datasets into R as `ratdat_plots`, `ratdat_species`, and `ratdat_surveys`, respectively. Use some of the skills you’ve learned to inspect these datasets and write a short description of what you can glean so far (1-2 sentences).

``` r
## add your code here
```

#### 1.2 It turns out `ratdat_surveys` is pretty untidy… So let’s try to fix that! Use what you’ve learned this week to create a new tidy dataframe called `ratdat_surveys_tidy`. Remove NAs from this resulting dataframe. Hint: The numbered columns include values for the mean weight of animals captured at different plots.

``` r
## add your code here
```

| species_id | date       | plot_number | mean_weight |
|:-----------|:-----------|:------------|------------:|
| BA         | 4-24-1990  | 1           |           7 |
| BA         | 10-10-1991 | 2           |           6 |
| BA         | 10-10-1991 | 20          |           6 |
| BA         | 1-12-1991  | 3           |           9 |
| BA         | 10-16-1990 | 3           |           8 |

#### 1.3 Unfortunately, there’s still an issue with `ratdat_surveys_tidy`! The `date` column actually includes three pieces of information: month, date, and year. Look into the functions `unite()` and `separate_wider_delim()` to see if you can find a way to split the `date` column into three.

``` r
## add your code here
```

| species_id | month | day | year | plot_number | mean_weight |
|:-----------|:------|:----|:-----|:------------|------------:|
| BA         | 4     | 24  | 1990 | 1           |           7 |
| BA         | 10    | 10  | 1991 | 2           |           6 |
| BA         | 10    | 10  | 1991 | 20          |           6 |
| BA         | 1     | 12  | 1991 | 3           |           9 |
| BA         | 10    | 16  | 1990 | 3           |           8 |

#### 1.4 Now, let’s work on joining our different datasets together. First, use a join function to add the detailed information on species names from one of your loaded datasets to `ratdat_surveys_tidy`.

``` r
## add your code here
```

| species_id | month | day | year | plot_number | mean_weight | genus   | species | taxa   |
|:-----------|:------|:----|:-----|:------------|------------:|:--------|:--------|:-------|
| BA         | 4     | 24  | 1990 | 1           |           7 | Baiomys | taylori | Rodent |
| BA         | 10    | 10  | 1991 | 2           |           6 | Baiomys | taylori | Rodent |
| BA         | 10    | 10  | 1991 | 20          |           6 | Baiomys | taylori | Rodent |
| BA         | 1     | 12  | 1991 | 3           |           9 | Baiomys | taylori | Rodent |
| BA         | 10    | 16  | 1990 | 3           |           8 | Baiomys | taylori | Rodent |

#### 1.5 Does the type of join matter for these two dataframes? Why or why not? (Test out some other joins to see…)

``` r
## add your code here
```

#### 1.6 Finally, use a join function to add the plot information to the dataframe created in exercise 1.4 (from the final remaining loaded dataset). Since the columns are not named the same, you’ll need to include a `by` term this time. The general syntax for these is: `by = join_by(<df1 column name> == <df2 column name>)`.

``` r
## add your code here
```

| species_id | month | day | year | plot_number | mean_weight | genus | species | taxa | plot_type |
|:---|:---|:---|:---|---:|---:|:---|:---|:---|:---|
| BA | 4 | 24 | 1990 | 1 | 7 | Baiomys | taylori | Rodent | Spectab exclosure |
| BA | 10 | 10 | 1991 | 2 | 6 | Baiomys | taylori | Rodent | Control |
| BA | 10 | 10 | 1991 | 20 | 6 | Baiomys | taylori | Rodent | Short-term Krat Exclosure |
| BA | 1 | 12 | 1991 | 3 | 9 | Baiomys | taylori | Rodent | Long-term Krat Exclosure |
| BA | 10 | 16 | 1990 | 3 | 8 | Baiomys | taylori | Rodent | Long-term Krat Exclosure |

### Exercise 2

Now for a bit more practice working with different dataframes… For this
exercise, we’re going to use the `tibble` package within tidyverse to
directly create tibbles (a particular type of dataframe used within the
tidyverse).

#### 2.1 Create a tibble `A` and a tibble `B` that look like the ones below. To do this, you will want to read about the `tibble()` function on this [help page](This%20help%20page%20will%20be%20most%20useful:%20%3Chttps://tibble.tidyverse.org/reference/tibble.html%3E).

``` r
## add your code here
```

|  a1 | a2  |
|----:|:----|
|   1 | v   |
|   2 | w   |
|   3 | x   |
|   4 | y   |
|   5 | z   |

|  b1 | b2  |
|----:|:----|
|   1 | a   |
|   3 | b   |
|   5 | c   |
|   7 | d   |
|   9 | e   |

#### 2.2 One simple way to join different tibbles together is using the functions `bind_rows()` or `bind_cols()`. Test both of these functions with your new tibbles to see what they do.

``` r
## add your code here
```

#### 2.3 What do these functions do if your tibbles instead have the same column names? Change the column names for `A` to match those of `B` and repeat `bind_rows()` and `bind_cols()` to find out.

``` r
## add your code here
```

#### 2.4 Write 1-2 sentences describing the difference between your answers from 2.2 and 2.3

\[write answer here\]

#### 2.5 Maybe you want to create a larger tibble `C` that has 100 rows with one column of numbers and one column of letters? Look into the functions `seq()` and `letters()` to see if they might make this easier. Show the first 10 lines of this tibble.

``` r
## add your code here
```

|  c1 | c2  |
|----:|:----|
|   1 | a   |
|   2 | b   |
|   3 | c   |
|   4 | d   |
|   5 | e   |
|   6 | f   |
|   7 | g   |
|   8 | h   |
|   9 | i   |
|  10 | j   |

#### 2.6 Finally, at some point in your analysis you will probably want to *save* your output! Read up on the `write_delim()` series of functions from the `readr` package. Use `write_csv()` to save your `C` tibble as `tibble_C.csv`. Include this with your problem set when you push to GitHub.

``` r
## add your code here
```
