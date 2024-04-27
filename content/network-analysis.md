---
title: Network analysis 🕸️
prev: data-description
next: text-analysis
---

Using the collected data, we constructed a network of international airport connections. Each node in the graph is an airport, and each edge is a flight between the airports. The **weight** of each edge is the number of flights on that route, and the **degree** of each node is the number of connections to other airports. Each node/airport also have a set of attributes collected from the data:
1. City
2. Country
3. Latitude
4. Longitude
5. Airport name
6. Continent
7. BNP per capita

Using the latitude and longitude, we were able to visualize our graph using each nodes spatial position. Beneath, we have visualized nodes using their degree and edges using weights (separately, to make things more manageable):
![Graph edges](https://raw.githubusercontent.com/kommodeskab/SocialProject/main/images/flightmap.png)

![Graph nodes](https://raw.githubusercontent.com/kommodeskab/SocialProjectWebsite/main/images/flightmap_nodes.png)

Evidently, the most air traffic occurs in Europe, Eastern Asia and North America. Not surprising, in North Africa, except along the coast, almost no air traffic occurs, due to the Sahara dessert and the low population density.