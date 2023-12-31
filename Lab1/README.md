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
and begin to explore the relationship between your workspace and the
file system of your machine.

``` r
getwd()
```

    [1] "C:/Users/rudzs/Рабочий стол/УНИВЕР/7сем/Threat Hunting/Lab1/Lab1"

``` r
ls()
```

    [1] "my_div"  "my_sqrt" "x"       "y"       "z"      

``` r
x <- 9

ls()
```

    [1] "my_div"  "my_sqrt" "x"       "y"       "z"      

``` r
dir()
```

    [1] "Lab1.qmd"       "Lab1.rmarkdown" "README.md"      "testdir"       

``` r
?list.files

args(list.files)
```

    function (path = ".", pattern = NULL, all.files = FALSE, full.names = FALSE, 
        recursive = FALSE, ignore.case = FALSE, include.dirs = FALSE, 
        no.. = FALSE) 
    NULL

``` r
old.dir <- getwd()

dir.create("testdir")
```

    Warning in dir.create("testdir"): 'testdir' уже существует

``` r
setwd("testdir")

file.create("mytest.R")
```

    [1] TRUE

``` r
list.files()
```

    [1] "mytest.R"  "mytest2.R" "mytest3.R" "testdir2" 

``` r
file.exists("mytest.R")
```

    [1] TRUE

``` r
file.info("mytest.R")
```

             size isdir mode               mtime               ctime
    mytest.R    0 FALSE  666 2023-09-24 14:29:53 2023-09-24 14:29:53
                           atime exe
    mytest.R 2023-09-24 14:29:53  no

``` r
file.rename("mytest.R", "mytest2.R")
```

    [1] TRUE

``` r
file.copy("mytest2.R", "mytest3.R")
```

    [1] FALSE

``` r
file.path("mytest3.R")
```

    [1] "mytest3.R"

``` r
file.path("folder1", "folder2")
```

    [1] "folder1/folder2"

``` r
?dir.create

dir.create(file.path('testdir2', 'testdir3'), recursive = TRUE)
```

    Warning in dir.create(file.path("testdir2", "testdir3"), recursive = TRUE):
    'testdir2\testdir3' уже существует

``` r
setwd(old.dir)
```

### Задание 3. Sequences of Numbers

In this lesson, you’ll learn how to create sequences of numbers in R.

``` r
1:20
```

     [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20

``` r
pi:10
```

    [1] 3.141593 4.141593 5.141593 6.141593 7.141593 8.141593 9.141593

``` r
15:1
```

     [1] 15 14 13 12 11 10  9  8  7  6  5  4  3  2  1

``` r
?':'
seq(1, 20)
```

     [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20

``` r
seq(0, 10, by=0.5)
```

     [1]  0.0  0.5  1.0  1.5  2.0  2.5  3.0  3.5  4.0  4.5  5.0  5.5  6.0  6.5  7.0
    [16]  7.5  8.0  8.5  9.0  9.5 10.0

``` r
my_seq <- seq(5, 10, length=30)
length(my_seq)
```

    [1] 30

``` r
1:length(my_seq)
```

     [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25
    [26] 26 27 28 29 30

``` r
seq(along.with = my_seq)
```

     [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25
    [26] 26 27 28 29 30

``` r
seq_along(my_seq)
```

     [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25
    [26] 26 27 28 29 30

``` r
rep(0, times = 40)
```

     [1] 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
    [39] 0 0

``` r
rep(c(0, 1, 2), times = 10)
```

     [1] 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2

``` r
rep(c(0, 1, 2), each = 10)
```

     [1] 0 0 0 0 0 0 0 0 0 0 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2

### Задание 4. Vectors

The simplest and most common data structure in R is the vector.

``` r
num_vect <- c(0.5, 55, -10, 6)
tf <- num_vect < 1
tf
```

    [1]  TRUE FALSE  TRUE FALSE

``` r
num_vect >= 6
```

    [1] FALSE  TRUE FALSE  TRUE

``` r
my_char <- c("My", "name", "is")
my_char
```

    [1] "My"   "name" "is"  

``` r
paste(my_char, collapse = " ")
```

    [1] "My name is"

``` r
c(my_char, "Sanches23rx")
```

    [1] "My"          "name"        "is"          "Sanches23rx"

``` r
my_name <- c(my_char, "Sanches23rx")
my_name
```

    [1] "My"          "name"        "is"          "Sanches23rx"

``` r
paste(my_name, collapse = " ")
```

    [1] "My name is Sanches23rx"

``` r
paste("Hello", "world!", sep = " ")
```

    [1] "Hello world!"

``` r
paste(c(1:3), c("X", "Y", "Z"), sep = "")
```

    [1] "1X" "2Y" "3Z"

``` r
paste(LETTERS, 1:4, sep = "-")
```

     [1] "A-1" "B-2" "C-3" "D-4" "E-1" "F-2" "G-3" "H-4" "I-1" "J-2" "K-3" "L-4"
    [13] "M-1" "N-2" "O-3" "P-4" "Q-1" "R-2" "S-3" "T-4" "U-1" "V-2" "W-3" "X-4"
    [25] "Y-1" "Z-2"

## Оценка результата

По итогам выполненных заданий в лабораторной работе №1 были получены
базовые навыки работы с языком R.

## Вывод

Таким образом, я изучил базовый синтаксис языка, научился работать с
файлами и векторами.
