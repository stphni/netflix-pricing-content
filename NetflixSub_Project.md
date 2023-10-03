Netflix Subscription Analysis (Data from Dec. 2021)
================
stphni
March 2022

<style type="text/css">
body p, div, h1, h2, h3, h4, h5 {
color: black;
font-family: Modern Computer Roman;
}
slides > slide.title-slide hgroup h1 {
color: #E50914; <!--the maroon color-->
}
h2 {
color: #E50914; <!-- the maroon color-->
}
</style>

<!-- end of defining font in various parts of slides -->

## Data Selection and Purpose

- Data set from Kaggle: Netflix Subscription Fee In Different Countries
  (Dec. 2021)
- CSV file based on the data collected from
  <https://www.comparitech.com/blog/vpn-privacy/countries-netflix-cost/>
- **Purpose**: Is there a correlation between Netflix’s basic, standard
  and premium monthly cost vs the total library content (movies + TV
  shows) per region?

## Sorting Countries by Region and Filtering

For the purpose of this data analysis, a column was added to the data
set called *Continent*, in order to categorize countries by their
region.

    netflix_df$Continent = countrycode(sourcevar = netflix_df[, "Country"],
                              origin = "country.name",
                              destination = "region23")

Code used to filter and summarize by region (ex. below is Australia &
New Zealand):

    netflix_AUS = netflix_df %>%
                    group_by(Continent) %>%
                    filter(Continent == "Australia and New Zealand") %>%
                    summarise(avg_shows = round(sum(No._of_TV_Shows) / 2),
                    avg_movies = round(sum(No._of_Movies) / 2)) %>% 
                    dplyr::select(Continent, avg_shows, avg_movies)

## Bar Plot

![](NetflixSub_Project_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

## Statistics and Analysis for Bar Plot:

- <span style="color: black"><font size="5"> Highest Average \# of
  Movies: 2,125 (Southern Asia) </font></span>
- <span style="color: black"><font size="5"> Highest Average \# of TV
  Shows: 4,068 (Eastern Europe, Northern America) </font></span>
- <span style="color: black"><font size="5"> Lowest Average \# of
  Movies: 1,350 (Southern Europe) </font></span>
- <span style="color: black"><font size="5"> Lowest Average \# of TV
  Shows: 3,076 (Southern Europe) </font></span>
- <span style="color: black"><font size="5"> Highest Average Library
  Size (Movies + TV Shows): 6,098 (Australia and New Zealand)
  </font></span>
- <span style="color: black"><font size="5"> Lowest Average Library
  Size: 4,426 (Southern Europe) </font></span>

## Scatter Plot

![](NetflixSub_Project_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

## Pearson Correlation Test:

- <span style="color: black"><font size="5">t = -0.4388, df = 63,
  p-value = 0.6623</font></span>
- <span style="color: black"><font size="5">alternative hypothesis: true
  correlation is not equal to 0</font></span>
- <span style="color: black"><font size="5">95 percent confidence
  interval: -0.2951257 0.1912744</font></span>
- <span style="color: black"><font size="5">sample estimates: cor
  -0.05519988 </font></span>
- <span style="color: black"><font size="5">The correlation coefficient
  between both variables is -0.05519988, which is close to 0. A
  coefficient of 0 means there is no linear correlation, but since our
  value is not 0 then it indicates there is possibly a very weak
  correlation between cost per month (standard) vs library content.
  </font></span>
- <span style="color: #E50914"><font size="5">The corresponding p-value
  is 0.6623. Since this value is greater than .05, we have sufficient
  evidence to say that the correlation between the two variables is NOT
  statistically significant</font></span>

## Visual Analysis for Scatter Plot:

- <span style="color: black"><font size="5">Scatter plot displays
  distribution of the monthly cost for the standard Netflix plan over
  the total content size based on region </font></span>
- <span style="color: black"><font size="5">**Mode** for monthly cost of
  standard subscription: \$11.29 and \$14.67 (8 country occurrences for
  each price)</font></span>
- <span style="color: black"><font size="5">**Mean** for monthly cost of
  standard subscription: \$11.29</font></span>
- <span style="color: black"><font size="5">**Median** for monthly cost
  of standard subscription: \$11.49</font></span>
- <span style="color: black"><font size="5">Outlier 1: Turkey (Western
  Asia), Monthly Cost: \$3.00, Total Library Size: 4639</font></span>
- <span style="color: black"><font size="5">Outlier 2: Liechtenstein &
  Switzerland (Western Europe), Monthly Cost: \$20.46, Total Library
  Size : 3048 and 5506 respectively</font></span>

## Statistics and Analysis for Scatter Plot (continued):

    ##        Continent Avg_Cost Avg_Library_Size
    ## 1 Western Europe    15.98             5185

    ##        Continent Avg_Cost Avg_Library_Size
    ## 1 Eastern Europe     10.8             5937

    ## [1] -0.05519988

    ## [1] -0.06287686

    ## [1] -0.07152106

- <span style="color: #E50914"><font size="4.5">No correlation between
  paying more per month for Netflix’s standard plan and receiving more
  library content and this was concluded by using corr
  function.</font></span>

## Pie Plots

![](NetflixSub_Project_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

## Statistics and Analysis for Pie Plots:

- <span style="color: black"><font size="5">Highest standard Netflix
  subscription plans: Switzerland and Liechtenstein (\$20.46 per
  month)</font></span>
- <span style="color: black"><font size="5">Percent difference of TV
  shows & movies (Switzerland & Liechtenstein): 10.2%</font></span>
- <span style="color: black"><font size="5">Lowest standard Netflix
  subscription plan: Turkey (\$3.00 per month)</font></span>
- <span style="color: black"><font size="5">By comparing Turkey’s
  proportion of content to Switzerland and Liechtenstein, Turkey’s
  percentage of TV shows and movies lies in between the percentages of
  Switzerland and Liechtenstein</font></span>
- <span style="color: black"><font size="5">Not a significant difference
  in content proportions between the lowest standard price subscriptions
  and highest</font></span>
- <span style="color: black"><font size="5">Netflix has more TV shows
  then movies in their library</font></span>

## 3D Scatter Plot

![](NetflixSub_Project_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

## Statistics and Analysis for 3D Scatter Plot:

- <span style="color: black"><font size="5"> **Outliers were grouped in
  the following categories:**</font></span>
- <span style="color: black"><font size="5"> Good Deal: India (Basic =
  \$2.64, Premium = \$8.60, Library Size = 5,843)</font></span>
- <span style="color: black"><font size="5"> Turkey (Basic = \$1.97,
  Premium = \$4.02, Library Size = 4,639)</font></span>
- <span style="color: black"><font size="5"> Bad Deal: Liechtenstein
  (Basic = \$12.88, Premium = \$26.96, Library Size =
  3,048)</font></span>
- <span style="color: black"><font size="5"> San Marino (Basic = \$9.03,
  Premium = \$20.32, Library Size = 2,310)</font></span>
- <span style="color: black"><font size="5"> Because of the occurring
  outliers, we can conclude that there is no relationship between
  Netflix’s basic and premium monthly plan vs total library
  size.</font></span>

## Conclusion:

<span style="color: #E50914"><font size="5.1">Based on the correlation
coefficient test conducted and by looking at the mean, median, mode and
several outliers found in this data, we can conclude that there is no
correlation between Netflix’s basic, standard and premium monthly cost
vs the total library content (TV shows + movies) per region.<br />
</font></span> <span style="color: black"><font size="5.1"><br />There
could possibly be other factors that contribute to Netflix’s pricing vs
total content per region. Factors such as economic status of each
region/country, taxes, studio company negotiations, etc. would have to
be taken into consideration to see how content available by region and
pricing is affected. </font></span>
