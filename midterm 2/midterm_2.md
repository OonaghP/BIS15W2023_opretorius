---
title: "BIS 15L Midterm 2"
name: "Oonagh Pretorius"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your code should be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run. Be sure to add your name to the author header above.  

After the first 50 minutes, please upload your code (5 points). During the second 50 minutes, you may get help from each other- but no copy/paste. Upload the last version at the end of this time, but be sure to indicate it as final. If you finish early, you are free to leave.

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean! Use the tidyverse and pipes unless otherwise indicated. To receive full credit, all plots must have clearly labeled axes, a title, and consistent aesthetics. This exam is worth a total of 35 points. 

Please load the following libraries.

```r
library("tidyverse")
library("janitor")
library("naniar")
library(RColorBrewer)
library(ggthemes)
```

## Data
These data are from a study on surgical residents. The study was originally published by Sessier et al. “Operation Timing and 30-Day Mortality After Elective General Surgery”. Anesth Analg 2011; 113: 1423-8. The data were cleaned for instructional use by Amy S. Nowacki, “Surgery Timing Dataset”, TSHS Resources Portal (2016). Available at https://www.causeweb.org/tshs/surgery-timing/.

Descriptions of the variables and the study are included as pdf's in the data folder.  

Please run the following chunk to import the data.

```r
surgery <- read_csv("data/surgery.csv")
```

1. (2 points) Use the summary function(s) of your choice to explore the data and get an idea of its structure. Please also check for NA's.

```r
glimpse(surgery)
```

```
## Rows: 32,001
## Columns: 25
## $ ahrq_ccs            <chr> "<Other>", "<Other>", "<Other>", "<Other>", "<Othe…
## $ age                 <dbl> 67.8, 39.5, 56.5, 71.0, 56.3, 57.7, 56.6, 64.2, 66…
## $ gender              <chr> "M", "F", "F", "M", "M", "F", "M", "F", "M", "F", …
## $ race                <chr> "Caucasian", "Caucasian", "Caucasian", "Caucasian"…
## $ asa_status          <chr> "I-II", "I-II", "I-II", "III", "I-II", "I-II", "IV…
## $ bmi                 <dbl> 28.04, 37.85, 19.56, 32.22, 24.32, 40.30, 64.57, 4…
## $ baseline_cancer     <chr> "No", "No", "No", "No", "Yes", "No", "No", "No", "…
## $ baseline_cvd        <chr> "Yes", "Yes", "No", "Yes", "No", "Yes", "Yes", "Ye…
## $ baseline_dementia   <chr> "No", "No", "No", "No", "No", "No", "No", "No", "N…
## $ baseline_diabetes   <chr> "No", "No", "No", "No", "No", "No", "Yes", "No", "…
## $ baseline_digestive  <chr> "Yes", "No", "No", "No", "No", "No", "No", "No", "…
## $ baseline_osteoart   <chr> "No", "No", "No", "No", "No", "No", "No", "No", "N…
## $ baseline_psych      <chr> "No", "No", "No", "No", "No", "Yes", "No", "No", "…
## $ baseline_pulmonary  <chr> "No", "No", "No", "No", "No", "No", "No", "No", "N…
## $ baseline_charlson   <dbl> 0, 0, 0, 0, 0, 0, 2, 0, 1, 2, 0, 1, 0, 0, 0, 0, 0,…
## $ mortality_rsi       <dbl> -0.63, -0.63, -0.49, -1.38, 0.00, -0.77, -0.36, -0…
## $ complication_rsi    <dbl> -0.26, -0.26, 0.00, -1.15, 0.00, -0.84, -1.34, 0.0…
## $ ccsmort30rate       <dbl> 0.0042508, 0.0042508, 0.0042508, 0.0042508, 0.0042…
## $ ccscomplicationrate <dbl> 0.07226355, 0.07226355, 0.07226355, 0.07226355, 0.…
## $ hour                <dbl> 9.03, 18.48, 7.88, 8.80, 12.20, 7.67, 9.53, 7.52, …
## $ dow                 <chr> "Mon", "Wed", "Fri", "Wed", "Thu", "Thu", "Tue", "…
## $ month               <chr> "Nov", "Sep", "Aug", "Jun", "Aug", "Dec", "Apr", "…
## $ moonphase           <chr> "Full Moon", "New Moon", "Full Moon", "Last Quarte…
## $ mort30              <chr> "No", "No", "No", "No", "No", "No", "No", "No", "N…
## $ complication        <chr> "No", "No", "No", "No", "No", "No", "No", "Yes", "…
```

```r
naniar::miss_var_summary(surgery) # NAs are represented by missing values.
```

```
## # A tibble: 25 × 3
##    variable          n_miss pct_miss
##    <chr>              <int>    <dbl>
##  1 bmi                 3290 10.3    
##  2 race                 480  1.50   
##  3 asa_status             8  0.0250 
##  4 gender                 3  0.00937
##  5 age                    2  0.00625
##  6 ahrq_ccs               0  0      
##  7 baseline_cancer        0  0      
##  8 baseline_cvd           0  0      
##  9 baseline_dementia      0  0      
## 10 baseline_diabetes      0  0      
## # … with 15 more rows
```

```r
head(surgery)
```

```
## # A tibble: 6 × 25
##   ahrq_ccs   age gender race       asa_s…¹   bmi basel…² basel…³ basel…⁴ basel…⁵
##   <chr>    <dbl> <chr>  <chr>      <chr>   <dbl> <chr>   <chr>   <chr>   <chr>  
## 1 <Other>   67.8 M      Caucasian  I-II     28.0 No      Yes     No      No     
## 2 <Other>   39.5 F      Caucasian  I-II     37.8 No      Yes     No      No     
## 3 <Other>   56.5 F      Caucasian  I-II     19.6 No      No      No      No     
## 4 <Other>   71   M      Caucasian  III      32.2 No      Yes     No      No     
## 5 <Other>   56.3 M      African A… I-II     24.3 Yes     No      No      No     
## 6 <Other>   57.7 F      Caucasian  I-II     40.3 No      Yes     No      No     
## # … with 15 more variables: baseline_digestive <chr>, baseline_osteoart <chr>,
## #   baseline_psych <chr>, baseline_pulmonary <chr>, baseline_charlson <dbl>,
## #   mortality_rsi <dbl>, complication_rsi <dbl>, ccsmort30rate <dbl>,
## #   ccscomplicationrate <dbl>, hour <dbl>, dow <chr>, month <chr>,
## #   moonphase <chr>, mort30 <chr>, complication <chr>, and abbreviated variable
## #   names ¹​asa_status, ²​baseline_cancer, ³​baseline_cvd, ⁴​baseline_dementia,
## #   ⁵​baseline_diabetes
```

2. (3 points) Let's explore the participants in the study. Show a count of participants by race AND make a plot that visually represents your output.

```r
surgery %>% 
  ggplot(aes(x=race))+
  geom_bar(na.rm=TRUE)+ 
  theme_classic()+
  theme(axis.text.x = element_text(angle = 60, hjust = 1)) +
  labs(title = "Study Participants by Race",
       x = "Race", y= "Number of Participants")
```

![](midterm_2_files/figure-html/unnamed-chunk-5-1.png)<!-- -->


3. (2 points) What is the mean age of participants by gender? (hint: please provide a number for each) Since only three participants do not have gender indicated, remove these participants from the data.

```r
surgery %>%
  group_by(gender) %>% 
  summarise(mean_age=mean(age, na.rm=TRUE))
```

```
## # A tibble: 3 × 2
##   gender mean_age
##   <chr>     <dbl>
## 1 F          56.7
## 2 M          58.8
## 3 <NA>       51.8
```

**4. (3 points) Make a plot that shows the range of age associated with gender.

```r
surgery %>% 
  ggplot(aes(x=age, na.rm=TRUE, fill=gender))+
  geom_boxplot()+
  coord_flip()+
  theme_classic()+
  theme(legend.position = "bottom",
        axis.text.x = element_text(angle = 60, hjust = 1)) +
  labs(title = "Age Range of Participants by Gender",
       x = "Age", y= "Gender")
```

```
## Warning: Removed 2 rows containing non-finite values (`stat_boxplot()`).
```

![](midterm_2_files/figure-html/unnamed-chunk-7-1.png)<!-- -->


5. (2 points) How healthy are the participants? The variable `asa_status` is an evaluation of patient physical status prior to surgery. Lower numbers indicate fewer comorbidities (presence of two or more diseases or medical conditions in a patient). Make a plot that compares the number of `asa_status` I-II, III, and IV-V. *The majority of the participants fall into the categories with fewer or moderate co-morbidities.* 

```r
surgery %>% 
  ggplot(aes(x=asa_status, fill=asa_status, na.rm=TRUE))+
  geom_bar()+
  theme_classic()+
  theme(legend.position = "bottom",
        axis.text.x = element_text(angle = 60, hjust = 1)) +
  labs(title = "Patient Health Status by ASA Classification",
       x = "Physical Status Category", y= "Number of Participants")
```

![](midterm_2_files/figure-html/unnamed-chunk-8-1.png)<!-- -->


**6. (3 points) Create a plot that displays the distribution of body mass index for each `asa_status` as a probability distribution- not a histogram. (hint: use faceting!)


```r
surgery %>% 
  ggplot(aes(x = bmi, fill=asa_status, na.rm=TRUE)) +
  geom_density(fill="seagreen4", alpha  =0.4, color = "black")+
  facet_wrap(~asa_status, ncol=4)+ #ncol is how many column plots you want per line
  theme_classic()+
  theme(axis.text.x = element_text(angle = 60, hjust = 1))+
  labs(title = "Participant BMI by ASA Health Status",
       x = "Participant BMI",
       y = "ASA Health Status",
       fill = "asa_status")
```

```
## Warning: Removed 3290 rows containing non-finite values (`stat_density()`).
```

![](midterm_2_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

The variable `ccsmort30rate` is a measure of the overall 30-day mortality rate associated with each type of operation. The variable `ccscomplicationrate` is a measure of the 30-day in-hospital complication rate. The variable `ahrq_ccs` lists each type of operation.  

7. (4 points) What are the 5 procedures associated with highest risk of 30-day mortality AND how do they compare with the 5 procedures with highest risk of complication? (hint: no need for a plot here)

```r
d30_mortality<- surgery %>% 
  count(ahrq_ccs, ccsmort30rate) %>% 
  arrange(desc(ccsmort30rate)) %>% 
  slice_head(., n=5)
d30_mortality
```

```
## # A tibble: 5 × 3
##   ahrq_ccs                                             ccsmort30rate     n
##   <chr>                                                        <dbl> <int>
## 1 Colorectal resection                                       0.0167   2519
## 2 Small bowel resection                                      0.0129    620
## 3 Gastrectomy; partial and total                             0.0127    394
## 4 Endoscopy and endoscopic biopsy of the urinary tract       0.00811   370
## 5 Spinal fusion                                              0.00742  2694
```


```r
d30_complication<- surgery %>% 
  count(ahrq_ccs, ccscomplicationrate) %>% 
  arrange(desc(ccscomplicationrate)) %>% 
  slice_head(., n=5)
d30_complication
```

```
## # A tibble: 5 × 3
##   ahrq_ccs                         ccscomplicationrate     n
##   <chr>                                          <dbl> <int>
## 1 Small bowel resection                          0.466   620
## 2 Colorectal resection                           0.312  2519
## 3 Nephrectomy; partial or complete               0.197  2894
## 4 Gastrectomy; partial and total                 0.190   394
## 5 Spinal fusion                                  0.183  2694
```
*The highest risk of complication within 30 days is for small bowel resection, whereas the highest risk for 30 day mortality is colorectal resection.* 

**8. (3 points) Make a plot that compares the `ccsmort30rate` for all listed `ahrq_ccs` procedures.

```r
surgery %>% 
  ggplot(aes(x=ahrq_ccs, y=ccsmort30rate, na.rm=TRUE))+
  geom_col()+
  coord_flip()+
  theme_classic()+
  theme(axis.text.x = element_text(angle = 60, hjust = 1))+
  labs(title = "Thirty Day Mortality Rate by Surgical Procedure",
       x = "Surgical Procedure",
       y = "Mortality Rate",
       fill = "ahrq_ccs")
```

![](midterm_2_files/figure-html/unnamed-chunk-12-1.png)<!-- -->


9. (4 points) When is the best month to have surgery? Make a chart that shows the 30-day mortality and complications for the patients by month. `mort30` is the variable that shows whether or not a patient survived 30 days post-operation. *December is the best month to have surgery*


```r
surgery2<- surgery %>%
  mutate(mort_new = ifelse(mort30 =="Yes", 1, 0))%>%
  count(month, mort_new)
surgery2
```

```
## # A tibble: 24 × 3
##    month mort_new     n
##    <chr>    <dbl> <int>
##  1 Apr          0  2686
##  2 Apr          1    12
##  3 Aug          0  3168
##  4 Aug          1     9
##  5 Dec          0  1835
##  6 Dec          1     4
##  7 Feb          0  2489
##  8 Feb          1    17
##  9 Jan          0  2651
## 10 Jan          1    19
## # … with 14 more rows
```



10. (4 points) Make a plot that visualizes the chart from question #9. Make sure that the months are on the x-axis. Do a search online and figure out how to order the months Jan-Dec.


```r
surgery2 %>% 
  filter(mort_new=="1") %>% 
  ggplot(aes(x=month, y=n, na.rm=TRUE))+
  geom_col()+
  theme_classic()+
  theme(axis.text.x = element_text(angle = 60, hjust = 1))+
  scale_x_discrete(limits = month.abb)
```

![](midterm_2_files/figure-html/unnamed-chunk-14-1.png)<!-- -->

```r
  labs(title = "Mortality by Month",
       x = "Month",
       y = "Mortality Count")
```

```
## $x
## [1] "Month"
## 
## $y
## [1] "Mortality Count"
## 
## $title
## [1] "Mortality by Month"
## 
## attr(,"class")
## [1] "labels"
```

Please provide the names of the students you have worked with with during the exam:

Please be 100% sure your exam is saved, knitted, and pushed to your github repository. No need to submit a link on canvas, we will find your exam in your repository.
