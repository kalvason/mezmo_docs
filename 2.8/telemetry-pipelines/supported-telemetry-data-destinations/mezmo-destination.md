---
type: page
title: Mezmo Log Analysis
listed: true
slug: mezmo-destination
description: 
index_title: Mezmo Log Analysis
hidden: 
keywords: 
tags: 
---


## [Description](https://docs.mezmo.com/docs/mezmo-log-analysis-pipeline-destination#description)

Sending your pipeline data to Mezmo Log Analysis enables you to use features like JSON Field Search, and [Views and Alerts](/docs/view-log-data), to analyze and visualize your log data.

## [Configuration](https://docs.mezmo.com/docs/mezmo-log-analysis-pipeline-destination#configuration)

You can send data to any Log Analysis account, not just the current account. If you want to use your current account, use the Ingestion Key associated with it as described in the **Configuration Options**.

### [Configuration Options](https://docs.mezmo.com/docs/mezmo-log-analysis-pipeline-destination#configuration-options)

Check out our [Pipeline Configuration Syntax](/telemetry-pipelines/syntax-for-editing-pipeline-component-configuration-values) guide for help with Log Analysis configuration. Template configuration options can be one or more **Data References** or **Static Values**, and will result in a string value. **Data Field** configuration options point to fields and can result in objects as well as string values.

{% table widths="103,0,0" %}

{% table %}
| Option | Category | Description |  | 
| ---- | ---- | ---- | ---- | 
| Mezmo Host | Ingestion | The URI for your Mezmo Log Analysis host environment. This option is auto-configured based on your Mezmo account. | Required | 
| Ingestion Key | Ingestion | Your Mezmo ingestion key. You can find this for the current account by logging into the Mezmo Web App and navigating to **Settings &gt; Organization &gt; API Key**. | Required | 
| Hostname | Query | Template used to identify the origin of your logs. | Required | 
| Tags | Query | Array of Templates used as the `tags` in Log Analysis. Default is no `tags`. | Optional | 
| IP | Query | Template used as the `IP` value in Log Analysis. Default is no `IP` . | Optional | 
| MAC | Query | Template used as the `MAC` value in Log Analysis. Default is no `MAC` . | Optional | 
| Log construction scheme | Message | How to build the log message, either explicitly field by field or as a pass-through of the current message object. The other Message category options below only apply to the `Explicit field selection`  scheme. \n\n\n\n\nNote that if you choose `Message pass-through`  it is expected that your message object has a `line`  property.\n\n\n\n\nIn addition to `line` only `timestamp`, `app`, `level`, and `meta` will be picked up and displayed by the line viewer in Log Analysis | Required | 
| Line | Message | Template or Data Field used as the `line` in Log Analysis.\n\n\n\n\n\n\n\nIf no configuration is provided the remainder of the **`message`** will be sent as the line after removing any other fields used in other Configuration Options. | Optional | 
| Meta | Message | Data Field used as the `meta` object in Log Analysis.\n\n\n\n\n\n\n\nIf no configuration is provided the remainder of the **`message`** will be sent as the **`Meta`** after removing any other fields used in other Configuration Options. If both **`Line`** and **`Meta`** and un-configured, **`Line`** will receive all the remaining `message`  data and `Meta`  will not be sent. | Optional | 
| Timestamp | Message | Data Field used as the `timestamp` field in Log Analysis. Default value is the current time. | Optional | 
| App | Message | Template used as the `app` in Log Analysis. Default is `mezmo-pipeline`. | Optional | 
| Env | Message | Template used as the `environment` value in Log Analysis. Default is `production`. | Optional | 
| File | Message | Template used as the `file`  value in Log Analysis. Default is no `file`. | Optional | 
{% /table %}

{% /table %}