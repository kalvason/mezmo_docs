---
type: page
title: Create a Graph
listed: true
slug: create-a-graph
description: 
index_title: Create a Graph
hidden: 
keywords: 
tags: 
---

You can use graphs to aggregate metrics about your log data over time. In this topic, and the topics on adding plots and breakdowns, you'll learn how to create a graph of HTTP response codes, with breakdowns to show which apps are sending the response codes.

{% callout type="info" title="Adding Graphs to Existing Boards" %}
You can also add a graph to an existing board without having to create it from scratch.
{% /callout %}

## Create the Graph

1. In the Mezmo Web App, click the **Boards** icon in the left-hand menu. 
2. Click **New Board.**
3. Click **Add a Graph**. 
4. Enter `response:(>=200 <300)` into **Graph log line counts**. This will return all lines that contain a response code greater than or equal to 200 and less than 300. 
5. Click **Add Graph**. 

You should see a graph showing the count for HTTP response codes over the selected time period. Next you'll add plots to show other response codes. 

Next, you'll add plots showing other response codes, then add a breakdown to analyze which apps are creating the response codes.