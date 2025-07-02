---
type: page
title: Edit Parsing Operations with the Mini-Map
listed: true
slug: edit-parsing-operations-with-the-mini-map
description: 
index_title: Edit Parsing Operations with the Mini-Map
hidden: 
keywords: 
tags: 
---

When using the Custom Parsing Template or Extract Fields, it includes a mini map. The mini map shows what operators have been used and how they relate to each other.

{% image url="https://uploads.developerhub.io/prod/2KW7/dwyees3a5hldb2n3ssbjp4aymqei3wzg30zmnwgfsb5wirc30x7o9ecsim4kr3fp.png" caption="Parsing mini map example showing the relationship between nodes." mode="responsive" height="1034" width="1938" %}
{% /image %}

The mini map is made of **Rule Paths** that show the chain of operations used to parse the data. The Rule Paths are end in **Nodes** that indicate the operation performed. 

The mini map can help you navigate complicated parsing structures. Hover over each node to see the operation. To jump to the operation, click each node. 

Nodes that are side by side are considered siblings and inherit from the parent node.