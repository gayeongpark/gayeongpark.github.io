---
layout: post
title: Practice AI service for search
subtitle: Building AI service using embeddings (vectors) with dot product for comparing similarity
tags: [ai, node.js, MongoDB, vector, dot product, linear algebra, se40]
comments: true
author: Lantana Park
---

# Calculation similarity of each input query to search movie (dot product applied example)

It is to have a better understanding of dot product

1. Set up server and DB using Node.js(express.js) and MongoDB

   ![server](../assets/img/aiSearch/server.png)

   ![server2](../assets/img/aiSearch/Screenshot%202024-04-26%20at%2021.30.06.png)

2. Generate sample DB in MongoDB

   ![mongoDB1](../assets/img/aiSearch/Screenshot%202024-04-26%20at%2017.17.17.png)

   ![mongoDB2](../assets/img/aiSearch/Screenshot%202024-04-26%20at%2017.17.32.png)

   ![mongoDB3](../assets/img/aiSearch/Screenshot%202024-04-26%20at%2017.17.42.png)

3. Using openai, generate query embeddings(vectors)

   ![qeuryEmbedding](../assets/img/aiSearch/queryEmbedding.png)

   if I input a qeury `http://localhost:8000/search?q=dragon`

   ![resultedEmbedding1](../assets/img/aiSearch/Screenshot%202024-04-26%20at%2020.18.26.png)

   ![resultedEmbedding2](../assets/img/aiSearch/Screenshot%202024-04-26%20at%2020.18.35.png)

4. Calculate similarity using dot product(particularity calculate cosine between these ones) between the `query embeddings` and `plot_embeddings`.

5. Display most similar movie title and plot (limit 5) with the query
