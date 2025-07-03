---
type: page
title: Shared Sources
listed: true
slug: shared-sources
description: 
index_title: Shared Sources
hidden: 
keywords: 
tags: 
---

{% synced id="beta-banner" %}
{% /synced %}

## What are Shared Sources?

When you create a Pipeline and add a Source to it, that Source is exclusive to that Pipeline, and the Pipeline itself is self-contained. There are many situations in which you may want to use that same Source for multiple Pipelines, but you need to define and configure it within each Pipeline independently.  This complicates the management of that same Source for multiple Pipelines, and also contributes to increased expense for ingress and egress data volume. 

Shared Sources offers a solution to these issues. Shared Sources are configured at the global level, and can be shared across multiple Pipelines. With a Shared Source, the same data is transmitted once across all Pipelines, rather than being transmitted separately for each Pipeline.

{% callout type="info" title="Push Sources Only" %}
At this time only push sources are supported in Shared Sources.
{% /callout %}

## Configuration

1. In the Mezmo Web App, go to **Pipelines &gt; Shared Sources**. 
2. Click **New Shared Source**. 
3. Select the type of Source to use as a Shared Source, for example HTTP. 
4. Configure the Source as you normally would, then **Save** it. 

{% image url="https://uploads.developerhub.io/prod/2KW7/kx3y0kgd7y9lbzxkkgd8nzcb14duqh6q2cetltt3hdrbhcq3zlz6em4iccoi49bu.png" caption="A Shared HTTP Source, showing the Log Types detected by automated parsing. Each Log Type can be sent along an independent processing chain." mode="300" height="204" width="223" %}
{% /image %}

{% callout type="info" title="Convert a Source to a Shared Source" %}
You can convert an already configured Source to a Shared Source. Click **Edit config** for the Source you want to convert, then click Convert to Shared Source. Be sure to Deploy the Pipeline to see this update. 

You can only convert a **push** source to shared source.
{% /callout %}