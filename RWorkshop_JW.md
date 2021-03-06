# In this workshop you will learn:
- Basics of R (objects, variables, data classes, vectors)
- How to write R functions
- How to import and export your own files
- How to install and load R and Bioconductor packages

# What is R?
- R is a language and environment for statistical computing and graphics (https://www.r-project.org/about.html). 
- It is free and can be tailored to your needs by installing and using specific packages (https://cran.r-project.org/web/packages/available_packages_by_name.html).
- You can use R interactively (e.g., enter commands into the R console or R Studio https://rstudio.com/) or into new cells in your Jupyter notebook.
- You can write and run R scripts or generate reports and documents using R notebooks (https://blog.rstudio.com/2016/10/05/r-notebooks/) and markdown files (https://rmarkdown.rstudio.com/).

# Interacting with R
- You can use R interactively and have it do some simple math:


```R
2 - 1
```

- It is generally more useful to assign your values to **variables**, which are R objects.
- You can assign values to R variables using the assignment operator **'<-'**, which assigns the value on the right to the variable on the left.
- There are other operators as well (like the `=` sign) but I would suggest you stick with the `<-` operator for now.
- Everything in R (including variables) is an object (https://cran.r-project.org/doc/manuals/r-release/R-lang.html#Objects)

<div class="alert alert-block alert-info">
<b>Tip:</b> We will use the words `object` and `variable` interchangably in this workshop.
</div>

Let's assign a variable called `a`:


```R
a <- 1
```

R won't print anything when you assign a value to a variable. We can look at the output of our assignment by typing `a`.


```R
a
```

- R also comes with a `print()` function that we can use to look at our variables.
- We will talk more about functions later in this workshop, but a **function** is a series of statements that work together to perform a specific task.
- All functions need pieces of information (or **arguments**) to perform their particular function, these arguments can be required or optional. 
- `print()` takes a single required argument -- the thing you want to print.

<div class="alert alert-block alert-info">
<b>Tip:</b> You can use `?function` in R to learn more about a particular function (for example: `?print`).
</div>

- Let's print variable `a`:


```R
print(a)
```

We can name our variables any combination of letters, numbers, or underscores (`_`) with a few exceptions:
- R has a few reserved words that can't be used as variable names in R:
    - `if`, `else`, `repeat`, `while`, `function`, `for`, `in`
    - see the whole list of reserved words here: https://stat.ethz.ch/R-manual/R-devel/library/base/html/Reserved.html). 
- Variables can't start with a number or an underscore
- You can technically use `.` in your variable names, but this is best avoided.

For example:


```R
bar <- 11
cat_1 <- 'cat' 
dog_ <- TRUE
egg <- (1L)
foo <- 2i
```

Now that we have assigned some values to variables, we can start using them:


```R
print(bar)
```


```R
print(bar * 2)
```


```R
print(a)
```


```R
print(a + bar)
```

# Data classes

- The variables you assign have some sort of data class associated with them.
- Data classes impact how functions will interact with your variables.
- R has 5 basic data classes, including:

1. `character`, which is a character 
2. `numeric`, which can be `real` (a rounded number) or `decimal` (a number including a decimal point).
3. `integer`, which can be a rounded number (but not a decimal) 
4. `logical`, which can be either `TRUE` or `FALSE`
5. `complex`, allows you to use imaginary numbers 

- You can also have missing data, which we will also talk about later in this workshop.

Let's look at the data classes of our variables we have just assigned:


```R
class(a)
class(bar)
class(cat_1)
class(dog_)
class(egg)
class(foo)
```

- The `L` we included when we assigned `egg` tells R that this object is an integer.
- The `i` we included when we assigned `foo` indicates an imaginary number, making `foo` complex data class object.


```R
#?class
```

# R data structures
- R objects can also contain more than one element.
- Objects that contain more than one element are organized into different data structures.
- Data structures in R include vectors (also referred to as 'atomic vectors' in R), lists, matrices, arrays, and data frames.

### Vectors
- Probably the simplest R object that contains more than one element is a **vector**. 
- You can create a vector using the concatenate function, `c()`, or directly assigning them. 
- The `c()` function will coerce all of the arguments to a common data type and combine them to form a vector. 
- Here's a few examples of how you can assign vectors:


```R
numeric_vector <- c(1,2,3,4,5) 
character_vector <- c('one', 'two', 'three', 'four', 'five') 
integer_vector <- (6:12) 
logical_vector <- c(TRUE, TRUE, FALSE)
character_vector_2 <- c('a', 'pug', 'is', 'not', 'a', 'big', 'dog')
```

Note that I used `:` when assigning `integer_vector`, which just generates a list from 6 through 12.


```R
print(numeric_vector)
print(character_vector)
print(integer_vector)
print(logical_vector) 
print(character_vector_2)
```

Vectors also have class:


```R
print(class(numeric_vector))
print(class(character_vector))
print(class(integer_vector))
print(class(logical_vector)) 
print(class(character_vector_2))
```

You can combine vectors using `c()`


```R
combined_vector <- c(numeric_vector, integer_vector)
```


```R
print(combined_vector)
```

You can use the `length()` function to see how long your vectors are:


```R
print(length(combined_vector))
```

You can also access elements of the vector based on the index (or its position in the vector):


```R
print(combined_vector[2])
```

You can combine these operations, but note that R code evaluates from the inside out:


```R
print(combined_vector[length(combined_vector)])
```

Here, R is reading `length(combined_vector)` first. The value returned by the `length()` function is then used to access the last entry in the `combined_vector` vector.

You can also name vector elements and then access them by their names:


```R
names(numeric_vector) <- c('one', 'two', 'three', 'four', 'five')
print(numeric_vector)
```


```R
print(numeric_vector['three'])
```

We can use `-c` to remove vector elements:


```R
print(combined_vector[-c(4)])
```

If a vector is numerical, we can also perform some math operations on the entire vector. Here, we can calculate the sum of a vector:


```R
print(combined_vector)
print(sum(combined_vector))
```


```R
print(combined_vector/sum(combined_vector))
```

Use the `round()` function to specify you only want 3 digits reported and assign it to a variable called `rounded`


```R
rounded <- round((combined_vector/sum(combined_vector)), digits = 3)
print(rounded)
```

You can also perform math operations on two vectors...


```R
print(rounded + combined_vector)
```

but you'll get weird results if the vectors are different lengths:


```R
print(combined_vector)
print(numeric_vector)
```


```R
print(combined_vector + numeric_vector)
```

It looks like R will give you an error message and then go back to the start of the shorter vector.

**Coercing between classes**

Let's say you're trying to import some data into R, maybe a vector of measurements:


```R
your_data <- c('6','5','3','2','11','0','9','9')
class(your_data)
```

You vector is a character vector because the elements of the vector are in quotes. You can coerce them back into numeric values using `as.numeric()`:


```R
your_new_data <- as.numeric(your_data)
print(your_new_data)
class(your_new_data)
```

What happens if we try to `as.numeric` things that aren't numbers?


```R
as.numeric(character_vector_2)
```

<div class="alert alert-block alert-warning">
<b>Example:</b> <b>&ltNA&gt</b> indicates that these are missing values, so be careful when converting between classes.
</div>

# Missing values
Missing values can result from things like inappropriate coersion, Excel turning everything into a date, encoding format problems, etc.


```R
here_is_a_vector <- as.numeric(c(4/61, 35/52, '19-May', 3/40))
```

We can use the `is.na()` function to see if our vector has any `<NA>` values in it:


```R
is.na(here_is_a_vector)
```

You can combine this with the `table()` function to see some tabulated results from `is.na()`:


```R
table(is.na(here_is_a_vector))
```

You might also encounter an `NaN`, which means 'not a number' and is the result of invalid math operations:


```R
0/0
```

`NULL` is another one you might encounter, and it is the result of trying to query a parameter that is undefined for a specific object. For example, you can use the `names()` function to retrieve names assigned to an object. What happens when you try to use this function on an object you haven't named?


```R
names(here_is_a_vector)
```

You might also see `Inf` or `-Inf` which are positive or negative infinity, which result from dividing by zero or operations that do not converge:


```R
1/0
```

# Matrices
- A matrix in R is a collection of elements organized into rows and columns.
- All columns must be the same data type and be the same length.
- Generate a matrix using the following general format:

```
my_matrix <- matrix(
    vector, 
    nrow = r, 
    ncol = c, 
    byrow = FALSE)
```

For example:


```R
my_matrix <- matrix(
    c(1:12), 
    nrow = 3, 
    ncol = 4, 
    byrow = FALSE)

print(my_matrix)
```

In the above code, we made `my_matrix`, we specified it should be populated by the vector `c(1:12)`, with 3 rows (`nrow = 3`) and 4 columns (`ncol = 4`) and be populated by column, not by row (`byrow = FALSE`)

We can access the rows and columns by their numerical index using a `[row, column]` format.
For example, here's how we access row 3 and column 4:


```R
my_matrix[3,4]
```

Access entire row 3:


```R
print(my_matrix[3,])
```

Access entire column 4:


```R
print(my_matrix[,4])
```

You can also name the rows and columns and then access them by name. 
For example, lets name the rows and columns of `my_matrix`


```R
dimnames(my_matrix) <- list(
    c('row_1', 'row_2', 'row_3'), 
    c('column_1', 'column_2', 'column_3', 'column_4'))
```

You can also name the rows and columns separately using `rownames()` and `colnames()` 


```R
rownames(my_matrix) <- c('row_1', 'row_2', 'row_3')
colnames(my_matrix) <- c('column_1', 'column_2', 'column_3', 'column_4')
```


```R
print(my_matrix)
```


```R
print(my_matrix['row_2',])
```


```R
print(my_matrix[,'column_2'])
```

# Arrays
- An array can be similar to a matrix but they can have more than 2 dimensions (e.g., more than rows and columns)
- So, an array with 1 dimension is similar to a vector and an array with 2 dimensions is similar to a matrix.
- Generate an array with the following generic format:

```
my_array <- array(vector),dim = c(rows, columns, other_dims))
```


```R
my_col_array <- array(
    c(1:12),
    dim = c(12,1,1))
print(my_col_array)
```


```R
my_row_array <- array(
    c(1:12),
    dim = c(1,12,1))
print(my_row_array)
```


```R
my_array <- array(
    c(1:12),
    dim = c(3,4,1))
print(my_array)
```


```R
another_array <- array(
    c(1:24),
    dim = c(3,4,2))
print(another_array)
```

Access elements of arrays like this `[row, column, other_dims]`


```R
print(another_array[3,2,1])
```


```R
print(another_array[3,2,2])
```

You can also give your array some `dimnames()`:


```R
dimnames(another_array) <- list(
    c('row_1', 'row_2', 'row_3'), 
    c('column_1', 'column_2', 'column_3', 'column_4'),
    c('matrix_1', 'matrix_2'))
print(another_array)
```

Then access your array elements by name:


```R
print(another_array['row_3', 'column_2', 'matrix_1'])
```


```R
print(another_array['row_3',,'matrix_1'])
```

# Lists

- Lists in R are very flexible, they are collections of elements that can be different classes, structures, whatever. You can even have lists of lists.
- You make lists using the `list()` function (or by coersion using `as.list()`.


```R
my_list <- list(character_vector, my_array, my_matrix)
print(my_list)
```

Use `[[]]` to access list elements:


```R
print(my_list[[3]])
```

Add more brackets to access sub-elements of a list:


```R
print(my_list[[3]][1])
```


```R
print(my_list[[3]][1,])
```

Name the list elements:


```R
names(my_list) <- c('character_vector', 'my_array', 'my_matrix')
print(my_list)
```

Use `unlist()` if you want to convert a list to a vector, let's make a new list (`list_1`)


```R
list_1 <- list(1:5)
print(list_1)
```

Use `str()` to look at the structure


```R
str(list_1)
```

Then `unlist()` and look at the structure


```R
print(unlist(list_1))
str(unlist(list_1))
```

# Data Frames

- A data frame is another way to organize a collection of rows and columns.
- It is a collection of lists organized into columns.
- It is similar to a matrix, except data frames allow different data types in different columns.
- We can use the `data.frame()` function to create a data frame from vectors using the following format:

```
dataframe <- data.frame(column_1, column_2, column_3)
```


```R
example_df <- data.frame(
    c('a','b','c'), 
    c(1, 3, 5), 
    c(TRUE, TRUE, FALSE))

print(example_df)
```

Use `names()` or `colnames()` to name columns,  `rownames()` to name rows, or `dimnames()` to assign both column and row names to the data frame:


```R
colnames(example_df) <- c('letters', 'numbers', 'boolean')
rownames(example_df) <- c('first', 'second', '')
print(example_df)
```


```R
names(example_df) <- c('_letters_', '_numbers_', '_boolean_')
print(example_df)
```


```R
dimnames(example_df) <- list(c('__first', '__second', '__third'), c('__letters', '__numbers', '__boolean'))
print(example_df)
```

We can use the `attributes()` and `str()` functions to get some information about our data frame:


```R
attributes(example_df)
```


```R
str(example_df)
```

# Adding columns to a data frame

Let's make a new example dataframe to work with:


```R
patients_1 <- data.frame(
    c('Boo','Rex','Chuckles'), 
    c(1, 3, 5), 
    c('dog', 'dog', 'dog'))
print(patients_1)
```

Use `names()` or `colnames()` to name columns,  `rownames()` to name rows, or `dimnames()` to assign both column and row names to the data frame.
Here we will use `names()` to namethe columns:


```R
names(patients_1) <- c('name', 'number_of_visits', 'type')
print(patients_1)
```

We can use the column names to extract a single column using the notation `dataframe$column`, e.g.:


```R
print(patients_1$name)
```

The `cbind()` function can be used to add more columns to a dataframe:


```R
column_4 <- c(4, 2, 6)
patients_1 <- cbind(patients_1, column_4)
print(patients_1)
```

We can also rename individual columns of the dataframe using index notation, lets rename the 4th column we just added:


```R
colnames(patients_1)[4] <- 'age_in_years'
print(patients_1)
```

We can also use the `dataframe$column` notation to add a new column and name it at the same time:


```R
patients_1$weight_in_pounds <- c(35, 75, 15)
print(patients_1)
```

Let's use `str()` and `attributes()` functions to look at the structure and attributes of this data frame:


```R
str(patients_1)
```


```R
attributes(patients_1$name)
```

**Notice that `patients_1$name` is a factor with three levels...**

# Factors
- In some situations, you might be dealing with categorical variable, which is known as a factor variable in R. 
- A factor is a type of variable that has a set number of distinct categories into which all observations fall, which are the levels.

*Factor variables are important because R's default behavior when reading in text files is to convert that text into a factor variable rather than a character variable, which can often lead to weird behavior if the user is trying to e.g. search that text.*
- In addition to `cbind()` for adding columns, there is another function in R called `rbind()`, which adds new rows to a data frame.
- Let's see what happens when we try to add a new row to our data frame:


```R
patients_1_rbind <- rbind(patients_1, c('Fluffy', 2, 'dog', 8, 105))
print(patients_1_rbind)
```

- The `patients_1$name` column is classed as a `factor`, and the factors levels are `Boo`, `Chuckles`, and `Rex`. 
- Recall that a factor is a type of variable that has a **set number of distinct categories into which all observations fall, which are the levels.**
- R isn't sure what to do with the new level we are trying to add (`Fluffy`), so we have to turn those factors into strings.

We can convert the `patients_1$name` column to a character as follows:


```R
patients_1$name <- as.character(patients_1$name)
str(patients_1)
```

Now we can use `rbind()` to add a new row:


```R
patients_1 <- rbind(patients_1, c('Fluffy', 2, 'dog', 8, 105))
print(patients_1)
```

# Re-ordering factor levels
- You might have ordinal data, like the following:


```R
sizes <- factor(c('extra small', 'small', 'large', 'extra large', 'large', 'small', 'medium', 'medium', 'medium', 'medium', 'medium'))
```

Use the `table()` function to look at the vector:


```R
table(sizes)
```

We might not necessarily want the factor levels in alphabetical order. You can re-order them like so:


```R
sizes_sorted <- factor(sizes, levels = c('extra small', 'small', 'medium', 'large', 'extra large'))
table(sizes_sorted)
```

You can also use the `relevel()` function to specify that there's a single factor you'd like to use as the reference factor, which will now be the first factor:


```R
sizes_releveled <- relevel(sizes, 'medium')
table(sizes_releveled)
```

You can also coerce a factor to a character:


```R
character_vector <- as.character(sizes)
class(character_vector)
print(character_vector)
```

Notice that print doesn't return the `Levels` and each element of the vector is now in quotes.
It is also possible to convert a factor into a numeric vector if you want to:


```R
print(sizes)
numeric_vector <- as.numeric(sizes)
print(numeric_vector)
```

This assigns numerical values based on alphabetical order of `sizes`


```R
print(sizes_sorted)
ordered_numeric_vector <- as.numeric(sizes_sorted)
print(ordered_numeric_vector)
```

This assigns numerical values based on the levels you set when you created `sizes_sorted`

# Data frame merging
Data is often spread across more than one file, reading each file into R will result in more than one data frame. If the data frames have some common identifying column, we can use that common ID to combine the data frames. 

For example:


```R
print(patients_1)
```

Let's make another data frame:


```R
patients_2 <- data.frame(
    c('Fluffy', 'Smokey', 'Kitty'), 
    c(1, 1, 2), 
    c('cat', 'dog', 'cat'),
    c(1, 3, 5))
colnames(patients_2) <- c('name', 'number_of_visits', 'type', 'age_in_years')
print(patients_2)
```

We can use the `merge()` function to combine them:


```R
patients_df <- merge(patients_1, patients_2, all = TRUE)
print(patients_df)
```

- Using `all = TRUE` will fill in blank values if needed (for example, the weight of any of the animals in `patients_2`).
- You can also return only the first data frame specified using the `all.x = TRUE` argument


```R
patients_df <- merge(patients_1, patients_2, all.x = TRUE)
print(patients_df)
```

- Similarly, return only the second data frame specified using the `all.y = TRUE` argument:


```R
patients_df <- merge(patients_1, patients_2, all.y = TRUE)
print(patients_df)
```

You can also specify which columns to join on:


```R
patients_df <- merge(patients_1, patients_2, by = c('name', 'type', 'number_of_visits', 'age_in_years'), all = TRUE)
print(patients_df)
```

# Built-in functions
- We have already used a few functions in this workshop (like print). 
- Functions are a series of statements that work together to form a specific task.
- All functions need pieces of information (or arguments) to perform their particular function. 
- Sometimes arguments are required, sometimes arguments are optional -- for example, `print()` requires only one argument -- the thing you want to print.
- R comes with some pre-loaded data sets -- you see the list by typing `print(data())`, but it is quite long.

Load the `DNase` data and turn it into a data frame:



```R
data(DNase)
DNase <- data.frame(DNase)
```

Let's use the `dim()`, `nrow()`, and `ncol()` functions to get the number of rows (`nrow()`), number of columns (`nrow()`), and number of both rows and columns (`dim()`)


```R
dim(DNase)
```


```R
nrow(DNase)
```


```R
ncol(DNase)
```

We can use the `head()` function to look at the first few lines of the data frame:


```R
head(DNase)
```

You can use the `n` argument to look at a different number of lines


```R
head(DNase, n = 3)
```

We can use the `tail()` function to look at the last few lines of the data frame:


```R
tail(DNase, n = 5)
```

The summary function, which can be applied to either a vector or a data frame (in the latter case, R applies it separately to each column in the data frame) yields a variety of summary statistics about each variable. 


```R
summary(DNase)
```

`summary()` is informative for numerical data, but not so helpful for factor data, as in the `Run` column. 
Let's make a smaller subset of the `DNase` data to work with:


```R
DNase_subset <- DNase[1:20, ]
DNase_subset
```



We can also sort our data. Let's look at the `conc` column:


```R
print(DNase_subset$conc)
```

Use the `order()` function to figure out the ascending rankings of the values


```R
order(DNase_subset$conc)
```

We can assign this ordering to a vector:


```R
reorder_vector <- order(DNase_subset$conc)
```

And use it to reorder our data frame:


```R
DNase_subset[reorder_vector, ]
```

Data frames can be classified into two broad categories: wide format and long format. All data frames shown so far have been presented in wide format. A wide format data frame has each row describe a sample and each column describe a feature. Here is a short example of a data frame in wide format, tabulating counts for three genes in three patients:


```R
wide_df <- data.frame(c("A", "B", "C"), c(1, 1, 2), c(5, 6, 7), c(0, 1, 0))
colnames(wide_df) <- c("id", "gene.1", "gene.2", "gene.3")
wide_df
```

Long format stacks features on top of one another; each row is the combination of a sample and a feature.  One column exists to denote the feature in question, and another column exists to denote that feature' value:


```R
long_df <- data.frame(c("A", "A", "A", "B", "B", "B", "C", "C", "C"), c("gene.1", "gene.2", "gene.3", "gene.1", "gene.2", "gene.3", "gene.1", "gene.2", "gene.3"), c(1, 5, 0, 1, 6, 1, 2, 7, 0))
colnames(long_df) <- c("id", "gene", "count")
long_df
```

These formats both contain the exact same data but represent it in different ways. Various functions exist to convert between wide and long format but these are beyond the scope of today's discussion. You can look up the `reshape2` or `tidyr` packages if you're interested in learning more about converting between long and wide formats -- alternatively, check out our tidyverse workshop.

# User defined functions
- In addition to the already available functions in R, you can also create your own functions. 
- Generally, if you find yourself re-writing the same pieces of code over and over again, it might be time to write a function. 

Functions take the following basic format:

```
myfunction <- function(argument_name){
  stuff <- this is the body of the function(
    it contains statements that use argument_names
    to do things and make stuff)
  return(stuff)
}
```

More formally, R functions are broken up into 3 pieces:
1. formals() - the list of arguments
2. body() - code inside the function
3. environment() - how the function finds the values associated with function names

Here's an example of a function called `roll()` that rolls any number of 6-sided dice:


```R
roll <- function(number_of_dice){
    rolled_dice <- sample(
        x = 6, 
        size = number_of_dice, 
        replace = TRUE)
    return(rolled_dice)
}
```

- The built-in R function `sample()` is nested inside our `roll()` function.
- `roll()` uses the argument `number_of_dice` as the `size`, `x` is the number of sides on the die, which we have hard-coded as `6`, and `replace = TRUE` means that we are sampling the space of all potential die roll outcomes with replacement.
- Lastly, we tell the function what it should return (`rolled_dice`).

To call that function and print the output:


```R
print(roll(number_of_dice = 10))
```

Lets look at the `formals()`


```R
formals(roll)
```

What about `body()`?


```R
body(roll)
```

What about `environment()`?


```R
environment(roll)
```

So, the function itself is called `roll`, it takes the argument or formals `number_of_dice` and the body of the function uses the built-in `sample` function in R to simulate dice rolls (use ?sample to learn more about the `sample()` function). 

## Anonymous functions

- You can also have something called an **anonymous function**, where you write the function but don't assign it to an object.
- The general format is:
```
(function(
     argument_name) 
     statements that use argument_name to create an object
  )(
    argument_name = argument)
```


```R
(function(
    anonymous_dice) 
    sample(
        x = 6, 
        size = anonymous_dice, 
        replace = TRUE)
 )(
    anonymous_dice = 5)
```

## More on user defined functions
- We can also have functions that take more than one argument. 
- Lets say we want to roll different numbers of dice (`number_of_dice`) and we want to change the size of the dice we roll (`number_of_sides`).


```R
roll <- function(
    number_of_dice, 
    number_of_sides){
    rolled_dice <- sample(
        x = number_of_sides, 
        size = number_of_dice, 
        replace = TRUE)
    return(rolled_dice)
}
```

- The new `roll()` uses the `sample()` function again, but this time it uses the `number_of_dice` and `number_of_sides`


```R
print(roll(number_of_dice = 5, number_of_sides = 20))
```

- Lets say we want to roll different numbers of dice (`number_of_dice`) and we want to change the size of the dice we roll (`number_of_sides`) as well as tweak the number of times we roll the dice (`number_of_rolls`).
- We can use `replicate()` and `sample()`


```R
roll <- function(
    number_of_rolls, 
    number_of_sides, 
    number_of_dice){
    rolled_dice <- replicate(
        number_of_rolls, 
        sample(
            x = number_of_sides, 
            size = number_of_dice, 
            replace = TRUE))
    return(rolled_dice)
}
```

- So, in the above function we use `number_of_dice`, `number_of_sides`, and `number_of_rolls` as arguments. 
- The `sample()` function takes the arguments `number_of_sides` and `number_of_dice`
- The `replicate()` function is takine `number_of_rolls` as an argument.


```R
rolled_dice <- roll(number_of_rolls = 10, number_of_sides = 20, number_of_dice = 5)
print(rolled_dice)
```

You can use `colSums()` or `rowSums()` to calculate the sum of the columns and rows:


```R
print(colSums(rolled_dice))
```


```R
print(rowSums(rolled_dice))
```

We can make `rolled_dice` into an **anonymous function**:


```R
print(
    (function(
        number_of_dice, 
        number_of_sides, 
        number_of_rolls) 
        replicate(
            number_of_dice, 
            sample(
                1:number_of_sides, 
                number_of_rolls, 
                replace = TRUE))
     )(
        number_of_dice = 5, 
        number_of_rolls = 10, 
        number_of_sides = 20))
```

Lets make another anonymous function that makes a boxplot of our dice rolls:


```R
(function(number_of_dice, 
          number_of_sides, 
          number_of_rolls) 
    boxplot((
        replicate(
            number_of_dice, 
            sample(
                1:number_of_sides, 
                number_of_rolls, 
                replace = TRUE))))
 )(
    number_of_dice = 5, 
    number_of_rolls = 10, 
    number_of_sides = 20)
```

We can give the boxplot a title:


```R
(function(number_of_dice, 
          number_of_sides, 
          number_of_rolls) 
    boxplot((
        replicate(
            number_of_dice, 
            sample(
                1:number_of_sides, 
                number_of_rolls, 
                replace = TRUE))), 
            main = 'here is a boxplot of some dice rolls')
 )(
    number_of_dice = 5, 
    number_of_rolls = 10, 
    number_of_sides = 20)
```

We can use `paste()` to pass the function arguments as parts of the title for the figure, by adding `main = paste('the ' , number_of_dice, ' ', number_of_sides, '-sided dice were rolled ', number_of_rolls, ' times', sep='')`


```R
(function(number_of_dice, 
          number_of_sides, 
          number_of_rolls) 
    boxplot((
        replicate(
            number_of_dice, 
            sample(
                1:number_of_sides, 
                number_of_rolls, 
                replace = TRUE))), 
            main = paste(
        'the ' , number_of_dice, ' ', number_of_sides, '-sided dice were rolled ', number_of_rolls, ' times', 
                sep=''))
 )(
    number_of_dice = 5, 
    number_of_rolls = 10, 
    number_of_sides = 20)
```

We can add some colors to the figure by adding `col = c(1:number_of_dice)`, this will generate enough colors so that each bar has a different color:


```R
(function(number_of_dice, 
          number_of_sides, 
          number_of_rolls) 
    boxplot((
        replicate(
            number_of_dice, 
            sample(
                1:number_of_sides, 
                number_of_rolls, 
                replace = TRUE))), 
            main = paste(
        'the ' , number_of_dice, ' ', number_of_sides, '-sided dice were rolled ', number_of_rolls, ' times', 
                sep=''), 
           col = c(1:number_of_dice))
 )(
    number_of_dice = 5, 
    number_of_rolls = 10, 
    number_of_sides = 20)
```

# Importing and Exporting files
- Use the `write.table` or `write.csv` functions to write outputs in R.
- Lets use some of the pre-loaded data that comes with R. 


```R
iris <- data.frame(iris)
head(iris)
```

You can write the output to a file using `write.table` or `write.csv`:


```R
write.table(iris, file = '~/iris_table.txt')
write.csv(iris, file = '~/iris_csv.csv')
```

Let's try using `read.table` and `read.csv` to test out importing data:


```R
row.names(iris_csv2)
```


```R
iris_table2 <- read.table('~/iris_table.txt')
```


```R
iris_csv2 <- read.csv('~/iris_csv.csv')
```


```R
head(iris_table2)
```


```R
head(iris_csv2)
```

Notice that the `Species` column is a factor (`<fct>`). If we'd like text strings to be characters instead of factors when we import we can use `stringsAsFactors = FALSE`:


```R
iris_table <- read.table('~/iris_table.txt', stringsAsFactors = FALSE)
iris_csv <- read.csv('~/iris_csv.csv', stringsAsFactors = FALSE)
```


```R
head(iris_table)
head(iris_csv)
```

To convert back into a factor:


```R
iris_table$Species <- as.factor(iris_table$Species)
iris_csv$Species <- as.factor(iris_csv$Species)
```


```R
head(iris_table)
head(iris_csv)
```

Use `list.files()` get a list of all files in a directory:


```R
list.files(path = '~', pattern = 'iris_*')
```

# R packages
- Although R comes with many built in functions, you will probably want to install and use various R packages.
- You can install the packages using `install.packages('package_name_here')` (where you would replace 'package_name_here' with your package of choice, in quotes). 
- This will download the package and any additional required dependencies. 
- Uncomment out the next line (e.g., remove the #) to install the the 'ggplot2' package:


```R
install.packages('ggplot2')
```

Before you can actually use the package, you have to load it as follows:


```R
library('ggplot2')
```

Most R packages are found in CRAN - the central repository for R package. However, packages can be found in different places. Many of the packages of interest for biologists will be in Bioconductor. 

There are two steps to downloading a package from Bioconductor -- first, install BiocManager (again, remove the # to actually run the install).


```R
install.packages("BiocManager")
```

Then, load `BiocManager` and use `BiocManager::install()` to install a package.


```R
library('BiocManager')
BiocManager::install("org.Hs.eg.db")
```

Use the `sessionInfo()` function to see more information about your loaded R packages and namespace:


```R
print(sessionInfo())
```

## The `apply()` functions
- R uses a family of `apply()` functions to repetitively manipulate objects while avoiding for loops. 
- How you use them will depend on the format of your data and what operations you're trying to perform.
- We will talk about `apply()`, `lapply()`, and `sapply()`.
- There is also `mapply()`, `vapply()`, `rapply()`, and `tapply()`, but we won't talk about those today.

- **`apply()`** Applies a function to an array (or matrix) and returns an array (or matrix)
- **`lapply()`** Applies a function to each element of a list or vector and returns a list
- **`sapply()`** Applies a function to each element of a list or vector and returns a vector


### `apply()` 
- `apply()` applies a function to an array (or matrix) and returns an array (or matrix)
- The general format of an `apply()` call is as follows:

```
apply(X, MARGIN, FUN, ...)

```
- `X` is the array or matrix to apply the function
- `MARGIN` is where the function should be applied - `1` is for rows, `2` is for columns, `c(1,2)` is rows and columns, can also be a character vector of dimension names if `X` has dimnames.
- `FUN` Function to be applied
Let's go back to the dice rolling function:


```R
rolled_dice <- roll(number_of_rolls = 10, number_of_sides = 20, number_of_dice = 5)
```


```R
print(rolled_dice)
```


```R
class(rolled_dice)
```

I'm going to name the rows and columns using the `paste()` and `dimnames()`:


```R
dimnames(rolled_dice) <- list(
paste('roll', 1:5, sep = '_'),
    paste('die', 1:10, sep = '_'))

print(rolled_dice)
```

Let's try using `apply()` to increase every value by 1:


```R
add_one <- apply(rolled_dice, c(1,2), function(element) element + 1)
class(add_one)
print(add_one)
```

- The `c(1,2)` argument to `apply()` means that the function should apply to all rows and columns.
- What about if we use apply to calculate sums for each row and column?

If we use `1` it will apply the function to each row:


```R
row_sums <- apply(rolled_dice, 1, function(element) sum(element))
print(row_sums)       
```


```R
If we use `2` it will apply the function to each column:
```


```R
col_sums <- apply(rolled_dice, 2, function(element) sum(element))
print(col_sums) 
```

### `lapply()`

- `lapply()` works on lists and returns a list.
- Since a data frame is a series of lists, if you apply it to a data frame it will execute the function on each column of the data frame.
- The general format is as follows:

```
lapply(X, FUN)

```
- `X`  A vector or an object
- `FUN` Function applied to each element of X



```R
rolled_dice_df <- as.data.frame(rolled_dice)
class(rolled_dice_df)
```


```R
print(rolled_dice_df)
```


```R
col_sums_df <- lapply(rolled_dice_df, sum)
```


```R
str(col_sums_df)
```


```R
rolled_dice
```

However, if you use `lapply()` to calculate sums on the `rolled_dice` matrix, you get back a very long list (since `lapply()` wants to return a list).


```R
class(rolled_dice)
```


```R
col_sums <- lapply(rolled_dice, sum)
str(col_sums)
```

### `sapply`


```R
- `sapply()` is similar to `lapply()`, but it returns a vector rather than a list.
- The general format for an `sapply()` call is as follows:

```
sapply(X, FUN)

```
- `X`  A vector or an object
- `FUN` Function applied to each element of x
```


```R
col_sums_df <- sapply(rolled_dice_df, sum)
```


```R
class(col_sums_df)
is.vector(col_sums_df)
```


```R
print(col_sums_df)
```
