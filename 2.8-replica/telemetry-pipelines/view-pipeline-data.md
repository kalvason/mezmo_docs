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


You can view the data streaming between the nodes  of your deployed Pipeline by using a **Pipeline Tap**. A Pipeline Tap also enables you sample data from your deployed pipeline to use to [auto$](/telemetry-pipelines/simulate-pipeline-data-flows).

## View Pipeline Data

{% callout type="info" title="Deployed Pipelines Only" %}
You can only open Pipeline Tap or sample Pipeline data on deployed Pipelines.
{% /callout %}

1. Log in to [the Mezmo Web App](https://app.mezmo.com/).
2. Click **Pipelines**.
3. Select the Pipeline where you want to examine the data stream.
4. In that Pipeline, click on the Source or Processor node where you want to examine the egress data.
5. Click **Tap**.

You will see the data flowing from that Source or Processor begin to stream in the Pipeline Tap window based on the number of Log Events you set.

{% callout type="info" title="Clear Previous Tap Information" %}
If you make a change to a Processor's configuration and want to view the effect with a Tap, make sure to **Clear** any previous Taps. Otherwise, the new Tap output will be added to the bottom of the previous output.
{% /callout %}

## Sample Pipeline Data

You can sample data from the Pipeline Tap to use in testing your Processors while you are developing your Pipeline.

1. Open a Pipeline Tap for the Source that you want to sample data from, and use the filters to select specific events that you want to sample.
2. Click **Save as sample**.
3. Enter a name for the sample,  then click **Save sample**. The sample will be added to the **Sample Management** inventory for the Pipeline.

[auto$](/telemetry-pipelines/simulate-pipeline-data-flows) provides more information on how to use samples for testing Pipelines in development, along with an overview video.

## Create Samples in a Pipeline

If you have a file or raw data you want to use in simulating a Pipeline, you can easily add that data to the sample sets with the **Create** option.

1. On any Pipeline Source, click the **Simulate** .
2. Click **Create New Sample.**
3. Either paste your data into the sample window, or upload a formatted file. You can  paste or upload these types of files
    1. Paste JSON objects or arrays with all of your events
    2. Paste NDJSON with all of your events
    3. Paste Text with each line as a separate event
    4. Upload a file with the events separated by line

4. Click **Add sample data** if you pasted the input.
5. Verify the resulting sample set in the preview.
6. Name the sample , or leave the default naming.

### Example Sample Sets

You can copy paste these examples for simulating and testing Pipelines.


#### JSON with an Array

{% code %}
{% tab language="json" %}
[
"190.237.106.125 - - [24/Jan/2024:16:10:31 +0000] \"GET /scripts7a8b3db5b26e04cb25eb3ea791b1d77 HTTP/1.1\" 404 8554",
"169.11.202.158 - - [24/Jan/2024:16:10:32 +0000] \"GET /assets0c298b776ddc46589743a4e31dc50a9 HTTP/2.0\" 200 8704",
"25.62.240.137 - - [24/Jan/2024:16:10:34 +0000] \"GET /static6e575b9537045bba10dd104bb0469dd HTTP/1.1\" 200 9179",
"244.200.45.38 - - [24/Jan/2024:16:10:36 +0000] \"GET / HTTP/1.1\" 404 8583",
"241.124.253.98 - - [24/Jan/2024:16:10:38 +0000] \"GET /api/customers/31220 HTTP/1.1\" 200 8867",
"80.182.201.242 - - [24/Jan/2024:16:10:40 +0000] \"GET /js15be8c06a20818bc6e193becd423264 HTTP/2.0\" 404 8919",
"72.232.11.241 - - [24/Jan/2024:16:10:42 +0000] \"POST /scripts476396d8e96e1e0b228e7b85a09c075 HTTP/1.1\" 503 10088",
"176.210.36.73 - - [24/Jan/2024:16:10:44 +0000] \"PUT /scriptseaeceaee3a3ddcb5b1b19cbb43d25ba HTTP/1.1\" 404 9141",
"127.200.157.13 - - [24/Jan/2024:16:10:46 +0000] \"GET /staticd7e58b4b3b28be999b44a39d3e03b45 HTTP/1.1\" 200 8892",
"139.171.195.242 - - [24/Jan/2024:16:10:47 +0000] \"GET /static1cc603e3e621654ee652513d3ac3a01 HTTP/1.1\" 200 9058",
"241.44.224.160 - - [24/Jan/2024:16:10:48 +0000] \"GET /favicon.ico HTTP/1.1\" 200 8255",
"86.180.122.137 - - [24/Jan/2024:16:10:49 +0000] \"PUT /api/notifications/21648 HTTP/1.1\" 403 8173"
]
{% /tab %}
{% /code %}


#### NDJSON

{% code %}
{% tab language="json" %}
"190.237.106.125 - - [24/Jan/2024:16:10:31 +0000] \"GET /scripts7a8b3db5b26e04cb25eb3ea791b1d77 HTTP/1.1\" 404 8554"
"169.11.202.158 - - [24/Jan/2024:16:10:32 +0000] \"GET /assets0c298b776ddc46589743a4e31dc50a9 HTTP/2.0\" 200 8704"
"25.62.240.137 - - [24/Jan/2024:16:10:34 +0000] \"GET /static6e575b9537045bba10dd104bb0469dd HTTP/1.1\" 200 9179"
"244.200.45.38 - - [24/Jan/2024:16:10:36 +0000] \"GET / HTTP/1.1\" 404 8583"
"241.124.253.98 - - [24/Jan/2024:16:10:38 +0000] \"GET /api/customers/31220 HTTP/1.1\" 200 8867"
"80.182.201.242 - - [24/Jan/2024:16:10:40 +0000] \"GET /js15be8c06a20818bc6e193becd423264 HTTP/2.0\" 404 8919"
"72.232.11.241 - - [24/Jan/2024:16:10:42 +0000] \"POST /scripts476396d8e96e1e0b228e7b85a09c075 HTTP/1.1\" 503 10088"
"176.210.36.73 - - [24/Jan/2024:16:10:44 +0000] \"PUT /scriptseaeceaee3a3ddcb5b1b19cbb43d25ba HTTP/1.1\" 404 9141"
"127.200.157.13 - - [24/Jan/2024:16:10:46 +0000] \"GET /staticd7e58b4b3b28be999b44a39d3e03b45 HTTP/1.1\" 200 8892"
"139.171.195.242 - - [24/Jan/2024:16:10:47 +0000] \"GET /static1cc603e3e621654ee652513d3ac3a01 HTTP/1.1\" 200 9058"
"241.44.224.160 - - [24/Jan/2024:16:10:48 +0000] \"GET /favicon.ico HTTP/1.1\" 200 8255"
"86.180.122.137 - - [24/Jan/2024:16:10:49 +0000] \"PUT /api/notifications/21648 HTTP/1.1\" 403 8173"
{% /tab %}
{% /code %}