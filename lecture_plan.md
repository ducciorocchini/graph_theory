# 🌿 **Lecture Plan: Ecological Graph Theory – Seeing Nature as a Network**

### 🎯 Learning Goals

By the end of this session, students should be able to:

1. Understand what an **ecological network** is.
2. Describe what **nodes** and **edges** represent in ecology.
3. Interpret a simple **food web graph**.
4. Use basic **R visualization** to see ecological connections.

---

## 🧠 1. The Big Idea

> **Everything in nature is connected.**

We can think of an ecosystem as a **network**:

* Each **species** = a **node**
* Each **interaction** (e.g., “A eats B” or “A pollinates B”) = an **edge**

This approach helps ecologists study:

* How energy flows through food webs
* Which species are most important (keystone species)
* How ecosystems might respond to disturbance or loss

🗣️ **Analogy:**
Think of a **social network** — each person is a node, and friendships are links.
If someone very connected leaves the group, the social web changes.
The same happens in ecosystems.

---

## 🐠 2. A Simple Example (Food Web)

Let’s take a tiny marine food web:

| Predator    | Prey        |
| ----------- | ----------- |
| Zooplankton | Algae       |
| Small Fish  | Zooplankton |
| Large Fish  | Small Fish  |
| Bird        | Small Fish  |
| Crab        | Algae       |

You can draw it on the board or show this conceptually:

```
Algae → Zooplankton → Small Fish → Large Fish → Bird
          ↓
         Crab
```

Now we’ll represent this in R as a **graph**.

---

## 💻 3. The R Demo (Simple & Visual)

```r
# install.packages("igraph") # run once
library(igraph)

species <- c("Algae", "Zooplankton", "Small Fish", "Large Fish", "Bird", "Crab")

interactions <- data.frame(
  predator = c("Zooplankton", "Small Fish", "Large Fish", "Bird", "Crab"),
  prey     = c("Algae", "Zooplankton", "Small Fish", "Small Fish", "Algae")
)

# Create graph
g <- graph_from_data_frame(interactions, vertices = species, directed = TRUE)

# Plot with clear labels
plot(
  g,
  layout = layout_with_fr,
  vertex.size = 30,
  vertex.color = "lightblue",
  vertex.label.color = "black",
  vertex.label.cex = 1,
  edge.arrow.size = 0.5,
  main = "A Simple Ecological Network"
)
```

🪄 **What to tell the class while showing the plot:**

* “Each circle is a species.”
* “Each arrow shows energy flow — who eats whom.”
* “This is how we can turn ecology into something computers can analyze!”

---

## 📈 4. Ask Questions That Make Them Think

Prompt some simple but deep questions:

* “What would happen if the **Small Fish** disappeared?”
* “Which species seems most connected?”
* “Can you find a species that no one eats?” (e.g., top predator)

Then show a quick calculation:

```r
degree(g, mode = "all")
```

🧩 Explain:

* A species with many links is **important** (like a “social butterfly” in an ecosystem).
* If it disappears, many others may be affected.

---

## 🌍 5. Why This Matters

* Helps us **predict extinctions** and **ecosystem collapse**.
* Identifies **keystone species** to protect.
* Supports **sustainable resource management**.

🧠 **Summary message:**

> “Graph theory gives us a map of life’s connections — and shows us what might happen when those connections break.”

---

## 🎨 6. Optional Hands-On Activity

If you have time or want student engagement:

* Give them a **list of 5–6 species** and ask them to draw arrows (“who eats whom”).
* Then show how R can represent the same thing in a few lines of code.

---

## 🧾 **Takeaway Slide**

| Concept          | Ecology Meaning                         |
| ---------------- | --------------------------------------- |
| Node             | A species                               |
| Edge             | An interaction (e.g., eats, pollinates) |
| Degree           | How connected a species is              |
| Keystone species | High-connectivity species               |
| Connectance      | How full the web is with interactions   |

---

## 🪶 Closing Thought

> “Ecology isn’t chaos — it’s a web of order.
> Graph theory helps us see that order.”


