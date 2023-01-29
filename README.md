JJJ Stock Analysis
================

``` r
# import data
away = read.csv(file = "data/jjj-away.csv")
home = read.csv(file = "data/jjj-home.csv")
```

``` r
first = function(x) {
  x[[1]]
}
```

``` r
away$MP = as.numeric(sapply(strsplit(away$MP, split = ":"), first))
home$MP = as.numeric(sapply(strsplit(home$MP, split = ":"), first))
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
data = data[, c("STOCK", "MP", "WHERE")]
```

``` r
# fit poisson regression
fit = glm(STOCK ~ WHERE + MP, data = data, family = "poisson")
```

``` r
# check results
summary(fit)
```

    ## 
    ## Call:
    ## glm(formula = STOCK ~ WHERE + MP, family = "poisson", data = data)
    ## 
    ## Deviance Residuals: 
    ##      Min        1Q    Median        3Q       Max  
    ## -2.76492  -0.61543   0.04499   0.54849   2.76299  
    ## 
    ## Coefficients:
    ##             Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)  0.35978    0.62264   0.578 0.563378    
    ## WHEREhome    0.66433    0.17888   3.714 0.000204 ***
    ## MP           0.02640    0.02274   1.161 0.245697    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for poisson family taken to be 1)
    ## 
    ##     Null deviance: 60.568  on 32  degrees of freedom
    ## Residual deviance: 45.403  on 30  degrees of freedom
    ## AIC: 149.23
    ## 
    ## Number of Fisher Scoring iterations: 5

- Original data source:
  <https://docs.google.com/spreadsheets/d/1Q8mgET8hyUOtn8XSchWZL-Jip9kPrwoF8eWS_7KOwwI/>
- Reddit thread:
  <https://old.reddit.com/r/nba/comments/10ni0nv/analysis_there_is_a_0000003_chance_that_the/>
