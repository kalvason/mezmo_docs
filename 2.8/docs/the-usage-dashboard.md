---
type: page
title: The Enterprise Dashboard
listed: true
slug: the-usage-dashboard
description: 
index_title: The Enterprise Dashboard
hidden: 
keywords: 
tags: 
---

The Enterprise Dashboard provides an overview of how much data your organization is ingesting. It shows:

- Retention of log lines per day in a stacked graph with categories for retention periods
- Restored data per day
- Ingested data v. retained data per day
- Trends in usage for the top 50 apps, sources, and tags

## Retained Data

The **Retained Data** graph displays the volume and count of retained log lines per day for the selected time period. For each day, the graph also displays the volume and count of log lines retained for each type of retention period.

{% image url="https://uploads.developerhub.io/prod/2KW7/9fgwtmtpv0h6zo3ql1xxbsmyi9nqwph6fbgbh18n57fmoppg1kagzcousgfl86cc.png" caption="The Retained Data graph. The marker indicates the end and beginning of the billing cycle." mode="responsive" height="371" width="568" %}
{% /image %}

## Restored Data

The Restored Data graph displays the volume of data restored per day for the selected time period 

## Ingested v. Retained Data

The Ingested v. Retained Data graph displays the volume of ingested data v. retained data per day for the selected time period. 

{% image url="https://uploads.developerhub.io/prod/2KW7/kytfrv4hjttu1bsvqryn8qfu9sfbalaqr9kes65z3025dnkdj0fjqfmzfcqs7t1x.png" caption="The Ingested v. Retained Data graph. The marker indicates the end and beginning of the billing cycle." mode="responsive" height="384" width="579" %}
{% /image %}

## Stacked and Unstacked

Toggling Stacked to on, will stack the data lines on top of each other and display the sum of all visible sources. The graph will also be updated to show how each app, source, or tag compares to the total.

## Trends

The Trends graph displays the volume of data for the selected data type for the top Apps, Sources, and Tags. In the Stacked view, the graph will display the data lines on top of each other and display the sum of all visible sources. The graph will also be updated to show how each app, source, or tag compares to the total.

{% image url="https://uploads.developerhub.io/prod/2KW7/gsb650803j7wo37ivohotpvsi9xkqwsw9dovp4e912kmn9oxthnzywc0gd4mxrx9.png" caption="The Trends graph in the Stacked view." mode="responsive" height="666" width="580" %}
{% /image %}