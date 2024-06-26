---
title: Data description 📊
prev: "/"
next: network-analysis
---

# Where did we get the data?
The data was (mainly) acquired from [openflights.org](https://openflights.org/data.php), which hosts a handful of interesting datasets surrounding aerospace and transportation. Other than that, we found text reviews of airports from [Skytrax](https://skytraxratings.com/), and info about continents of countries and BNP per capita of countries from [Our World In Data](https://ourworldindata.org/). 
We used the following datasets:

* [airports.dat](https://raw.githubusercontent.com/jpatokal/openflights/master/data/airports.dat): The ID, city, country, and much more information (13 attributes) of 7698 airports all over the globe. **Source**: January 2017, DAFIF (Digital Aeronautical Flight Information File) and OurAirports
* [routes.dat](https://raw.githubusercontent.com/jpatokal/openflights/master/data/routes.dat): The source and destination, and more (9 attributes) of 67663 flights connecting between airports. **Source:** June 2014, Airline Route Mapper.
* [Airport reviews](https://github.com/quankiquanki/skytrax-reviews-dataset): 17721 text reviews of airports all over the world. Most text reviews also have a numerical rating. **Source**: github-user quankiquanki, obtained from Skytrax between 2007 and 2015.
* [BNP per capita](https://ourworldindata.org/grapher/gdp-per-capita-worldbank?time=2015): The BNP per capita of most countries in the world. Multiple years are available, we choose 2015 to overlap with the reviews. **Source**: World Bank (2023).
* [Continents](https://ourworldindata.org/world-region-map-definitions): The contient/region of every country. There are multiple ways of classifying regions of countries, we went with the more "traditional" way. **Source**: Our World In Data.

# Preprocessing
The data required for our project was available online, and we therefore did not have to do any webscraping. Still, some preprocessing was neccesary. 

For example, country names differed from dataset to dataset. **Macedonia** was sometimes named **North Macedonia**, **Swaziland** was sometimes named **Eswatini**, and **Czech Republic** was sometimes simply called **Czechia**. These disagreements mostly stems from politics and cultural controversies, which we did not dwell on for too long, since it will not affect this analysis (as long as the region is correctly choosen). Therefore, we could resolve these disagreements manually by looking up alternative names for the relative few cases.

Similarily, airport names were also different between datasets (Openflights and Skytrax). These differences was not manually solveable, since the differences consisted of, for example, **u** instead of **ü**, **-** instead of **space**, and sometimes whole words missing. We fixed this issue using the [**Levenshtein distance**](https://en.wikipedia.org/wiki/Levenshtein_distance), i.e. computing the pairwise distances between airport names that did not match, finding the minimum pairwise distance and then considering these airports as matching. The Levenshtein distance is defined as:
<div>
$$
lev(a[1..m], b[1..n]) = 
\begin{cases} 
m & \text{if } n = 0 \\
n & \text{if } m = 0 \\
lev(a[1..m-1], b[1..n-1]) & \text{if } a[m] = b[n] \\
1 + \min\begin{cases}
lev(a[1..m-1], b[1..n]) \\
lev(a[1..m], b[1..n-1]) \\
lev(a[1..m-1], b[1..n-1])
\end{cases} & \text{if } a[m] \neq b[n]
\end{cases}
$$
</div>
and it measures the number of deletions, substitutions, and insertions neccesary to go from string \(a\) to string \(b\). 

We combined the dataset over airports with the datasets over BNP, continents, and user reviews, to construct our final [airport-dataset](https://github.com/kommodeskab/SocialProject/blob/main/data/airports_cleaned.csv).

When the preprocessing was done, we were ready to construct the network. 
