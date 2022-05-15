Crimes from 1975-2015 - Final Report
================

## by Beatriz Mendoza

### Executive summary

The research provides a better understanding of crimes from 1975 to 2015
caused in the United States. Although there have been many changes over
the years, it predicts that violent crime cases have decreased over
time. According to the data provided, crimes are more committed towards
the end of the year. Especially in December, there’s a high rate of
crimes committed that month. However, out of the four most violent
crimes, homicides have subsided by the end of 2015. It’s predictable to
say that the year and month influence the reported crimes.

### Summary of learning

I enjoyed messing with the data visuals to distinguish the correlation
between data. Furthermore, it is interesting to see more homicides in
the 70s. It could be because of the serial hype back in the day, but now
it has decreased. Unfortunately, I didn’t get a chance to compare the
populations and cities of people who committed these violent crimes. I
had challenges in how to represent that on the report.

### Data set

The Marshall Project, a non-profit news organization, seeks to create
and sustain a sense of national urgency about the U.S criminal justice
system. The data used in this project is a report collected from the FBI
Uniform Reporting program’s “Offenses Known and Clearances by Arrest”
database for the years between 1975-2015. This data set is from Kaggle
named ‘report.csv.’ The information contains four major crimes:
homicide, rape, robbery, and assault.

``` r
setwd("/Users/Beatrisss/Desktop/INFO 3010/Final")
df <- read.csv('report.csv')
head(df)
```

    ##   report_year agency_code  agency_jurisdiction population violent_crimes
    ## 1        1975     NM00101      Albuquerque, NM     286238           2383
    ## 2        1975     TX22001        Arlington, TX     112478            278
    ## 3        1975     GAAPD00          Atlanta, GA     490584           8033
    ## 4        1975     CO00101           Aurora, CO     116656            611
    ## 5        1975     TX22701           Austin, TX     300400           1215
    ## 6        1975     MD00301 Baltimore County, MD     642154           1259
    ##   homicides rapes assaults robberies months_reported crimes_percapita
    ## 1        30   181     1353       819              12           832.52
    ## 2         5    28      132       113              12           247.16
    ## 3       185   443     3518      3887              12          1637.44
    ## 4         7    44      389       171              12           523.76
    ## 5        33   190      463       529              12           404.46
    ## 6        25   137      347       750              12           196.06
    ##   homicides_percapita rapes_percapita assaults_percapita robberies_percapita
    ## 1               10.48           63.23             472.68              286.13
    ## 2                4.45           24.89             117.36              100.46
    ## 3               37.71           90.30             717.10              792.32
    ## 4                6.00           37.72             333.46              146.58
    ## 5               10.99           63.25             154.13              176.10
    ## 6                3.89           21.33              54.04              116.79

### Exploratory Data Analysis

#### Statistical Summary of Data

The following will describe the statistical summary of the data set
from  
‘report.csv.’ Using the library ‘Hmisc’ package to calculate the
distinct value of each column and the frequency of each data set value.
The earliest agency jurisdiction is the following cities, Albuquerque,
Arlington, Atlanta, Aurora, and Austin from the year 1975. Across the
United States, there were 1,932,274 violent crimes committed between
1975-2015. If you compare based on the four violent crimes, robberies
are on top.There are 68 police jurisdictions in charge of the violent
crimes committed.

``` r
library(Hmisc)
```

    ## Warning: package 'Hmisc' was built under R version 4.1.3

    ## Loading required package: lattice

    ## Warning: package 'lattice' was built under R version 4.1.3

    ## Loading required package: survival

    ## Loading required package: Formula

    ## Loading required package: ggplot2

    ## Warning: package 'ggplot2' was built under R version 4.1.3

    ## 
    ## Attaching package: 'Hmisc'

    ## The following objects are masked from 'package:base':
    ## 
    ##     format.pval, units

``` r
describe(df)
```

    ## df 
    ## 
    ##  15  Variables      2829  Observations
    ## --------------------------------------------------------------------------------
    ## report_year 
    ##        n  missing distinct     Info     Mean      Gmd      .05      .10 
    ##     2829        0       41    0.999     1995    13.66     1977     1979 
    ##      .25      .50      .75      .90      .95 
    ##     1985     1995     2005     2011     2013 
    ## 
    ## lowest : 1975 1976 1977 1978 1979, highest: 2011 2012 2013 2014 2015
    ## --------------------------------------------------------------------------------
    ## agency_code 
    ##        n  missing distinct 
    ##     2788       41       68 
    ## 
    ## lowest : AZ00717 AZ00723 AZ01003 CA00109 CA01005
    ## highest: UT01803 VA02901 VA12800 WASPD00 WIMPD00
    ## --------------------------------------------------------------------------------
    ## agency_jurisdiction 
    ##        n  missing distinct 
    ##     2829        0       69 
    ## 
    ## lowest : Albuquerque, NM    Arlington, TX      Atlanta, GA        Aurora, CO         Austin, TX        
    ## highest: Tulsa, OK          United States      Virginia Beach, VA Washington, DC     Wichita, KS       
    ## --------------------------------------------------------------------------------
    ## population 
    ##        n  missing distinct     Info     Mean      Gmd      .05      .10 
    ##     2760       69     2740        1   795698   683025   221103   289452 
    ##      .25      .50      .75      .90      .95 
    ##   377931   536615   816856  1270623  1955848 
    ## 
    ## lowest :  100763  107470  112478  112994  113176
    ## highest: 8345075 8396126 8400907 8473938 8550861
    ## --------------------------------------------------------------------------------
    ## violent_crimes 
    ##        n  missing distinct     Info     Mean      Gmd      .05      .10 
    ##     2794       35     2526        1    29633    50361     1140     1706 
    ##      .25      .50      .75      .90      .95 
    ##     3015     5136     9058    17585    31034 
    ## 
    ## lowest :     154     249     267     274     278
    ## highest: 1820127 1857670 1911767 1926017 1932274
    ## --------------------------------------------------------------------------------
    ## homicides 
    ##        n  missing distinct     Info     Mean      Gmd      .05      .10 
    ##     2795       34      521        1    398.4    682.4     13.0     17.0 
    ##      .25      .50      .75      .90      .95 
    ##     32.0     64.0    131.0    312.0    563.1 
    ## 
    ## lowest :     1     2     3     4     5, highest: 23326 23438 23760 24526 24703
    ## --------------------------------------------------------------------------------
    ## rapes 
    ##        n  missing distinct     Info     Mean      Gmd      .05      .10 
    ##     2754       75      878        1    416.3    378.5     77.0    103.0 
    ##      .25      .50      .75      .90      .95 
    ##    176.2    291.0    465.0    749.7   1181.1 
    ## 
    ## lowest :   15   20   22   23   28, highest: 3866 3875 3880 3882 3899
    ## --------------------------------------------------------------------------------
    ## assaults 
    ##        n  missing distinct     Info     Mean      Gmd      .05      .10 
    ##     2753       76     2280        1     4405     4731    477.4    816.4 
    ##      .25      .50      .75      .90      .95 
    ##   1467.0   2597.0   4556.0   7862.4  12068.2 
    ## 
    ## lowest :    15    42   130   132   140, highest: 64244 66832 68891 70951 71030
    ## --------------------------------------------------------------------------------
    ## robberies 
    ##        n  missing distinct     Info     Mean      Gmd      .05      .10 
    ##     2754       75     2148        1     4000     4845    451.0    570.6 
    ##      .25      .50      .75      .90      .95 
    ##   1032.0   1940.0   3609.8   7464.8  12315.5 
    ## 
    ## lowest :     83     85     89     98     99, highest:  95944  98512 100280 100550 107475
    ## --------------------------------------------------------------------------------
    ## months_reported 
    ##        n  missing distinct     Info     Mean      Gmd      .05      .10 
    ##     2692      137       12    0.058    11.87   0.2591       12       12 
    ##      .25      .50      .75      .90      .95 
    ##       12       12       12       12       12 
    ## 
    ## lowest :  0  1  3  4  5, highest:  8  9 10 11 12
    ##                                                                             
    ## Value          0     1     3     4     5     6     7     8     9    10    11
    ## Frequency     18     1     2     2     3     3     1     4     3     7     9
    ## Proportion 0.007 0.000 0.001 0.001 0.001 0.001 0.000 0.001 0.001 0.003 0.003
    ##                 
    ## Value         12
    ## Frequency   2639
    ## Proportion 0.980
    ## --------------------------------------------------------------------------------
    ## crimes_percapita 
    ##        n  missing distinct     Info     Mean      Gmd      .05      .10 
    ##     2794       35     2781        1     1093    722.8    212.7    384.0 
    ##      .25      .50      .75      .90      .95 
    ##    625.1    949.7   1409.5   1991.6   2378.4 
    ## 
    ## lowest :   16.49   26.26   49.90   58.64   61.02
    ## highest: 4041.18 4050.51 4085.36 4190.84 4352.83
    ## --------------------------------------------------------------------------------
    ## homicides_percapita 
    ##        n  missing distinct     Info     Mean      Gmd      .05      .10 
    ##     2795       34     1872        1    15.37    12.63    2.307    3.464 
    ##      .25      .50      .75      .90      .95 
    ##    6.955   11.980   20.230   31.986   40.662 
    ## 
    ## lowest :  0.21  0.57  0.61  0.62  0.65, highest: 78.55 80.35 80.60 85.83 94.74
    ## --------------------------------------------------------------------------------
    ## rapes_percapita 
    ##        n  missing distinct     Info     Mean      Gmd      .05      .10 
    ##     2754       75     2430        1    59.31    35.46    14.10    22.84 
    ##      .25      .50      .75      .90      .95 
    ##    35.77    55.90    77.80   102.13   118.40 
    ## 
    ## lowest :   1.64   2.09   2.18   2.67   2.72, highest: 181.25 184.75 185.65 187.76 199.30
    ## --------------------------------------------------------------------------------
    ## assaults_percapita 
    ##        n  missing distinct     Info     Mean      Gmd      .05      .10 
    ##     2753       76     2723        1    566.6    392.9    89.56   163.50 
    ##      .25      .50      .75      .90      .95 
    ##   319.09   487.48   728.24  1095.61  1290.01 
    ## 
    ## lowest :    1.61    4.43   13.51   17.57   21.01
    ## highest: 2231.09 2240.82 2299.90 2306.91 2368.22
    ## --------------------------------------------------------------------------------
    ## robberies_percapita 
    ##        n  missing distinct     Info     Mean      Gmd      .05      .10 
    ##     2754       75     2706        1      460    356.8    88.03   115.76 
    ##      .25      .50      .75      .90      .95 
    ##   210.24   374.40   612.00   914.22  1129.12 
    ## 
    ## lowest :   11.46   18.25   28.54   30.39   31.29
    ## highest: 2183.10 2187.70 2279.19 2303.88 2337.52
    ## --------------------------------------------------------------------------------

#### Data visualizations

1st plot displays the correlation between all four violent crimes that
police jurisdiction has reported from 1975-to 2015. The Scatterplot
illustrates the increase in rapes, assaults, and robberies.

``` r
data <- df[!is.na(df)]
pairs(~homicides+rapes+assaults+robberies, data=df,
   main="ScatterPlot Matrix")
```

![](ExploratoryAnalysis_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->
The following is a Box plot demonstration of what month the violent
reported crimes throughout the years. It shows high and low reports each
month, but December has the most.

``` r
data <- df[!is.na(df)]
boxplot(report_year~months_reported,data=df, main="Violent Crimes Committed between 1975-2015",
   xlab="Months in a year", ylab="Year reported")
```

![](ExploratoryAnalysis_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->
It is a bar graph showing each violent crime committed throughout the
year. Assault had a prominent peak between the late 1980s and 2000.

``` r
data <- df[!is.na(df)]
ggplot(data =df, aes(x=report_year, y=robberies_percapita, fill=report_year)) + geom_bar(stat = 'identity')
```

    ## Warning: Removed 75 rows containing missing values (position_stack).

![](ExploratoryAnalysis_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

``` r
ggplot(data =df, aes(x=report_year, y=assaults_percapita, fill=report_year)) + geom_bar(stat = 'identity')
```

    ## Warning: Removed 76 rows containing missing values (position_stack).

![](ExploratoryAnalysis_files/figure-gfm/unnamed-chunk-5-2.png)<!-- -->

``` r
ggplot(data =df, aes(x=report_year, y=rapes_percapita, fill=report_year)) + geom_bar(stat = 'identity')
```

    ## Warning: Removed 75 rows containing missing values (position_stack).

![](ExploratoryAnalysis_files/figure-gfm/unnamed-chunk-5-3.png)<!-- -->

``` r
ggplot(data =df, aes(x=report_year, y=homicides_percapita, fill=report_year)) + geom_bar(stat = 'identity')
```

    ## Warning: Removed 34 rows containing missing values (position_stack).

![](ExploratoryAnalysis_files/figure-gfm/unnamed-chunk-5-4.png)<!-- -->
#### Statistical test

The statistical test demonstrates a split within the data set. Next, the
data is trained and tested to see the residuals and coefficients between
all four violent crimes, followed by a linear regression matrix model.

``` r
sample_size <- floor(0.8*nrow(df))
sample_size
```

    ## [1] 2263

``` r
dt <- sample(seq_len(nrow(df)), size= sample_size)
train<-df[dt,]
test<-df[-dt,]
head(train)
```

    ##      report_year agency_code agency_jurisdiction population violent_crimes
    ## 1059        1990     INIPD00    Indianapolis, IN     483549           6224
    ## 2157        2006     TX07102         El Paso, TX     615553           2422
    ## 2645        2013     TXHPD00         Houston, TX    2180606          20993
    ## 105         1976     WIMPD00       Milwaukee, WI     652517           2692
    ## 1767        2000     NY03030   New York City, NY    8008278          75692
    ## 300         1979     INIPD00    Indianapolis, IN     513877           4178
    ##      homicides rapes assaults robberies months_reported crimes_percapita
    ## 1059        58   541     3983      1642              12          1287.15
    ## 2157        13   300     1606       503              12           393.47
    ## 2645       214   618    10270      9891              12           962.71
    ## 105         57   168      846      1621              12           412.56
    ## 1767       673  1630    40831     32558              12           945.17
    ## 300         92   439     1594      2053              12           813.04
    ##      homicides_percapita rapes_percapita assaults_percapita robberies_percapita
    ## 1059               11.99          111.88             823.70              339.57
    ## 2157                2.11           48.74             260.90               81.72
    ## 2645                9.81           28.34             470.97              453.59
    ## 105                 8.74           25.75             129.65              248.42
    ## 1767                8.40           20.35             509.86              406.55
    ## 300                17.90           85.43             310.19              399.51

``` r
model <- lm(report_year~robberies_percapita+assaults_percapita+rapes_percapita+homicides_percapita, data = df)
model
```

    ## 
    ## Call:
    ## lm(formula = report_year ~ robberies_percapita + assaults_percapita + 
    ##     rapes_percapita + homicides_percapita, data = df)
    ## 
    ## Coefficients:
    ##         (Intercept)  robberies_percapita   assaults_percapita  
    ##           2.000e+03           -9.760e-03            1.057e-02  
    ##     rapes_percapita  homicides_percapita  
    ##          -1.088e-01           -2.298e-03

``` r
summary(model)
```

    ## 
    ## Call:
    ## lm(formula = report_year ~ robberies_percapita + assaults_percapita + 
    ##     rapes_percapita + homicides_percapita, data = df)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -25.384  -8.276   0.194   8.603  30.874 
    ## 
    ## Coefficients:
    ##                       Estimate Std. Error  t value Pr(>|t|)    
    ## (Intercept)          2.000e+03  4.652e-01 4299.070   <2e-16 ***
    ## robberies_percapita -9.760e-03  1.105e-03   -8.833   <2e-16 ***
    ## assaults_percapita   1.057e-02  7.824e-04   13.507   <2e-16 ***
    ## rapes_percapita     -1.088e-01  8.117e-03  -13.407   <2e-16 ***
    ## homicides_percapita -2.298e-03  2.630e-02   -0.087     0.93    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 10.93 on 2748 degrees of freedom
    ##   (76 observations deleted due to missingness)
    ## Multiple R-squared:  0.1494, Adjusted R-squared:  0.1482 
    ## F-statistic: 120.7 on 4 and 2748 DF,  p-value: < 2.2e-16

``` r
layout(matrix(c(1,2,3,4),2,2)) 
plot(model)
```

![](ExploratoryAnalysis_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

``` r
prediction <- predict(model, newdata = test)
summary(prediction)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
    ##    1975    1992    1996    1995    1998    2005      15

``` r
install.packages('caret',repos = "http://cran.us.r-project.org")
```

    ## Installing package into 'C:/Users/Beatrisss/Documents/R/win-library/4.1'
    ## (as 'lib' is unspecified)

    ## package 'caret' successfully unpacked and MD5 sums checked

    ## Warning: cannot remove prior installation of package 'caret'

    ## Warning in file.copy(savedcopy, lib, recursive = TRUE): problem copying C:
    ## \Users\Beatrisss\Documents\R\win-library\4.1\00LOCK\caret\libs\i386\caret.dll
    ## to C:\Users\Beatrisss\Documents\R\win-library\4.1\caret\libs\i386\caret.dll:
    ## Permission denied

    ## Warning: restored 'caret'

    ## 
    ## The downloaded binary packages are in
    ##  C:\Users\Beatrisss\AppData\Local\Temp\Rtmp0eYmrC\downloaded_packages

``` r
library('caret')
```

    ## Warning: package 'caret' was built under R version 4.1.3

    ## 
    ## Attaching package: 'caret'

    ## The following object is masked from 'package:survival':
    ## 
    ##     cluster

``` r
train<-df[dt,]
test<-df[-dt,]
head(train)
```

    ##      report_year agency_code agency_jurisdiction population violent_crimes
    ## 1059        1990     INIPD00    Indianapolis, IN     483549           6224
    ## 2157        2006     TX07102         El Paso, TX     615553           2422
    ## 2645        2013     TXHPD00         Houston, TX    2180606          20993
    ## 105         1976     WIMPD00       Milwaukee, WI     652517           2692
    ## 1767        2000     NY03030   New York City, NY    8008278          75692
    ## 300         1979     INIPD00    Indianapolis, IN     513877           4178
    ##      homicides rapes assaults robberies months_reported crimes_percapita
    ## 1059        58   541     3983      1642              12          1287.15
    ## 2157        13   300     1606       503              12           393.47
    ## 2645       214   618    10270      9891              12           962.71
    ## 105         57   168      846      1621              12           412.56
    ## 1767       673  1630    40831     32558              12           945.17
    ## 300         92   439     1594      2053              12           813.04
    ##      homicides_percapita rapes_percapita assaults_percapita robberies_percapita
    ## 1059               11.99          111.88             823.70              339.57
    ## 2157                2.11           48.74             260.90               81.72
    ## 2645                9.81           28.34             470.97              453.59
    ## 105                 8.74           25.75             129.65              248.42
    ## 1767                8.40           20.35             509.86              406.55
    ## 300                17.90           85.43             310.19              399.51

``` r
train <- train[complete.cases(train),]
test <- test[complete.cases(test),]
fitControl <- trainControl(
method = "repeatedcv",
number = 5,
repeats = 2)

svmpoly <- train(report_year~robberies_percapita+assaults_percapita+rapes_percapita+homicides_percapita, data = train, method = "svmPoly", 
trControl = fitControl)

svmpoly
```

    ## Support Vector Machines with Polynomial Kernel 
    ## 
    ## 2156 samples
    ##    4 predictor
    ## 
    ## No pre-processing
    ## Resampling: Cross-Validated (5 fold, repeated 2 times) 
    ## Summary of sample sizes: 1725, 1724, 1725, 1725, 1725, 1724, ... 
    ## Resampling results across tuning parameters:
    ## 
    ##   degree  scale  C     RMSE      Rsquared   MAE     
    ##   1       0.001  0.25  11.12207  0.1048890  9.462463
    ##   1       0.001  0.50  10.96519  0.1202037  9.252980
    ##   1       0.001  1.00  10.82529  0.1360412  9.071414
    ##   1       0.010  0.25  10.70347  0.1484687  8.905343
    ##   1       0.010  0.50  10.66372  0.1532094  8.829572
    ##   1       0.010  1.00  10.67022  0.1551817  8.793280
    ##   1       0.100  0.25  10.69574  0.1559151  8.779798
    ##   1       0.100  0.50  10.70464  0.1562550  8.775564
    ##   1       0.100  1.00  10.71219  0.1563720  8.774641
    ##   2       0.001  0.25  10.96523  0.1201901  9.252866
    ##   2       0.001  0.50  10.82488  0.1360305  9.070995
    ##   2       0.001  1.00  10.72838  0.1463119  8.937517
    ##   2       0.010  0.25  10.64260  0.1565624  8.788143
    ##   2       0.010  0.50  10.61578  0.1624258  8.712977
    ##   2       0.010  1.00  10.58785  0.1686825  8.637703
    ##   2       0.100  0.25  10.46659  0.1927522  8.445348
    ##   2       0.100  0.50  10.47708  0.1939435  8.447703
    ##   2       0.100  1.00  10.48941  0.1945925  8.454572
    ##   3       0.001  0.25  10.87854  0.1294083  9.139461
    ##   3       0.001  0.50  10.76725  0.1422309  8.990234
    ##   3       0.001  1.00  10.68674  0.1503247  8.877605
    ##   3       0.010  0.25  10.59286  0.1646126  8.696073
    ##   3       0.010  0.50  10.54722  0.1733314  8.596827
    ##   3       0.010  1.00  10.50972  0.1817496  8.511038
    ##   3       0.100  0.25  10.13212  0.2396358  8.092381
    ##   3       0.100  0.50  10.09994  0.2478624  8.048540
    ##   3       0.100  1.00  10.10798  0.2511415  8.029150
    ## 
    ## RMSE was used to select the optimal model using the smallest value.
    ## The final values used for the model were degree = 3, scale = 0.1 and C = 0.5.

``` r
svmlinear <- train(report_year~robberies_percapita+assaults_percapita+rapes_percapita+homicides_percapita, data = train, 
method = "svmLinear", 
trControl = fitControl)

svmlinear
```

    ## Support Vector Machines with Linear Kernel 
    ## 
    ## 2156 samples
    ##    4 predictor
    ## 
    ## No pre-processing
    ## Resampling: Cross-Validated (5 fold, repeated 2 times) 
    ## Summary of sample sizes: 1723, 1726, 1725, 1724, 1726, 1725, ... 
    ## Resampling results:
    ## 
    ##   RMSE      Rsquared   MAE     
    ##   10.70774  0.1583605  8.766373
    ## 
    ## Tuning parameter 'C' was held constant at a value of 1

``` r
svmradial <- train(report_year~robberies_percapita+assaults_percapita+rapes_percapita+homicides_percapita, data = train, 
method = "svmRadial", 
trControl = fitControl)
svmradial
```

    ## Support Vector Machines with Radial Basis Function Kernel 
    ## 
    ## 2156 samples
    ##    4 predictor
    ## 
    ## No pre-processing
    ## Resampling: Cross-Validated (5 fold, repeated 2 times) 
    ## Summary of sample sizes: 1725, 1725, 1726, 1724, 1724, 1724, ... 
    ## Resampling results across tuning parameters:
    ## 
    ##   C     RMSE      Rsquared   MAE     
    ##   0.25  9.198947  0.3693307  7.084191
    ##   0.50  9.082850  0.3872192  6.923260
    ##   1.00  9.003609  0.3997708  6.808544
    ## 
    ## Tuning parameter 'sigma' was held constant at a value of 0.6230338
    ## RMSE was used to select the optimal model using the smallest value.
    ## The final values used for the model were sigma = 0.6230338 and C = 1.
