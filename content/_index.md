---
title: Flights connections and regional reviews of global airports ✈️
layout: single
next: data-description
---

In this project, we will be looking at international airports and how they are connected. We will model the connectivity of the airports using a directed graph, such that each node in the graph is an airport, and each edge going from node *a* to *b* is a flight flying from airport *a* to airport *b*. Therefore, the degree of each node will be the number of flight connections of the airport, and the weight of each edge is how often that flight has been flown. One interesting aspect of this graph is the fact that each node also has a set spatial coordinates, latitude and longitude, indirectly connecting airports that are close in space, in the sense that spatially close airports may not be connected by an edge but by culture, economics, regional development, and so on. 

Also, we will be looking at textual reviews of the airports aswell as numerical ratings. Using these reviews and ratings, we seek to find connections between the quality of airports and the quality of connected and spatially close airports. We have formulated our research questions as follows:

> Where are the best airports located in the world? Are these airports connected to other airports of high quality? And, when adjusted for BNP per capita, where are the best airports compared to regional development?

By "best airport", we will be looking at the following measures:
* How are people describing/talking about the airport? (sentiment score of textual reviews)
* How are people reviewing the airports? (numerical reviews)
* How well-connected are the airports?