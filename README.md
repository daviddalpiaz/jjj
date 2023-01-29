JJJ Stock Analysis
================

``` r
# import data
away = read.csv(file = "data/jjj-away.csv")
home = read.csv(file = "data/jjj-home.csv")
```

``` r
# add "where" variable
home$WHERE = "home"
away$WHERE = "away"
```

``` r
# combine data
data = rbind(home, away)
```

``` r
# subset to relevant columns
data = data[, c("STOCK", "WHERE")]
```

``` r
# fit poisson regression
fit = glm(STOCK ~ WHERE, data = data, family = "poisson")
summary(fit)
```

    ## 
    ## Call:
    ## glm(formula = STOCK ~ WHERE, family = "poisson", data = data)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -3.3166  -0.5503   0.0688   0.6215   2.4694  
    ## 
    ## Coefficients:
    ##             Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)   1.0586     0.1429   7.410 1.26e-13 ***
    ## WHEREhome     0.6461     0.1782   3.625 0.000289 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for poisson family taken to be 1)
    ## 
    ##     Null deviance: 60.568  on 32  degrees of freedom
    ## Residual deviance: 46.821  on 31  degrees of freedom
    ## AIC: 148.64
    ## 
    ## Number of Fisher Scoring iterations: 5

- Original data source:
  <https://docs.google.com/spreadsheets/d/1Q8mgET8hyUOtn8XSchWZL-Jip9kPrwoF8eWS_7KOwwI/>
