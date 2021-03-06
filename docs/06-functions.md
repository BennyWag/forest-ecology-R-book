# Functions in R
## Introduction

Basic mathematical operations are the heart of data analysis. While statistical analysis can seem far removed from the arithmetic you learned in primary school, complex analyses are still built on very basic mathematics! As a computing language, the main purpose of R is to streamline these operations, allowing you to build up complex analyses with relatively little work. Even very basic, commonly used operations like `mean()` are actually functions. That is, they take basic inputs and evaluate some string of mathematical operations, and produce an output. 

There are many built-in R functions, and endless others available in R packages. One of the most useful tools in R is the ability to write user-defined functions that simplify your processing and reduce the risk of making simple errors.

This section will introduce basic function structure and show you how to write your own.

### Mathematical operations

A quick reminder about mathematical and conditional operators in R:

<table class="table" style="margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> Operator </th>
   <th style="text-align:left;"> Description </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> + </td>
   <td style="text-align:left;"> Addition </td>
  </tr>
  <tr>
   <td style="text-align:left;"> - </td>
   <td style="text-align:left;"> Subtraction </td>
  </tr>
  <tr>
   <td style="text-align:left;"> * </td>
   <td style="text-align:left;"> Multiplication </td>
  </tr>
  <tr>
   <td style="text-align:left;"> / </td>
   <td style="text-align:left;"> Division </td>
  </tr>
  <tr>
   <td style="text-align:left;"> ^ </td>
   <td style="text-align:left;"> Exponential </td>
  </tr>
  <tr>
   <td style="text-align:left;"> &gt; </td>
   <td style="text-align:left;"> Greater than </td>
  </tr>
  <tr>
   <td style="text-align:left;"> &lt; </td>
   <td style="text-align:left;"> Less than </td>
  </tr>
  <tr>
   <td style="text-align:left;"> == </td>
   <td style="text-align:left;"> *Equal to </td>
  </tr>
  <tr>
   <td style="text-align:left;"> &gt;= and &lt;= </td>
   <td style="text-align:left;"> Greater than/less than or equal to </td>
  </tr>
  <tr>
   <td style="text-align:left;"> != </td>
   <td style="text-align:left;"> Not equal to </td>
  </tr>
</tbody>
<tfoot>
<tr>
<td style = 'padding: 0; border:0;' colspan='100%'><sup>1</sup> The = symbol alone assigns a value; you need == for a conditional statement</td>
</tr>
</tfoot>
</table>



## What is an R function?

Functions in R take an input value, run a chunk of code, and generate an output. R packages include numerous functions that can do nearly anything you desire, but research often requires specific processes or sequences of commands designed specifically to work with your data structure. You can write your own functions in R to perform these tasks.

Here is a very simple function:


```r
fun1 <- function (a, b){
  a + b
}
```

Here, `a` and `b` are identified as the required input variables. The code written within the brackets describes the mathematical operation to be applied to the input variables.

Let's run the function on some numbers:


```r
fun1(a = 7, b = 12)
```

```
## [1] 19
```
  
  
A function can be applied to a vector of inputs. In this scenario, the function will be applied to each pair of values in the vector sequence:


```r
vals_a <- c(4, 7, 1)
vals_b <- c(2, 1, 3)

fun1(a = vals_a, b = vals_b)
```

```
## [1] 6 8 4
```

User defined functions can include as many variables as you want, and the inputs can even be labeled with words:


```r
fun2 <- function (length, width, height){
  length * width * height
}
```

When executing a function, you don't need to type up the variable names, but they should be in the correct order.


```r
fun2(3,6,9)
```

```
## [1] 162
```

## Nesting functions

Functions can also include other functions, which is particularly useful in the context of repeating complex data analyses. Here is a basic example:


```r
fun3 <- function (a, b){
  mean(a) + b
}


fun3(vals_a, vals_b)
```

```
## [1] 6 5 7
```

It is important to note that in this situation, the internal function (`mean()`) takes a vector of input values. This function will calculate the mean of the `vals_a` vector and then add this to each separate value of `vals_b`.

This can be very useful, but it's critical that you know exactly how your function processes input values or you may run into problems!

### Some basic built-in mathematical functions

Here are a base R functions that might be useful (most are self explanatory!):

<table class="table" style="margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> Function </th>
   <th style="text-align:left;"> Description </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> mean() </td>
   <td style="text-align:left;"> Mean </td>
  </tr>
  <tr>
   <td style="text-align:left;"> max() </td>
   <td style="text-align:left;"> Maximum value </td>
  </tr>
  <tr>
   <td style="text-align:left;"> min() </td>
   <td style="text-align:left;"> Minimum value </td>
  </tr>
  <tr>
   <td style="text-align:left;"> median() </td>
   <td style="text-align:left;"> Median </td>
  </tr>
  <tr>
   <td style="text-align:left;"> sum() </td>
   <td style="text-align:left;"> Sum </td>
  </tr>
  <tr>
   <td style="text-align:left;"> var() </td>
   <td style="text-align:left;"> Variance </td>
  </tr>
  <tr>
   <td style="text-align:left;"> cor() </td>
   <td style="text-align:left;"> Correlation </td>
  </tr>
  <tr>
   <td style="text-align:left;"> sd() </td>
   <td style="text-align:left;"> Standard deviation </td>
  </tr>
</tbody>
</table>


## Assigning variables within functions 

In some more complex analyses, the nested functions may generate data that needs to be stored as variables so they can be used as input for the next process. Here is a function that calculates the mean of our a values, adds b, and then squares the value calculated in the first step.


```r
fun4 <- function (a, b){
  val <- mean(a) + b
  sqval <- val^2
}


output <- fun4(a = vals_a, b = 3)
output
```

```
## [1] 49
```


### Challenge 1

**Write a function that identifies the median value of a, adds the minimum value of a to the median value, and then calculates the square root of that value.**

Execute the function on this vector: `a <- c(1, 3, 4, 2, 8, 10, 3, 8)`

## Using `return()`


If your function assigns multiple variables, you can use `return()` to determine the data that is output from the function. This can be useful if your function includes writing a data set, or includes another process that is not intended to return anything to R as well as some process intended to return data to the R environment.



```r
#Let's see what happens without using the return() function
fun5 <- function (a, b){
  val <- mean(a) + b
  sqval <- val^2
  write.csv(sqval, "outputs/filename.csv")
}
```

```r
output <- fun5(a = vals_a, b = 3)
output
```

```
## NULL
```

Our output here is NULL because the default output for a function will come from the last command within the function. Here, `write.csv()` does not produce data to be returned to R. If we add `return()`, our function will write the .csv and also return the data we want into the environment:


```r
#Now let's add return()
fun6 <- function (a, b){
  val <- mean(a) + b
  sqval <- val^2
  write.csv(sqval, "outputs/filename.csv")
  return(sqval)
}


output <- fun6(a = vals_a, b = 3)
output
```

```
## [1] 49
```

Much better!

### Challenge 2

**Write a function for two vectors a and b that:**

1. Calculates the sum of the means of a and b and assigns this value to a variable "m"
2. Calculates m to the power of 7 and assgins this value to a variable "s"
3. Removes "m" from the environment (Hint: `rm()`) 
4. Returns the value of "s"

Execute the function on the following vectors:

a <- c(7, 2, 4)
b <- c(20, 3, 5)


## Solutions to challenges

### Challenge 1


```r
a <- c(1, 3, 4, 2, 8, 10, 3, 8)

#One way:

challenge1a <- function(a) {
  medval <- median(a)
  minval <- min(a)
  (medval + minval)^-2
}

challenge1a(a)
```

```
## [1] 0.04938272
```

```r
#Even simpler:

challenge1b <- function(a) {
  (median(a) + min(a))^-2
}

challenge1b(a)
```

```
## [1] 0.04938272
```

### Challenge 2


```r
a <- c(7, 2, 4)
b <- c(20, 3, 5)

challenge2 <- function(a, b) {
  m <- mean(a) + mean(b)
  s <- m^7
  rm(m)
  return(s)
}

challenge2(a, b)
```

```
## [1] 89050880
```

