---
layout: post
title:  "Introduction to EmbDI"
date:   2021-01-02 22:33:00 +0100
tag: embdi
---
# Introducing EmbDI
EmbDI is a data integration system written in Python that I have been working on over the course of my PhD to automate 
some data treatment procedures, namely Entity Resolution and Schema Matching. While the ideas behind the implementation 
of the code were developed together my supervisor (Paolo Papotti), and another researcher from a different institution 
(Saravanan Thirumuruganathan), I wrote the vast majority of the code alone. 
This, of course, means that the code was a mess, then it got a bit better as I kept on hammering on it to clean up bugs 
and make it available to other researchers. The code has its repository on 
[gitlab](https://gitlab.eurecom.fr/cappuzzo/embdi), together with a very in-depth readme and instructions on how to run it. 

The code has also been *thoroughly* tested to produce results for a paper that made it to SIGMOD 2020, which can be 
found [here](/assets/publications/sigmod-2020-embdi.pdf). 
(unfortunately, I didn't make it there because SIGMOD 2020 went online because of the still ongoing Coronavirus pandemic)
The slides used for the SIGMOD 2020 presentation are also available 
[here](https://docs.google.com/presentation/d/e/2PACX-1vRqWYodB5N6J68WxohcnmxIIWMaac98TwNsM4K8fh15u5wKNQxUtlIpIa7_nebVEeedD8ZhJXgoizPf/pub?start=true&loop=true&delayms=3000). 

The paper is of course much more detailed than I will be in this post, so if you want to know more about the design of 
the system, please go ahead and check that out.

# How does EmbDI work, in short? 
EmbDI is a Python-based data integration system that takes as input relational tables as CSV files, and returns as output
a list of matches of tuples that represent the same entity (a task I'll call Entity Resolution), or a list of matches 
between columns that represent the same attribute (Schema Matching).
![.](/assets/images/embdi_workflow.png)

The procedure followed by EmbDI is the following:

1. Take a pair of relational tables, then clean them to remove problematic strings and characters. 
2. Convert the relational tables into a graph. 
3. Traverse the graph by using random walks, then gather the random walks in a training corpus (that is, a text file that contains all the
random walks). 
4. Feed the training corpus to the word2vec embeddings training algorithm. 
5. Use the geometric properties of the embeddings to find related tuples and columns. 

This is, of course, extremely summarized. I would like to explore how EmbDI works more in depth over the course of a series
of blog posts that will go into far more detail than what I'll do here, so I'll make sure to link back to those posts once 
they're ready. 
