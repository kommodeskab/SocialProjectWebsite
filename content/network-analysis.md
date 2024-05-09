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

To investigate a network, we have to understand why we are doing it. So with the network analysis, we aim to answer the following questions:

1. Where are the best airports located in the world?
2. Are these airports connected to other airports of high quality? 
3. And, when adjusted for BNP per capita, where are the best airports compared to regional development?

The first step is to find the basic properties of our network G which is the degree. The degree describes how many connections each airport has, and is a valuable insight. Here we have the degree distribution and the log-log scale of the distribution.

![Degree](https://raw.githubusercontent.com/kommodeskab/SocialProject/main/images/degree.png)

At first, we see a skewness of the degree distribution, this indicates that there exists a lot of airports with few connections and few airports that are well-connected. This aligns well with the [spoke-hub distribution paradigm](https://en.wikipedia.org/wiki/Spoke%E2%80%93hub_distribution_paradigm) which is important in transport networks and means that some airports connect multiple airports. Furthermore, due to the graph being a real-world graph a heavy tale was expected. The log-log plot further emphasizes that our graph follows a power-law distribution and the graph also says that there are few nodes (airports) with very high connectivity. These must function as major international traveling hubs, which means that they connect many airports and have an important role as a bridge between them, as predicted by the spoke-hub distribution. This tells us about the nature of the network, now we have to look into the mean, mode, median, maximum, and minimum degree. Which showed a pretty big difference in the values of average, median, and mode degrees (see Explainer) reflecting that there is an influence of highly connected airports. Furthermore, the network shows a moderate clustering coefficient, indicating regional clustering despite the low density. This could mean that not all potential connections are utilized and that the network is sparsely connected but still regionally clustered. To finish up the initial analysis, the network is in the supercritical regime, aligning with typical behavior observed in real networks that have surpassed the critical point.

The next thing is to start answering the questions, to do this we need a measure of how good the airports are. An alternative to recommendation and review could be centrality measurements. Therefore we performed a centrality analysis on the network regarding closeness, eigenvector, and [betweenness centrality](https://en.wikipedia.org/wiki/Betweenness_centrality). What we found was the scatterplot on left:
 
![Centrality measures](https://raw.githubusercontent.com/kommodeskab/SocialProject/main/images/Centrality_measures.png)

A brief description of the values; closeness describes how fast you can come to all the other airports, and eigenvector centrality gives a measure of the influence of an airport given the neighbors. Last is the betweenness centrality, which tells how often the airports act as a bridge in the shortest path. As the graph tells us, the closeness centrality tells us that highly connected airports tend to have many connections. However, the results of the eigenvector centrality, say that even airports with less degree can influence the network. Lastly, the Betweenness score does not give us a clear tendency, which can make sense given that airports with lower degrees still can hold an important influence.

We had to come up with a way to combine these centrality measures, in such a way that each measure was weighted. What we went with was the [composite score](https://www.statisticssolutions.com/composite-scores/), with the formula:

<div>
$$
\begin{gather*}
\text{Composite centrality}=\frac{1}{3} \cdot \left( \frac{Cc(n)}{\max(CC(n) | n \in G)}  \frac{EC(n)}{\max(EC(n) | n \in G)} + \frac{BC(n)}{\max(BC(n) | n \in G)} \right) \\
CC = \text{Closeness Centrality}, \hspace{5mm} EC = \text{Eigenvector centrality}, \hspace{5mm} BC = \text{betweenness centrality}
\end{gather*}
$$
</div>

Here is a list to show the 6 most central airports:

1. Charles de Gaulle International Airport (0.98)
2. Frankfurt am Main Airport (0.94)
3. Amsterdam Airport Schiphol (0.89)
4. Dubai International Airport (0.84)
5. London Heathrow Airport (0.81)
6. Istanbul Airport (0.80)

The point of using this score is to combine the three different ways of incorporating and analyzing the different centrality aspects of the network in one score.

The first step toward an answer to the research question is now possible to answer if we see the composite score as a way to describe a “good” airport. To analyze this we looked at the assortativity for 4 different topics: Degree, country, continent, and composite score. To those, we used different formulas, one for scalar values and one for categorial values. What we found was that there is a tendency for airports within the same continent to have connections with a value of 0.80, for the country it was less dominant with a value of 0.44. The graph is therefore assortative for both of those values. For degree, it was pretty neutral with a value of -0.0185. For the composite score, there was no sign of significant assortativity, since the value is 0.12. So to research question 2, for this measurement it was not the case.

The next we did was to look at the BNP per capita. what we found here was that there was a correlation between the amount of connection that a country had summarized, with a coefficient of 0.32. For each airport, it is 0.1, which is a very low correlation value.

To look at where the best airports were we looked at the communities in the network. The first we discovered was that the network had few major communities, which tend to have one major continent to belong to. Therefore, we split the graph into all the continents and looked at where the top 100 airports of composite score belong. We found that most of them were located in and around Europe, but also  Asia and North America. Then we looked at the correlation between different values. First, there seems to be a correlation with the 100 and to degree, edges and nodes. But this is probably due to how the score is computed. What we then found was that there is a correlation between BNP per capita and the score of around 0.6. But to the score depending on centrality, we did expect that Europe would have more than the others. This answers the 3. research question.

The last thing was to include the average recommendation. We found that there is no sign of assortativity between airports in regards to the average recommendation. This means that highly popular airports do not necessarily connect more with other airports of high ratings. In general, we found that the average recommendation was negatively correlated with BNP per capita, suggesting that the economy is not everything. But this will be answered better in the next section.
