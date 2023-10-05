Основы обработки данных с помощью R - 3
================
sanches23rx

## Цель работы

1.  Зекрепить практические навыки использования языка программирования R
    для обработки данных
2.  Закрепить знания основных функций обработки данных экосистемы
    tidyverse языка R
3.  Развить пркатические навыки использования функций обработки данных
    пакета dplyr – функции select(), filter(), mutate(), arrange(),
    group_by()

## Ход работы

### Проанализировать встроенные в пакет nycflights13 наборы данных с помощью языка R и ответить на вопросы:

``` r
library(dplyr)
```

    Warning: пакет 'dplyr' был собран под R версии 4.2.3


    Присоединяю пакет: 'dplyr'

    Следующие объекты скрыты от 'package:stats':

        filter, lag

    Следующие объекты скрыты от 'package:base':

        intersect, setdiff, setequal, union

``` r
library(nycflights13)
```

    Warning: пакет 'nycflights13' был собран под R версии 4.2.3

### 1. Сколько встроенных в пакет nycflights13 датафреймов?

nycflights13::

Ответ: 5 датафреймов

### 2. Сколько строк в каждом датафрейме?

``` r
nycflights13::airlines %>% nrow()
```

    [1] 16

``` r
nycflights13::airports %>% nrow()
```

    [1] 1458

``` r
nycflights13::flights %>% nrow()
```

    [1] 336776

``` r
nycflights13::planes %>% nrow()
```

    [1] 3322

``` r
nycflights13::weather %>% nrow()
```

    [1] 26115

### 3. Сколько столбцов в каждом датафрейме?

``` r
nycflights13::airlines %>% ncol()
```

    [1] 2

``` r
nycflights13::airports %>% ncol()
```

    [1] 8

``` r
nycflights13::flights %>% ncol()
```

    [1] 19

``` r
nycflights13::planes %>% ncol()
```

    [1] 9

``` r
nycflights13::weather %>% ncol()
```

    [1] 15

### 4. Как просмотреть примерный вид датафрейма?

``` r
nycflights13::airports %>% glimpse()
```

    Rows: 1,458
    Columns: 8
    $ faa   <chr> "04G", "06A", "06C", "06N", "09J", "0A9", "0G6", "0G7", "0P2", "…
    $ name  <chr> "Lansdowne Airport", "Moton Field Municipal Airport", "Schaumbur…
    $ lat   <dbl> 41.13047, 32.46057, 41.98934, 41.43191, 31.07447, 36.37122, 41.4…
    $ lon   <dbl> -80.61958, -85.68003, -88.10124, -74.39156, -81.42778, -82.17342…
    $ alt   <dbl> 1044, 264, 801, 523, 11, 1593, 730, 492, 1000, 108, 409, 875, 10…
    $ tz    <dbl> -5, -6, -6, -5, -5, -5, -5, -5, -5, -8, -5, -6, -5, -5, -5, -5, …
    $ dst   <chr> "A", "A", "A", "A", "A", "A", "A", "A", "U", "A", "A", "U", "A",…
    $ tzone <chr> "America/New_York", "America/Chicago", "America/Chicago", "Ameri…

### 5. Сколько компаний-перевозчиков (carrier) учитывают эти наборы данных (представлено в наборах данных)?

``` r
nycflights13::airlines %>% nrow()
```

    [1] 16

### 6. Сколько рейсов принял аэропорт John F Kennedy Intl в мае?

``` r
nycflights13::flights %>% filter(month == 5, origin == "JFK") %>% nrow()
```

    [1] 9397

### 7. Какой самый северный аэропорт?

``` r
maxx <- max(nycflights13::airports$lat, na.rm = TRUE)
nycflights13::airports %>% select(name, lat) %>% filter(lat == maxx)
```

    # A tibble: 1 × 2
      name                      lat
      <chr>                   <dbl>
    1 Dillant Hopkins Airport  72.3

### 8. Какой аэропорт самый высокогорный (находится выше всех над уровнем моря)?

``` r
nycflights13::airports %>% arrange(desc(alt)) %>% select(name, alt) %>% top_n(1)
```

    Selecting by alt

    # A tibble: 1 × 2
      name        alt
      <chr>     <dbl>
    1 Telluride  9078

### 9. Какие бортовые номера у самых старых самолетов?

``` r
nycflights13::planes %>% select(tailnum, year) %>% filter(year == min(year, na.rm = TRUE))
```

    # A tibble: 1 × 2
      tailnum  year
      <chr>   <int>
    1 N381AA   1956

### 10. Какая средняя температура воздуха была в сентябре в аэропорту John F Kennedy Intl (в градусах Цельсия).

``` r
nycflights13::weather %>% filter(month == 9, origin == "JFK") %>% summarise('temperature' = ((temp_mean = mean(temp, 0, na.rm = TRUE))-32)*5/9)
```

    # A tibble: 1 × 1
      temperature
            <dbl>
    1        19.4

### 11. Самолеты какой авиакомпании совершили больше всего вылетов в июне?

``` r
df1 <- nycflights13::flights %>% group_by(carrier) %>% summarise('count_of_flights' = n())
arran <- arrange(df1, desc(count_of_flights))
topn <- top_n(arran, 1)
```

    Selecting by count_of_flights

``` r
filter(nycflights13::airlines, carrier == topn$carrier)
```

    # A tibble: 1 × 2
      carrier name                 
      <chr>   <chr>                
    1 UA      United Air Lines Inc.

### 12. Самолеты какой авиакомпании задерживались чаще других в 2013 году?

``` r
df2 <- nycflights13::flights %>% group_by(carrier) %>% filter(dep_delay > 0, arr_delay > 0) %>% summarise('counts' = n())
arran2 <- arrange(df2, desc(counts))
topn2 <- top_n(arran2, 1)
```

    Selecting by counts

``` r
filter(nycflights13::airlines, carrier == topn2$carrier)
```

    # A tibble: 1 × 2
      carrier name                    
      <chr>   <chr>                   
    1 EV      ExpressJet Airlines Inc.
