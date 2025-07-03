---
type: page
title: Exclude Log Data
listed: true
slug: excluding-log-lines
description: Control what you log by setting up exclusion rules for logs that you don’t need to store
index_title: Exclude Log Data
hidden: 
keywords: 
tags: 
---

You can use Exclusion Rules to filter out log data that you don’t need to store, which can help you manage storage costs and focus your analysis on data that contains meaningful information. 

{% callout type="error" title="Excluded Data is Lost Data" %}
Log data that matches an Exclusion Rule is not saved. Be careful when setting exclusion rules that you don't create rules that are too strict, and may result in the loss of data you need.
{% /callout %}

## Feature Notes

- You can filter log data by source, app, or specific queries
- Log data that is filtered out with Exclusion Rules will not count toward your usage
- Any Admin or organization member can create exclusion rules, and can add as many as needed
- Exclusion rules will begin filtering log data within a few minutes of being saved

## Validate Exclusion Rules

To validate that your Exclusion Rule is filtering log data as expected before saving it, [create a view](/docs/create-and-edit-views) the same criteria as the rule and save it. In the view you should see the same log data that will be excluded by the rule. 

When you save the Exclusion Rule, if you **don't** select the option to **Preserve for Live-Tail and Alerts**, then you can check if the rule is applied correctly by seeing if any log data continues to appear in the view. If you do select this option, you may want to monitor the usage from the specified sources in your Usage Dashboard to make sure the rule is being applied.  

## Create an Exclusion Rule

1. Go to **Usage &gt; Exclusion Rules**.
2. Click **Add Rule**. 
3. Enter a functional title for the rule, like **Exclude daemon.log**.
4. Select any **Sources** from which you want to exclude log data. 
5. Select **Apps** from which you want to exclude log data. 
6. Enter any **Query** you want to use to exclude log data. 
7. Click **Save**.

{% callout type="info" title="Option to Preserve Data for Live-Tail and Alerting" %}
If you select this option, your log data will first come through a live tail and be processed for alerts before the exclusion rule is applied.
{% /callout %}

### Exclusion Rule Limitations

Certain fields are restricted from use within your Exclusion Rule. Utilizing any of these values in your Exclusion Rule will render the rule ineffective.

- `_retention`
- `_mezmo_line_size`