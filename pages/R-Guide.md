# R Guide

We follow the general guidelines in Hadley Wickham's [Style Guide](http://adv-r.had.co.nz/Style.html). We also try not to use base R if there is a Wickham alternative. About 99% of what we do can be found in one of these packages:
* `dplyr` or `data.table` for data manipulation.
* `lubridate` for dealing with dates/
* `readr` and `readxl` for reading in rectangular data. 
* `tibble` is a modern re-imagining of data.frames; it provides stricter checking and better formatting than the traditional data frame.
* `stringr` for character manipulation and string detection. 
* `tidyr` makes it easier to tidy up data. The main two functions here are 
   * `gather()`, which converts wide data to longer format, and 
   * `spread()`, which converts long data to wider format. 
* `sf` for spatial data manipulation
* `ggplot2` for plotting and mapping
* `purrr` is the functional programming toolkit for R. The main functions here are 
   * `map()` family which replace the `apply` family from base R and 
   * `reduce` which replaces the `Reduce` function from base R that iteratively applies a function to a list. 

Once you have written your code in an .R or .txt file, use source() in R to read the file and execute the commands in the file.

### Piping

We want to use the piping style as much as can because it organizes code in a very readable fashion. Pipes take the output from one function and feed it to the first argument of the next function. In R, you pipe using the `%>%` symbol. A simple example for finding the maximum of a vector (instead of of `max(c(1, 2, 3))`) is 

`c(1, 2, 3) %>% max`

The cool part of piping with `dplyr` is creating piping chains, which basically allows us to order the data manipulation steps in an easily understandable fashion and avoid creating temporary variables in between steps. The example data frame below are weights for different animals, and the piping example will show how we would find the species with the greatest mean weight.

```
df <-
  tibble(
    ID = c(1, 2, 3, 4, 5), 
    Animal = c("Dog", "Cat", "Dog", "Raven", "Cat"), 
    Weight = c(100, 40, 80, 16, 50),
    Height = c(23, 18, 40, 3, 16),
    Family = c("Mammal", "Mammal", "Mammal", "Bird", "Mammal")
  )

df %>%
  group_by(Animal) %>%
  summarise(MeanWeight = mean(Weight)) %>%
  arrange(desc(MeanWeight))
``` 

Without piping, the operation would look like 

`arrange(summarise(group_by(df, Animal), MeanWeight = mean(Weight)))`

For further ease of reading, we want to have one function per line when piping. Bad piping style would look like 
```
df %>% group_by(Animal) %>%  summarise(MeanWeight = mean(Weight)) %>%
  arrange(desc(MeanWeight))
```
rather than what we have above. 

### Using data.table

Generally, `dplyr` is good for 90% of what we need to do, but it has a tendency to use RAM inefficiently. When this constraint becomes binding, it's time to switch over to `data.table`.

Almost everything you can do in `dplyr` can also be done in `data.table` but it is generally less elegant. Let's keep working with the example animal data-frame we had before. First we will convert it to a `data.table`:

```
df <-
  as.data.table(df)
```
The general format of a data table command is

```
table[rows to act on, columns to update/keep, grouping]
```
so to summarize the average weight of each animal, we would write

```
df[,.(MeanWeight = mean(Weight)), by = Animal]
```
If we didn't want to lose that height data, we would instead write

```
df[,`:=`(MeanWeight = mean(Weight)), by = Animal]
```
Similar to piping in `dplyr`, there is chaining in `data.table`. Let's say after computing the average weight by animal, we want to compute the average height by family of animals, then we would chain these operations as follows: 

```
df[,`:=`(MeanWeight = mean(Weight)), by = Animal][
   ,`:=`(MeanHeight = mean(Height)), by = Family]
```

One more trick that is very useful is `.SD`. This allows you to manipulate each group of data. Let's say we wanted for each animal the height of the heaviest animal of that type. One approach to doing this is

```
df[, `:=`(BiggestWeight = max(Weight)), by = Animal][
   Weight == BiggestWeight, .(GoodHeight = Height, Animal)]
```
But what if we wanted this `GoodHeight` column to be added to our original table, this would require us to use a `.SD`:

```
df[, GoodHeight := .SD[, .(BiggestWeight = max(Weight),
                           Weight,
                           Height)][
                       Weight == BiggestWeight, Height]
   , by = Animal]
```
A comprehensive guide to `data.table` is linked below.

### Style Highlights

* In order to make file paths system agnostic, we use the function `file.path()` to point to directories. 
* Keep code to 80 characters per line. You can add an 80 character margin in your source pane by going to Tools > Code > Display > Show Margin
* Use <-, not =, for assignment.
* Make sure all datasets are stored as a tibble
* add carriage return for code that is longer than one line 

```
check <-
  intersect(c(1, 1, 2), c(0, 1, 2)) %>%
  as_tibble
```
rather than

```
check <- intersect(c(1, 1, 2), c(0, 1, 2)) %>%
  as_tibble
```

### Learning Materials
* [RStudio setup and tutorial](https://www.sitepoint.com/introduction-r-rstudio/)
* [The entire foundations section of Hadley's Advanced R book](http://adv-r.had.co.nz/)
* [dplyr tutorial](http://seananderson.ca/2014/09/13/dplyr-intro.html)
* [Programming in R tutorial](http://swcarpentry.github.io/r-novice-inflammation/)
* [Spatial data manipulation with `sf`](https://edzer.github.io/UseR2017/)
* [Extensive data.table guide](https://cran.r-project.org/web/packages/data.table/vignettes/datatable-intro.html)
* Regular expression in R [tutorial](https://stringr.tidyverse.org/articles/regular-expressions.html)

### Random

Running bash job on server
1. In the first line of R program write #!/usr/bin/Rscript
2. After finalizing your batch script, type into the command line `chmod +x rprogram.R` followed by `Rscript rprogram.R --verbose`
