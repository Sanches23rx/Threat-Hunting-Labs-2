Основы обработки данных с помощью R - 2
================
sanches23rx

## Цель работы

1.  Развить практические навыки использования языка программирования R
    для обработки данных
2.  Закрепить знания базовых типов данных языка R
3.  Развить пркатические навыки использования функций обработки данных
    пакета dplyr – функции select(), filter(), mutate(), arrange(),
    group_by()

## Ход работы

### Проанализировать встроенный в пакет dplyr набор данных starwars с помощью языка R и ответить на вопросы:

``` r
library(dplyr)
```

    Warning: пакет 'dplyr' был собран под R версии 4.2.3


    Присоединяю пакет: 'dplyr'

    Следующие объекты скрыты от 'package:stats':

        filter, lag

    Следующие объекты скрыты от 'package:base':

        intersect, setdiff, setequal, union

#### 1. Сколько строк в датафрейме?

``` r
starwars %>% nrow()
```

    [1] 87

#### 2. Сколько столбцов в датафрейме?

``` r
starwars %>% ncol()
```

    [1] 14

#### 3. Как просмотреть примерный вид датафрейма?

``` r
starwars %>% glimpse()
```

    Rows: 87
    Columns: 14
    $ name       <chr> "Luke Skywalker", "C-3PO", "R2-D2", "Darth Vader", "Leia Or…
    $ height     <int> 172, 167, 96, 202, 150, 178, 165, 97, 183, 182, 188, 180, 2…
    $ mass       <dbl> 77.0, 75.0, 32.0, 136.0, 49.0, 120.0, 75.0, 32.0, 84.0, 77.…
    $ hair_color <chr> "blond", NA, NA, "none", "brown", "brown, grey", "brown", N…
    $ skin_color <chr> "fair", "gold", "white, blue", "white", "light", "light", "…
    $ eye_color  <chr> "blue", "yellow", "red", "yellow", "brown", "blue", "blue",…
    $ birth_year <dbl> 19.0, 112.0, 33.0, 41.9, 19.0, 52.0, 47.0, NA, 24.0, 57.0, …
    $ sex        <chr> "male", "none", "none", "male", "female", "male", "female",…
    $ gender     <chr> "masculine", "masculine", "masculine", "masculine", "femini…
    $ homeworld  <chr> "Tatooine", "Tatooine", "Naboo", "Tatooine", "Alderaan", "T…
    $ species    <chr> "Human", "Droid", "Droid", "Human", "Human", "Human", "Huma…
    $ films      <list> <"The Empire Strikes Back", "Revenge of the Sith", "Return…
    $ vehicles   <list> <"Snowspeeder", "Imperial Speeder Bike">, <>, <>, <>, "Imp…
    $ starships  <list> <"X-wing", "Imperial shuttle">, <>, <>, "TIE Advanced x1",…

#### 4. Сколько уникальных рас персонажей (species) представлено в данных?

``` r
length(unique(starwars$species))
```

    [1] 38

#### 5. Найти самого высокого персонажа.

``` r
max(starwars$height, na.rm = TRUE)
```

    [1] 264

#### 6. Найти всех персонажей ниже 170

``` r
starwars %>% select(name, height) %>% filter(height < 170)
```

    # A tibble: 23 × 2
       name                  height
       <chr>                  <int>
     1 C-3PO                    167
     2 R2-D2                     96
     3 Leia Organa              150
     4 Beru Whitesun lars       165
     5 R5-D4                     97
     6 Yoda                      66
     7 Mon Mothma               150
     8 Wicket Systri Warrick     88
     9 Nien Nunb                160
    10 Watto                    137
    # ℹ 13 more rows

#### 7. Подсчитать ИМТ (индекс массы тела) для всех персонажей.

``` r
imt <- round((starwars$mass/((starwars$height/100)**2)), digits = 0)
data.frame(starwars$name, imt)
```

               starwars.name imt
    1         Luke Skywalker  26
    2                  C-3PO  27
    3                  R2-D2  35
    4            Darth Vader  33
    5            Leia Organa  22
    6              Owen Lars  38
    7     Beru Whitesun lars  28
    8                  R5-D4  34
    9      Biggs Darklighter  25
    10        Obi-Wan Kenobi  23
    11      Anakin Skywalker  24
    12        Wilhuff Tarkin  NA
    13             Chewbacca  22
    14              Han Solo  25
    15                Greedo  25
    16 Jabba Desilijic Tiure 443
    17        Wedge Antilles  27
    18      Jek Tono Porkins  34
    19                  Yoda  39
    20             Palpatine  26
    21             Boba Fett  23
    22                 IG-88  35
    23                 Bossk  31
    24      Lando Calrissian  25
    25                 Lobot  26
    26                Ackbar  26
    27            Mon Mothma  NA
    28          Arvel Crynyd  NA
    29 Wicket Systri Warrick  26
    30             Nien Nunb  27
    31          Qui-Gon Jinn  24
    32           Nute Gunray  25
    33         Finis Valorum  NA
    34         Jar Jar Binks  17
    35          Roos Tarpals  16
    36            Rugor Nass  NA
    37              Ric Olié  NA
    38                 Watto  NA
    39               Sebulba  32
    40         Quarsh Panaka  NA
    41        Shmi Skywalker  NA
    42            Darth Maul  26
    43           Bib Fortuna  NA
    44           Ayla Secura  17
    45              Dud Bolt  51
    46               Gasgano  NA
    47        Ben Quadinaros  24
    48            Mace Windu  24
    49          Ki-Adi-Mundi  21
    50             Kit Fisto  23
    51             Eeth Koth  NA
    52            Adi Gallia  15
    53           Saesee Tiin  NA
    54           Yarael Poof  NA
    55              Plo Koon  23
    56            Mas Amedda  NA
    57          Gregar Typho  25
    58                 Cordé  NA
    59           Cliegg Lars  NA
    60     Poggle the Lesser  24
    61       Luminara Unduli  19
    62         Barriss Offee  18
    63                 Dormé  NA
    64                 Dooku  21
    65   Bail Prestor Organa  NA
    66            Jango Fett  24
    67            Zam Wesell  19
    68       Dexter Jettster  26
    69               Lama Su  17
    70               Taun We  NA
    71            Jocasta Nu  NA
    72         Ratts Tyerell  24
    73                R4-P17  NA
    74            Wat Tambor  13
    75              San Hill  NA
    76              Shaak Ti  18
    77              Grievous  34
    78               Tarfful  25
    79       Raymus Antilles  22
    80             Sly Moore  15
    81            Tion Medon  19
    82                  Finn  NA
    83                   Rey  NA
    84           Poe Dameron  NA
    85                   BB8  NA
    86        Captain Phasma  NA
    87         Padmé Amidala  17

#### 8. Найти 10 самых “вытянутых” персонажей. “Вытянутость” оценить по отношению массы (mass) к росту (height) персонажей.

``` r
vityanutost <- starwars$mass/starwars$height
df <- data.frame(starwars$name, vityanutost)
df <- arrange(df, desc(vityanutost))
top_n(df, 10)
```

    Selecting by vityanutost

               starwars.name vityanutost
    1  Jabba Desilijic Tiure   7.7600000
    2               Grievous   0.7361111
    3                  IG-88   0.7000000
    4              Owen Lars   0.6741573
    5            Darth Vader   0.6732673
    6       Jek Tono Porkins   0.6111111
    7                  Bossk   0.5947368
    8                Tarfful   0.5811966
    9        Dexter Jettster   0.5151515
    10             Chewbacca   0.4912281

#### 9. Найти средний возраст персонажей каждой расы вселенной Звездных войн

``` r
library(tidyr)
```

    Warning: пакет 'tidyr' был собран под R версии 4.2.3

``` r
starwars %>% group_by(species) %>% drop_na() %>% summarise(mean(birth_year, trim = 0, na.rm = TRUE))
```

    # A tibble: 11 × 2
       species      `mean(birth_year, trim = 0, na.rm = TRUE)`
       <chr>                                             <dbl>
     1 Cerean                                             92  
     2 Ewok                                                8  
     3 Gungan                                             52  
     4 Human                                              45.5
     5 Kel Dor                                            22  
     6 Mirialan                                           49  
     7 Mon Calamari                                       41  
     8 Trandoshan                                         53  
     9 Twi'lek                                            48  
    10 Wookiee                                           200  
    11 Zabrak                                             54  

#### 10. Найти самый распространенный цвет глаз персонажей вселенной Звездных войн.

``` r
df1 <- starwars %>% group_by(eye_color) %>% summarise('count' = n())
arran <- arrange(df1, desc(count))
top_n(arran, 1)
```

    Selecting by count

    # A tibble: 1 × 2
      eye_color count
      <chr>     <int>
    1 brown        21

#### 11. Подсчитать среднюю длину имени в каждой расе вселенной Звездных войн.

``` r
starwars %>% group_by(species) %>% summarise(mean(nchar(name), trim = 0, na.rm = TRUE))
```

    # A tibble: 38 × 2
       species   `mean(nchar(name), trim = 0, na.rm = TRUE)`
       <chr>                                           <dbl>
     1 Aleena                                          13   
     2 Besalisk                                        15   
     3 Cerean                                          12   
     4 Chagrian                                        10   
     5 Clawdite                                        10   
     6 Droid                                            4.83
     7 Dug                                              7   
     8 Ewok                                            21   
     9 Geonosian                                       17   
    10 Gungan                                          11.7 
    # ℹ 28 more rows
