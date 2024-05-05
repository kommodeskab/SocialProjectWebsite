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
![Graph nodes](https://raw.githubusercontent.com/kommodeskab/SocialProject/main/images/flightmap_nodes.png)
***Top pane**: flight routes between airports. The routes have been visualized as "great circles", i.e. the shortest path when between two points on a globe. **Bottom pane**: All the different airports. The bigger the dot, the higher degree.*

Evidently, the most air traffic occurs in Europe, Eastern Asia and North America. Not surprising, in North Africa, except along the coast, almost no air traffic occurs, due to the Sahara dessert and the low population density.
![Centrality measures](https://raw.githubusercontent.com/kommodeskab/SocialProject/main/images/Centrality_measures.png)
To get a better understanding of the network some analytical methods have to be used. Firstly, we conducted different network centrality measurements such as clossness-, eigenvector-, and betweenness centrality. Then we compared it to the degree so that we achieved three scatter plots.

On the scatter plot the closeness centrality is somehow positively correlated with the degree. The closeness centrality says something about how fast information spreads in the graph and depends on how many connections the airport has. The positive correlation means that airports with more connections tend to be more central and therefore are a critical point for efficiency of transport.
The eigenvector centrality seems to be quite linear and positively correlated. However, the spread of values with the airports of high degree means that even airports with less degree can influence the network due to them being connected to other major hubs.
When it comes to the betweenness centrality, which tells if an airport lies on paths between other airports, we do not see a clear tendency. This amplifies the tendency in eigenvector centrality because nodes with a moderate degree still have importance in the connection between different parts of the network.
To combine this result we use the composite index where every centrality is weighted equally we follow the formula: 

<div>
$$
\begin{gather*}
\text{Composite centrality}=\frac{1}{3} \cdot \left( \frac{Cc(n)}{\max(CC(n) | n \in G)}  \frac{EC(n)}{\max(EC(n) | n \in G)} + \frac{BC(n)}{\max(BC(n) | n \in G)} \right) \\
CC = \text{Closeness Centrality}, \hspace{5mm} EC = \text{Eigenvector centrality}, \hspace{5mm} BC = \text{betweenness centrality}
\end{gather*}
$$
</div>
Here is a list to show the 6 most central airports:

1. Charles de Gaulle International Airport has a composite score of 0.9846
2. Frankfurt am Main Airport has a composite score of 0.9403
3. Amsterdam Airport Schiphol has a composite score of 0.8890
4. Dubai International Airport has a composite score of 0.8438
5. London Heathrow Airport has a composite score of 0.8102
6. Istanbul Airport has a composite score of 0.8013

We also want to figure out if the graphs tend to connect with other airports that are alike. To do this we use assortativity by degree with -0.0185, this means that there is very little or next to no tendency for airports to connect more with those that have less connection. For further analysis, we want to see if there is a tendency for airports in countries with high BNP to connect with similar ones. To do this we used assortativity by attribute and the result is 0.8016. A result like that means airports tend to connect with airports that are similar in BNP. Furthermore, we can try to see if our graph differs from 100 random graphs, where we used the double edge swap from the lecture. The 100 random graphs have an assortativity by degree on -0.1104. Even a little difference says something about our graph, namely that it is not a random graph.

Another interesting aspect we could look into is a country's BNP the number of connections to other countries and amount of airport connections and BNP. In image … we can see both graphs for both scenarios. As we can see, there is a positive correlation between both of the graphs. But most visible on the country connection and BNP.

![Tendency line](https://raw.githubusercontent.com/kommodeskab/SocialProject/main/images/Tendency_line.png)

The communities in a graph are also an important factor to look at. If we just look after communities we find 24. But we have decided that we would like to look at each continent, although we had to remove Antarctica duo to not having sufficient enough data. On the plot below the general information about the networks are plotted:

![Continent data](https://raw.githubusercontent.com/kommodeskab/SocialProject/main/images/Continent_data.png)

As we can see on the plots there seems to be a connection between the different centrality measurements and the BNP of the countries. So to investigate that further, we created a heatmap for this and for each airport (for those that have BNP assigned).

![Heat map](https://raw.githubusercontent.com/kommodeskab/SocialProject/main/images/Heatmaps.png)

The heat maps tell two different things. When we look at the continents BNP does show a strong correlation with the centrality measurements and the degree. On the heatmap at the right, there is no correlation at all. To return to the world map, it is now possible to plot the top 10 airports on the map:

![Airports on the map](https://raw.githubusercontent.com/kommodeskab/SocialProject/main/images/MapWithAirports.png)