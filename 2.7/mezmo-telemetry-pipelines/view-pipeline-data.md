---
type: page
title: View and Sample Pipeline Data
listed: true
slug: view-pipeline-data
description: 
index_title: View and Sample Pipeline Data
hidden: 
keywords: 
tags: 
---

You can view the data flowing between segments of your pipeline by using a **Pipeline Tap**. A Pipeline Tap also enables you sample data from your deployed pipeline to use in simulating data flows and testing your Pipelines. 

{% callout type="info" title="Deployed Pipelines Only" %}
You can only insert a Pipeline Tap or sample pipeline data on deployed Pipelines.
{% /callout %}

## [Insert a Pipeline Tap](https://docs.mezmo.com/docs/view-and-sample-pipeline-data#insert-a-pipeline-tap)

1. Log in to [the Mezmo Web App](https://app.mezmo.com/).
2. Click **Pipelines**.
3. Select the Pipeline where you want to insert a Pipeline Tap.
4. In that Pipeline, hover on the right edge of a Source or Processor tile until it turns blue, then click to open the **Pipeline Tap** window.
5. Enter the number of log events you want to view in the Pipeline Tab, then click **Play**.

You will see the data flowing from that Source or Processor begin to stream in the Pipeline Tap window based on the number of Log Events you set.

## Sample Pipeline Data

You can sample data from the Pipeline tap to use in testing your Processors and other Pipeline components while you are developing your Pipeline.

1. Insert a Pipeline tap for the component that you want to sample data from, and use the filters to select specific events that you want to sample.
2. When you have identified the events you want to use in your sample, click **Pause**.
3. Select the events you want to include in your sample.
4. Click **Save Sample**.
5. Enter an optional name for your sample, then click **Save Sample**.

When you [edit a Pipeline](/docs/edit-a-log-data-pipeline), you can select your sample from the **Test Pipeline** options.

## [Video Overview](https://docs.mezmo.com/docs/view-and-sample-pipeline-data#video-overview)

{% video videoId="30ba3d9493264ea681b622d9369c4b7c" provider="loom" %}
{% /video %}