---
type: page
title: OpenTelemetry Traces
listed: true
slug: open-telemetry-traces-source
description: 
index_title: OpenTelemetry Traces
hidden: 
keywords: 
tags: 
---


## Description

You can send your traces to a Mezmo Pipeline via any OTLP compliant sender.

{% callout type="info" title="Use HTTP Transport for Payload" %}
Mezmo currently requires that you use the HTTP transport for your payload, not the standard gRPC transport mechanism, to send in data via OTLP.
{% /callout %}

## Configuration

The OTLP Traces source provides a unique endpoint URL that uses **Bearer Token** authentication. You can obtain the unique endpoint and Bearer Token from the Mezmo pipeline app when you create a new OTLP Traces source.

### Configuration Options

{% table widths="239,0" %}

{% table %}
| Option |  | Description | 
| ---- | ---- | ---- | 
| `url / endpoint` |  | unique URL for your OTLP source | 
| `token` |  | token used for authorization for your OTLP source | 
{% /table %}

{% /table %}

### OpenTelemetry Collector Configuration

To configure an OTel collector to export to Mezmo, you can add the following to your `exporters` section of your OTel Collector config file:

{% code %}
{% tab language="yaml" %}
exporters:
otlphttp/mezmo-traces:
endpoint: "https://pipeline.mezmo.com/v1/&lt;YOUR ROUTE ID&gt;"
headers:
Authorization: "&lt;YOUR_PIPELINE_INGEST_KEY&gt;"
{% /tab %}
{% /code %}

{% callout type="warning" title="Must Match the OpenTelemetry Traces URL" %}
The endpoint in the exporters configuration must exactly match the URL provided by the OpenTelemetry Traces. You don't need to specify the `/v1/traces` path, which will otherwise by ignored by the Source.
{% /callout %}

## Data Structure

Once trace data ingested into a Mezmo pipeline each span will be converted into a Mezmo event and the data structure will differ from the Otel structure. Look at the example below to know what to expect and how to navigate your data.

{% code %}
{% tab language="json" %}
{
"message": { // Moved from resource_spans.[].scope_spans.[].spans.[]
"name": "string",
"hostname": "string", // optional, scrapped from spans.[].attributes "host.name"
"trace_id": "HEX string", // spans.[].trace_id converted from [u8; 16] to HEX string
"trace_state": "string",
"span_id": "HEX string", // spans.[].span_id converted from [u8; 8] to HEX string,
"parent_span_id": "HEX string", // spans.[].span_id converted from [u8; 8] to HEX string,
"start_timestamp": "unix timestamp", // spans.[].start_time_unix_nano
"end_timestamp": "unix timestamp", // spans.[].end_time_unix_nano
"kind": "number",
"events": [
{
"name": "string",
"timestamp": "unix timestamp", // events.[].time_unix_nano
"attributes": {
"key": "value"
},
"dropped_attributes_count": "number",
}
],
"dropped_events_count": "number",
"links": [
{
"trace_id": "HEX string", // links.[].trace_id converted from [u8; 16] to HEX string,
"span_id": "HEX string", // links.[].span_id converted from [u8; 8] to HEX string,
"trace_state": "string",
"attributes": {
"key": "value"
},
"dropped_attributes_count": "number",
}
],
"dropped_links_count": "number"
},
"metadata": {
"level": "string", // It always equals "trace"
"span_uniq_id": "HEX string", // It is a unique id which groups traces event by a span within one otel source request
"resource": { // Moved from resource_spans.[].resource
"attributes": {
"key": "value"
},
"dropped_attributes_count": "number",
"schema_url": "string"
}
"scope": { // Moved from resource_spans.[].scope_spans.[].scope
"name": "string",
"version": "string",
"attributes": {
"key": "value"
},
"schema_url": "string"
}
"attributes": { // Moved from resource_spans.[].scope_spans.[].spans.[].attributes
"key": "value"
},
"headers": { // Moved from an otel request headers
"key": "value"
}
}
}
{% /tab %}
{% /code %}

{% callout type="warning" title="Send Otel Traces to Otel Destination" %}
In order to send Otel traces data into the Otel Destination the structure must remain unchanged, otherwise the Otel Destination will either not recognize the event as a trace or failed to handle an event.

Arbitrary fields are allowed.
{% /callout %}