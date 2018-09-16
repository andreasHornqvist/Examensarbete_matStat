Summary statistics and modeling approach to Booli housing data
================

### Summary statistics

###### Table 1. Summary statistics of the Booli dataset

    ## Skim summary statistics  
    ##  n obs: 397048    
    ##  n variables: 30    
    ## 
    ## Variable type: factor
    ## 
    ##              variable                missing    complete      n       n_unique                      top_counts                    
    ## ----------------------------------  ---------  ----------  --------  ----------  -------------------------------------------------
    ##          apartmentNumber             282522      114526     397048      2595       NA: 282522, 120: 11062, 120: 10225, 100: 7011  
    ##       location.address.city          159524      237524     397048      2427      NA: 159524, Göt: 28200, Mal: 19131, Upp: 10811  
    ##   location.address.streetAddress        0        397048     397048     177067          Adr: 682, Kun: 124, Öst: 100, Bor: 92      
    ##        location.namedAreas             696       396352     397048     15945        Cen: 20259, Vas: 7934, Kun: 7855, Söd: 7029   
    ##     location.region.countyName          0        397048     397048       21       Sto: 165507, Väs: 58961, Skå: 43584, Upp: 17033 
    ##  location.region.municipalityName       0        397048     397048      290       Sto: 87302, Göt: 25944, Mal: 20053, Upp: 12235  
    ##             objectType                  0        397048     397048       10       Läg: 305639, Vil: 54280, Fri: 14182, Rad: 11185 
    ##             published                   0        397048     397048      2080          201: 921, 201: 902, 201: 899, 201: 868      
    ##              soldDate                   0        397048     397048      2069          201: 1454, 201: 801, 201: 773, 201: 772     
    ##          soldPriceSource                0        397048     397048       7          bid: 390503, mak: 4346, adm: 2090, kop: 42    
    ##            source.name                  0        397048     397048      564       Fas: 103952, Sve: 50027, Län: 34178, Ska: 22710 
    ##            source.type                  0        397048     397048       2                 Bro: 396874, Con: 174, NA: 0           
    ##             source.url                  0        397048     397048      571       htt: 103952, htt: 50027, htt: 34178, htt: 22710 
    ##                url                      0        397048     397048     395539             htt: 4, htt: 4, htt: 4, htt: 4          
    ## 
    ## Variable type: integer
    ## 
    ##         variable            missing    complete      n          mean          sd          p0         p25         p50        p75         p100   
    ## -------------------------  ---------  ----------  --------  ------------  -----------  --------  ------------  -------  ------------  ---------
    ##          booliId               0        397048     397048    2131438.9     539205.29    269376    1738313.25    2e+06    2334060.25    3238500 
    ##     constructionYear         51632      345416     397048     1961.92        33.19        0          1944       1962        1983        2020   
    ##     isNewConstruction       391188       5860      397048        1             0          1           1           1          1            1    
    ##  location.distance.ocean    194978      202070     397048     2530.26       2376.34       1          806        1838      3477.75       27649  
    ##           rent               85128      311920     397048      3612.8       1343.1        0          2681       3489        4406        42334  
    ##         source.id              0        397048     397048    1184865.27     1.2e+07       10         713        1566        1573        3e+08  
    ## 
    ## Variable type: logical
    ## 
    ##             variable                missing    complete      n       mean            count          
    ## ---------------------------------  ---------  ----------  --------  ------  ------------------------
    ##  location.position.isApproximate    302968      94080      397048     1      NA: 302968, TRU: 94080 
    ## 
    ## Variable type: numeric
    ## 
    ##           variable              missing    complete      n          mean           sd         p0        p25        p50        p75       p100   
    ## -----------------------------  ---------  ----------  --------  ------------  ------------  -------  ---------  ---------  ---------  ---------
    ##        additionalArea           310753      86295      397048      32.44         61.14         0         0         10         50        1025   
    ##             floor               157117      239931     397048       2.64          2.13        -3         1          2          3        99.9   
    ##           listPrice              2547       394501     397048    2216956.68    1797729.83      0       1e+06     1800000    2800000     6e+07  
    ##          livingArea              5774       391274     397048      77.46         40.37         0        53        69.2        92        1445   
    ##  location.position.latitude        0        397048     397048      58.89          1.81       55.34     57.78      59.3       59.39      68.46  
    ##  location.position.longitude       0        397048     397048      16.06          2.49       10.99     13.3       17.3       18.03      24.14  
    ##           plotArea              299381      97667      397048     4353.11       46170.04       0        248        903       1667      4444000 
    ##             rooms                6544       390504     397048       2.96          1.52         1         2          3          4         39    
    ##           soldPrice                0        397048     397048    2429977.38    1909707.74    15000    1200000     2e+06     3100000    9.8e+07

### First ten rows

###### Table 2. The first ten rows of the Booli dataset

| location.address.streetAddress | location.position.latitude | location.position.longitude |  location.namedAreas  | location.region.municipalityName | location.region.countyName | location.distance.ocean | listPrice | rent | floor | livingArea |               source.name              | source.id | source.type |             source.url            | rooms |  published | constructionYear | objectType | booliId |  soldDate  | soldPrice | soldPriceSource |                  url                  | plotArea | additionalArea | apartmentNumber | isNewConstruction | location.address.city | location.position.isApproximate |
|:------------------------------:|:--------------------------:|:---------------------------:|:---------------------:|:--------------------------------:|:--------------------------:|:-----------------------:|:---------:|:----:|:-----:|:----------:|:--------------------------------------:|:---------:|:-----------:|:---------------------------------:|:-----:|:----------:|:----------------:|:----------:|:-------:|:----------:|:---------:|:---------------:|:-------------------------------------:|:--------:|:--------------:|:---------------:|:-----------------:|:---------------------:|:-------------------------------:|
|         Pingstvägen 12         |          59.30168          |           18.00093          | Hägersten-Liljeholmen |             Stockholm            |       Stockholms län       |           4674          |  1995000  | 2069 |   1   |     35     |             Fastighetsbyrån            |    1573   |    Broker   |  <http://www.fastighetsbyran.se/> |   1   | 2018-08-30 |       1939       |  Lägenhet  | 3227686 | 2018-09-14 |  2330000  |       bid       | <https://www.booli.se/annons/3227686> |    NA    |       NA       |        NA       |         NA        |           NA          |                NA               |
|       Nidarosslingan 18D       |          59.39829          |           17.83805          |         Skälby        |             Järfälla             |       Stockholms län       |            NA           |  1995000  | 3639 |   1   |     61     |             Fastighetsbyrån            |    1573   |    Broker   |  <http://www.fastighetsbyran.se/> |   2   | 2018-08-30 |       2009       |  Lägenhet  | 3227682 | 2018-09-14 |  2100000  |       bid       | <https://www.booli.se/annons/3227682> |    NA    |       NA       |        NA       |         NA        |           NA          |                NA               |
|        Grantoppsgränd 11       |          59.38742          |           17.82380          |   Hässelby-Vällingby  |             Stockholm            |       Stockholms län       |            NA           |  3975000  |  NA  |   NA  |     125    |             Fastighetsbyrån            |    1573   |    Broker   |  <http://www.fastighetsbyran.se/> |   5   | 2018-07-30 |       1975       |  Kedjehus  | 3204170 | 2018-09-14 |  3975000  |       bid       | <https://www.booli.se/annons/3204170> |    312   |       NA       |        NA       |         NA        |           NA          |                NA               |
|          Tulegatan 48A         |          59.36727          |           17.96760          |    Sundbyberg/Duvbo   |            Sundbyberg            |       Stockholms län       |           3748          |  2995000  | 4315 |   3   |     57     |             Fastighetsbyrån            |    1573   |    Broker   |  <http://www.fastighetsbyran.se/> |   2   | 2018-07-15 |       1996       |  Lägenhet  | 3200995 | 2018-09-14 |  3000000  |       bid       | <https://www.booli.se/annons/3200995> |    NA    |       NA       |        NA       |         NA        |           NA          |                NA               |
|        Älvdalsvägen 105        |          59.38187          |           17.81173          |   Hässelby-Vällingby  |             Stockholm            |       Stockholms län       |            NA           |  3595000  |  NA  |   NA  |     107    |             Fastighetsbyrån            |    1573   |    Broker   |  <http://www.fastighetsbyran.se/> |   4   | 2018-08-06 |       1984       |   Radhus   | 3185964 | 2018-09-14 |  3700000  |       bid       | <https://www.booli.se/annons/3185964> |    147   |       NA       |        NA       |         NA        |           NA          |                NA               |
|       Skottspolsliden 21       |          59.40000          |           13.61569          |         Alster        |             Karlstad             |        Värmlands län       |            NA           |  2495000  |  NA  |   NA  |     127    |             SkandiaMäklarna            |    1570   |    Broker   |  <http://www.skandiamaklarna.se/> |   5   | 2018-08-26 |       1978       |    Villa   | 3221831 | 2018-09-14 |  2900000  |       bid       | <https://www.booli.se/annons/3221831> |    800   |        0       |        NA       |         NA        |           NA          |                NA               |
|         Pipersgatan 18         |          59.33070          |           18.04597          |      Kungsholmen      |             Stockholm            |       Stockholms län       |           1402          |  3395000  | 2828 |   2   |     38     |            Magnusson Mäkleri           |    2030   |    Broker   | <http://www.magnussonmakleri.se/> |   2   | 2018-08-24 |       1935       |  Lägenhet  | 3223055 | 2018-09-14 |  3625000  |       bid       | <https://www.booli.se/annons/3223055> |    NA    |        0       |        NA       |         NA        |           NA          |                NA               |
|           Solgatan 8           |          59.36032          |           18.01013          |     Centrum Solna     |               Solna              |       Stockholms län       |           2782          |  2995000  | 2975 |   5   |     58     |  Länsförsäkringar Fastighetsförmedling |     64    |    Broker   |     <https://www.lansfast.se/>    |   2   | 2018-09-08 |       2011       |  Lägenhet  | 3235387 | 2018-09-14 |  3350000  |       bid       | <https://www.booli.se/annons/3235387> |    NA    |        0       |       1402      |         NA        |           NA          |                NA               |
|          Ringgatan 18          |          59.52364          |           13.48807          |         Skived        |             Forshaga             |        Värmlands län       |            NA           |  1550000  |  NA  |   NA  |     118    |             SkandiaMäklarna            |    1570   |    Broker   |  <http://www.skandiamaklarna.se/> |   7   | 2018-08-24 |       1969       |    Villa   | 3221576 | 2018-09-14 |  2000000  |       bid       | <https://www.booli.se/annons/3221576> |    663   |       94       |        NA       |         NA        |           NA          |                NA               |
|        Ekensbergskajen 4       |          59.31697          |           17.99782          |        Gröndal        |             Stockholm            |       Stockholms län       |           4327          |  4195000  | 3168 |   NA  |     75     | Edward & Partners Fastighetsmäklare AB |    410    |    Broker   |  <http://www.edwardpartners.se/>  |   2   | 2018-05-07 |       2018       |  Lägenhet  | 3146229 | 2018-09-14 |  4195000  |       bid       | <https://www.booli.se/annons/3146229> |    NA    |        0       |        NA       |         1         |           NA          |                NA               |

Cleaning and other considerations about the data
------------------------------------------------

We notice a large amount of NAs in many of the variables, some seem to be actual unknowns (such as apartmentNumber) others (e.g. isNewConstruction) seem to be badly formatted boolean values with NAs instead of 0, or FALSE.

Most of the NAs looks fairly easy to handle either by imputing, converting to zeroes or by exclusion.

Another feature of the dataset is the fact that some factor variables have a very large amount of levels, something which could potentially hamper some algoritms.

Furthermore we can conclude that the dataset is well formated, in a tabular sense, and that it contains a fairly large amount of observations.

Some feature engineering will probably have to take place, on one hand in consideration to domain knowledge and on another to eleviate some of the more troblesome NAs e.g. binning of location.distance.ocean.

We can also note that the set of 30 features might necessitate some forms of more advanced feauture selection algorithms in case of more traditional modeling techniques like multivariate linear regression and the like.

Modeling
--------

Predicting the selling price (SoldPrice) is, in machinelearning nomenclature, a supervised regression problem in the sense that outcomes are labeled and continous. I desbribe some plausible modeling approaches below.

### Classic regression modeling

A first approach to this kind of problem could be some variation of multivarate regression e.g. Linear, Lasso or the like.

This probably isn't the best approach due to the nature of the data, lots of factor variabels (whith many levels), inherently non-linear dependencies (it´s timeseries data) and so on. However it´s probably possible the create a decent model with the help of som feature engineering which might serve as a baseline. The inherent interpretability of classical regression models could also aid in modeling using more novel algoritms.

Another advantage of the above approach is the expected wealth of previous work using such modeling techniques.

### Boosted trees

Approaches using variations of boosted trees (forests really), e.g. gradient boosting have proven quite successfull on tabular data. Advantages are ease of implementation, interpretability, good performance out of the box (i.e. without much tuning) boosted trees are however prone to overfitting so thats something to be wary of. They also lend themselves to feature engineering.

### Deep learning and other neural network techniques

And dont know that much about it but hope to learn :)

They are of course black box, requires large datasets, and are sensitive to tuning. Have proven to deliver amazing results in certain settings though, but perhaps most so in reinforcement learning.

### Ensemble techniques

Ensemble techniques are know to be prevalous for prediction, for example on competition sites like kaggle, and are a good reason to explore several different modeling aproaches.

The technique entails using several different models and letting them "vote" on the result.

/Andreas

``` r
sessionInfo()
```

    ## R version 3.4.3 (2017-11-30)
    ## Platform: x86_64-apple-darwin15.6.0 (64-bit)
    ## Running under: macOS High Sierra 10.13.1
    ## 
    ## Matrix products: default
    ## BLAS: /Library/Frameworks/R.framework/Versions/3.4/Resources/lib/libRblas.0.dylib
    ## LAPACK: /Library/Frameworks/R.framework/Versions/3.4/Resources/lib/libRlapack.dylib
    ## 
    ## locale:
    ## [1] sv_SE.UTF-8/sv_SE.UTF-8/sv_SE.UTF-8/C/sv_SE.UTF-8/sv_SE.UTF-8
    ## 
    ## attached base packages:
    ## [1] stats     graphics  grDevices utils     datasets  methods   base     
    ## 
    ## other attached packages:
    ## [1] bindrcpp_0.2 dplyr_0.7.4  skimr_1.0.3  knitr_1.18  
    ## 
    ## loaded via a namespace (and not attached):
    ##  [1] Rcpp_0.12.15     bindr_0.1        magrittr_1.5     tidyselect_0.2.4
    ##  [5] R6_2.2.2         rlang_0.2.2      highr_0.6        stringr_1.2.0   
    ##  [9] tools_3.4.3      htmltools_0.3.6  yaml_2.1.16      rprojroot_1.3-2 
    ## [13] digest_0.6.15    assertthat_0.2.0 tibble_1.4.2     purrr_0.2.4     
    ## [17] tidyr_0.7.2      glue_1.2.0       evaluate_0.10.1  rmarkdown_1.8   
    ## [21] stringi_1.1.6    compiler_3.4.3   pillar_1.1.0     backports_1.1.2 
    ## [25] pkgconfig_2.0.1
