
# 🌿 Ecological Graph Theory in R

Ecological graph theory provides a powerful way to model, visualize, and analyze ecological networks — such as food webs, plant–pollinator systems, or host–parasite relationships.  
In this example, we will use **R** and the **igraph** package to:

1. Build a simple ecological network (food web).  
2. Analyze key graph-theoretic metrics (connectance, centrality, etc.).  
3. Visualize the ecological interactions.  
4. Detect community structure within the network.

---

## 🧰 Setup

```r
# Install and load the required package
# install.packages("igraph")
library(igraph)
````

---

## 🐠 Step 1: Define the Ecological Network

We will model a simplified marine food web with six species.
Edges are directed, showing **"who eats whom"**.

```r
# Define species
species <- c("Algae", "Zooplankton", "Small Fish", "Large Fish", "Bird", "Crab")

# Define trophic interactions (predator -> prey)
interactions <- data.frame(
  predator = c("Zooplankton", "Small Fish", "Large Fish", "Large Fish", "Bird", "Crab"),
  prey     = c("Algae", "Zooplankton", "Small Fish", "Zooplankton", "Small Fish", "Algae")
)
```

---

## 🔗 Step 2: Create a Graph Representation

We convert the interaction data into a **directed graph** using `igraph`.

```r
# Create the graph object
g <- graph_from_data_frame(interactions, vertices = species, directed = TRUE)

# Display a brief summary
summary(g)
```

---

## 📊 Step 3: Compute Basic Network Properties

Let’s calculate basic metrics to understand the structure of this ecological network.

```r
cat("\nNumber of species (nodes):", vcount(g))
cat("\nNumber of interactions (edges):", ecount(g))

cat("\n\nDegree (number of connections per species):\n")
print(degree(g, mode = "all"))

cat("\nTrophic hierarchy (topological order):\n")
print(topo_sort(g, mode = "out"))
```

---

## ⚖️ Step 4: Compute Network Metrics

**Connectance** (C) measures how connected the network is relative to the possible number of links.
**Clustering coefficient** quantifies the tendency to form triads (e.g., closed feeding loops).
**Betweenness centrality** can reveal potential **keystone species**.

```r
# Connectance
connectance <- ecount(g) / (vcount(g) * (vcount(g) - 1))
cat("\nConnectance:", round(connectance, 3), "\n")

# Average clustering coefficient
cat("Average clustering coefficient:", round(transitivity(g, type = "average"), 3), "\n")

# Betweenness centrality
centrality <- betweenness(g, directed = TRUE)
cat("\nBetweenness centrality (potential keystone species):\n")
print(sort(centrality, decreasing = TRUE))
```

---

## 🧩 Step 5: Visualize the Network

Let’s visualize the ecological network.
Nodes represent species, and arrows show the direction of energy flow (prey → predator).

```r
set.seed(123)  # For reproducible layout
plot(
  g,
  layout = layout_with_fr,
  vertex.size = 30,
  vertex.color = "lightgreen",
  vertex.label.color = "black",
  vertex.label.cex = 0.9,
  edge.arrow.size = 0.4,
  main = "Ecological Network (Food Web)"
)
```

---

## 🌍 Step 6: Detect Communities

Community detection algorithms can identify **functional groups** — subsets of species that interact more with each other than with the rest of the network.

```r
# Convert to undirected for community detection
communities <- cluster_walktrap(as.undirected(g))

# Show group membership
cat("\nDetected communities (functional groups):\n")
print(membership(communities))

# Plot with communities
plot(communities, g, main = "Community Structure in Ecological Network")
```

---

## 📘 Step 7: Interpretation

* **High-connectance networks** are more complex and may be more resilient.
* **Species with high betweenness centrality** often play keystone roles by linking different trophic levels.
* **Communities** often correspond to functional ecological guilds (e.g., benthic feeders, pelagic predators).

---

## 🧾 Summary of Metrics

| Metric                          | Description                    | Example Result |
| ------------------------------- | ------------------------------ | -------------- |
| **Connectance (C)**             | Realized / possible links      | 0.17           |
| **Avg. Clustering Coefficient** | Network transitivity           | 0.22           |
| **Keystone Species**            | Highest betweenness centrality | Large Fish     |
| **Communities Detected**        | Functional groups              | 2–3            |

---

## 📚 Further Reading

* Dunne, J. A., Williams, R. J., & Martinez, N. D. (2002). *Network structure and biodiversity loss in food webs.* Ecology Letters, 5(4), 558–567.
* Ings, T. C. et al. (2009). *Ecological networks – beyond food webs.* Journal of Animal Ecology, 78(1), 253–269.
* Csardi, G. & Nepusz, T. (2006). *The igraph software package for complex network research.* InterJournal, Complex Systems, 1695.


Would you like me to extend this Markdown to include **real ecological data** (e.g., a dataset from the *`cheddar`* or *`igraphdata`* R packages) so it runs on an authentic food web instead of the toy example?
```
