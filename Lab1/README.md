Базовая работа с R
================
sanches23rx

## Цель работы

Изучить базовые принципы работы языка R

## Ход работы

### Задание 1. Basic Building Blocks

In its simplest form, R can be used as an interactive calculator. Type
5 + 7 and press

``` r
5 + 7
```

    [1] 12

To assign the result of 5 + 7 to a new variable called x, you type x \<-
5 + 7. This can be | read as ‘x gets 5 plus 7’. Give it a try now. | To
view the contents of the variable x, just type x and press Enter. Try it
now.

``` r
x <- 5 + 7
x
```

    [1] 12

Now, store the result of x - 3 in a new variable called y. | What is the
value of y? Type y to find out.

``` r
y <- x - 3
y
```

    [1] 9

The easiest way to create a vector is with the c() function, which
stands for ‘concatenate’ | or ‘combine’. To create a vector containing
the numbers 1.1, 9, and 3.14, type c(1.1, 9, | 3.14). Try it now and
store the result in a variable called z.

``` r
z <- c(1.1, 9, 3.14)
```

Anytime you have questions about a particular function, you can access
R’s built-in help | files via the `?` command. For example, if you want
more information on the c() function, | type ?c without the parentheses
that normally follow a function name. Give it a try.

``` r
?c
```

    запускаю httpd сервер помощи... готово

Type z to view its contents. Notice that there are no commas separating
the values in the | output

``` r
z
```

    [1] 1.10 9.00 3.14

You can combine vectors to make a new vector. Create a new vector that
contains z, 555, then | z again in that order. Don’t assign this vector
to a new variable, so that we can just see | the result immediately.

``` r
c(z, 555, z)
```

    [1]   1.10   9.00   3.14 555.00   1.10   9.00   3.14

Numeric vectors can be used in arithmetic expressions. Type the
following to see what | happens: z \* 2 + 100.

``` r
z * 2 + 100
```

    [1] 102.20 118.00 106.28

Take the square root of z - 1 and assign it to a new variable called
my_sqrt.

``` r
my_sqrt <- sqrt(z - 1)
```

Before we view the contents of the my_sqrt variable, what do you think
it contains?

1: a vector of length 0 (i.e. an empty vector) 2: a vector of length 3
3: a single number (i.e a vector of length 1)

Answer: 2

Print the contents of my_sqrt.

``` r
my_sqrt
```

    [1] 0.3162278 2.8284271 1.4628739

Now, create a new variable called my_div that gets the value of z
divided by my_sqrt.  
Go ahead and print the contents of my_div.

``` r
my_div <- z / my_sqrt
my_div
```

    [1] 3.478505 3.181981 2.146460

To see another example of how this vector ‘recycling’ works, try adding
c(1, 2, 3, 4) and  
c(0, 10). Don’t worry about saving the result in a new variable.

``` r
c(1, 2, 3, 4) + c(0, 10)
```

    [1]  1 12  3 14

Try c(1, 2, 3, 4) + c(0, 10, 100) for an example.

``` r
c(1, 2, 3, 4) + c(0, 10, 100)
```

    Warning in c(1, 2, 3, 4) + c(0, 10, 100): длина большего объекта не является
    произведением длины меньшего объекта

    [1]   1  12 103   4

In many programming environments, the up arrow will cycle through
previous commands. Try  
hitting the up arrow on your keyboard until you get to this command (z
\* 2 + 100), then  
change 100 to 1000 and hit Enter. If the up arrow doesn’t work for you,
just type the  
corrected command.

``` r
z * 2 + 1000
```

    [1] 1002.20 1018.00 1006.28

You can type the first two letters of the variable name, then hit the
Tab key (possibly more  
than once). Most programming environments will provide a list of
variables that you’ve  
created that begin with ‘my’. This is called auto-completion and can be
quite handy when you  
have many variables in your workspace. Give it a try. (If
auto-completion doesn’t work for  
you, just type my_div and press Enter.)

``` r
my_div
```

    [1] 3.478505 3.181981 2.146460

### Задание 2. Workspace and Files

In this lesson, you’ll learn how to examine your local workspace in R
and begin to explore | the relationship between your workspace and the
file system of your machine.

    [1] "C:/Users/rudzs/OneDrive/Рабочий стол/УНИВЕР/7сем/Threat Hunting/Lab1/Lab1"

    [1] "my_div"  "my_sqrt" "x"       "y"       "z"      

    [1] "my_div"  "my_sqrt" "x"       "y"       "z"      

    [1] "Lab1.qmd"       "Lab1.rmarkdown" "README.md"      "testdir"       

    function (path = ".", pattern = NULL, all.files = FALSE, full.names = FALSE, 
        recursive = FALSE, ignore.case = FALSE, include.dirs = FALSE, 
        no.. = FALSE) 
    NULL

    Warning in dir.create("testdir"): 'testdir' уже существует

    [1] TRUE

    [1] "mytest.R"  "mytest2.R" "mytest3.R" "testdir2" 

    [1] TRUE

             size isdir mode               mtime               ctime
    mytest.R    0 FALSE  666 2023-09-21 11:46:41 2023-09-21 11:46:41
                           atime exe
    mytest.R 2023-09-21 11:46:41  no

    [1] TRUE

    [1] FALSE

    [1] "mytest3.R"

    [1] "folder1/folder2"

    Warning in dir.create(file.path("testdir2", "testdir3"), recursive = TRUE):
    'testdir2\testdir3' уже существует

### Задание 3. Sequences of Numbers

### Задание 4
