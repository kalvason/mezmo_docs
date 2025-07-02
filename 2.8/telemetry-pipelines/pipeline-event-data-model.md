---
type: page
title: Pipeline Event Data Model
listed: true
slug: pipeline-event-data-model
description: 
index_title: Pipeline Event Data Model
hidden: 
keywords: 
tags: 
---

## Event Envelope

When data is moving from Sources through Processors to Destinations in a Pipeline, the key details of these events come through the `message` object.

While this may be all you need in your Pipeline, there is other data that may be available to you in what we refer to as the **event envelope**.

### Envelope Fields

{% table widths="111" %}
| Field | Purpose | 
| ---- | ---- | 
| `message` | The main field that carries the important data elements of an event. This field will always be present.\n\n\n\nDepending on the source, this field could be a string or an object.\n\n\n\n**Metrics: w**hile there is no prescribed schema for log events, metrics have a [prescribed data model](/telemetry-pipelines/metric-data-within-the-pipeline) you must follow. | 
| `metadata` | This field contains properties that describe the message. In most cases this data is only accessible in a Pipeline, and is not passed to the Destination.\n\n\n\nYou can move Items in this field  into `message`  with the [auto$](/telemetry-pipelines/map-fields-processor). | 
| `timestamp` | This field is a ISO8601/RFC3339 formatted timestamp. For most Sources, this will be the date and time the event was received into the Pipeline.\n\n\n\nWhen there is a standard data format (OTLP, Auto-parsed logs in known formats, etc), Mezmo will set this field to the timestamp it finds in the standard field.\n\n\nYou can override this value with the [auto$](/telemetry-pipelines/set-timestamp-processor) or the [auto$](/telemetry-pipelines/js-script-processor). | 
{% /table %}

{% code %}
{% tab language="json" title="Example Event (entire envelope)" %}
{
  "message":{
    "bytes": 22322,
    "datetime": "24/Jan/2023:18:54:09",
    "host": "127.219.215.140",
    "method": "DELETE",
    "protocol": "HTTP/1.1",
    "referer": "https://names.de/apps/deploy",
    "request": "/secret-info/open-sesame",
    "status": "300",
    "user-identifier": "meln1ks",
    "data": {
      "extra-data": "mydata"
    }
  }
  "metadata":{
    "headers":{}
    "query":{}
  }
  "timestamp":"2024-06-28T19:41:00.995+00:00"
}
{% /tab %}
{% tab language="json" title="Example Event (message only)" %}
{
  "bytes": 22322,
  "datetime": "24/Jan/2023:18:54:09",
  "host": "127.219.215.140",
  "method": "DELETE",
  "protocol": "HTTP/1.1",
  "referer": "https://names.de/apps/deploy",
  "request": "/secret-info/open-sesame",
  "status": "300",
  "user-identifier": "meln1ks",
  "data": {
  	"extra-data": "mydata"
  }
}
{% /tab %}
{% /code %}

### View Envelope Fields

You can view the contents of the envelope with the [Pipeline Tap and Simulation features. ](/telemetry-pipelines/view-pipeline-data)If it isn't displayed, make sure **Show data envelope** is set to **ON**.  

{% image url="https://uploads.developerhub.io/prod/2KW7/qhfvo6nfja6ibkhklcyawsfoi5uraz2g8wl2ipwv8ou669e0032fl86ko12dtpx3.png" caption="Data envelope display control set to **On**" mode="responsive" height="45" width="199" %}
{% /image %}

Fields in `message`, `metadata` and `timestamp` can be referenced in most processors and destinations. The message field also has a shortcut syntax of `.`

For example, to access `host` from the example above, you could reference it as `message.host` or `.host`