mini-data-analysis-milestone1
================
Lorenzo Lindo
07/10/2021

# STAT545A - Mini Data Analysis Project: Milestone 1 (LINDO, Lorenzo)

## Load the required packages.

Run the following code to load the required packages for this mini data
analysis.

``` r
library(datateachr)
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──

    ## ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
    ## ✓ tibble  3.1.5     ✓ dplyr   1.0.7
    ## ✓ tidyr   1.1.4     ✓ stringr 1.4.0
    ## ✓ readr   2.0.2     ✓ forcats 0.5.1

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(ggplot2)
library(dplyr)
```

## Task 1 - Exploring My Datasets of Interest

### These datasets that will be used explored for this mini data analysis.

| Dataset Number | Dataset Name     | Description of Data Set                                                                     | Credit                                                        | Dimensions                 |
|----------------|------------------|---------------------------------------------------------------------------------------------|---------------------------------------------------------------|----------------------------|
| 1              | cancer_sample    | Diagnostic Breast Cancer Data                                                               | Acquired courtesy of UCI Machine Learning Repository          | 569 rows and 32 columns    |
| 2              | steam_games      | Contains games from Steam shop with detailed data downloaded from kaggle with a CC0 license | Acquired courtesy of Kaggle                                   | 40833 rows and 21 columns  |
| 3              | building_permits | Data about the City of Vancouver’s building permits                                         | Acquired courtesy of the City of Vancouver’s Open Data Portal | 20680 rows and 14 columns  |
| 4              | vancouver_trees  | Data about Vancouver’s trees                                                                | Acquired courtesy of the City of Vancouver’s Open Data Portal | 146611 rows and 20 columns |

#### Exploring the cancer_sample dataset

``` r
head(cancer_sample) #Returns the first few rows
```

    ## # A tibble: 6 × 32
    ##         ID diagnosis radius_mean texture_mean perimeter_mean area_mean
    ##      <dbl> <chr>           <dbl>        <dbl>          <dbl>     <dbl>
    ## 1   842302 M                18.0         10.4          123.      1001 
    ## 2   842517 M                20.6         17.8          133.      1326 
    ## 3 84300903 M                19.7         21.2          130       1203 
    ## 4 84348301 M                11.4         20.4           77.6      386.
    ## 5 84358402 M                20.3         14.3          135.      1297 
    ## 6   843786 M                12.4         15.7           82.6      477.
    ## # … with 26 more variables: smoothness_mean <dbl>, compactness_mean <dbl>,
    ## #   concavity_mean <dbl>, concave_points_mean <dbl>, symmetry_mean <dbl>,
    ## #   fractal_dimension_mean <dbl>, radius_se <dbl>, texture_se <dbl>,
    ## #   perimeter_se <dbl>, area_se <dbl>, smoothness_se <dbl>,
    ## #   compactness_se <dbl>, concavity_se <dbl>, concave_points_se <dbl>,
    ## #   symmetry_se <dbl>, fractal_dimension_se <dbl>, radius_worst <dbl>,
    ## #   texture_worst <dbl>, perimeter_worst <dbl>, area_worst <dbl>, …

``` r
dim(cancer_sample) #Returns the dimensions of the dataset (how many rows and columns)
```

    ## [1] 569  32

``` r
class(cancer_sample) #Returns the class of the dataset
```

    ## [1] "spec_tbl_df" "tbl_df"      "tbl"         "data.frame"

``` r
cancer_sample %>% 
  group_by(diagnosis) %>% 
  summarise(perimeter_mean_median = mean(perimeter_mean, na.rm = TRUE))
```

    ## # A tibble: 2 × 2
    ##   diagnosis perimeter_mean_median
    ##   <chr>                     <dbl>
    ## 1 B                          78.1
    ## 2 M                         115.

#### Exploring the steam_games dataset

``` r
head(steam_games) #Returns the first few rows
```

    ## # A tibble: 6 × 21
    ##      id url    types  name  desc_snippet recent_reviews all_reviews release_date
    ##   <dbl> <chr>  <chr>  <chr> <chr>        <chr>          <chr>       <chr>       
    ## 1     1 https… app    DOOM  Now include… Very Positive… Very Posit… May 12, 2016
    ## 2     2 https… app    PLAY… PLAYERUNKNO… Mixed,(6,214)… Mixed,(836… Dec 21, 2017
    ## 3     3 https… app    BATT… Take comman… Mixed,(166),-… Mostly Pos… Apr 24, 2018
    ## 4     4 https… app    DayZ  The post-so… Mixed,(932),-… Mixed,(167… Dec 13, 2018
    ## 5     5 https… app    EVE … EVE Online … Mixed,(287),-… Mostly Pos… May 6, 2003 
    ## 6     6 https… bundle Gran… Grand Theft… NaN            NaN         NaN         
    ## # … with 13 more variables: developer <chr>, publisher <chr>,
    ## #   popular_tags <chr>, game_details <chr>, languages <chr>,
    ## #   achievements <dbl>, genre <chr>, game_description <chr>,
    ## #   mature_content <chr>, minimum_requirements <chr>,
    ## #   recommended_requirements <chr>, original_price <dbl>, discount_price <dbl>

``` r
dim(steam_games) #Returns the dimensions of the dataset (how many rows and columns)
```

    ## [1] 40833    21

``` r
class(steam_games) #Returns the class of the dataset
```

    ## [1] "spec_tbl_df" "tbl_df"      "tbl"         "data.frame"

``` r
steam_games %>% 
  group_by(genre) %>% 
  summarize(n())
```

    ## # A tibble: 1,769 × 2
    ##    genre                                                                   `n()`
    ##    <chr>                                                                   <int>
    ##  1 Accounting                                                                  2
    ##  2 Accounting,Animation & Modeling,Audio Production,Design & Illustration…     1
    ##  3 Accounting,Animation & Modeling,Audio Production,Design & Illustration…     2
    ##  4 Accounting,Education,Software Training,Utilities,Early Access               1
    ##  5 Action                                                                   2386
    ##  6 Action,Adventure                                                          809
    ##  7 Action,Adventure,Casual                                                    64
    ##  8 Action,Adventure,Casual,Early Access                                        1
    ##  9 Action,Adventure,Casual,Free to Play                                        1
    ## 10 Action,Adventure,Casual,Free to Play,Early Access                           1
    ## # … with 1,759 more rows

#### Exploring the building_permits dataset

``` r
head(building_permits) #Returns the first few rows
```

    ## # A tibble: 6 × 14
    ##   permit_number issue_date project_value type_of_work  address  project_descrip…
    ##   <chr>         <date>             <dbl> <chr>         <chr>    <chr>           
    ## 1 BP-2016-02248 2017-02-01             0 Salvage and … 4378 W … <NA>            
    ## 2 BU468090      2017-02-01             0 New Building  1111 RI… <NA>            
    ## 3 DB-2016-04450 2017-02-01         35000 Addition / A… 3732 W … <NA>            
    ## 4 DB-2017-00131 2017-02-01         15000 Addition / A… 88 W PE… <NA>            
    ## 5 DB452250      2017-02-01        181178 New Building  492 E 6… <NA>            
    ## 6 BP-2016-01458 2017-02-02             0 Salvage and … 3332 W … <NA>            
    ## # … with 8 more variables: building_contractor <chr>,
    ## #   building_contractor_address <chr>, applicant <chr>,
    ## #   applicant_address <chr>, property_use <chr>, specific_use_category <chr>,
    ## #   year <dbl>, bi_id <dbl>

``` r
dim(building_permits) #Returns the dimensions of the dataset (how many rows and columns)
```

    ## [1] 20680    14

``` r
class(building_permits) #Returns the class of the dataset
```

    ## [1] "spec_tbl_df" "tbl_df"      "tbl"         "data.frame"

``` r
building_permits %>% 
  group_by(type_of_work) %>% 
  summarize(n())
```

    ## # A tibble: 6 × 2
    ##   type_of_work                         `n()`
    ##   <chr>                                <int>
    ## 1 Addition / Alteration                10380
    ## 2 Demolition / Deconstruction           2565
    ## 3 New Building                          4728
    ## 4 Outdoor Uses (No Buildings Proposed)    27
    ## 5 Salvage and Abatement                 2763
    ## 6 Temporary Building / Structure         217

#### Exploring the vancouver_trees dataset

``` r
head(vancouver_trees) #Returns the first few rows
```

    ## # A tibble: 6 × 20
    ##   tree_id civic_number std_street genus_name species_name cultivar_name  
    ##     <dbl>        <dbl> <chr>      <chr>      <chr>        <chr>          
    ## 1  149556          494 W 58TH AV  ULMUS      AMERICANA    BRANDON        
    ## 2  149563          450 W 58TH AV  ZELKOVA    SERRATA      <NA>           
    ## 3  149579         4994 WINDSOR ST STYRAX     JAPONICA     <NA>           
    ## 4  149590          858 E 39TH AV  FRAXINUS   AMERICANA    AUTUMN APPLAUSE
    ## 5  149604         5032 WINDSOR ST ACER       CAMPESTRE    <NA>           
    ## 6  149616          585 W 61ST AV  PYRUS      CALLERYANA   CHANTICLEER    
    ## # … with 14 more variables: common_name <chr>, assigned <chr>,
    ## #   root_barrier <chr>, plant_area <chr>, on_street_block <dbl>,
    ## #   on_street <chr>, neighbourhood_name <chr>, street_side_name <chr>,
    ## #   height_range_id <dbl>, diameter <dbl>, curb <chr>, date_planted <date>,
    ## #   longitude <dbl>, latitude <dbl>

``` r
dim(vancouver_trees) #Returns the dimensions of the dataset (how many rows and columns)
```

    ## [1] 146611     20

``` r
class(vancouver_trees) #Returns the class of the dataset
```

    ## [1] "tbl_df"     "tbl"        "data.frame"

``` r
vancouver_trees %>% 
  group_by(genus_name) %>% 
  summarize(n())
```

    ## # A tibble: 97 × 2
    ##    genus_name  `n()`
    ##    <chr>       <int>
    ##  1 ABIES         190
    ##  2 ACER        36062
    ##  3 AESCULUS     2570
    ##  4 AILANTHUS       4
    ##  5 ALBIZIA         1
    ##  6 ALNUS          74
    ##  7 AMELANCHIER   226
    ##  8 ARALIA          4
    ##  9 ARAUCARIA      10
    ## 10 ARBUTUS        10
    ## # … with 87 more rows

### Narrowing down to 2 datasets of interest

| Dataset       | Why I chose this?                                                                                                                                                        |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| cancer_sample | I chose to continue exploring this dataset because my research is focussed on cancer and I wanted to practice data wrangling and analysis on a dataset related to cancer |
| steam_games   | I chose to continue exploring this dataset because I used to be a big Steam gamer and I wanted to analyze some data about games                                          |

### The final decision - which one will I continue analyzing?

| Dataset       | Why I chose this?                                                                                                                                                       |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| cancer_sample | This will be the dataset that I will continue to explore because my research focusses on cancer and the analyses I can attempt here are relevant to my research project |

## Task 2 - Exploring the cancer_samples dataset

### Some Initial Manipulation of the Datasets

#### Exercise Option 1:

Plotting the distribution of the mean radius of nuclei present in the
sample images in this dataset (variable = radius_mean). **Rationale**:
This was done to get a sense of the distribution of the radius_mean
variable.

``` r
cancer_sample %>% 
  ggplot(aes(x = radius_mean)) +
  geom_histogram(binwidth = 0.5)
```

![](mini-data-analysis-milestone1_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

#### Exercise Option 2:

Calculating the expected area_mean of the nuclei present based on the
observed radius_mean and assigning it as a new variable. **Rationale**:
This was done to calculate what the expected mean area would be of the
nuclei given the observed mean radii of the nuclei observed. This could
be explored later as a research question to see how close the observed
mean area is to the expected mean area.

``` r
cancer_sample %>% 
  mutate(expected_area_mean = (radius_mean)^2 * pi) %>% 
  relocate(expected_area_mean, .after = radius_mean) %>% 
  relocate(area_mean, .after = expected_area_mean)
```

    ## # A tibble: 569 × 33
    ##          ID diagnosis radius_mean expected_area_mean area_mean texture_mean
    ##       <dbl> <chr>           <dbl>              <dbl>     <dbl>        <dbl>
    ##  1   842302 M                18.0              1017.     1001          10.4
    ##  2   842517 M                20.6              1329.     1326          17.8
    ##  3 84300903 M                19.7              1218.     1203          21.2
    ##  4 84348301 M                11.4               410.      386.         20.4
    ##  5 84358402 M                20.3              1293.     1297          14.3
    ##  6   843786 M                12.4               487.      477.         15.7
    ##  7   844359 M                18.2              1046.     1040          20.0
    ##  8 84458202 M                13.7               591.      578.         20.8
    ##  9   844981 M                13                 531.      520.         21.8
    ## 10 84501001 M                12.5               488.      476.         24.0
    ## # … with 559 more rows, and 27 more variables: perimeter_mean <dbl>,
    ## #   smoothness_mean <dbl>, compactness_mean <dbl>, concavity_mean <dbl>,
    ## #   concave_points_mean <dbl>, symmetry_mean <dbl>,
    ## #   fractal_dimension_mean <dbl>, radius_se <dbl>, texture_se <dbl>,
    ## #   perimeter_se <dbl>, area_se <dbl>, smoothness_se <dbl>,
    ## #   compactness_se <dbl>, concavity_se <dbl>, concave_points_se <dbl>,
    ## #   symmetry_se <dbl>, fractal_dimension_se <dbl>, radius_worst <dbl>, …

#### Exercise Option 4:

Exploring the relationship between the radius_mean and the area_mean.
**Rationale**: This was done to see if there is any correlation between
these two variables.

``` r
cancer_sample %>% 
  ggplot(aes(x = radius_mean, y = area_mean)) +
  geom_point()
```

![](mini-data-analysis-milestone1_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

#### Exercise Option 6:

A boxplot of the frequency of different observations of the area_mean in
either “M” malignant or “B” benign observations. **Rationale**: This was
done to see if there is any difference in the mean area of the nuclei in
between those who were ultimately diagnosed with a malignant breast mass
or a benign breast mass.

``` r
cancer_sample %>% 
  group_by(diagnosis) %>% 
  ggplot(aes(x = diagnosis, y = area_mean, fill = diagnosis)) +
  geom_boxplot() +
  labs(title = "Mean Area in Benign and Malignant Samples" ) +
  xlab("Diagnosis (diagnosis)") +
  ylab("Mean Area of Nuclei (area_mean)") +
  theme_minimal()
```

![](mini-data-analysis-milestone1_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

## Task 3 - Writing my Research Questions

Below are my proposed research questions for this dataset. I also
include some rationale and expected outcomes

| Question Number | Research Question                                                                                                                                                                       | Rationale                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1               | Is there a significant difference in the mean area of the nuclei present in sample images between those who had a malignant breast mass compared to those who had a benign breast mass. | This will give us a sense as to whether there is any relationship between mean nuclei area and diagnosis. We would expect that those with a malignant diagnosis would have a greater nuclei mass, which would be consistent with observations in the literature. I would want to test the significance of this difference in this dataset.                                                                                                                                       |
| 2               | What is the relationship between the mean smoothness of nuclei and the mean area of nuclei?                                                                                             | I would predict that larger nuclei would be less smooth. This is because larger nuclei typically denote actively replicating cells, so if the genetic material is replicating, it may make the morphology of the nuclei look more rough. Therefore, I would predict that there is an inverse relationship between mean area and mean smoothness. I would also want to explore if this relationship is modified when I subset between those with a benign or malignant diagnosis. |
| 3               | Can we predict the mean area based on the mean radius?                                                                                                                                  | It would make sense that if given a mean radius, we could calculate a mean area. However, nuclei are often not perfect circles, and therefore we would expect a degree of variation. I would therefore first calculate the expected mean area from the mean radius (as I had done in Task 2), then I would want to determine the correlation between the expected mean area and the observed mean area.                                                                          |
| 4               | Is there a significant difference in the standard error of smoothness of nuclei between those with a malignant or benign breast mass?                                                   | I would predict that those with a malignant breast mass would have a greater standard error of smoothness of nuclei because cancerous cells tend to be dysregulated and as a result often have more variability in their morphology.                                                                                                                                                                                                                                             |
