---
type: page
title: Simulate and Test Pipeline Data Streams
listed: true
slug: simulate-pipeline-data-flows
description: 
index_title: Simulate and Test Pipeline Data Streams
hidden: 
keywords: 
tags: 
---

You can use Simulation mode to test the data stream through your Processors to your destinations with sample data before streaming live operational data. 

{% callout type="info" title="Deployed Pipelines Only" %}
You can only use Simulation mode with deployed Pipelines.
{% /callout %}

1. Select a Pipeline to simulate. 
2. In **Edit** mode, click **Simulate** for the Source you want to test. The topic [auto$](/telemetry-pipelines/view-pipeline-data) provides more information on how to use Pipeline Taps to view data, and to collect samples.
3. Choose a data sample to use, and click **Run simulation**. 
4. Click **X Close** to end the simulation.
5. Select any Source, Processor, or Destination to view egressing or ingressing data for that node. 

You can repeat these steps as necessary until you are satisfied with the data processing and routing for you Pipeline. 

## Using Downloaded and Custom Sample Data

You can use saved data from other Pipeline Sources, or custom data, in your simulation. 

1. Click the **Simulate** button for the pipeline on any source
2. Click the **Create New Sample**
3. Either paste your data or upload a formatted file
    1. Paste JSON objects or arrays with all of your events
    2. Paste NDJSON with all of your events
    3. Paste text with each line as a separate event
    4. Upload a file with the events separated by line

4. Click Add sample data if you pasted the input
5. Verify the resulting sample set in the preview
6. Name the sample if you wish or leave the default naming

Repeat as needed to add more sample sets. The limit on sample size is 1000 events or 4 MB, whichever is reached first.

## Demo Overview

{% video videoId="813305911" provider="vimeo" %}
{% /video %}