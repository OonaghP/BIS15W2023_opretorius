---
title: "Lab 4 Homework"
author: "Please Add Your Name Here"
date: "2023-01-22"
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

## Data
For the homework, we will use data about vertebrate home range sizes. The data are in the class folder, but the reference is below.  

**Database of vertebrate home range sizes.**  
Reference: Tamburello N, Cote IM, Dulvy NK (2015) Energy and the scaling of animal space use. The American Naturalist 186(2):196-211. http://dx.doi.org/10.1086/682070.  
Data: http://datadryad.org/resource/doi:10.5061/dryad.q5j65/1  

**1. Load the data into a new object called `homerange`.**


```r
homerange <-  readr::read_csv("data/Tamburelloetal_HomeRangeDatabase.csv")
```

```
## Rows: 569 Columns: 24
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (16): taxon, common.name, class, order, family, genus, species, primarym...
## dbl  (8): mean.mass.g, log10.mass, mean.hra.m2, log10.hra, dimension, preyma...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


**2. Explore the data. Show the dimensions, column names, classes for each variable, and a statistical summary. Keep these as separate code chunks.**  


```r
dim(homerange)
```

```
## [1] 569  24
```

```r
names(homerange)
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```
glimpse() allows us to see the class of each variable without specifying each variable separately.

```r
glimpse(homerange)
```

```
## Rows: 569
## Columns: 24
## $ taxon                      <chr> "lake fishes", "river fishes", "river fishe…
## $ common.name                <chr> "american eel", "blacktail redhorse", "cent…
## $ class                      <chr> "actinopterygii", "actinopterygii", "actino…
## $ order                      <chr> "anguilliformes", "cypriniformes", "cyprini…
## $ family                     <chr> "anguillidae", "catostomidae", "cyprinidae"…
## $ genus                      <chr> "anguilla", "moxostoma", "campostoma", "cli…
## $ species                    <chr> "rostrata", "poecilura", "anomalum", "fundu…
## $ primarymethod              <chr> "telemetry", "mark-recapture", "mark-recapt…
## $ N                          <chr> "16", NA, "20", "26", "17", "5", "2", "2", …
## $ mean.mass.g                <dbl> 887.00, 562.00, 34.00, 4.00, 4.00, 3525.00,…
## $ log10.mass                 <dbl> 2.9479236, 2.7497363, 1.5314789, 0.6020600,…
## $ alternative.mass.reference <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ mean.hra.m2                <dbl> 282750.00, 282.10, 116.11, 125.50, 87.10, 3…
## $ log10.hra                  <dbl> 5.4514026, 2.4504031, 2.0648696, 2.0986437,…
## $ hra.reference              <chr> "Minns, C. K. 1995. Allometry of home range…
## $ realm                      <chr> "aquatic", "aquatic", "aquatic", "aquatic",…
## $ thermoregulation           <chr> "ectotherm", "ectotherm", "ectotherm", "ect…
## $ locomotion                 <chr> "swimming", "swimming", "swimming", "swimmi…
## $ trophic.guild              <chr> "carnivore", "carnivore", "carnivore", "car…
## $ dimension                  <dbl> 3, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 3, 3…
## $ preymass                   <dbl> NA, NA, NA, NA, NA, NA, 1.39, NA, NA, NA, N…
## $ log10.preymass             <dbl> NA, NA, NA, NA, NA, NA, 0.1430148, NA, NA, …
## $ PPMR                       <dbl> NA, NA, NA, NA, NA, NA, 530, NA, NA, NA, NA…
## $ prey.size.reference        <chr> NA, NA, NA, NA, NA, NA, "Brose U, et al. 20…
```
summary() also gives the classes

```r
summary(homerange)
```

```
##     taxon           common.name           class              order          
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##     family             genus             species          primarymethod     
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##       N              mean.mass.g        log10.mass     
##  Length:569         Min.   :      0   Min.   :-0.6576  
##  Class :character   1st Qu.:     50   1st Qu.: 1.6990  
##  Mode  :character   Median :    330   Median : 2.5185  
##                     Mean   :  34602   Mean   : 2.5947  
##                     3rd Qu.:   2150   3rd Qu.: 3.3324  
##                     Max.   :4000000   Max.   : 6.6021  
##                                                        
##  alternative.mass.reference  mean.hra.m2          log10.hra     
##  Length:569                 Min.   :0.000e+00   Min.   :-1.523  
##  Class :character           1st Qu.:4.500e+03   1st Qu.: 3.653  
##  Mode  :character           Median :3.934e+04   Median : 4.595  
##                             Mean   :2.146e+07   Mean   : 4.709  
##                             3rd Qu.:1.038e+06   3rd Qu.: 6.016  
##                             Max.   :3.551e+09   Max.   : 9.550  
##                                                                 
##  hra.reference         realm           thermoregulation    locomotion       
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  trophic.guild        dimension        preymass         log10.preymass   
##  Length:569         Min.   :2.000   Min.   :     0.67   Min.   :-0.1739  
##  Class :character   1st Qu.:2.000   1st Qu.:    20.02   1st Qu.: 1.3014  
##  Mode  :character   Median :2.000   Median :    53.75   Median : 1.7304  
##                     Mean   :2.218   Mean   :  3989.88   Mean   : 2.0188  
##                     3rd Qu.:2.000   3rd Qu.:   363.35   3rd Qu.: 2.5603  
##                     Max.   :3.000   Max.   :130233.20   Max.   : 5.1147  
##                                     NA's   :502         NA's   :502      
##       PPMR         prey.size.reference
##  Min.   :  0.380   Length:569         
##  1st Qu.:  3.315   Class :character   
##  Median :  7.190   Mode  :character   
##  Mean   : 31.752                      
##  3rd Qu.: 15.966                      
##  Max.   :530.000                      
##  NA's   :502
```

**3. Change the class of the variables `taxon` and `order` to factors and display their levels.**  


```r
homerange$taxon <- as.factor(homerange$taxon)
class(homerange$taxon)
```

```
## [1] "factor"
```


```r
levels(homerange$taxon)
```

```
## [1] "birds"         "lake fishes"   "lizards"       "mammals"      
## [5] "marine fishes" "river fishes"  "snakes"        "tortoises"    
## [9] "turtles"
```

```r
homerange$order <- as.factor(homerange$order)
class(homerange$order)
```

```
## [1] "factor"
```


```r
levels(homerange$order)
```

```
##  [1] "accipitriformes"       "afrosoricida"          "anguilliformes"       
##  [4] "anseriformes"          "apterygiformes"        "artiodactyla"         
##  [7] "caprimulgiformes"      "carnivora"             "charadriiformes"      
## [10] "columbidormes"         "columbiformes"         "coraciiformes"        
## [13] "cuculiformes"          "cypriniformes"         "dasyuromorpha"        
## [16] "dasyuromorpia"         "didelphimorphia"       "diprodontia"          
## [19] "diprotodontia"         "erinaceomorpha"        "esociformes"          
## [22] "falconiformes"         "gadiformes"            "galliformes"          
## [25] "gruiformes"            "lagomorpha"            "macroscelidea"        
## [28] "monotrematae"          "passeriformes"         "pelecaniformes"       
## [31] "peramelemorphia"       "perciformes"           "perissodactyla"       
## [34] "piciformes"            "pilosa"                "proboscidea"          
## [37] "psittaciformes"        "rheiformes"            "roden"                
## [40] "rodentia"              "salmoniformes"         "scorpaeniformes"      
## [43] "siluriformes"          "soricomorpha"          "squamata"             
## [46] "strigiformes"          "struthioniformes"      "syngnathiformes"      
## [49] "testudines"            "tinamiformes"          "tetraodontiformes\xa0"
```

**4. What taxa are represented in the `homerange` data frame? Make a new data frame `taxa` that is restricted to taxon, common name, class, order, family, genus, species.**  


```r
levels(homerange$taxon)
```

```
## [1] "birds"         "lake fishes"   "lizards"       "mammals"      
## [5] "marine fishes" "river fishes"  "snakes"        "tortoises"    
## [9] "turtles"
```

```r
taxa <- data.frame(select(homerange, c( "taxon", "common.name", "class", "order", "family", "genus", "species")))
#taxa
```

or you could use select(homerange, taxon:species)

**5. The variable `taxon` identifies the large, common name groups of the species represented in `homerange`. Make a table the shows the counts for each of these `taxon`.**  


```r
table(homerange$taxon)
```

```
## 
##         birds   lake fishes       lizards       mammals marine fishes 
##           140             9            11           238            90 
##  river fishes        snakes     tortoises       turtles 
##            14            41            12            14
```

**6. The species in `homerange` are also classified into trophic guilds. How many species are represented in each trophic guild.**  

```r
table(homerange$trophic.guild)
```

```
## 
## carnivore herbivore 
##       342       227
```

**7. Make two new data frames, one which is restricted to carnivores and another that is restricted to herbivores.**  

```r
carnivores <- data.frame(filter(homerange, trophic.guild == "carnivore"))
#carnivores
```


```r
herbivores <- data.frame(filter(homerange, trophic.guild == "herbivore"))
#herbivores
```

**8. Do herbivores or carnivores have, on average, a larger `mean.hra.m2`? Remove any NAs from the data.**  

```r
anyNA(homerange$mean.hra.m2)
```

```
## [1] FALSE
```
There are no NAs in this variable, but we include the "na.rm = TRUE" statement in case we did not know this.

```r
mean(herbivores$mean.hra.m2, na.rm = TRUE) > mean(carnivores$mean.hra.m2, na.rm = TRUE)
```

```
## [1] TRUE
```
Herbivores, on average have the larger home range areas.

**9. Make a new dataframe `deer` that is limited to the mean mass, log10 mass, family, genus, and species of deer in the database. The family for deer is cervidae. Arrange the data in descending order by log10 mass. Which is the largest deer? What is its common name?**  


```r
deer <-data.frame(select(homerange, c("mean.mass.g", "log10.mass", "family", "genus", "species")))
deer <-data.frame(filter(deer, family == "cervidae"))
deer
```

```
##    mean.mass.g log10.mass   family      genus     species
## 1    307227.44    5.48746 cervidae      alces       alces
## 2     62823.19    4.79812 cervidae       axis        axis
## 3     24050.27    4.38112 cervidae  capreolus   capreolus
## 4    234757.78    5.37062 cervidae     cervus     elaphus
## 5     29450.32    4.46909 cervidae     cervus      nippon
## 6     71449.63    4.85400 cervidae       dama        dama
## 7     13499.88    4.13033 cervidae  muntiacus     reevesi
## 8     53864.17    4.73130 cervidae odocoileus    hemionus
## 9     87884.04    4.94391 cervidae odocoileus virginianus
## 10    35000.16    4.54407 cervidae ozotoceros bezoarticus
## 11     7499.98    3.87506 cervidae       pudu        puda
## 12   102058.69    5.00885 cervidae   rangifer    tarandus
```
## Arrange data into descending order using desc()

```r
arrange(deer, desc(log10.mass))
```

```
##    mean.mass.g log10.mass   family      genus     species
## 1    307227.44    5.48746 cervidae      alces       alces
## 2    234757.78    5.37062 cervidae     cervus     elaphus
## 3    102058.69    5.00885 cervidae   rangifer    tarandus
## 4     87884.04    4.94391 cervidae odocoileus virginianus
## 5     71449.63    4.85400 cervidae       dama        dama
## 6     62823.19    4.79812 cervidae       axis        axis
## 7     53864.17    4.73130 cervidae odocoileus    hemionus
## 8     35000.16    4.54407 cervidae ozotoceros bezoarticus
## 9     29450.32    4.46909 cervidae     cervus      nippon
## 10    24050.27    4.38112 cervidae  capreolus   capreolus
## 11    13499.88    4.13033 cervidae  muntiacus     reevesi
## 12     7499.98    3.87506 cervidae       pudu        puda
```
According to the data, the largest deer is Alces alces. To find its common name, we will have to look it up on the full dataframe:

```r
filter(homerange, species == "alces")
```

```
## # A tibble: 1 × 24
##   taxon   commo…¹ class order family genus species prima…² N     mean.…³ log10…⁴
##   <fct>   <chr>   <chr> <fct> <chr>  <chr> <chr>   <chr>   <chr>   <dbl>   <dbl>
## 1 mammals moose   mamm… arti… cervi… alces alces   teleme… <NA>  307227.    5.49
## # … with 13 more variables: alternative.mass.reference <chr>,
## #   mean.hra.m2 <dbl>, log10.hra <dbl>, hra.reference <chr>, realm <chr>,
## #   thermoregulation <chr>, locomotion <chr>, trophic.guild <chr>,
## #   dimension <dbl>, preymass <dbl>, log10.preymass <dbl>, PPMR <dbl>,
## #   prey.size.reference <chr>, and abbreviated variable names ¹​common.name,
## #   ²​primarymethod, ³​mean.mass.g, ⁴​log10.mass
```
Now we can see that this entry correlates to "moose".

**10. As measured by the data, which snake species has the smallest homerange? Show all of your work, please. Look this species up online and tell me about it!** **Snake is found in taxon column**    


```r
snakes <- data.frame(filter(homerange, taxon == "snakes"))
#snakes
```


```r
arrange(snakes, desc(mean.hra.m2))
```

```
##     taxon                common.name    class    order     family         genus
## 1  snakes         timber rattlesnake reptilia squamata  viperidae      crotalus
## 2  snakes       eastern indigo snake reptilia squamata colubridae    drymarchon
## 3  snakes   midget faded rattlesnake reptilia squamata  viperidae      crotalus
## 4  snakes                 pine snake reptilia squamata colubridae     pituophis
## 5  snakes              hognose snake reptilia squamata colubridae     heterodon
## 6  snakes          Eastern kingsnake reptilia squamata colubridae  lampropeltis
## 7  snakes                  coachwhip reptilia squamata colubridae   masticophis
## 8  snakes        giant garter snakes reptilia squamata colubridae    thamnophis
## 9  snakes         Mojave rattlesnake reptilia squamata  viperidae      crotalus
## 10 snakes             Armenian viper reptilia squamata  viperidae   montivipera
## 11 snakes                  milksnake reptilia squamata colubridae  lampropeltis
## 12 snakes southwestern carpet python reptilia squamata pythonidae       morelia
## 13 snakes                      racer reptilia squamata colubridae       coluber
## 14 snakes      great plains ratsnake reptilia squamata colubridae        elaphe
## 15 snakes     copperbelly watersnake reptilia squamata colubridae       nerodia
## 16 snakes                 copperhead reptilia squamata  viperidae   agkistrodon
## 17 snakes       yellow bellied racer reptilia squamata colubridae       coluber
## 18 snakes         European whipsnake reptilia squamata colubridae     hierophis
## 19 snakes                grass snake reptilia squamata colubridae        natrix
## 20 snakes                 blacksnake reptilia squamata   elapidae    pseudechis
## 21 snakes          Aesculapian snake reptilia squamata colubridae       zamenis
## 22 snakes               fer-de-lance reptilia squamata  viperidae      bothrops
## 23 snakes        western diamondback reptilia squamata  viperidae      crotalus
## 24 snakes           western ratsnake reptilia squamata colubridae        elaphe
## 25 snakes        Northern watersnake reptilia squamata colubridae       nerodia
## 26 snakes                tiger snake reptilia squamata   elapidae      notechis
## 27 snakes    blacktailed rattlesnake reptilia squamata  viperidae      crotalus
## 28 snakes          tiger rattlesnake reptilia squamata  viperidae      crotalus
## 29 snakes                 sidewinder reptilia squamata  viperidae      crotalus
## 30 snakes          broadheaded snake reptilia squamata   elapidae hoplocephalus
## 31 snakes   twin-spotted rattlesnake reptilia squamata  viperidae      crotalus
## 32 snakes               gopher snake reptilia squamata colubridae     pituophis
## 33 snakes         redbacked ratsnake reptilia squamata colubridae    oocatochus
## 34 snakes                cottonmouth reptilia squamata  viperidae   agkistrodon
## 35 snakes             ringneck snake reptilia squamata colubridae     diadophis
## 36 snakes          chinese pit viper reptilia squamata  viperidae      gloydius
## 37 snakes            snubnosed viper reptilia squamata  viperidae        vipera
## 38 snakes         western worm snake reptilia squamata colubridae     carphopis
## 39 snakes       butlers garter snake reptilia squamata colubridae    thamnophis
## 40 snakes         eastern worm snake reptilia squamata colubridae     carphopis
## 41 snakes        namaqua dwarf adder reptilia squamata  viperidae         bitis
##                     species  primarymethod    N mean.mass.g log10.mass
## 1                  horridus      telemetry    6     1020.00  3.0086002
## 2                   couperi      telemetry    1      450.00  2.6532125
## 3         oreganus concolor      telemetry   21      138.70  2.1420765
## 4              melanoleucus      telemetry   12     1004.00  3.0017337
## 5               platirhinos      telemetry    8      147.32  2.1682617
## 6             getula getula      telemetry   12      315.72  2.4993021
## 7                 flagellum      telemetry    4      534.50  2.7279477
## 8                     gigal      telemetry   11      306.00  2.4857214
## 9                scutulatus      telemetry   19      280.30  2.4476231
## 10                   raddei      telemetry   14      162.14  2.2098902
## 11               triangulum      telemetry   10      165.00  2.2174839
## 12        spilota imbricata      telemetry   33     1226.85  3.0887915
## 13              constrictor      telemetry   15      556.15  2.7451919
## 14           guttata emoryi      telemetry   12      256.70  2.4094259
## 15            erythrogaster      telemetry   15      313.24  2.4958772
## 16               contortrix      telemetry   18      231.12  2.3638375
## 17 constrictor flaviventris      telemetry   12      144.50  2.1598678
## 18             viridiflavus      telemetry   32      234.10  2.3694014
## 19                   natrix      telemetry    4       78.50  1.8948697
## 20             porphyriacus      telemetry   44      479.00  2.6803355
## 21              longissimus      telemetry   32      249.30  2.3967223
## 22                    asper      telemetry    6      826.23  2.9171010
## 23                    atrox      telemetry   14      319.90  2.5050142
## 24                 obsoleta      telemetry   18      642.80  2.8080759
## 25                 sipeodon      telemetry   13      190.55  2.2800090
## 26                 scutatus      telemetry    5      330.00  2.5185139
## 27                 molossus      telemetry    3      414.00  2.6170003
## 28                   tigris      telemetry    3      234.70  2.3705131
## 29                 cerastes      telemetry   25      106.70  2.0281644
## 30              bungaroides      telemetry   24       48.79  1.6883308
## 31                   pricei      telemetry    5       67.20  1.8273693
## 32                catenifer      telemetry    4      375.00  2.5740313
## 33             rufodorsatus      telemetry   21       62.50  1.7958800
## 34              piscivorous      telemetry   15      188.00  2.2741578
## 35                punctatus mark-recapture <NA>        9.00  0.9542425
## 36              shedaoensis      telemetry   16      196.81  2.2940472
## 37                 latastei      telemetry    7       97.40  1.9885590
## 38                   vermis       radiotag    1        3.46  0.5390761
## 39                  butleri mark-recapture    1       21.51  1.3326404
## 40                  viridis       radiotag   10        3.65  0.5622929
## 41               schneideri      telemetry   11       16.95  1.2291697
##    alternative.mass.reference mean.hra.m2 log10.hra
## 1                        <NA>  2579600.00  6.411552
## 2                        <NA>  1853000.00  6.267875
## 3                        <NA>  1178000.00  6.071145
## 4                        <NA>   701000.00  5.845718
## 5                        <NA>   516375.00  5.712965
## 6                        <NA>   495000.00  5.694605
## 7                        <NA>   429300.00  5.632761
## 8                        <NA>   374800.00  5.573800
## 9                        <NA>   316000.00  5.499687
## 10                       <NA>   245928.57  5.390809
## 11                       <NA>   240400.00  5.380934
## 12                       <NA>   171600.00  5.234517
## 13                       <NA>   151000.00  5.178977
## 14                       <NA>   150600.00  5.177825
## 15                       <NA>   131000.00  5.117271
## 16                       <NA>   119288.89  5.076600
## 17                       <NA>   114500.00  5.058805
## 18                       <NA>   110900.00  5.044932
## 19                       <NA>    99000.00  4.995635
## 20                       <NA>    96000.00  4.982271
## 21                       <NA>    77400.00  4.888741
## 22                       <NA>    60700.00  4.783189
## 23                       <NA>    54200.00  4.733999
## 24                       <NA>    46000.00  4.662758
## 25                       <NA>    40000.00  4.602060
## 26                       <NA>    38800.00  4.588832
## 27                       <NA>    34900.00  4.542825
## 28                       <NA>    34800.00  4.541579
## 29                       <NA>    28000.00  4.447158
## 30                       <NA>    27379.00  4.437418
## 31                       <NA>    22900.00  4.359835
## 32                       <NA>    17400.00  4.240549
## 33                       <NA>    15400.00  4.187521
## 34                       <NA>    10655.00  4.027553
## 35                       <NA>     6476.00  3.811307
## 36                       <NA>     2613.69  3.417254
## 37                       <NA>     2400.00  3.380211
## 38                       <NA>      700.00  2.845098
## 39                       <NA>      600.00  2.778151
## 40                       <NA>      253.00  2.403121
## 41                       <NA>      200.00  2.301030
##                                                                                                                                                                                                                                             hra.reference
## 1  Bauder JM, Blodgett D, Briggs KV, Jenkins CL. 2011. The Ecology of Timber Rattlesnakes (Crotalus horridus) in Vermont: A First Year Progress Report Submitted to the Vermont Department of Fish and Wildlife. Vermont Department of Fish and Wildlife.
## 2                                                                                                            Dodd CK, Barichivich WJ. 2007. Movements of large snakes (Drymarchon, Masticophis_ in North-central Florida. Florida Scientist 70(1), 83-94.
## 3                                                                                            Parker JM, Anderson SH. 2007. Ecology and Behavior of the Midget Faded Rattlesnake (Crotalus Oreganus Concolor) in Wyoming. Journal of Herpetology 1, 41-51.
## 4                                                                                    Miller GJ, Smith LL, Johnson SA, Franz R. 2012. Home Range Size and Habitat Selection in the Florida Pine Snake (Pituophis melanoleucus mugitus). Copeia 4, 706-713.
## 5                                                                                 Plummer MV, Mills NE. 2000. Spatial Ecology and Survivorship of Resident and Translocated Hognose Snakes (Heterodonplatirhinos). Journal of Herpetology 34(4), 565-575.
## 6                              Linehan JM, Smith LL, Steen DA. 2010. Ecology of the Eastern kingsnake (Lampropeltis getula getula) in a longleaf pine (Pinus palustris) forest in Southwestern Georgia. Herpetological Conservation Biology 5(1), 94-101.
## 7                                                                                                            Dodd CK, Barichivich WJ. 2007. Movements of large snakes (Drymarchon, Masticophis_ in North-central Florida. Florida Scientist 70(1), 83-94.
## 8     Wylie G, Amarello M. 2006.  For the Bank Protection Project on the Left Bank of the Colusa Basin Drainage Canal in Reclamation District. Progress report for the U.S. Army Corps of Engineers.\nSacramento River Bank Protection Project, Phase II.
## 9                                                                                                                                                      Cardwell MD. 2008. The reproductive ecology of Mohave rattlesnakes. Journal of Zoology 274, 65-76.
## 10                                                                                         Ettling JA, Aghasyan LA, Aghasyan AL, Parker PG. 2013. Spatial Ecology of Armenian Vipers, Montivipera raddei, in a Human-Modified Landscape. Copeia 1, 64-71.
## 11                                                                                                                             Row JR, Blouin-Demers G. 2006. Kernels are not Accurate Estimators of Home-Range Size For Herpetofauna. Copeia 4, 797-802.
## 12                                                                 Pearson D, Shine R, Williams A. 2005. Spatial ecology of a threatened python (Morelia spilota imbricata) and the effects of anthropogenic habitat change. Austral Ecology 30, 261-274.
## 13                                                  Carfagno GLF, Weatherhead PJ. 2008. Energetics and space use: intraspecific and interspecific comparisons of movements and home ranges of two Colubrid snakes. Journal of Animal Ecology 77, 416-424.
## 14         Klug PE, Fill J, With KA. 2011. Spatial ecology of Eastern yellow-bellies racer (Coluber constrictor flaviventris) and great plains rat snake (Pantherophis emoryi) in a contiguous tallgrass-prairie landscape. Herpetologica 67(4), 428-439.
## 15                                                                     Roe JH, Kingsbury BA, Herbert NR. 2004. Comparative water snake ecology: conservation of mobile animals that use temporally dynamic resources. Biological Conservation 118, 79-89.
## 16                                        Smith CF, Schuett GW, Early RL, Schwenk K. 2009. The Spatial and Resproductive Ecology of the Copperhead (Agkistrodon contortrix) at the Northeastern Extrme of its Range. Herpetological Monographs 23, 45-73.
## 17         Klug PE, Fill J, With KA. 2011. Spatial ecology of Eastern yellow-bellies racer (Coluber constrictor flaviventris) and great plains rat snake (Pantherophis emoryi) in a contiguous tallgrass-prairie landscape. Herpetologica 67(4), 428-439.
## 18                                                           Herbe L, Moreau C, Blouin-Demers G, Bonnet X, Lourdais O. 2012. Two Syntopic Colubrid Snakes Differ In Their Energetic Requirements and In Their Use of Space. Herpetologica 68(3), 358-364.
## 19                                                                                                        Madsen T. 1984. Movements, Home Range Size and Habitat Use of Radio-Tracked Grass Snakes (Natrix natrix) in Southern Sweden. Copeia 3, 707-713.
## 20                                                            Shine R. 1987. Intraspecific Variation in Thermoregulation, Movements and Habitat Use by Australian Blacksnakes, Pseudechis porphyriacus (Elapidae). Journal of Herpetology 21(3), 165-177.
## 21                                                           Herbe L, Moreau C, Blouin-Demers G, Bonnet X, Lourdais O. 2012. Two Syntopic Colubrid Snakes Differ In Their Energetic Requirements and In Their Use of Space. Herpetologica 68(3), 358-364.
## 22                                        Wasko DK, Sasa M. 2012. Food resources influence spatial ecology, habitat selection, and foraging behavior in an ambush-hunting snake (Viperidae: Bothrops asper): an experimental study. Zoology 115, 179-187.
## 23                                                                                                             Beck DD. 1995. Ecology and Energetics of Three Sympatric Rattlesnake Species in the Sonoran Desert. Journal of Herpetology 29(2), 211-223.
## 24                                                  Carfagno GLF, Weatherhead PJ. 2008. Energetics and space use: intraspecific and interspecific comparisons of movements and home ranges of two Colubrid snakes. Journal of Animal Ecology 77, 416-424.
## 25                                                                     Roe JH, Kingsbury BA, Herbert NR. 2004. Comparative water snake ecology: conservation of mobile animals that use temporally dynamic resources. Biological Conservation 118, 79-89.
## 26                                                                   Butler H, Malone B, Clemann N. 2005. The effects of translocation on the spatial ecology of tiger snakes (Notechis scutatus) in a suburban landscape. Wildlife Research 32, 165-171.
## 27                                                                                                             Beck DD. 1995. Ecology and Energetics of Three Sympatric Rattlesnake Species in the Sonoran Desert. Journal of Herpetology 29(2), 211-223.
## 28                                                                                                             Beck DD. 1995. Ecology and Energetics of Three Sympatric Rattlesnake Species in the Sonoran Desert. Journal of Herpetology 29(2), 211-223.
## 29                                                                                                                      Secor SM. 1994. Ecological Significance of Movements and Activity Range for the Sidewinder, Crotalus cerastes. Copeia 3, 631-645.
## 30                                                                                  Webb JK, Shine R. 1997. A Field Study of Spatial Ecology and Movements of a Threatened Snake Species, Hoplocephalus bungaroides. Biological Conservation 82, 203-217.
## 31                                                           Prival DB, Goode MJ, Swann DE, Schwalbe CR, Schroff MJ. 2002. Natural History of a Northern Population of Twin-Spotted Rattlesnakes, Crotalus pricei. Journal of Herpetology 36(4), 598-607.
## 32                                                                                                                    Rodriguez-Robles JA. 2003. Home Ranges of Gopher Snakes (Pituophis catenifer, Colubridae) in Central California. Copeia 2, 391-396.
## 33                                                                       Lee H-J, Lee J-H, Park D. 2011. Habitat Use and Movement Patterns of the Viviparous Aquatic Snake, Oocatochus rufodorsatus, from Northeast Asia. Zoological Science 28, 593-599.
## 34                                                                                                             Roth ED. 2005. Spatial Ecology of a Cottonmouth (Agkistrodon piscivorus) Population in East Texas. Journal of Herpetology  39(2), 308-312.
## 35                                                                            Fitch HS. 1975. A Demographic Study of the Ringneck Snake (Diadophis punctatus) in Kansas. University of Kansas Museum of Natural History Miscellaneous Publication No. 62.
## 36                                                                                           Shine R, Sun L-X. 2003. Attack strategy of an ambush predator: which attributes of the prey trigger a pit-viper\x92s strike? Functional Ecology 17, 340-348.
## 37                                                                                      Brito JC. 2003. Seasonal Variation in Movements, Home Range, and Habitat Use by Male Vipera latastei in Northern Portugal. Journal of Herpetology 37(1), 155-160.
## 38                                                                                        Clark DR. 1970. Age-Specific "Reproductive Effort" in the Worm Snake Carphophis vermis (Kennicott). Transactions of the Kansas Academy of Science 73(1), 20-24.
## 39                                                                                                              Freedman B, Catling PM. 1979. Movements of sympatric species of snakes at Amherstburg, Ontatio. Canadian Field-Naturalist 93(4): 399-404.
## 40                                                                                         Barbour RW, Harvey MJ, and Hardin JW. 1969. Home Range, Movements, and Activity of the Eastern Worm Snake, Carphophis Amoenus Amoenus. Ecology 50(3), 470-476.
## 41                                                                                                                  Maritz B, Alexander GJ. 2012. Dwarfs on the Move: Spatial Ecology of the World's Smallest Viper, Bitis schneideri. Copeia 1, 115-120.
##          realm thermoregulation locomotion trophic.guild dimension preymass
## 1  terrestrial        ectotherm   crawling     carnivore         2  2684.21
## 2  terrestrial        ectotherm   crawling     carnivore         2       NA
## 3  terrestrial        ectotherm   crawling     carnivore         2    51.56
## 4  terrestrial        ectotherm   crawling     carnivore         2    53.75
## 5  terrestrial        ectotherm   crawling     carnivore         2       NA
## 6  terrestrial        ectotherm   crawling     carnivore         2       NA
## 7  terrestrial        ectotherm   crawling     carnivore         2       NA
## 8  terrestrial        ectotherm   crawling     carnivore         2       NA
## 9  terrestrial        ectotherm   crawling     carnivore         2       NA
## 10 terrestrial        ectotherm   crawling     carnivore         2       NA
## 11 terrestrial        ectotherm   crawling     carnivore         2       NA
## 12 terrestrial        ectotherm   crawling     carnivore         2       NA
## 13 terrestrial        ectotherm   crawling     carnivore         2   617.94
## 14 terrestrial        ectotherm   crawling     carnivore         2       NA
## 15 terrestrial        ectotherm   crawling     carnivore         2       NA
## 16 terrestrial        ectotherm   crawling     carnivore         2       NA
## 17 terrestrial        ectotherm   crawling     carnivore         2   160.56
## 18 terrestrial        ectotherm   crawling     carnivore         2    40.78
## 19 terrestrial        ectotherm   crawling     carnivore         2    13.99
## 20 terrestrial        ectotherm   crawling     carnivore         2       NA
## 21 terrestrial        ectotherm    walking     carnivore         2       NA
## 22 terrestrial        ectotherm   crawling     carnivore         2   165.25
## 23 terrestrial        ectotherm   crawling     carnivore         2    12.80
## 24 terrestrial        ectotherm   crawling     carnivore         2    71.50
## 25 terrestrial        ectotherm   crawling     carnivore         2    97.72
## 26 terrestrial        ectotherm   crawling     carnivore         2    45.90
## 27 terrestrial        ectotherm   crawling     carnivore         2       NA
## 28 terrestrial        ectotherm   crawling     carnivore         2       NA
## 29 terrestrial        ectotherm   crawling     carnivore         2       NA
## 30 terrestrial        ectotherm   crawling     carnivore         2       NA
## 31 terrestrial        ectotherm   crawling     carnivore         2       NA
## 32 terrestrial        ectotherm   crawling     carnivore         2       NA
## 33 terrestrial        ectotherm   crawling     carnivore         2       NA
## 34 terrestrial        ectotherm   crawling     carnivore         2    51.93
## 35 terrestrial        ectotherm   crawling     carnivore         2       NA
## 36 terrestrial        ectotherm   crawling     carnivore         2    14.00
## 37 terrestrial        ectotherm   crawling     carnivore         2     8.97
## 38 terrestrial        ectotherm   crawling     carnivore         2       NA
## 39 terrestrial        ectotherm   crawling     carnivore         2       NA
## 40 terrestrial        ectotherm   crawling     carnivore         2       NA
## 41 terrestrial        ectotherm   crawling     carnivore         2       NA
##    log10.preymass  PPMR
## 1       3.4288165  0.38
## 2              NA    NA
## 3       1.7123129  2.69
## 4       1.7303785 18.68
## 5              NA    NA
## 6              NA    NA
## 7              NA    NA
## 8              NA    NA
## 9              NA    NA
## 10             NA    NA
## 11             NA    NA
## 12             NA    NA
## 13      2.7909463  0.90
## 14             NA    NA
## 15             NA    NA
## 16             NA    NA
## 17      2.2056374  0.90
## 18      1.6104472  5.74
## 19      1.1458177  5.61
## 20             NA    NA
## 21             NA    NA
## 22      2.2181415  5.00
## 23      1.1072100 25.00
## 24      1.8543060  8.99
## 25      1.9899835 14.63
## 26      1.6618127  7.19
## 27             NA    NA
## 28             NA    NA
## 29             NA    NA
## 30             NA    NA
## 31             NA    NA
## 32             NA    NA
## 33             NA    NA
## 34      1.7154183  3.62
## 35             NA    NA
## 36      1.1461280 14.06
## 37      0.9527924 10.86
## 38             NA    NA
## 39             NA    NA
## 40             NA    NA
## 41             NA    NA
##                                                                                                                                                                                                                                                                               prey.size.reference
## 1                                                                                                                                                                                       Clark RW. 2002. Diet of the timber rattlesnake, Crotalus horridus. Journal of Herpetology 36(3), 494-499.
## 2                                                                                                                                                                                                                                                                                            <NA>
## 3                                                                                             Carbone C, Daryl C, Conrad S, Marcus C, Belby J. 2014. Geometric factors influencing the diet of vertebrate predators in marine and terrestrial environments. Ecology Letters 17(12): 1553\x961559.
## 4                                                                                             Carbone C, Daryl C, Conrad S, Marcus C, Belby J. 2014. Geometric factors influencing the diet of vertebrate predators in marine and terrestrial environments. Ecology Letters 17(12): 1553\x961559.
## 5                                                                                                                                                                                                                                                                                            <NA>
## 6                                                                                                                                                                                                                                                                                            <NA>
## 7                                                                                                                                                                                                                                                                                            <NA>
## 8                                                                                                                                                                                                                                                                                            <NA>
## 9                                                                                                                                                                                                                                                                                            <NA>
## 10                                                                                                                                                                                                                                                                                           <NA>
## 11                                                                                                                                                                                                                                                                                           <NA>
## 12                                                                                                                                                                                                                                                                                           <NA>
## 13                                                                                            Carbone C, Daryl C, Conrad S, Marcus C, Belby J. 2014. Geometric factors influencing the diet of vertebrate predators in marine and terrestrial environments. Ecology Letters 17(12): 1553\x961559.
## 14                                                                                                                                                                                                                                                                                           <NA>
## 15                                                                                                                                                                                                                                                                                           <NA>
## 16                                                                                                                                                                                                                                                                                           <NA>
## 17                                                                                            Carbone C, Daryl C, Conrad S, Marcus C, Belby J. 2014. Geometric factors influencing the diet of vertebrate predators in marine and terrestrial environments. Ecology Letters 17(12): 1553\x961559.
## 18                                                                                            Carbone C, Daryl C, Conrad S, Marcus C, Belby J. 2014. Geometric factors influencing the diet of vertebrate predators in marine and terrestrial environments. Ecology Letters 17(12): 1553\x961559.
## 19                                                                                                                               Gregory PT, Isaac LA. 2004. Food Habits of the Grass Snake in Southeastern England: Is Natrix natrix a Generalist Predator? Journal of Herpetology 38(1): 88-95.
## 20                                                                                                                                                                                                                                                                                           <NA>
## 21                                                                                                                                                                                                                                                                                           <NA>
## 22 Martins M, Marques OAV, Sazima I. 2002. Ecological and phylogenetic correlates of feeding habits in Neotropical pitvipers of the genus Bothrops. In G. W. Schuett, M. E. Douglas, M. H\xf6ggren, and H. W. Greene (eds.), Biology of the Vipers. Eagle Mountain Publishing, Eagle Mountain, UT
## 23                                                                                            Carbone C, Daryl C, Conrad S, Marcus C, Belby J. 2014. Geometric factors influencing the diet of vertebrate predators in marine and terrestrial environments. Ecology Letters 17(12): 1553\x961559.
## 24                                                                                                              Weatherhead PJ, Blouin-Demers G, Cavey KM. 2003. Seasonal and Prey-size Dietary Patterns of Black Ratsnakes (Elaphe obsoleta obsoleta). American Midland Naturalist 150, 275-281.
## 25                                                                                                                                                                             King RB. 2002. Predicted and Observed Maximum Prey Size - Snake Size Allometry. Functional Ecology 16(6), 766-772.
## 26                                                                                            Carbone C, Daryl C, Conrad S, Marcus C, Belby J. 2014. Geometric factors influencing the diet of vertebrate predators in marine and terrestrial environments. Ecology Letters 17(12): 1553\x961559.
## 27                                                                                                                                                                                                                                                                                           <NA>
## 28                                                                                                                                                                                                                                                                                           <NA>
## 29                                                                                                                                                                                                                                                                                           <NA>
## 30                                                                                                                                                                                                                                                                                           <NA>
## 31                                                                                                                                                                                                                                                                                           <NA>
## 32                                                                                                                                                                                                                                                                                           <NA>
## 33                                                                                                                                                                                                                                                                                           <NA>
## 34                                                                                                                   Vincent SW, Herrel A, Irschick DJ. 2004. Sexual dimorphism in head shape and diet in the cottonmouth. Journal of Zoology, London 264, 53-59.\nsnake (Agkistrodon piscivorus)
## 35                                                                                                                                                                                                                                                                                           <NA>
## 36                                                                                                                                   Shine R, Sun L-X. 2003. Attack strategy of an ambush predator: which attributes of the prey trigger a pit-viper\x92s strike? Functional Ecology 17, 340-348.
## 37                                           Jaksic FM, Delibes M.1987. A Comparative Analysis of Food-Niche Relationships and Trophic Guild Structure in TwoAssemblages of Vertebrate Predators Differing in Species Richness: Causes, Correlations, and Consequences. Oecologia 71(3), 461-472.
## 38                                                                                                                                                                                                                                                                                           <NA>
## 39                                                                                                                                                                                                                                                                                           <NA>
## 40                                                                                                                                                                                                                                                                                           <NA>
## 41                                                                                                                                                                                                                                                                                           <NA>
```
Now we can look at the last entry for the smallest home range, which belongs to the Namaqua Dwarf Adder which has a mean home range of only $200m^2$.

### **Namaqua Dwarf Adder (*Bitis schneideri*)**
Measuring only 15-20cm, this tiny snake is the world's smallest viper. Like me, it comes from southern Africa. It lives in the coastal dunes of Namaqualand (South Africa) and southern Namibia.  Days are spent hidden in the sand with only eyes exposed, both waiting for prey and avoiding predators. Feeding mainly on lizards and frogs, its venom is mildly cytotoxic. Human envenomation does not require antivenom administration.

Reference: https://www.africansnakebiteinstitute.com/snake/namaqua-dwarf-adder/

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
