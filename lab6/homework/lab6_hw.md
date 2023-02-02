---
title: "Lab 6 Homework"
author: "Oonagh Pretorius"
date: "2023-02-02"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
library(skimr)
```

For this assignment we are going to work with a large data set from the [United Nations Food and Agriculture Organization](http://www.fao.org/about/en/) on world fisheries. These data are pretty wild, so we need to do some cleaning. First, load the data.  

Load the data `FAO_1950to2012_111914.csv` as a new object titled `fisheries`.

```r
fisheries <- readr::read_csv(file = "data/FAO_1950to2012_111914.csv")
```

```
## Rows: 17692 Columns: 71
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (69): Country, Common name, ISSCAAP taxonomic group, ASFIS species#, ASF...
## dbl  (2): ISSCAAP group#, FAO major fishing area
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

1. Do an exploratory analysis of the data (your choice). What are the names of the variables, what are the dimensions, are there any NA's, what are the classes of the variables?  

```r
glimpse(fisheries)
```

```
## Rows: 17,692
## Columns: 71
## $ Country                   <chr> "Albania", "Albania", "Albania", "Albania", …
## $ `Common name`             <chr> "Angelsharks, sand devils nei", "Atlantic bo…
## $ `ISSCAAP group#`          <dbl> 38, 36, 37, 45, 32, 37, 33, 45, 38, 57, 33, …
## $ `ISSCAAP taxonomic group` <chr> "Sharks, rays, chimaeras", "Tunas, bonitos, …
## $ `ASFIS species#`          <chr> "10903XXXXX", "1750100101", "17710001XX", "2…
## $ `ASFIS species name`      <chr> "Squatinidae", "Sarda sarda", "Sphyraena spp…
## $ `FAO major fishing area`  <dbl> 37, 37, 37, 37, 37, 37, 37, 37, 37, 37, 37, …
## $ Measure                   <chr> "Quantity (tonnes)", "Quantity (tonnes)", "Q…
## $ `1950`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1951`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1952`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1953`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1954`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1955`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1956`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1957`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1958`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1959`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1960`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1961`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1962`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1963`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1964`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1965`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1966`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1967`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1968`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1969`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1970`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1971`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1972`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1973`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1974`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1975`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1976`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1977`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1978`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1979`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1980`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1981`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1982`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1983`                    <chr> NA, NA, NA, NA, NA, NA, "559", NA, NA, NA, N…
## $ `1984`                    <chr> NA, NA, NA, NA, NA, NA, "392", NA, NA, NA, N…
## $ `1985`                    <chr> NA, NA, NA, NA, NA, NA, "406", NA, NA, NA, N…
## $ `1986`                    <chr> NA, NA, NA, NA, NA, NA, "499", NA, NA, NA, N…
## $ `1987`                    <chr> NA, NA, NA, NA, NA, NA, "564", NA, NA, NA, N…
## $ `1988`                    <chr> NA, NA, NA, NA, NA, NA, "724", NA, NA, NA, N…
## $ `1989`                    <chr> NA, NA, NA, NA, NA, NA, "583", NA, NA, NA, N…
## $ `1990`                    <chr> NA, NA, NA, NA, NA, NA, "754", NA, NA, NA, N…
## $ `1991`                    <chr> NA, NA, NA, NA, NA, NA, "283", NA, NA, NA, N…
## $ `1992`                    <chr> NA, NA, NA, NA, NA, NA, "196", NA, NA, NA, N…
## $ `1993`                    <chr> NA, NA, NA, NA, NA, NA, "150 F", NA, NA, NA,…
## $ `1994`                    <chr> NA, NA, NA, NA, NA, NA, "100 F", NA, NA, NA,…
## $ `1995`                    <chr> "0 0", "1", NA, "0 0", "0 0", NA, "52", "30"…
## $ `1996`                    <chr> "53", "2", NA, "3", "2", NA, "104", "8", NA,…
## $ `1997`                    <chr> "20", "0 0", NA, "0 0", "0 0", NA, "65", "4"…
## $ `1998`                    <chr> "31", "12", NA, NA, NA, NA, "220", "18", NA,…
## $ `1999`                    <chr> "30", "30", NA, NA, NA, NA, "220", "18", NA,…
## $ `2000`                    <chr> "30", "25", "2", NA, NA, NA, "220", "20", NA…
## $ `2001`                    <chr> "16", "30", NA, NA, NA, NA, "120", "23", NA,…
## $ `2002`                    <chr> "79", "24", NA, "34", "6", NA, "150", "84", …
## $ `2003`                    <chr> "1", "4", NA, "22", NA, NA, "84", "178", NA,…
## $ `2004`                    <chr> "4", "2", "2", "15", "1", "2", "76", "285", …
## $ `2005`                    <chr> "68", "23", "4", "12", "5", "6", "68", "150"…
## $ `2006`                    <chr> "55", "30", "7", "18", "8", "9", "86", "102"…
## $ `2007`                    <chr> "12", "19", NA, NA, NA, NA, "132", "18", NA,…
## $ `2008`                    <chr> "23", "27", NA, NA, NA, NA, "132", "23", NA,…
## $ `2009`                    <chr> "14", "21", NA, NA, NA, NA, "154", "20", NA,…
## $ `2010`                    <chr> "78", "23", "7", NA, NA, NA, "80", "228", NA…
## $ `2011`                    <chr> "12", "12", NA, NA, NA, NA, "88", "9", NA, "…
## $ `2012`                    <chr> "5", "5", NA, NA, NA, NA, "129", "290", NA, …
```
Yes there are many NAs.

2. Use `janitor` to rename the columns and make them easier to use. As part of this cleaning step, change `country`, `isscaap_group_number`, `asfis_species_number`, and `fao_major_fishing_area` to data class factor. 

```r
fisheries <- janitor::clean_names(fisheries)
```


```r
fisheries <- fisheries %>% 
        mutate(across(c("country", "isscaap_group_number", "asfis_species_number", "fao_major_fishing_area"), as.factor))
```


```r
glimpse(fisheries)
```

```
## Rows: 17,692
## Columns: 71
```

```
## Warning in grepl(",", levels(x), fixed = TRUE): input string 1 is invalid UTF-8
```

```
## Warning in grepl(",", levels(x), fixed = TRUE): input string 2 is invalid UTF-8
```

```
## Warning in grepl(",", levels(x), fixed = TRUE): input string 3 is invalid UTF-8
```

```
## Warning in grepl(",", levels(x), fixed = TRUE): input string 4 is invalid UTF-8
```

```
## $ country                 <fct> "Albania", "Albania", "Albania", "Albania", "A…
## $ common_name             <chr> "Angelsharks, sand devils nei", "Atlantic boni…
## $ isscaap_group_number    <fct> 38, 36, 37, 45, 32, 37, 33, 45, 38, 57, 33, 57…
## $ isscaap_taxonomic_group <chr> "Sharks, rays, chimaeras", "Tunas, bonitos, bi…
## $ asfis_species_number    <fct> 10903XXXXX, 1750100101, 17710001XX, 2280203101…
## $ asfis_species_name      <chr> "Squatinidae", "Sarda sarda", "Sphyraena spp",…
## $ fao_major_fishing_area  <fct> 37, 37, 37, 37, 37, 37, 37, 37, 37, 37, 37, 37…
## $ measure                 <chr> "Quantity (tonnes)", "Quantity (tonnes)", "Qua…
## $ x1950                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1951                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1952                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1953                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1954                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1955                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1956                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1957                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1958                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1959                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1960                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1961                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1962                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1963                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1964                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1965                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1966                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1967                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1968                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1969                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1970                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1971                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1972                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1973                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1974                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1975                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1976                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1977                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1978                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1979                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1980                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1981                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1982                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1983                   <chr> NA, NA, NA, NA, NA, NA, "559", NA, NA, NA, NA,…
## $ x1984                   <chr> NA, NA, NA, NA, NA, NA, "392", NA, NA, NA, NA,…
## $ x1985                   <chr> NA, NA, NA, NA, NA, NA, "406", NA, NA, NA, NA,…
## $ x1986                   <chr> NA, NA, NA, NA, NA, NA, "499", NA, NA, NA, NA,…
## $ x1987                   <chr> NA, NA, NA, NA, NA, NA, "564", NA, NA, NA, NA,…
## $ x1988                   <chr> NA, NA, NA, NA, NA, NA, "724", NA, NA, NA, NA,…
## $ x1989                   <chr> NA, NA, NA, NA, NA, NA, "583", NA, NA, NA, NA,…
## $ x1990                   <chr> NA, NA, NA, NA, NA, NA, "754", NA, NA, NA, NA,…
## $ x1991                   <chr> NA, NA, NA, NA, NA, NA, "283", NA, NA, NA, NA,…
## $ x1992                   <chr> NA, NA, NA, NA, NA, NA, "196", NA, NA, NA, NA,…
## $ x1993                   <chr> NA, NA, NA, NA, NA, NA, "150 F", NA, NA, NA, N…
## $ x1994                   <chr> NA, NA, NA, NA, NA, NA, "100 F", NA, NA, NA, N…
## $ x1995                   <chr> "0 0", "1", NA, "0 0", "0 0", NA, "52", "30", …
## $ x1996                   <chr> "53", "2", NA, "3", "2", NA, "104", "8", NA, "…
## $ x1997                   <chr> "20", "0 0", NA, "0 0", "0 0", NA, "65", "4", …
## $ x1998                   <chr> "31", "12", NA, NA, NA, NA, "220", "18", NA, "…
## $ x1999                   <chr> "30", "30", NA, NA, NA, NA, "220", "18", NA, "…
## $ x2000                   <chr> "30", "25", "2", NA, NA, NA, "220", "20", NA, …
## $ x2001                   <chr> "16", "30", NA, NA, NA, NA, "120", "23", NA, "…
## $ x2002                   <chr> "79", "24", NA, "34", "6", NA, "150", "84", NA…
## $ x2003                   <chr> "1", "4", NA, "22", NA, NA, "84", "178", NA, "…
## $ x2004                   <chr> "4", "2", "2", "15", "1", "2", "76", "285", "1…
## $ x2005                   <chr> "68", "23", "4", "12", "5", "6", "68", "150", …
## $ x2006                   <chr> "55", "30", "7", "18", "8", "9", "86", "102", …
## $ x2007                   <chr> "12", "19", NA, NA, NA, NA, "132", "18", NA, "…
## $ x2008                   <chr> "23", "27", NA, NA, NA, NA, "132", "23", NA, "…
## $ x2009                   <chr> "14", "21", NA, NA, NA, NA, "154", "20", NA, "…
## $ x2010                   <chr> "78", "23", "7", NA, NA, NA, "80", "228", NA, …
## $ x2011                   <chr> "12", "12", NA, NA, NA, NA, "88", "9", NA, "90…
## $ x2012                   <chr> "5", "5", NA, NA, NA, NA, "129", "290", NA, "1…
```


We need to deal with the years because they are being treated as characters and start with an X. We also have the problem that the column names that are years actually represent data. We haven't discussed tidy data yet, so here is some help. You should run this ugly chunk to transform the data for the rest of the homework. It will only work if you have used janitor to rename the variables in question 2!

```r
fisheries_tidy <- fisheries %>% 
pivot_longer(-c(country,common_name,isscaap_group_number,isscaap_taxonomic_group,
              asfis_species_number,asfis_species_name,fao_major_fishing_area,measure),
              names_to = "year",
              values_to = "catch",
              values_drop_na = TRUE) %>% 
  mutate(year= as.numeric(str_replace(year, 'x', ''))) %>% 
  mutate(catch= str_replace(catch, c(' F'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('...'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('-'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('0 0'), replacement = ''))

fisheries_tidy$catch <- as.numeric(fisheries_tidy$catch)
```

3. How many countries are represented in the data? Provide a count and list their names.

```r
fisheries %>% 
  tabyl(country, total=n())
```

```
##                    country   n      percent
##        Saint Barth\xe9lemy   1 5.652272e-05
##                 R\xe9union  37 2.091341e-03
##           C\xf4te d'Ivoire  67 3.787022e-03
##                 Cura\xe7ao   9 5.087045e-04
##                    Albania  67 3.787022e-03
##                    Algeria  59 3.334841e-03
##             American Samoa  32 1.808727e-03
##                     Angola  88 4.974000e-03
##                   Anguilla   3 1.695682e-04
##        Antigua and Barbuda  22 1.243500e-03
##                  Argentina 140 7.913181e-03
##                      Aruba   5 2.826136e-04
##                  Australia 301 1.701334e-02
##                    Bahamas  14 7.913181e-04
##                    Bahrain  62 3.504409e-03
##                 Bangladesh   8 4.521818e-04
##                   Barbados  21 1.186977e-03
##                    Belgium  57 3.221795e-03
##                     Belize 133 7.517522e-03
##                      Benin  68 3.843545e-03
##                    Bermuda  47 2.656568e-03
##   Bonaire/S.Eustatius/Saba   2 1.130454e-04
##     Bosnia and Herzegovina   1 5.652272e-05
##                     Brazil 136 7.687090e-03
##   British Indian Ocean Ter   7 3.956591e-04
##     British Virgin Islands  18 1.017409e-03
##          Brunei Darussalam   8 4.521818e-04
##                   Bulgaria 197 1.113498e-02
##                 Cabo Verde  26 1.469591e-03
##                   Cambodia   8 4.521818e-04
##                   Cameroon  36 2.034818e-03
##                     Canada 125 7.065340e-03
##             Cayman Islands   4 2.260909e-04
##            Channel Islands  65 3.673977e-03
##                      Chile 141 7.969704e-03
##                      China 236 1.333936e-02
##       China, Hong Kong SAR  32 1.808727e-03
##           China, Macao SAR   4 2.260909e-04
##                   Colombia  81 4.578340e-03
##                    Comoros  43 2.430477e-03
##    Congo, Dem. Rep. of the  21 1.186977e-03
##         Congo, Republic of  53 2.995704e-03
##               Cook Islands  55 3.108750e-03
##                 Costa Rica  45 2.543522e-03
##                    Croatia 103 5.821840e-03
##                       Cuba 162 9.156681e-03
##                     Cyprus  96 5.426181e-03
##                    Denmark 103 5.821840e-03
##                   Djibouti  14 7.913181e-04
##                   Dominica  13 7.347954e-04
##         Dominican Republic  50 2.826136e-03
##                    Ecuador 100 5.652272e-03
##                      Egypt  87 4.917477e-03
##                El Salvador  25 1.413068e-03
##          Equatorial Guinea  15 8.478408e-04
##                    Eritrea  49 2.769613e-03
##                    Estonia 184 1.040018e-02
##                   Ethiopia   5 2.826136e-04
##     Falkland Is.(Malvinas)  33 1.865250e-03
##              Faroe Islands  96 5.426181e-03
##          Fiji, Republic of  50 2.826136e-03
##                    Finland  16 9.043636e-04
##                     France 489 2.763961e-02
##              French Guiana  18 1.017409e-03
##           French Polynesia  31 1.752204e-03
##       French Southern Terr   3 1.695682e-04
##                      Gabon  45 2.543522e-03
##                     Gambia  49 2.769613e-03
##                    Georgia  86 4.860954e-03
##                    Germany 306 1.729595e-02
##                      Ghana  94 5.313136e-03
##                  Gibraltar   1 5.652272e-05
##                     Greece 125 7.065340e-03
##                  Greenland  60 3.391363e-03
##                    Grenada  47 2.656568e-03
##                 Guadeloupe   8 4.521818e-04
##                       Guam  23 1.300023e-03
##                  Guatemala  38 2.147863e-03
##                     Guinea  56 3.165272e-03
##               GuineaBissau  32 1.808727e-03
##                     Guyana  11 6.217499e-04
##                      Haiti   6 3.391363e-04
##                   Honduras  68 3.843545e-03
##                    Iceland 107 6.047931e-03
##                      India 108 6.104454e-03
##                  Indonesia 223 1.260457e-02
##     Iran (Islamic Rep. of)  64 3.617454e-03
##                       Iraq  16 9.043636e-04
##                    Ireland 191 1.079584e-02
##                Isle of Man  41 2.317432e-03
##                     Israel  79 4.465295e-03
##                      Italy 261 1.475243e-02
##                    Jamaica   6 3.391363e-04
##                      Japan 611 3.453538e-02
##                     Jordan  12 6.782727e-04
##                      Kenya  31 1.752204e-03
##                   Kiribati  27 1.526113e-03
##   Korea, Dem. People's Rep  14 7.913181e-04
##         Korea, Republic of 620 3.504409e-02
##                     Kuwait  23 1.300023e-03
##                     Latvia 162 9.156681e-03
##                    Lebanon  20 1.130454e-03
##                    Liberia  76 4.295727e-03
##                      Libya  56 3.165272e-03
##                  Lithuania 215 1.215239e-02
##                 Madagascar  35 1.978295e-03
##                   Malaysia 166 9.382772e-03
##                   Maldives  12 6.782727e-04
##                      Malta 104 5.878363e-03
##           Marshall Islands  13 7.347954e-04
##                 Martinique  16 9.043636e-04
##                 Mauritania  93 5.256613e-03
##                  Mauritius  30 1.695682e-03
##                    Mayotte  14 7.913181e-04
##                     Mexico 198 1.119150e-02
##  Micronesia, Fed.States of  13 7.347954e-04
##                     Monaco   1 5.652272e-05
##                 Montenegro  24 1.356545e-03
##                 Montserrat   1 5.652272e-05
##                    Morocco 153 8.647976e-03
##                 Mozambique  30 1.695682e-03
##                    Myanmar   5 2.826136e-04
##                    Namibia  76 4.295727e-03
##                      Nauru   9 5.087045e-04
##                Netherlands 155 8.761022e-03
##       Netherlands Antilles  17 9.608863e-04
##              New Caledonia  26 1.469591e-03
##                New Zealand 208 1.175673e-02
##                  Nicaragua  59 3.334841e-03
##                    Nigeria  50 2.826136e-03
##                       Niue  11 6.217499e-04
##             Norfolk Island   1 5.652272e-05
##       Northern Mariana Is.  19 1.073932e-03
##                     Norway 188 1.062627e-02
##                       Oman  53 2.995704e-03
##                  Other nei 100 5.652272e-03
##                   Pakistan  60 3.391363e-03
##                      Palau  33 1.865250e-03
##    Palestine, Occupied Tr.  25 1.413068e-03
##                     Panama 121 6.839249e-03
##           Papua New Guinea  20 1.130454e-03
##                       Peru  54 3.052227e-03
##                Philippines 138 7.800136e-03
##           Pitcairn Islands   1 5.652272e-05
##                     Poland 263 1.486548e-02
##                   Portugal 763 4.312684e-02
##                Puerto Rico  49 2.769613e-03
##                      Qatar  35 1.978295e-03
##                    Romania 191 1.079584e-02
##         Russian Federation 523 2.956138e-02
##               Saint Helena  19 1.073932e-03
##      Saint Kitts and Nevis  28 1.582636e-03
##                Saint Lucia  27 1.526113e-03
##   Saint Vincent/Grenadines  71 4.013113e-03
##                SaintMartin   1 5.652272e-05
##                      Samoa  15 8.478408e-04
##      Sao Tome and Principe  35 1.978295e-03
##               Saudi Arabia 128 7.234908e-03
##                    Senegal 140 7.913181e-03
##      Serbia and Montenegro  45 2.543522e-03
##                 Seychelles  70 3.956591e-03
##               Sierra Leone  59 3.334841e-03
##                  Singapore  40 2.260909e-03
##               Sint Maarten   2 1.130454e-04
##                   Slovenia  50 2.826136e-03
##            Solomon Islands  18 1.017409e-03
##                    Somalia   3 1.695682e-04
##               South Africa 200 1.130454e-02
##                      Spain 915 5.171829e-02
##                  Sri Lanka  34 1.921773e-03
##    St. Pierre and Miquelon  40 2.260909e-03
##                      Sudan   3 1.695682e-04
##             Sudan (former)   3 1.695682e-04
##                   Suriname  27 1.526113e-03
##     Svalbard and Jan Mayen   1 5.652272e-05
##                     Sweden  72 4.069636e-03
##       Syrian Arab Republic  34 1.921773e-03
##   Taiwan Province of China 310 1.752204e-02
##   Tanzania, United Rep. of  49 2.769613e-03
##                   Thailand 150 8.478408e-03
##                 TimorLeste   7 3.956591e-04
##                       Togo  78 4.408772e-03
##                    Tokelau  10 5.652272e-04
##                      Tonga  14 7.913181e-04
##        Trinidad and Tobago  39 2.204386e-03
##                    Tunisia  85 4.804431e-03
##                     Turkey  76 4.295727e-03
##       Turks and Caicos Is.   6 3.391363e-04
##                     Tuvalu  10 5.652272e-04
##                    Ukraine 294 1.661768e-02
##         Un. Sov. Soc. Rep. 515 2.910920e-02
##       United Arab Emirates  52 2.939182e-03
##             United Kingdom 362 2.046123e-02
##   United States of America 627 3.543975e-02
##                    Uruguay 131 7.404477e-03
##          US Virgin Islands  29 1.639159e-03
##                    Vanuatu  71 4.013113e-03
##    Venezuela, Boliv Rep of  80 4.521818e-03
##                   Viet Nam  14 7.913181e-04
##      Wallis and Futuna Is.   5 2.826136e-04
##             Western Sahara   3 1.695682e-04
##                      Yemen  39 2.204386e-03
##             Yugoslavia SFR  36 2.034818e-03
##                   Zanzibar  19 1.073932e-03
```

4. Refocus the data only to include country, isscaap_taxonomic_group, asfis_species_name, asfis_species_number, year, catch.

```r
fisheries_tidy %>% 
  select(country, isscaap_taxonomic_group, asfis_species_name, asfis_species_number, year, catch)
```

```
## # A tibble: 376,771 × 6
##    country isscaap_taxonomic_group asfis_species_name asfis_specie…¹  year catch
##    <fct>   <chr>                   <chr>              <fct>          <dbl> <dbl>
##  1 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      1995    NA
##  2 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      1996    53
##  3 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      1997    20
##  4 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      1998    31
##  5 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      1999    30
##  6 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      2000    30
##  7 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      2001    16
##  8 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      2002    79
##  9 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      2003     1
## 10 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      2004     4
## # … with 376,761 more rows, and abbreviated variable name ¹​asfis_species_number
```

5. Based on the asfis_species_number, how many distinct fish species were caught as part of these data?

```r
fisheries_tidy %>% 
  summarize(distinct_sp_catch = n_distinct(asfis_species_number))
```

```
## # A tibble: 1 × 1
##   distinct_sp_catch
##               <int>
## 1              1551
```

6. Which country had the largest overall catch in the year 2000?

```r
fisheries_tidy %>% 
  filter(year == "2000") %>% 
  group_by(country) %>% 
  summarize(max_catch= max(catch, na.rm = TRUE)) %>% 
  #arrange(desc(max_catch)) #we can either arrange the whole list, or just extract the max value with slice_max()
  slice_max(max_catch)
```

```
## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf
```

```
## # A tibble: 1 × 2
##   country max_catch
##   <fct>       <dbl>
## 1 China        9068
```

7. Which country caught the most sardines (_Sardina pilchardus_) between the years 1990-2000?

```r
fisheries_tidy %>% 
  filter(between(year, 1990, 2000), asfis_species_name == "Sardina pilchardus") %>% 
  group_by(country) %>% 
  summarise(max_sardines = max(catch, na.rm = TRUE)) %>% 
  slice_max(max_sardines)
```

```
## # A tibble: 1 × 2
##   country max_sardines
##   <fct>          <dbl>
## 1 Morocco          947
```

8. Which five countries caught the most cephalopods between 2008-2012?

```r
fisheries_tidy %>% 
  filter(between(year, 2008, 2012), asfis_species_name == "Cephalopoda") %>% 
  group_by(country) %>% 
  summarise(max_cephalopods = max(catch, na.rm = TRUE)) %>% 
  arrange(desc(max_cephalopods)) %>% 
  slice_max(max_cephalopods, n=5)
```

```
## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf
```

```
## # A tibble: 5 × 2
##   country max_cephalopods
##   <fct>             <dbl>
## 1 India                94
## 2 China                86
## 3 Italy                66
## 4 Spain                57
## 5 Algeria              54
```



9. Which species had the highest catch total between 2008-2012? (hint: Osteichthyes is not a species) *Truchuris lepturus*

```r
fisheries_tidy %>% 
  filter(between(year, 2008, 2012), !isscaap_taxonomic_group == "Marine fishes not identified") %>% 
  group_by(asfis_species_name) %>% 
  summarise(max_species = max(catch, na.rm = TRUE)) %>% 
  arrange(desc(max_species)) %>% 
  slice_max(max_species, n=5)
```

```
## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf
```

```
## # A tibble: 5 × 2
##   asfis_species_name    max_species
##   <chr>                       <dbl>
## 1 Trichiurus lepturus          8221
## 2 Theragra chalcogramma        8188
## 3 Engraulis ringens            7981
## 4 Clupea harengus              7873
## 5 Katsuwonus pelamis            997
```

10. Use the data to do at least one analysis of your choice.

What are the three most common species of fish caught each decade, and how do they compare? (We will exclude 1969 and 2010-12 as these are not complete decades.)

1970s

```r
d70 <- fisheries_tidy %>% 
      filter(!isscaap_taxonomic_group == "Marine fishes not identified", between(year, 1970, 1979)) %>% 
      group_by(asfis_species_name) %>% 
      summarise(max_species = max(catch, na.rm = TRUE)) %>% 
      arrange(max_species) %>% 
      slice_max(max_species, n=3)
```

```
## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf
```

```r
d70
```

```
## # A tibble: 3 × 2
##   asfis_species_name    max_species
##   <chr>                       <dbl>
## 1 Engraulis ringens           77000
## 2 Theragra chalcogramma        9600
## 3 Mallotus villosus            9105
```
1980s

```r
d80 <- fisheries_tidy %>% 
      filter(!isscaap_taxonomic_group == "Marine fishes not identified", between(year, 1980, 1989)) %>% 
      group_by(asfis_species_name) %>% 
      summarise(max_species = max(catch, na.rm = TRUE)) %>% 
      arrange(max_species) %>% 
      slice_max(max_species, n=3)
```

```
## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf
```

```r
d80
```

```
## # A tibble: 3 × 2
##   asfis_species_name      max_species
##   <chr>                         <dbl>
## 1 Sardinops melanostictus        9954
## 2 Sardinops sagax                9904
## 3 Theragra chalcogramma          9758
```
1990s

```r
d90 <- fisheries_tidy %>% 
      filter(!isscaap_taxonomic_group == "Marine fishes not identified", between(year, 1990, 1999)) %>% 
      group_by(asfis_species_name) %>% 
      summarise(max_species = max(catch, na.rm = TRUE)) %>% 
      arrange(max_species) %>% 
      slice_max(max_species, n=3)
```

```
## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf
```

```r
d90
```

```
## # A tibble: 3 × 2
##   asfis_species_name    max_species
##   <chr>                       <dbl>
## 1 Engraulis ringens            9966
## 2 Theragra chalcogramma        9844
## 3 Trachurus murphyi            9689
```
2000s

```r
d00 <- fisheries_tidy %>% 
      filter(!isscaap_taxonomic_group == "Marine fishes not identified", between(year, 2000, 2009)) %>% 
      group_by(asfis_species_name) %>% 
      summarise(max_species = max(catch, na.rm = TRUE)) %>% 
      arrange(max_species) %>% 
      slice_max(max_species, n=3)
```

```
## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf

## Warning in max(catch, na.rm = TRUE): no non-missing arguments to max; returning
## -Inf
```

```r
d00
```

```
## # A tibble: 3 × 2
##   asfis_species_name    max_species
##   <chr>                       <dbl>
## 1 Trachurus murphyi            9941
## 2 Theragra chalcogramma        9928
## 3 Engraulis ringens            9802
```
In the 70s, Engraulis ringens was the most numerous fish species caught by far. In the 80s, sardines were favoured. Both in the 1990s and 2000s, the same top three species of fish were caught, namely, Trachurus murphyi, Theragra chalcogramma, and Engraulis ringens.

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences. 


================================================================================
================================================================================
#### **QUESTIONS FOR JOEL**

================================================================================
================================================================================

```r
decade <- as.data.frame(c(d70, d80, d90, d00))
decade
```

```
##      asfis_species_name max_species    asfis_species_name.1 max_species.1
## 1     Engraulis ringens       77000 Sardinops melanostictus          9954
## 2 Theragra chalcogramma        9600         Sardinops sagax          9904
## 3     Mallotus villosus        9105   Theragra chalcogramma          9758
##    asfis_species_name.2 max_species.2  asfis_species_name.3 max_species.3
## 1     Engraulis ringens          9966     Trachurus murphyi          9941
## 2 Theragra chalcogramma          9844 Theragra chalcogramma          9928
## 3     Trachurus murphyi          9689     Engraulis ringens          9802
```

What would be a better way to code for my question above? I tried these two methods but no success.

#```{r}
fisheries_tidy %>% 
  filter(!isscaap_taxonomic_group == "Marine fishes not identified") %>% 
  mutate(as.numeric(decade = rename(d70 = between(year, 1970, 1979)))) %>%
  mutate(decade = rename(d80 = between(year, 1980, 1989))) %>% 
  mutate(decade = rename(d90 = between(year, 1990, 1999))) %>%
  mutate(decade = rename(d00 = between(year, 2000, 2009))) %>%
  group_by(asfis_species_name, decade) %>% 
  summarise(min_species = min(catch, na.rm = TRUE)) %>% 
  arrange(min_species) %>% 
  slice_min(min_species, n=5)
```

#```{r}
fisheries_tidy %>% 
  filter(!isscaap_taxonomic_group == "Marine fishes not identified") %>% 
  mutate(decade = rename(year, between(year, 1970, 1979), d70, year)) %>%
  mutate(decade = if_else(year, between(year, 1980, 1989), d80, year)) %>% 
  mutate(decade = if_else(year, between(year, 1990, 1999), d90, year)) %>%
  mutate(decade = if_else(year, between(year, 2000, 2009), d00, year)) %>%
  group_by(asfis_species_name, decade) %>% 
  summarise(min_species = min(catch, na.rm = TRUE)) %>% 
  arrange(min_species) %>% 
  slice_min(min_species, n=5)
```
  
