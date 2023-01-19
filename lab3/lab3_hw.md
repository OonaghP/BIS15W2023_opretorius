---
title: "Lab 3 Homework"
author: "Oonagh Pretorius"
date: "2023-01-18"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---

## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the tidyverse

```r
library(tidyverse)
```

## Mammals Sleep
  
1. For this assignment, we are going to use built-in data on mammal sleep patterns. From which publication are these data taken from? Since the data are built-in you can use the help function in R.

```r
msleep
```

```
## # A tibble: 83 × 11
##    name         genus vore  order conse…¹ sleep…² sleep…³ sleep…⁴ awake  brainwt
##    <chr>        <chr> <chr> <chr> <chr>     <dbl>   <dbl>   <dbl> <dbl>    <dbl>
##  1 Cheetah      Acin… carni Carn… lc         12.1    NA    NA      11.9 NA      
##  2 Owl monkey   Aotus omni  Prim… <NA>       17       1.8  NA       7    0.0155 
##  3 Mountain be… Aplo… herbi Rode… nt         14.4     2.4  NA       9.6 NA      
##  4 Greater sho… Blar… omni  Sori… lc         14.9     2.3   0.133   9.1  0.00029
##  5 Cow          Bos   herbi Arti… domest…     4       0.7   0.667  20    0.423  
##  6 Three-toed … Brad… herbi Pilo… <NA>       14.4     2.2   0.767   9.6 NA      
##  7 Northern fu… Call… carni Carn… vu          8.7     1.4   0.383  15.3 NA      
##  8 Vesper mouse Calo… <NA>  Rode… <NA>        7      NA    NA      17   NA      
##  9 Dog          Canis carni Carn… domest…    10.1     2.9   0.333  13.9  0.07   
## 10 Roe deer     Capr… herbi Arti… lc          3      NA    NA      21    0.0982 
## # … with 73 more rows, 1 more variable: bodywt <dbl>, and abbreviated variable
## #   names ¹​conservation, ²​sleep_total, ³​sleep_rem, ⁴​sleep_cycle
```

```r
?msleep
```

```
## starting httpd help server ... done
```
It is from V. M. Savage and G. B. West. A quantitative, theoretical framework for understanding mammalian sleep. Proceedings of the National Academy of Sciences, 104 (3):1051-1056, 2007.
  
2. Store these data into a new data frame `sleep`.

```r
sleep <- data.frame(msleep)
names(sleep)
```

```
##  [1] "name"         "genus"        "vore"         "order"        "conservation"
##  [6] "sleep_total"  "sleep_rem"    "sleep_cycle"  "awake"        "brainwt"     
## [11] "bodywt"
```
  
3. What are the dimensions of this data frame (variables and observations)? How do you know? Please show the *code* that you used to determine this below.  

```r
dim(sleep)
```

```
## [1] 83 11
```
This shows that there are 83 rows by 11 columns.

Alternatively, we can use str(), which provides additional metadata.

```r
str(sleep)
```

```
## 'data.frame':	83 obs. of  11 variables:
##  $ name        : chr  "Cheetah" "Owl monkey" "Mountain beaver" "Greater short-tailed shrew" ...
##  $ genus       : chr  "Acinonyx" "Aotus" "Aplodontia" "Blarina" ...
##  $ vore        : chr  "carni" "omni" "herbi" "omni" ...
##  $ order       : chr  "Carnivora" "Primates" "Rodentia" "Soricomorpha" ...
##  $ conservation: chr  "lc" NA "nt" "lc" ...
##  $ sleep_total : num  12.1 17 14.4 14.9 4 14.4 8.7 7 10.1 3 ...
##  $ sleep_rem   : num  NA 1.8 2.4 2.3 0.7 2.2 1.4 NA 2.9 NA ...
##  $ sleep_cycle : num  NA NA NA 0.133 0.667 ...
##  $ awake       : num  11.9 7 9.6 9.1 20 9.6 15.3 17 13.9 21 ...
##  $ brainwt     : num  NA 0.0155 NA 0.00029 0.423 NA NA NA 0.07 0.0982 ...
##  $ bodywt      : num  50 0.48 1.35 0.019 600 ...
```
  
4. Are there any NAs in the data? How did you determine this? Please show your code.  

```r
is.na(sleep)
```

```
##        name genus  vore order conservation sleep_total sleep_rem sleep_cycle
##  [1,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
##  [2,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE        TRUE
##  [3,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
##  [4,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
##  [5,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
##  [6,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
##  [7,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
##  [8,] FALSE FALSE  TRUE FALSE         TRUE       FALSE      TRUE        TRUE
##  [9,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [10,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [11,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [12,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [13,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [14,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [15,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [16,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE        TRUE
## [17,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [18,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [19,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [20,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [21,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [22,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [23,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [24,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [25,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [26,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [27,] FALSE FALSE FALSE FALSE         TRUE       FALSE      TRUE        TRUE
## [28,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [29,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
## [30,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [31,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [32,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [33,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [34,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
## [35,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [36,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [37,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [38,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
## [39,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [40,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [41,] FALSE FALSE FALSE FALSE         TRUE       FALSE      TRUE        TRUE
## [42,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [43,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
## [44,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [45,] FALSE FALSE FALSE FALSE         TRUE       FALSE      TRUE        TRUE
## [46,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [47,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [48,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [49,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [50,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
## [51,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [52,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [53,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [54,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
## [55,] FALSE FALSE  TRUE FALSE        FALSE       FALSE     FALSE        TRUE
## [56,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [57,] FALSE FALSE  TRUE FALSE         TRUE       FALSE      TRUE        TRUE
## [58,] FALSE FALSE  TRUE FALSE         TRUE       FALSE     FALSE        TRUE
## [59,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [60,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [61,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE        TRUE
## [62,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [63,] FALSE FALSE  TRUE FALSE        FALSE       FALSE     FALSE        TRUE
## [64,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [65,] FALSE FALSE FALSE FALSE         TRUE       FALSE      TRUE        TRUE
## [66,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE        TRUE
## [67,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [68,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
## [69,] FALSE FALSE  TRUE FALSE         TRUE       FALSE     FALSE        TRUE
## [70,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [71,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [72,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [73,] FALSE FALSE  TRUE FALSE         TRUE       FALSE     FALSE       FALSE
## [74,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [75,] FALSE FALSE FALSE FALSE         TRUE       FALSE      TRUE        TRUE
## [76,] FALSE FALSE FALSE FALSE         TRUE       FALSE      TRUE        TRUE
## [77,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [78,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE        TRUE
## [79,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
## [80,] FALSE FALSE FALSE FALSE         TRUE       FALSE      TRUE        TRUE
## [81,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE        TRUE
## [82,] FALSE FALSE FALSE FALSE         TRUE       FALSE      TRUE        TRUE
## [83,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
##       awake brainwt bodywt
##  [1,] FALSE    TRUE  FALSE
##  [2,] FALSE   FALSE  FALSE
##  [3,] FALSE    TRUE  FALSE
##  [4,] FALSE   FALSE  FALSE
##  [5,] FALSE   FALSE  FALSE
##  [6,] FALSE    TRUE  FALSE
##  [7,] FALSE    TRUE  FALSE
##  [8,] FALSE    TRUE  FALSE
##  [9,] FALSE   FALSE  FALSE
## [10,] FALSE   FALSE  FALSE
## [11,] FALSE   FALSE  FALSE
## [12,] FALSE   FALSE  FALSE
## [13,] FALSE    TRUE  FALSE
## [14,] FALSE   FALSE  FALSE
## [15,] FALSE   FALSE  FALSE
## [16,] FALSE   FALSE  FALSE
## [17,] FALSE   FALSE  FALSE
## [18,] FALSE   FALSE  FALSE
## [19,] FALSE   FALSE  FALSE
## [20,] FALSE   FALSE  FALSE
## [21,] FALSE   FALSE  FALSE
## [22,] FALSE   FALSE  FALSE
## [23,] FALSE   FALSE  FALSE
## [24,] FALSE   FALSE  FALSE
## [25,] FALSE   FALSE  FALSE
## [26,] FALSE   FALSE  FALSE
## [27,] FALSE    TRUE  FALSE
## [28,] FALSE   FALSE  FALSE
## [29,] FALSE   FALSE  FALSE
## [30,] FALSE    TRUE  FALSE
## [31,] FALSE    TRUE  FALSE
## [32,] FALSE   FALSE  FALSE
## [33,] FALSE   FALSE  FALSE
## [34,] FALSE   FALSE  FALSE
## [35,] FALSE    TRUE  FALSE
## [36,] FALSE   FALSE  FALSE
## [37,] FALSE    TRUE  FALSE
## [38,] FALSE   FALSE  FALSE
## [39,] FALSE    TRUE  FALSE
## [40,] FALSE   FALSE  FALSE
## [41,] FALSE    TRUE  FALSE
## [42,] FALSE   FALSE  FALSE
## [43,] FALSE   FALSE  FALSE
## [44,] FALSE    TRUE  FALSE
## [45,] FALSE   FALSE  FALSE
## [46,] FALSE    TRUE  FALSE
## [47,] FALSE    TRUE  FALSE
## [48,] FALSE   FALSE  FALSE
## [49,] FALSE   FALSE  FALSE
## [50,] FALSE   FALSE  FALSE
## [51,] FALSE    TRUE  FALSE
## [52,] FALSE   FALSE  FALSE
## [53,] FALSE    TRUE  FALSE
## [54,] FALSE   FALSE  FALSE
## [55,] FALSE   FALSE  FALSE
## [56,] FALSE    TRUE  FALSE
## [57,] FALSE    TRUE  FALSE
## [58,] FALSE   FALSE  FALSE
## [59,] FALSE    TRUE  FALSE
## [60,] FALSE    TRUE  FALSE
## [61,] FALSE    TRUE  FALSE
## [62,] FALSE   FALSE  FALSE
## [63,] FALSE   FALSE  FALSE
## [64,] FALSE   FALSE  FALSE
## [65,] FALSE    TRUE  FALSE
## [66,] FALSE   FALSE  FALSE
## [67,] FALSE   FALSE  FALSE
## [68,] FALSE   FALSE  FALSE
## [69,] FALSE   FALSE  FALSE
## [70,] FALSE   FALSE  FALSE
## [71,] FALSE   FALSE  FALSE
## [72,] FALSE    TRUE  FALSE
## [73,] FALSE   FALSE  FALSE
## [74,] FALSE   FALSE  FALSE
## [75,] FALSE   FALSE  FALSE
## [76,] FALSE    TRUE  FALSE
## [77,] FALSE   FALSE  FALSE
## [78,] FALSE   FALSE  FALSE
## [79,] FALSE   FALSE  FALSE
## [80,] FALSE    TRUE  FALSE
## [81,] FALSE   FALSE  FALSE
## [82,] FALSE   FALSE  FALSE
## [83,] FALSE   FALSE  FALSE
```

```r
#is.na.data.frame(sleep) does the same thing.
```
Yes, there are several NAs as shown when each entry is evaluated.

To simply ask if there are any NAs at all, we can use any(is.na(x)) 


```r
any(is.na(sleep))
```

```
## [1] TRUE
```
  
5. Show a list of the column names is this data frame.

```r
colnames(sleep)
```

```
##  [1] "name"         "genus"        "vore"         "order"        "conservation"
##  [6] "sleep_total"  "sleep_rem"    "sleep_cycle"  "awake"        "brainwt"     
## [11] "bodywt"
```
  
6. How many herbivores are represented in the data?  

```r
herbivores <- filter(sleep, vore=="herbi")
herbivores
```

```
##                              name        genus  vore          order
## 1                 Mountain beaver   Aplodontia herbi       Rodentia
## 2                             Cow          Bos herbi   Artiodactyla
## 3                Three-toed sloth     Bradypus herbi         Pilosa
## 4                        Roe deer    Capreolus herbi   Artiodactyla
## 5                            Goat        Capri herbi   Artiodactyla
## 6                      Guinea pig        Cavis herbi       Rodentia
## 7                      Chinchilla   Chinchilla herbi       Rodentia
## 8                      Tree hyrax  Dendrohyrax herbi     Hyracoidea
## 9                  Asian elephant      Elephas herbi    Proboscidea
## 10                          Horse        Equus herbi Perissodactyla
## 11                         Donkey        Equus herbi Perissodactyla
## 12      Western american chipmunk     Eutamias herbi       Rodentia
## 13                        Giraffe      Giraffa herbi   Artiodactyla
## 14                     Gray hyrax  Heterohyrax herbi     Hyracoidea
## 15                 Mongoose lemur        Lemur herbi       Primates
## 16               African elephant    Loxodonta herbi    Proboscidea
## 17               Mongolian gerbil     Meriones herbi       Rodentia
## 18                 Golden hamster Mesocricetus herbi       Rodentia
## 19                          Vole      Microtus herbi       Rodentia
## 20                    House mouse          Mus herbi       Rodentia
## 21           Round-tailed muskrat     Neofiber herbi       Rodentia
## 22                           Degu      Octodon herbi       Rodentia
## 23                         Rabbit  Oryctolagus herbi     Lagomorpha
## 24                          Sheep         Ovis herbi   Artiodactyla
## 25                        Potoroo     Potorous herbi  Diprotodontia
## 26                 Laboratory rat       Rattus herbi       Rodentia
## 27                     Cotton rat     Sigmodon herbi       Rodentia
## 28         Arctic ground squirrel Spermophilus herbi       Rodentia
## 29 Thirteen-lined ground squirrel Spermophilus herbi       Rodentia
## 30 Golden-mantled ground squirrel Spermophilus herbi       Rodentia
## 31      Eastern american chipmunk       Tamias herbi       Rodentia
## 32                Brazilian tapir      Tapirus herbi Perissodactyla
##    conservation sleep_total sleep_rem sleep_cycle awake brainwt   bodywt
## 1            nt        14.4       2.4          NA   9.6      NA    1.350
## 2  domesticated         4.0       0.7   0.6666667  20.0 0.42300  600.000
## 3          <NA>        14.4       2.2   0.7666667   9.6      NA    3.850
## 4            lc         3.0        NA          NA  21.0 0.09820   14.800
## 5            lc         5.3       0.6          NA  18.7 0.11500   33.500
## 6  domesticated         9.4       0.8   0.2166667  14.6 0.00550    0.728
## 7  domesticated        12.5       1.5   0.1166667  11.5 0.00640    0.420
## 8            lc         5.3       0.5          NA  18.7 0.01230    2.950
## 9            en         3.9        NA          NA  20.1 4.60300 2547.000
## 10 domesticated         2.9       0.6   1.0000000  21.1 0.65500  521.000
## 11 domesticated         3.1       0.4          NA  20.9 0.41900  187.000
## 12         <NA>        14.9        NA          NA   9.1      NA    0.071
## 13           cd         1.9       0.4          NA  22.1      NA  899.995
## 14           lc         6.3       0.6          NA  17.7 0.01227    2.625
## 15           vu         9.5       0.9          NA  14.5      NA    1.670
## 16           vu         3.3        NA          NA  20.7 5.71200 6654.000
## 17           lc        14.2       1.9          NA   9.8      NA    0.053
## 18           en        14.3       3.1   0.2000000   9.7 0.00100    0.120
## 19         <NA>        12.8        NA          NA  11.2      NA    0.035
## 20           nt        12.5       1.4   0.1833333  11.5 0.00040    0.022
## 21           nt        14.6        NA          NA   9.4      NA    0.266
## 22           lc         7.7       0.9          NA  16.3      NA    0.210
## 23 domesticated         8.4       0.9   0.4166667  15.6 0.01210    2.500
## 24 domesticated         3.8       0.6          NA  20.2 0.17500   55.500
## 25         <NA>        11.1       1.5          NA  12.9      NA    1.100
## 26           lc        13.0       2.4   0.1833333  11.0 0.00190    0.320
## 27         <NA>        11.3       1.1   0.1500000  12.7 0.00118    0.148
## 28           lc        16.6        NA          NA   7.4 0.00570    0.920
## 29           lc        13.8       3.4   0.2166667  10.2 0.00400    0.101
## 30           lc        15.9       3.0          NA   8.1      NA    0.205
## 31         <NA>        15.8        NA          NA   8.2      NA    0.112
## 32           vu         4.4       1.0   0.9000000  19.6 0.16900  207.501
```

```r
count(herbivores)
```

```
##    n
## 1 32
```
There are 32 herbivores in the dataframe.
Another approach is to use table():

```r
table(sleep$vore=="herbi")
```

```
## 
## FALSE  TRUE 
##    44    32
```
  
7. We are interested in two groups; small and large mammals. Let's define small as less than or equal to 1kg body weight and large as greater than or equal to 200kg body weight. Make two new dataframes (large and small) based on these parameters.

```r
large <- filter(sleep, bodywt>1)
large
```

```
##                      name         genus    vore           order conservation
## 1                 Cheetah      Acinonyx   carni       Carnivora           lc
## 2         Mountain beaver    Aplodontia   herbi        Rodentia           nt
## 3                     Cow           Bos   herbi    Artiodactyla domesticated
## 4        Three-toed sloth      Bradypus   herbi          Pilosa         <NA>
## 5       Northern fur seal   Callorhinus   carni       Carnivora           vu
## 6                     Dog         Canis   carni       Carnivora domesticated
## 7                Roe deer     Capreolus   herbi    Artiodactyla           lc
## 8                    Goat         Capri   herbi    Artiodactyla           lc
## 9                  Grivet Cercopithecus    omni        Primates           lc
## 10   Long-nosed armadillo       Dasypus   carni       Cingulata           lc
## 11             Tree hyrax   Dendrohyrax   herbi      Hyracoidea           lc
## 12 North American Opossum     Didelphis    omni Didelphimorphia           lc
## 13         Asian elephant       Elephas   herbi     Proboscidea           en
## 14                  Horse         Equus   herbi  Perissodactyla domesticated
## 15                 Donkey         Equus   herbi  Perissodactyla domesticated
## 16           Patas monkey  Erythrocebus    omni        Primates           lc
## 17           Domestic cat         Felis   carni       Carnivora domesticated
## 18                Giraffe       Giraffa   herbi    Artiodactyla           cd
## 19            Pilot whale Globicephalus   carni         Cetacea           cd
## 20              Gray seal  Haliochoerus   carni       Carnivora           lc
## 21             Gray hyrax   Heterohyrax   herbi      Hyracoidea           lc
## 22                  Human          Homo    omni        Primates         <NA>
## 23         Mongoose lemur         Lemur   herbi        Primates           vu
## 24       African elephant     Loxodonta   herbi     Proboscidea           vu
## 25                Macaque        Macaca    omni        Primates         <NA>
## 26             Slow loris     Nyctibeus   carni        Primates         <NA>
## 27                 Rabbit   Oryctolagus   herbi      Lagomorpha domesticated
## 28                  Sheep          Ovis   herbi    Artiodactyla domesticated
## 29             Chimpanzee           Pan    omni        Primates         <NA>
## 30                  Tiger      Panthera   carni       Carnivora           en
## 31                 Jaguar      Panthera   carni       Carnivora           nt
## 32                   Lion      Panthera   carni       Carnivora           vu
## 33                 Baboon         Papio    omni        Primates         <NA>
## 34                  Potto  Perodicticus    omni        Primates           lc
## 35              Phalanger     Phalanger    <NA>   Diprotodontia         <NA>
## 36           Caspian seal         Phoca   carni       Carnivora           vu
## 37        Common porpoise      Phocoena   carni         Cetacea           vu
## 38                Potoroo      Potorous   herbi   Diprotodontia         <NA>
## 39        Giant armadillo    Priodontes insecti       Cingulata           en
## 40             Rock hyrax      Procavia    <NA>      Hyracoidea           lc
## 41                    Pig           Sus    omni    Artiodactyla domesticated
## 42    Short-nosed echidna  Tachyglossus insecti     Monotremata         <NA>
## 43        Brazilian tapir       Tapirus   herbi  Perissodactyla           vu
## 44   Bottle-nosed dolphin      Tursiops   carni         Cetacea         <NA>
## 45                  Genet       Genetta   carni       Carnivora         <NA>
## 46             Arctic fox        Vulpes   carni       Carnivora         <NA>
## 47                Red fox        Vulpes   carni       Carnivora         <NA>
##    sleep_total sleep_rem sleep_cycle awake brainwt   bodywt
## 1         12.1        NA          NA 11.90      NA   50.000
## 2         14.4       2.4          NA  9.60      NA    1.350
## 3          4.0       0.7   0.6666667 20.00 0.42300  600.000
## 4         14.4       2.2   0.7666667  9.60      NA    3.850
## 5          8.7       1.4   0.3833333 15.30      NA   20.490
## 6         10.1       2.9   0.3333333 13.90 0.07000   14.000
## 7          3.0        NA          NA 21.00 0.09820   14.800
## 8          5.3       0.6          NA 18.70 0.11500   33.500
## 9         10.0       0.7          NA 14.00      NA    4.750
## 10        17.4       3.1   0.3833333  6.60 0.01080    3.500
## 11         5.3       0.5          NA 18.70 0.01230    2.950
## 12        18.0       4.9   0.3333333  6.00 0.00630    1.700
## 13         3.9        NA          NA 20.10 4.60300 2547.000
## 14         2.9       0.6   1.0000000 21.10 0.65500  521.000
## 15         3.1       0.4          NA 20.90 0.41900  187.000
## 16        10.9       1.1          NA 13.10 0.11500   10.000
## 17        12.5       3.2   0.4166667 11.50 0.02560    3.300
## 18         1.9       0.4          NA 22.10      NA  899.995
## 19         2.7       0.1          NA 21.35      NA  800.000
## 20         6.2       1.5          NA 17.80 0.32500   85.000
## 21         6.3       0.6          NA 17.70 0.01227    2.625
## 22         8.0       1.9   1.5000000 16.00 1.32000   62.000
## 23         9.5       0.9          NA 14.50      NA    1.670
## 24         3.3        NA          NA 20.70 5.71200 6654.000
## 25        10.1       1.2   0.7500000 13.90 0.17900    6.800
## 26        11.0        NA          NA 13.00 0.01250    1.400
## 27         8.4       0.9   0.4166667 15.60 0.01210    2.500
## 28         3.8       0.6          NA 20.20 0.17500   55.500
## 29         9.7       1.4   1.4166667 14.30 0.44000   52.200
## 30        15.8        NA          NA  8.20      NA  162.564
## 31        10.4        NA          NA 13.60 0.15700  100.000
## 32        13.5        NA          NA 10.50      NA  161.499
## 33         9.4       1.0   0.6666667 14.60 0.18000   25.235
## 34        11.0        NA          NA 13.00      NA    1.100
## 35        13.7       1.8          NA 10.30 0.01140    1.620
## 36         3.5       0.4          NA 20.50      NA   86.000
## 37         5.6        NA          NA 18.45      NA   53.180
## 38        11.1       1.5          NA 12.90      NA    1.100
## 39        18.1       6.1          NA  5.90 0.08100   60.000
## 40         5.4       0.5          NA 18.60 0.02100    3.600
## 41         9.1       2.4   0.5000000 14.90 0.18000   86.250
## 42         8.6        NA          NA 15.40 0.02500    4.500
## 43         4.4       1.0   0.9000000 19.60 0.16900  207.501
## 44         5.2        NA          NA 18.80      NA  173.330
## 45         6.3       1.3          NA 17.70 0.01750    2.000
## 46        12.5        NA          NA 11.50 0.04450    3.380
## 47         9.8       2.4   0.3500000 14.20 0.05040    4.230
```


```r
small <- filter(sleep, bodywt<=1)
small
```

```
##                              name        genus    vore           order
## 1                      Owl monkey        Aotus    omni        Primates
## 2      Greater short-tailed shrew      Blarina    omni    Soricomorpha
## 3                    Vesper mouse      Calomys    <NA>        Rodentia
## 4                      Guinea pig        Cavis   herbi        Rodentia
## 5                      Chinchilla   Chinchilla   herbi        Rodentia
## 6                 Star-nosed mole    Condylura    omni    Soricomorpha
## 7       African giant pouched rat   Cricetomys    omni        Rodentia
## 8       Lesser short-tailed shrew    Cryptotis    omni    Soricomorpha
## 9                   Big brown bat    Eptesicus insecti      Chiroptera
## 10              European hedgehog    Erinaceus    omni  Erinaceomorpha
## 11      Western american chipmunk     Eutamias   herbi        Rodentia
## 12                         Galago       Galago    omni        Primates
## 13           Thick-tailed opposum   Lutreolina   carni Didelphimorphia
## 14               Mongolian gerbil     Meriones   herbi        Rodentia
## 15                 Golden hamster Mesocricetus   herbi        Rodentia
## 16                          Vole      Microtus   herbi        Rodentia
## 17                    House mouse          Mus   herbi        Rodentia
## 18               Little brown bat       Myotis insecti      Chiroptera
## 19           Round-tailed muskrat     Neofiber   herbi        Rodentia
## 20                           Degu      Octodon   herbi        Rodentia
## 21     Northern grasshopper mouse    Onychomys   carni        Rodentia
## 22                Desert hedgehog  Paraechinus    <NA>  Erinaceomorpha
## 23                     Deer mouse   Peromyscus    <NA>        Rodentia
## 24                 Laboratory rat       Rattus   herbi        Rodentia
## 25          African striped mouse    Rhabdomys    omni        Rodentia
## 26                Squirrel monkey      Saimiri    omni        Primates
## 27          Eastern american mole     Scalopus insecti    Soricomorpha
## 28                     Cotton rat     Sigmodon   herbi        Rodentia
## 29                       Mole rat       Spalax    <NA>        Rodentia
## 30         Arctic ground squirrel Spermophilus   herbi        Rodentia
## 31 Thirteen-lined ground squirrel Spermophilus   herbi        Rodentia
## 32 Golden-mantled ground squirrel Spermophilus   herbi        Rodentia
## 33                     Musk shrew       Suncus    <NA>    Soricomorpha
## 34      Eastern american chipmunk       Tamias   herbi        Rodentia
## 35                         Tenrec       Tenrec    omni    Afrosoricida
## 36                     Tree shrew       Tupaia    omni      Scandentia
##    conservation sleep_total sleep_rem sleep_cycle awake brainwt bodywt
## 1          <NA>        17.0       1.8          NA   7.0 0.01550  0.480
## 2            lc        14.9       2.3   0.1333333   9.1 0.00029  0.019
## 3          <NA>         7.0        NA          NA  17.0      NA  0.045
## 4  domesticated         9.4       0.8   0.2166667  14.6 0.00550  0.728
## 5  domesticated        12.5       1.5   0.1166667  11.5 0.00640  0.420
## 6            lc        10.3       2.2          NA  13.7 0.00100  0.060
## 7          <NA>         8.3       2.0          NA  15.7 0.00660  1.000
## 8            lc         9.1       1.4   0.1500000  14.9 0.00014  0.005
## 9            lc        19.7       3.9   0.1166667   4.3 0.00030  0.023
## 10           lc        10.1       3.5   0.2833333  13.9 0.00350  0.770
## 11         <NA>        14.9        NA          NA   9.1      NA  0.071
## 12         <NA>         9.8       1.1   0.5500000  14.2 0.00500  0.200
## 13           lc        19.4       6.6          NA   4.6      NA  0.370
## 14           lc        14.2       1.9          NA   9.8      NA  0.053
## 15           en        14.3       3.1   0.2000000   9.7 0.00100  0.120
## 16         <NA>        12.8        NA          NA  11.2      NA  0.035
## 17           nt        12.5       1.4   0.1833333  11.5 0.00040  0.022
## 18         <NA>        19.9       2.0   0.2000000   4.1 0.00025  0.010
## 19           nt        14.6        NA          NA   9.4      NA  0.266
## 20           lc         7.7       0.9          NA  16.3      NA  0.210
## 21           lc        14.5        NA          NA   9.5      NA  0.028
## 22           lc        10.3       2.7          NA  13.7 0.00240  0.550
## 23         <NA>        11.5        NA          NA  12.5      NA  0.021
## 24           lc        13.0       2.4   0.1833333  11.0 0.00190  0.320
## 25         <NA>         8.7        NA          NA  15.3      NA  0.044
## 26         <NA>         9.6       1.4          NA  14.4 0.02000  0.743
## 27           lc         8.4       2.1   0.1666667  15.6 0.00120  0.075
## 28         <NA>        11.3       1.1   0.1500000  12.7 0.00118  0.148
## 29         <NA>        10.6       2.4          NA  13.4 0.00300  0.122
## 30           lc        16.6        NA          NA   7.4 0.00570  0.920
## 31           lc        13.8       3.4   0.2166667  10.2 0.00400  0.101
## 32           lc        15.9       3.0          NA   8.1      NA  0.205
## 33         <NA>        12.8       2.0   0.1833333  11.2 0.00033  0.048
## 34         <NA>        15.8        NA          NA   8.2      NA  0.112
## 35         <NA>        15.6       2.3          NA   8.4 0.00260  0.900
## 36         <NA>         8.9       2.6   0.2333333  15.1 0.00250  0.104
```

8. What is the mean weight for both the small and large mammals?

```r
mean(large$bodywt)
```

```
## [1] 293.1908
```


```r
mean(small$bodywt)
```

```
## [1] 0.2596667
```

9. Using a similar approach as above, do large or small animals sleep longer on average?  

```r
mean(large$sleep_total)
```

```
## [1] 8.729787
```


```r
mean(small$sleep_total)
```

```
## [1] 12.65833
```

```r
mean(large$sleep_total) < mean(small$sleep_total)
```

```
## [1] TRUE
```
On average, small animals sleep longer than large animals.


10. Which animal is the sleepiest among the entire dataframe?

```r
which.max(sleep$sleep_total)
```

```
## [1] 43
```
This tells us that the animal in row 43 sleeps the longest. By indexing, we can request that row and see that the sleepiest animal is the little brown bat.

```r
sleep[43,]
```

```
##                name  genus    vore      order conservation sleep_total
## 43 Little brown bat Myotis insecti Chiroptera         <NA>        19.9
##    sleep_rem sleep_cycle awake brainwt bodywt
## 43         2         0.2   4.1 0.00025   0.01
```

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
