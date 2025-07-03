---
type: page
title: Tag Cardinality Limit Processor
listed: true
slug: metrics-tag-cardinality-limit-processor
description: 
index_title: Tag Cardinality Limit Processor
hidden: 
keywords: 
tags: 
---


## Description

The Tag Cardinality Limit processor limits the number of unique tag values for a specified metric measurement within defined constraints.

## Use

Metrics often have associated tag information included along with the metric value. These tags can provide useful information for searching, defining views, and organizing metric values. However, too many unique tag values can result in poor performance and instability.

**High cardinality metrics** refers to the case where metrics have a large number of non-unique tag values. Limiting the tag cardinality ensures that metrics storage and processing systems downstream are only retaining the most significant metrics.

### Exact Matches v. Probabilistic

Mezmo will automatically handle building up a cache for your tag values as your metric events pass through this processor, based on your configuration.

**Exact match** means Mezmo will add new tag values for each tag up to a maximum number, at which point the drop action is executed. Exact match requires allocated memory space for every tag.

**Probabilistic match** means Mezmo will build a model based on the unique tag values passing through, and reject new tag values based on the model's probability of whether a tag is new and unique, or not.

Exact match works well for cases where the total number of tags is low. Probabilistic match allows for a higher total limit at the expense of potentially allowing occasional false positives to pass through.

{% callout type="info" title="Error Rate for Probabilistic Matching" %}
The calculated error rate for probabilistic matching false positives is less than 1%.
{% /callout %}

## Configuration

This processor uses the same settings across all tag values defined by the user. If different settings are needed for different tags, use multiple processors in series with one for each configuration.

The tags you specify are the only tags that are excluded. All other tags are are subject to the cardinality limits defined by the **Value Limit** in your configuration.

There are two **Drop** actions for handling the tag cardinality:

1. Drop the high cardinality tag or tags.
2. Drop the entire metric event.

{% callout type="warning" title="500 Unique Values Limit for Exact Match Option" %}
**Mezmo limits the total number of tags in the exact match option to 500 unique values**. If you need more than 500 unique tag values, you can choose a probabilistic match for up to 5000 unique values.
{% /callout %}

{% callout type="info" title="Tag List and Predictive Model Duration" %}
Mezmo automatically builds the tag list after the pipeline is deployed and retains that list for you in the case of exact match.

In the case of probabilistic match, Mezmo will build the predictive model for the tags and maintain it going forward.
{% /callout %}

{% table %}

{% table %}
| Option | Description | Example | 
| ---- | ---- | ---- | 
| Tags | The tags you want the Processor to exclude from matching | hostname | 
| Action | Either drop the tag or drop the entire metric | Drop tag | 
| Value Limit | The maximum number of unique values you want to allow through | 500 | 
| Mode | Select either the exact or probabilistic mode | Exact | 
{% /table %}

{% /table %}

## Examples

### General Tag Hygiene and Hostnames in the Metric Tags

Metrics may include the hostnames, machine IDs, or container IDs within the tags. While this is useful for debugging purposes, including an unbounded tag value set can be very problematic for downstream metrics storage solutions that aggregate across a wide set of metrics.

In this example, we will look at metric values that include the container ID as a part of the tag set. We will limit all of the tags to ensure good hygiene, though we would be most concerned about the container ID.

Once we deploy the pipeline, we will send the example values through. This begins to fill out the tag cache, and then will apply the action once the value limit is reached.

{% callout type="info" title="Using the Remove Fields Processor" %}
Note that you could entirely drop the `containerId` tag if desired using the [auto$](/telemetry-pipelines/drop-fields-processor).
{% /callout %}


#### Before

{% code %}
{% tab language="json" %}
{
"kind":"absolute",
"name":"memory_usage_k8s_compapp",
"namespace":"k8s_prod_set1",
"tags": {
"environment":"prod",
"pod":"pod01",
"source":"prometheus_collector",
"containerId": "80f1bc1e7feb"
},
"value":{
"type":"counter",
"value": 520032
}
}
{
"kind":"absolute",
"name":"memory_usage_k8s_compapp",
"namespace":"k8s_prod_set1",
"tags": {
"environment":"prod",
"pod":"pod01",
"source":"prometheus_collector"
"containerId": "acdea168264a"
},
"value":{
"type":"counter",
"value": 564321
}
}
{
"kind":"absolute",
"name":"memory_usage_k8s_compapp",
"namespace":"k8s_prod_set1",
"tags": {
"environment":"prod",
"pod":"pod01",
"source":"prometheus_collector",
"containerId": "0cbfc6c17009"
},
"value":{
"type":"counter",
"value": 547679
}
}
{% /tab %}
{% /code %}


#### Options

We're going to set the limit for all of the tags. For the purpose of this example, we will artificially limit the `containerId` to two values. The remainder of the tags will be limited, but will not be affected by their settings.

{% table %}

{% table %}
| Option | Value | 
| ---- | ---- | 
| Tag | `environment` | 
| Tag | `pod` | 
| Tag | `source` | 
| Tag | `containerId` | 
| Action | Drop tag | 
| Value limit | 2 | 
| Mode | Exact | 
{% /table %}

{% /table %}


#### After

The only change here is that the tag `containerId` has now been removed after filling the exact match requirements with the first two names.

{% code %}
{% tab language="json" %}
{
"kind":"absolute",
"name":"memory_usage_k8s_compapp",
"namespace":"k8s_prod_set1",
"tags": {
"environment":"prod",
"pod":"pod01",
"source":"prometheus_collector",
"containerId": "80f1bc1e7feb"
},
"value":{
"type":"counter",
"value": 520032
}
}
{
"kind":"absolute",
"name":"memory_usage_k8s_compapp",
"namespace":"k8s_prod_set1",
"tags": {
"environment":"prod",
"pod":"pod01",
"source":"prometheus_collector"
"containerId": "acdea168264a"
},
"value":{
"type":"counter",
"value": 564321
}
}
{
"kind":"absolute",
"name":"memory_usage_k8s_compapp",
"namespace":"k8s_prod_set1",
"tags": {
"environment":"prod",
"pod":"pod01",
"source":"prometheus_collector"
},
"value":{
"type":"counter",
"value": 547679
}
}
{% /tab %}
{% /code %}