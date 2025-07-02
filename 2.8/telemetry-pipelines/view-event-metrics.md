---
type: page
title: View Event Metrics
listed: true
slug: view-event-metrics
description: 
index_title: View Event Metrics
hidden: 
keywords: 
tags: 
---


### Event Metrics

The **Event Metrics** view for a Pipeline shows historic event volume and trends per `app`, `host`, `level` and `label` for a selected time window. This data is continuously updated based on the volume of telemetry streaming through the pipeline. There are two key components in this data:

- Line graph of log volume
- Trends such as:

    - % change (increase or decrease) of total volume in the selected time window
    - Top 5 `app`, `host`, `level` and `label` with biggest change

{% callout type="info" title="Limits on Data Data Displayed" %}
Becasue there can be unlimited number of apps or hosts, Event Metrics only collects and displays data for first 300 apps or hosts. Data is retained for 30 days, after which it is replaced by new data.
{% /callout %}

You can view the Event Metrics for a Pipeline by clicking the arrow next to the name of the Pipeline, then selecting **Event Metrics**.

{% image url="https://uploads.developerhub.io/prod/2KW7/yr1sdcnuvge1bcb7x0so2ymqw3jr41pbfcwrog8y530imzquwsb0pd2uqf6pzhpa.png" caption="The Event Metrics option for the Transactions Pipeline" mode="responsive" height="258" width="286" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/2KW7/tenysjuflznpr3lubg928yr3y715qm4ltw25qc5br8trx6oho4fnmf6jwf2a46uo.png" caption="The Event Metrics view for a Pipeline showing the Event Volume by App for the last 7 days." mode="full" height="574" width="903" %}
{% /image %}