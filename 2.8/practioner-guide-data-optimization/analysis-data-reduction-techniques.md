---
type: page
title: Analysis of Telemetry Data Optimization Techniques
listed: true
slug: analysis-data-reduction-techniques
description: 
index_title: Analysis of Telemetry Data Optimization Techniques
hidden: 
keywords: 
tags: 
---

**Estimated Reading Time**: 3 minutes

This topic summarizes the results of an initial round of analysis for data reduction techniques applied to sample data collected from Priority 1 sources. All sample data was generated from internal Mezmo sources, except as noted. 

## Priority 1 Telemetry Data Sources

{% table %}
| Sample | Input Size | Number of Lines | Avg Reduction | 
| ---- | ---- | ---- | ---- | 
| Palo Alto Firewall Logs | 2.8 MB | 2825 | 62% | 
| Java Logs Kafka | 452.5MB | 441969 | 61% | 
| Java Logs Kafka (OTel) | 4.4 MB | 22956 | 75% | 
| Kubernetes Logs | 1.7 MB | 14832 | 77% | 
| AWS Network Firewall | 502.9 MB | 942248 | 95% | 
| Prometheus Metrics | 3.65 MB | 4883405 | 96% | 
{% /table %}

## Overall Findings

We tested four representative log samples and one representative metric sample. Our findings are:

**Every sample could be reduced in volume by at least 50% (often more) without reducing data quality.**

Note that data quality means no substantial loss in the ability to understand the data at a higher level. For example, in combining firewall events, we can realize a substantial savings by merging multiple events into a single event where all of the unique fields are still retained. The original events could be recreated if desired from the merged event.

**Dropping redundant events results in a reasonable savings for informational logs such as weblogs. An additional enhancement of including a count of the logs dropped representing the removed lines was introduced as well to aid in visibility.**

This technique is most effective when noise reduction is needed and any additional metrics regarding the noise are largely unnecessary. This technique uses a moving window and is the easiest approach for many different log types

**Turning logs into metrics based on criteria or extracting numeric values from the event itself to make a metric is highly effective at reducing data size while still retaining trending information.**

This technique results in removal of most of the log message, meaning it can lead to permanent data loss if not tuned carefully. Because of this, this technique is best suited for messages where the value of the message content is low, such as informational or notice type messages, but insights can be drawn from looking at the log trend over time.

This technique can be taken to extremes, meaning 99% of the data can be thrown out and turned into numeric data, but it would not be likely to be desired in practice due to the loss of data fidelity.

**Grouping logs based on similar information is also highly effective at reducing total size, but has the benefit of retaining specific data fields that are valuable.**

This must be targeted based on the fields, so there is some moderate complexity in configuring the processors. 

Downstream tools must also be able to handle the higher complexity of the message structure resulting from how the logs are merged together.

**The technique of trimming excess data from the event was only applicable to Java logs in our sample set and resulted in the lowest reduction.**

This technique is typically used when payloads are very large, which was not the case in our samples. It also requires complex processor configuration, and so, while not a usual technique, can provide benefits in very specific cases. 

For metrics, aggregation of incremental values and sampling of gauge values was successful in reducing volume at the cost of granularity of the data. This technique is easy to implement and can also be easily tuned.