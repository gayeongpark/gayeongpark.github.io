---
layout: post
title: Search recommending AI model practice
subtitle: Practice to building AI model using vector embedding, used dot product for similarity
tags: [ai, javascript, MongoDB, vector, dot product, math, Node.js]
comments: true
author: Lantana Park
---

# Calculation similarity of each input queries to search movie (dot product applied example)

1. Set up server and DB using Node.js(express.js) and MongoDB

2. Generate sample DB in MongoDB for movie

3. Using `hugging face`, generate vectors of each movie title in DB

4. Using dot product (math concept), calculate similarity(cosine between two vectors) with each DB and input string

5. Result in most similar movie (limit 5), that means find lowest cosine value between input queries and movie DB
