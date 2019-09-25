Exploring Gapminder and using `dplyr`
================
Rachel Han
20/09/2019

# Exercise 1: Basic `dplyr`

## Filter

``` r
three_countries <- filter(gapminder, country %in% c("Hong Kong, China","Canada","Korea, Rep."))

three_countries %>% datatable()
```

<!--html_preserve-->

<div id="htmlwidget-b0e604103e4bd82df77c" class="datatables html-widget" style="width:100%;height:auto;">

</div>

<script type="application/json" data-for="htmlwidget-b0e604103e4bd82df77c">{"x":{"filter":"none","data":[["1","2","3","4","5","6","7","8","9","10","11","12","13","14","15","16","17","18","19","20","21","22","23","24","25","26","27","28","29","30","31","32","33","34","35","36"],["Canada","Canada","Canada","Canada","Canada","Canada","Canada","Canada","Canada","Canada","Canada","Canada","Hong Kong, China","Hong Kong, China","Hong Kong, China","Hong Kong, China","Hong Kong, China","Hong Kong, China","Hong Kong, China","Hong Kong, China","Hong Kong, China","Hong Kong, China","Hong Kong, China","Hong Kong, China","Korea, Rep.","Korea, Rep.","Korea, Rep.","Korea, Rep.","Korea, Rep.","Korea, Rep.","Korea, Rep.","Korea, Rep.","Korea, Rep.","Korea, Rep.","Korea, Rep.","Korea, Rep."],["Americas","Americas","Americas","Americas","Americas","Americas","Americas","Americas","Americas","Americas","Americas","Americas","Asia","Asia","Asia","Asia","Asia","Asia","Asia","Asia","Asia","Asia","Asia","Asia","Asia","Asia","Asia","Asia","Asia","Asia","Asia","Asia","Asia","Asia","Asia","Asia"],[1952,1957,1962,1967,1972,1977,1982,1987,1992,1997,2002,2007,1952,1957,1962,1967,1972,1977,1982,1987,1992,1997,2002,2007,1952,1957,1962,1967,1972,1977,1982,1987,1992,1997,2002,2007],[68.75,69.96,71.3,72.13,72.88,74.21,75.76,76.86,77.95,78.61,79.77,80.653,60.96,64.75,67.65,70,72,73.6,75.45,76.2,77.601,80,81.495,82.208,47.453,52.681,55.292,57.716,62.612,64.766,67.123,69.81,72.244,74.647,77.045,78.623],[14785584,17010154,18985849,20819767,22284500,23796400,25201900,26549700,28523502,30305843,31902268,33390141,2125900,2736300,3305200,3722800,4115700,4583700,5264500,5584510,5829696,6495918,6762476,6980412,20947571,22611552,26420307,30131000,33505000,36436000,39326000,41622000,43805450,46173816,47969150,49044790],[11367.16112,12489.95006,13462.48555,16076.58803,18970.57086,22090.88306,22898.79214,26626.51503,26342.88426,28954.92589,33328.96507,36319.23501,3054.421209,3629.076457,4692.648272,6197.962814,8315.928145,11186.14125,14560.53051,20038.47269,24757.60301,28377.63219,30209.01516,39724.97867,1030.592226,1487.593537,1536.344387,2029.228142,3030.87665,4657.22102,5622.942464,8533.088805,12104.27872,15993.52796,19233.98818,23348.13973]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>country<\/th>\n      <th>continent<\/th>\n      <th>year<\/th>\n      <th>lifeExp<\/th>\n      <th>pop<\/th>\n      <th>gdpPercap<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[3,4,5,6]},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script>

<!--/html_preserve-->

## Pipe

``` r
gdp_dat <- three_countries %>% select(country, gdpPercap)
```

## Countries with a drop in life expectancy

All countries that have experienced a drop in life
expectancy.

``` r
gapminder_lifeExpChange <- gapminder %>%  group_by(country) %>% mutate(lifeExpChange = lifeExp - lag(lifeExp)) %>% drop_na()

gapminder_lifeExpChange %>% filter( lifeExpChange < 0) %>%  select(country,continent,year,lifeExp,lifeExpChange) %>%  datatable()
```

<!--html_preserve-->

<div id="htmlwidget-3bf71ee355d2d8c42e61" class="datatables html-widget" style="width:100%;height:auto;">

</div>

<script type="application/json" data-for="htmlwidget-3bf71ee355d2d8c42e61">{"x":{"filter":"none","data":[["1","2","3","4","5","6","7","8","9","10","11","12","13","14","15","16","17","18","19","20","21","22","23","24","25","26","27","28","29","30","31","32","33","34","35","36","37","38","39","40","41","42","43","44","45","46","47","48","49","50","51","52","53","54","55","56","57","58","59","60","61","62","63","64","65","66","67","68","69","70","71","72","73","74","75","76","77","78","79","80","81","82","83","84","85","86","87","88","89","90","91","92","93","94","95","96","97","98","99","100","101","102"],["Albania","Angola","Benin","Botswana","Botswana","Botswana","Bulgaria","Bulgaria","Bulgaria","Burundi","Cambodia","Cambodia","Cameroon","Cameroon","Cameroon","Central African Republic","Central African Republic","Central African Republic","Chad","Chad","China","Congo, Dem. Rep.","Congo, Dem. Rep.","Congo, Dem. Rep.","Congo, Dem. Rep.","Congo, Rep.","Congo, Rep.","Cote d'Ivoire","Cote d'Ivoire","Cote d'Ivoire","Croatia","Czech Republic","Denmark","El Salvador","El Salvador","Eritrea","Gabon","Gabon","Gabon","Ghana","Hungary","Hungary","Iraq","Iraq","Iraq","Jamaica","Jamaica","Kenya","Kenya","Kenya","Korea, Dem. Rep.","Korea, Dem. Rep.","Korea, Dem. Rep.","Lesotho","Lesotho","Lesotho","Liberia","Malawi","Malawi","Montenegro","Mozambique","Mozambique","Myanmar","Namibia","Namibia","Netherlands","Nigeria","Nigeria","Norway","Poland","Poland","Puerto Rico","Romania","Romania","Rwanda","Rwanda","Serbia","Sierra Leone","Slovak Republic","Somalia","South Africa","South Africa","South Africa","Swaziland","Swaziland","Swaziland","Tanzania","Tanzania","Togo","Trinidad and Tobago","Trinidad and Tobago","Uganda","Uganda","Uganda","Uganda","Zambia","Zambia","Zambia","Zambia","Zimbabwe","Zimbabwe","Zimbabwe"],["Europe","Africa","Africa","Africa","Africa","Africa","Europe","Europe","Europe","Africa","Asia","Asia","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Asia","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Europe","Europe","Europe","Americas","Americas","Africa","Africa","Africa","Africa","Africa","Europe","Europe","Asia","Asia","Asia","Americas","Americas","Africa","Africa","Africa","Asia","Asia","Asia","Africa","Africa","Africa","Africa","Africa","Africa","Europe","Africa","Africa","Asia","Africa","Africa","Europe","Africa","Africa","Europe","Europe","Europe","Americas","Europe","Europe","Africa","Africa","Europe","Africa","Europe","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Americas","Americas","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa"],[1992,1987,2002,1992,1997,2002,1977,1992,1997,1992,1972,1977,1992,1997,2002,1992,1997,2002,1997,2002,1962,1982,1987,1992,1997,1992,1997,1992,1997,2002,1982,1972,1982,1977,1982,1982,1997,2002,2007,2002,1982,1992,1992,1997,2002,1992,2002,1992,1997,2002,1992,1997,2002,1997,2002,2007,1992,1997,2002,2002,2002,2007,2002,1997,2002,1972,1997,2002,1987,1977,1987,1992,1987,1992,1987,1992,1982,1992,1972,1992,1997,2002,2007,1997,2002,2007,1992,1997,2002,1997,2002,1977,1982,1992,1997,1987,1992,1997,2002,1992,1997,2002],[71.581,39.906,54.406,62.745,52.556,46.634,70.81,71.19,70.32,44.736,40.317,31.22,54.314,52.199,49.856,49.396,46.066,43.308,51.573,50.525,44.50136,47.784,47.412,45.548,42.587,56.433,52.962,52.044,47.991,46.832,70.46,70.29,74.63,56.696,56.604,43.89,60.461,56.761,56.735,58.453,69.39,69.17,59.461,58.811,57.046,71.766,72.047,59.285,54.407,50.992,69.978,67.727,66.662,55.558,44.593,42.592,40.802,47.495,45.009,73.981,44.026,42.082,59.908,58.909,51.479,73.75,47.464,46.608,75.89,70.67,70.98,73.911,69.53,69.36,44.02,23.599,70.162,38.333,70.35,39.658,60.236,53.365,49.339,54.289,43.869,39.613,50.44,48.466,57.561,69.465,68.976,50.35,49.849,48.825,44.578,50.821,46.1,40.238,39.193,60.377,46.809,39.989],[-0.418999999999997,-0.0360000000000014,-0.371000000000002,-0.877000000000002,-10.189,-5.922,-0.0900000000000034,-0.150000000000006,-0.870000000000005,-3.475,-5.098,-9.097,-0.670999999999999,-2.115,-2.343,-1.089,-3.33,-2.758,-0.150999999999996,-1.048,-6.0476,-0.0200000000000031,-0.372,-1.864,-2.961,-1.037,-3.471,-2.611,-4.053,-1.159,-0.180000000000007,-0.0899999999999892,-0.0600000000000023,-1.511,-0.0919999999999987,-0.644999999999996,-0.905000000000001,-3.7,-0.0260000000000034,-0.102999999999994,-0.560000000000002,-0.409999999999997,-5.583,-0.649999999999999,-1.765,-0.00399999999999068,-0.215000000000003,-0.054000000000002,-4.878,-3.415,-0.669000000000011,-2.25099999999999,-1.065,-4.127,-10.965,-2.001,-5.225,-1.925,-2.486,-1.464,-2.318,-1.944,-0.420000000000002,-3.09,-7.43,-0.0699999999999932,-0.00800000000000267,-0.856000000000002,-0.0799999999999983,-0.179999999999993,-0.339999999999989,-0.718999999999994,-0.129999999999995,-0.170000000000002,-2.198,-20.421,-0.137999999999991,-1.673,-0.63000000000001,-4.843,-1.652,-6.871,-4.026,-4.185,-10.42,-4.256,-1.095,-1.974,-0.829000000000001,-0.396999999999991,-0.489000000000004,-0.665999999999997,-0.501000000000005,-2.684,-4.247,-1,-4.721,-5.862,-1.045,-1.974,-13.568,-6.82]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>country<\/th>\n      <th>continent<\/th>\n      <th>year<\/th>\n      <th>lifeExp<\/th>\n      <th>lifeExpChange<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[3,4,5]},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script>

<!--/html_preserve-->

## Max GDP per capita

``` r
gapminder %>% group_by(country) %>% mutate(max_gdpPercap = max(gdpPercap)) %>% filter(gdpPercap == max_gdpPercap) %>% select(country,year,max_gdpPercap) %>% datatable()
```

<!--html_preserve-->

<div id="htmlwidget-c3127f6d4e0097440f92" class="datatables html-widget" style="width:100%;height:auto;">

</div>

<script type="application/json" data-for="htmlwidget-c3127f6d4e0097440f92">{"x":{"filter":"none","data":[["1","2","3","4","5","6","7","8","9","10","11","12","13","14","15","16","17","18","19","20","21","22","23","24","25","26","27","28","29","30","31","32","33","34","35","36","37","38","39","40","41","42","43","44","45","46","47","48","49","50","51","52","53","54","55","56","57","58","59","60","61","62","63","64","65","66","67","68","69","70","71","72","73","74","75","76","77","78","79","80","81","82","83","84","85","86","87","88","89","90","91","92","93","94","95","96","97","98","99","100","101","102","103","104","105","106","107","108","109","110","111","112","113","114","115","116","117","118","119","120","121","122","123","124","125","126","127","128","129","130","131","132","133","134","135","136","137","138","139","140","141","142"],["Afghanistan","Albania","Algeria","Angola","Argentina","Australia","Austria","Bahrain","Bangladesh","Belgium","Benin","Bolivia","Bosnia and Herzegovina","Botswana","Brazil","Bulgaria","Burkina Faso","Burundi","Cambodia","Cameroon","Canada","Central African Republic","Chad","Chile","China","Colombia","Comoros","Congo, Dem. Rep.","Congo, Rep.","Costa Rica","Cote d'Ivoire","Croatia","Cuba","Czech Republic","Denmark","Djibouti","Dominican Republic","Ecuador","Egypt","El Salvador","Equatorial Guinea","Eritrea","Ethiopia","Finland","France","Gabon","Gambia","Germany","Ghana","Greece","Guatemala","Guinea","Guinea-Bissau","Haiti","Honduras","Hong Kong, China","Hungary","Iceland","India","Indonesia","Iran","Iraq","Ireland","Israel","Italy","Jamaica","Japan","Jordan","Kenya","Korea, Dem. Rep.","Korea, Rep.","Kuwait","Lebanon","Lesotho","Liberia","Libya","Madagascar","Malawi","Malaysia","Mali","Mauritania","Mauritius","Mexico","Mongolia","Montenegro","Morocco","Mozambique","Myanmar","Namibia","Nepal","Netherlands","New Zealand","Nicaragua","Niger","Nigeria","Norway","Oman","Pakistan","Panama","Paraguay","Peru","Philippines","Poland","Portugal","Puerto Rico","Reunion","Romania","Rwanda","Sao Tome and Principe","Saudi Arabia","Senegal","Serbia","Sierra Leone","Singapore","Slovak Republic","Slovenia","Somalia","South Africa","Spain","Sri Lanka","Sudan","Swaziland","Sweden","Switzerland","Syria","Taiwan","Tanzania","Thailand","Togo","Trinidad and Tobago","Tunisia","Turkey","Uganda","United Kingdom","United States","Uruguay","Venezuela","Vietnam","West Bank and Gaza","Yemen, Rep.","Zambia","Zimbabwe"],[1982,2007,2007,1967,2007,2007,2007,2007,2007,2007,2007,2007,2007,2007,2007,2007,2007,1992,2007,1987,2007,1962,2007,2007,2007,2007,1972,1957,1982,2007,1982,2007,2007,2007,2007,1972,2007,1997,2007,2007,2007,1997,2007,2007,2007,1977,1977,2007,2007,2007,2007,2002,1982,1982,2007,2007,2007,2007,2007,2007,1977,1977,2007,2007,2007,1972,2007,2007,2007,1982,2007,1957,2007,2007,1972,1977,1972,2007,2007,2007,2007,2007,2007,2007,1987,2007,2007,2007,2007,2007,2007,2007,1977,1967,2007,2007,2007,2007,2007,1982,2007,2007,2007,2007,2007,2007,2007,1982,1982,1977,2007,1987,1982,2007,2007,2007,1977,2007,2007,2007,2007,2007,2007,2007,2007,2007,2007,2007,1972,2007,2007,2007,2007,2007,2007,2007,1977,2007,1997,2007,1967,1972],[978.0114388,5937.029526,6223.367465,5522.776375,12779.37964,34435.36744,36126.4927,29796.04834,1391.253792,33692.60508,1441.284873,3822.137084,7446.298803,12569.85177,9065.800825,10680.79282,1217.032994,631.6998778,1713.778686,2602.664206,36319.23501,1193.068753,1704.063724,13171.63885,4959.114854,7006.580419,1937.577675,905.8602303,4879.507522,9645.06142,2602.710169,14619.22272,8948.102923,22833.30851,35278.41874,3694.212352,6025.374752,7429.455877,5581.180998,5728.353514,12154.08975,913.47079,690.8055759,33207.0844,30470.0167,21745.57328,884.7552507,32170.37442,1327.60891,27538.41188,5186.050003,945.5835837,838.1239671,2011.159549,3548.330846,39724.97867,18008.94444,36180.78919,2452.210407,3540.651564,11888.59508,14688.23507,40675.99635,25523.2771,28569.7197,7433.889293,31656.06806,4519.461171,1463.249282,4106.525293,23348.13973,113523.1329,10461.05868,1569.331442,803.0054535,21951.21176,1748.562982,759.3499101,12451.6558,1042.581557,1803.151496,10956.99112,11977.57496,3095.772271,11732.51017,3820.17523,823.6856205,944,4811.060429,1091.359778,36797.93332,25185.00911,5486.371089,1054.384891,2013.977305,49357.19017,22316.19287,2605.94758,9809.185636,4258.503604,7408.905561,3190.481016,15389.92468,20509.64777,19328.70901,7670.122558,10808.47561,881.5706467,1890.218117,34167.7626,1712.472136,15870.87851,1465.010784,47143.17964,18678.31435,25768.25759,1450.992513,9269.657808,28821.0637,3970.095407,2602.394995,4513.480643,33859.74835,37506.41907,4184.548089,28718.27684,1107.482182,7458.396327,1649.660188,18008.50924,7092.923025,8458.276384,1056.380121,33203.26128,42951.65309,10611.46299,13143.95095,2441.576404,7110.667619,2280.769906,1777.077318,799.3621758]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>country<\/th>\n      <th>year<\/th>\n      <th>max_gdpPercap<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[2,3]},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script>

<!--/html_preserve-->

## Canada’s life expectancy vs. GDP per capita

``` r
gapminder %>% filter(country=="Canada") %>% ggplot(aes(lifeExp,gdpPercap)) + geom_point(alpha = 0.5, color="red") + scale_y_log10("GDP per capita") + xlab("Life Expectancy") 
```

![](homework2_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

# Exercise 2: Explore inidividual variables with `dplyr`

### Quantitative variable

#### Possible values

``` r
range <-gapminder %>% select(gdpPercap) %>% range()
print(range)
```

    ## [1]    241.1659 113523.1329

``` r
mingdp <- range[1]
maxgdp <- range[2]
```

This tells us that minimum value of gdpPercap is 241.1659 and the
maximum is 113523.1329. Let’s find the corresponding
countries.

``` r
gapminder %>% select(country, year,gdpPercap) %>% filter(gdpPercap == mingdp) %>% kable()
```

| country          | year | gdpPercap |
| :--------------- | ---: | --------: |
| Congo, Dem. Rep. | 2002 |  241.1659 |

Congo is the country that recorded the minimum
gdpPercap.

``` r
gapminder %>% select(country, year,gdpPercap) %>% filter(gdpPercap == maxgdp) %>% kable()
```

| country | year | gdpPercap |
| :------ | ---: | --------: |
| Kuwait  | 1957 |  113523.1 |

Kuwait is the country that recorded the maximum gdpPercap.

#### Typical values / Spread of data / Distribution

Let’s get a statistical summary of life expectancy, populartion and gdp
per capita for
Europe:

``` r
gapminder %>%filter(continent=="Europe") %>% select(lifeExp,pop,gdpPercap) %>% summary() %>% kable()
```

|  |    lifeExp    |       pop        |    gdpPercap    |
|  | :-----------: | :--------------: | :-------------: |
|  |  Min. :43.59  |  Min. : 147962   |  Min. : 973.5   |
|  | 1st Qu.:69.57 | 1st Qu.: 4331500 | 1st Qu.: 7213.1 |
|  | Median :72.24 | Median : 8551125 | Median :12081.8 |
|  |  Mean :71.90  |  Mean :17169765  |  Mean :14469.5  |
|  | 3rd Qu.:75.45 | 3rd Qu.:21802867 | 3rd Qu.:20461.4 |
|  |  Max. :81.76  |  Max. :82400996  |  Max. :49357.2  |

The distribution of gdpPercap across all the countries in
Europe:

``` r
gapminder %>% filter(continent=="Europe") %>% ggplot(aes(country,gdpPercap, color = country)) + geom_point(alpha=0.3) + theme(axis.text.x = element_text(angle = 60, hjust = 1)) + theme(legend.position = "none")
```

![](homework2_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

The following plots the density estimates of gdp per capita for each
continent (estimates the underlying distribution of the data).

``` r
ggplot(gapminder, aes(gdpPercap, continent, color = continent)) +
  ggridges::geom_density_ridges(bins = 50)
```

    ## Picking joint bandwidth of 1650

![](homework2_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

### Categorical variable

``` r
library(datasets)
```

We will use a different data set to explore a categorical variable.
Let’s explore cut variable

``` r
diamonds <- as_tibble(diamonds)
```

#### Possible values of the variable

``` r
cut_unique <- diamonds %>% select(cut) %>% unique()
cut_unique %>% kable()
```

| cut       |
| :-------- |
| Ideal     |
| Premium   |
| Good      |
| Very Good |
| Fair      |

#### Typical values / Spread of data / Distribution

``` r
diamonds %>% count(cut) %>% kable()
```

| cut       |     n |
| :-------- | ----: |
| Fair      |  1610 |
| Good      |  4906 |
| Very Good | 12082 |
| Premium   | 13791 |
| Ideal     | 21551 |

We can plot this count data:

``` r
diamonds %>%  ggplot(aes(cut,fill = cut)) + geom_bar() 
```

![](homework2_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

We see that a ‘fair’ cut diamond is very rare, and ‘ideal’ cut is the
most common one.

## More plots

Exploring the country with biggest drop in 10 years and plot it over the
years.

``` r
gapminder %>% group_by(country) %>% arrange(year) %>% mutate(dec_gdpPercap=difference(gdpPercap,2)) %>% drop_na() %>% ungroup() %>%  group_by(continent) %>% filter(dec_gdpPercap == min(dec_gdpPercap)) %>% select(country,continent,year,gdpPercap,dec_gdpPercap) %>% arrange(dec_gdpPercap) %>% kable()
```

| country     | continent | year | gdpPercap | dec\_gdpPercap |
| :---------- | :-------- | ---: | --------: | -------------: |
| Kuwait      | Asia      | 1982 | 31354.036 |   \-77993.8313 |
| Libya       | Africa    | 1987 | 11770.590 |   \-10180.6220 |
| Serbia      | Europe    | 1997 |  7914.320 |    \-7956.5582 |
| Venezuela   | Americas  | 1987 |  9883.585 |    \-3260.3663 |
| New Zealand | Oceania   | 1992 | 18363.325 |       730.9145 |

Kuwait recorded the biggest drop of GDP in 10 years. Let’s see what
happened over the years in
Kuwait.

``` r
gapminder %>% filter(country=="Kuwait") %>% ggplot(aes(year, gdpPercap,fill=year)) + geom_col(stat="identity") + coord_flip()
```

    ## Warning: Ignoring unknown parameters: stat

![](homework2_files/figure-gfm/unnamed-chunk-20-1.png)<!-- --> There
seemed to have been a huge boom around 1960’s but in the 2000’s it
dratically decreased. Could there have been some other factors that came
into
play?

``` r
gapminder %>% filter(country=="Kuwait") %>% ggplot(aes(x = year)) + geom_point(aes(y=scale(lifeExp)), color = "red") +  geom_point(aes(y=scale(pop))) + geom_point(aes(y=scale(gdpPercap)), color="blue") 
```

![](homework2_files/figure-gfm/unnamed-chunk-21-1.png)<!-- -->

It seems as though gdp per capita has an inverse relationship with the
population and life expectancy in
Kuwait.

``` r
gapminder %>% ggplot(aes(continent,gdpPercap, color = continent)) + geom_boxplot() 
```

![](homework2_files/figure-gfm/unnamed-chunk-22-1.png)<!-- -->

We see that Asia has the most fluctuations in gdpPercap.

# Reasoning

``` r
filter(gapminder, country == c("Rwanda", "Afghanistan"))
```

    ## # A tibble: 12 x 6
    ##    country     continent  year lifeExp      pop gdpPercap
    ##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
    ##  1 Afghanistan Asia       1957    30.3  9240934      821.
    ##  2 Afghanistan Asia       1967    34.0 11537966      836.
    ##  3 Afghanistan Asia       1977    38.4 14880372      786.
    ##  4 Afghanistan Asia       1987    40.8 13867957      852.
    ##  5 Afghanistan Asia       1997    41.8 22227415      635.
    ##  6 Afghanistan Asia       2007    43.8 31889923      975.
    ##  7 Rwanda      Africa     1952    40    2534927      493.
    ##  8 Rwanda      Africa     1962    43    3051242      597.
    ##  9 Rwanda      Africa     1972    44.6  3992121      591.
    ## 10 Rwanda      Africa     1982    46.2  5507565      882.
    ## 11 Rwanda      Africa     1992    23.6  7290203      737.
    ## 12 Rwanda      Africa     2002    43.4  7852401      786.

This code runs fine but the result returned is off in the sense that it
is missing half of its entries (the entries for every five years is
missing). The correct way to do this is:

``` r
gapminder %>% filter(country %in% c("Afghanistan","Rwanda"))
```

    ## # A tibble: 24 x 6
    ##    country     continent  year lifeExp      pop gdpPercap
    ##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
    ##  1 Afghanistan Asia       1952    28.8  8425333      779.
    ##  2 Afghanistan Asia       1957    30.3  9240934      821.
    ##  3 Afghanistan Asia       1962    32.0 10267083      853.
    ##  4 Afghanistan Asia       1967    34.0 11537966      836.
    ##  5 Afghanistan Asia       1972    36.1 13079460      740.
    ##  6 Afghanistan Asia       1977    38.4 14880372      786.
    ##  7 Afghanistan Asia       1982    39.9 12881816      978.
    ##  8 Afghanistan Asia       1987    40.8 13867957      852.
    ##  9 Afghanistan Asia       1992    41.7 16317921      649.
    ## 10 Afghanistan Asia       1997    41.8 22227415      635.
    ## # … with 14 more rows

`%in` checks if an element is in the vector whereas `==` checks if it is
exactly the same as the specified value. By using `%in` in checks if
each entry is in the specified vector `c("Afghanistan","Rwanda")`. Using
`==` actually checks if each entry is equal to
`c("Afghanistan","Rwanda")` which is not what we want.
