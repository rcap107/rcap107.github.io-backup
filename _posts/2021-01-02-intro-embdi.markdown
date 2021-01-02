---
layout: post
title:  "Introduction to EmbDI"
date:   2021-01-02 22:33:00 +0100
tag: embdi
---
# Introducing EmbDI
EmbDI is a data cleaning system written in Python that I have been working on over the course of my PhD to automate some data treatment procedures, namely Entity Resolution and Schema Matching. While the ideas behind the implementation of the code were developed together my supervisor (Paolo Papotti), and another researcher from a different institution (Saravanan Thirumuruganathan), I wrote the vast majority of the code alone. 
This, of course, means that the code was a mess, then it got a bit better as I kept on hammering on it to clean up bugs and make it available to other researchers. The code has its repository on [gitlab](https://gitlab.eurecom.fr/cappuzzo/embdi), together with a very in-depth readme and instructions on how to run it. 

The code has also been *thoroughly* tested to produce results for a paper that made it to SIGMOD 2020, which can be found [here](/assets/publications/sigmod-2020-embdi.pdf). 
(unfortunately, I didn't make it there because SIGMOD 2020 went online because of the still ongoing Coronavirus pandemic)
The slides used for the SIGMOD 2020 presentation are also available [here](https://docs.google.com/presentation/d/e/2PACX-1vRqWYodB5N6J68WxohcnmxIIWMaac98TwNsM4K8fh15u5wKNQxUtlIpIa7_nebVEeedD8ZhJXgoizPf/pub?start=true&loop=true&delayms=3000). 

The paper is of course much more detailed than I will be in this post, so if you want to know more about the design of the system, please read that. 

# How does EmbDI work, in short? 
EmbDI performs data deduplication and schema matching on csv files by converting them into a graph representation, which is then fed to a word2vec training algorithm to produce node embeddings. This is a very complicated sentence that can be reformulated as: EmbDI looks for duplicated rows and columns in dirty tables and signals them to the user, so that they can act on it. 

The search for duplicated rows and columns is done by exploiting the geometric properties of the embeddings to find those points in the vector space that are closest to each other.

![.](/assets/images/embdi_workflow.png)