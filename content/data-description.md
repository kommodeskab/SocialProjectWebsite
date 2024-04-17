---
title: Data description 📊
prev: "/"
next: network-analysis
---

# Where did we get the data?
The data was acquired from [openflights.org](https://openflights.org/data.php). This website hosts a handful of aerospace related datasets. We opted for the following datasets:

* [airports.dat](https://raw.githubusercontent.com/jpatokal/openflights/master/data/airports.dat): The ID, city, country, and much more information (13 attributes) of 7698 airports all over the globe. **Source**: January 2017, DAFIF (Digital Aeronautical Flight Information File) and OurAirports
* [routes.dat](https://raw.githubusercontent.com/jpatokal/openflights/master/data/routes.dat): The source and destination, and more (9 attributes) of 67663 flights connecting between airports. **Source:** June 2014, Airline Route Mapper.
* [Airport reviews](https://github.com/quankiquanki/skytrax-reviews-dataset): 17721 text reviews of airports all over the world. Most text reviews also have a numerical rating. **Source**: github-user quankiquanki, obtained from Skytrax between 2007 and 2015. 