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

   I am going to use `sample_mflix.movies`

   With this sample DB, I am going to

3. Using openai, generate query embeddings(vectors)

   ![queryEmbedding](../assets/img/aiSearch/queryEmbedding.png)

   if I input this query `http://localhost:8000/search?q=dragon`

   ![resultedEmbedding1](../assets/img/aiSearch/Screenshot%202024-04-26%20at%2020.18.26.png)

   ![resultedEmbedding2](../assets/img/aiSearch/Screenshot%202024-04-26%20at%2020.18.35.png)

4. Update pre-existed DB for adding embeddings based on the plot.

   ![addRoute](../assets/img/aiSearch/addRoute.png)

   ![update](../assets/img/aiSearch/updateEmbedding.png)

5. Calculate similarity using dot product(particularity calculate cosine between these ones) between the `query embeddings` and `plot_embeddings`.

   In order to calculate the cosine value between two vectors. I needed to know dot product. It is to calculate the angle between two vectors and projection of one vector onto another.

   Dot product formula,

   u(=vector a) X v(=vector b) = |u|(=normal vector a) x |v|(=normal vector b) X cos(theta)

   ![dotProduct](../assets/img/aiSearch/dotProduct.jpg)

   Since we need to calculate cosine to determine similarity

   cos(theta) = (u X v)/ (|u| x |v|)

   ![cosine](../assets/img/aiSearch/cosine%20calculation.png)

   The cosine value (= similarity) between two vectors means these two vectors are similar

   ![similarCalculation](../assets/img/aiSearch/calculationSimilar.png)

   ![searchRoute](../assets/img/aiSearch/searchRoute.png)

6. Display most similar movie title and plot (limit 10) with the query

   ![wholeCode](../assets/img/aiSearch/wholeCode.png)

   According to the results, I could recognize it was quite accurate.

   ![result](../assets/img/aiSearch/result.png)

GitHub repository:
