---
layout: post
title: Simple AI service for fancy search functionality
subtitle: Building AI service using embeddings (vectors) with dot product for comparing similarity between two vectors
tags: [ai, node.js, MongoDB, vector, dot product, linear algebra, se40]
comments: true
author: Lantana Park
---

# Calculation similarity of search input query vector and plot embedding vector to search similar **top 10** movie (dot product applied example)

It is to have a better understanding of dot product and its applied method.

1. Set up server and DB using Node.js(express.js) and MongoDB

   ![server](../assets/img/aiSearch/server.png)

   ![server2](../assets/img/aiSearch/Screenshot%202024-04-26%20at%2021.30.06.png)

2. Generate sample movie DB in MongoDB

   ![mongoDB1](../assets/img/aiSearch/Screenshot%202024-04-26%20at%2017.17.17.png)

   With this sample DB, I am going to use `sample_mflix.movies`

3. Using openai, generate query embeddings(vectors)

   ![queryEmbedding](../assets/img/aiSearch/queryEmbedding.png)

   if I input this query `http://localhost:8000/search?q=dragon`

   ![resultedEmbedding1](../assets/img/aiSearch/Screenshot%202024-04-26%20at%2020.18.26.png)

   ![resultedEmbedding2](../assets/img/aiSearch/Screenshot%202024-04-26%20at%2020.18.35.png)

4. Update preexisting movie DB by adding embeddings based on the plot.

   ![addRoute](../assets/img/aiSearch/addRoute.png)

   ![update](../assets/img/aiSearch/updateEmbedding.png)

5. Calculate similarity using dot product(particularity calculate cosine between these ones) and normal vectors between the `query embeddings` and `plot_embeddings`.

   In order to calculate the cosine value between two vectors. it is required to know dot product. It is to calculate the angle between two vectors and projection of one vector onto another.

   Dot product formula,

   ![dotProduct](../assets/img/aiSearch/dotProduct.jpg)

   Since we need to determine the cosine value for finding similarity and display 10 top similar movies

   ![cosine](../assets/img/aiSearch/cosine%20calculation.png)

   The cosine value (= similarity) between two vectors means these two vectors are similar

   ![similarCalculation](../assets/img/aiSearch/calculationSimilar.png)

   ![searchRoute](../assets/img/aiSearch/searchRoute.png)

6. Display most similar movie titles (top 10) with the query

   ![wholeCode](../assets/img/aiSearch/wholeCode.png)

   According to the results, I could recognize it was quite accurate.

   ![result](../assets/img/aiSearch/result.png)

GitHub repository:
