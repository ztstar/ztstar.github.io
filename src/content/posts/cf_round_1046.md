---
title: CF Round 1046 (div1)
published: 2025-09-01
description: ''
image: ''
tags: []
category: 'ICPC'
draft: false 
lang: 'en'
---

[Problem A](https://codeforces.com/problemset/problem/2135/A)

This is an easy 1D DP problem. ~ Leetcode Difficulty. 

[Problem B](https://codeforces.com/problemset/problem/2135/B)

An interactive problem. 

No idea for it when I first see it. 

09.13: I read the tutorial of this problem. Really amazing, can't think of it on my own. 

Basically: want to get rid of the absolute value sign -- move to bottom left corner, can determine $X+Y$ (where $(X, Y)$ is the initial coordinate). To my surprise, move to the bottom right corner, can determine $X-Y$. then $X$ and $Y$ all known. 

[Problem C](https://codeforces.com/problemset/problem/2135/B)

Keyword: Graph, xor, path, counting. 

You need to discover the property of the graph to satisfy the condition. After that, it's almost template for finding Edge Biconnectted Component (边双连通分量). When I first made guesses about the property, there is a situation I overlooked. Analyzing the giving example inputs and outputs will help with it. 

Some knowledge that are similar to each other: Strongly Connected Component (SCC, 强连通分量), Edge Biconnected Component(边双连通分量), Vertex Biconnected Component(点双连通分量). In this problem we don't need to use Tarjan. We can use a difference array. Here is an OI wiki link about BCC: [link](https://oi-wiki.org/graph/bcc/).

The official solution uses Tarjan, and it looks simpler.

My submission: [link](https://codeforces.com/contest/2029/submission/290767326)

[Problem D2](https://codeforces.com/problemset/problem/2135/D2)

another interacitve problem. 

[Problem E2](https://codeforces.com/problemset/problem/2135/E2)

not sure if I'm going to do this for my current training?