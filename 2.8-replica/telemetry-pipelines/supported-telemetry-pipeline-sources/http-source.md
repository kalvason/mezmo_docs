---
type: page
title: HTTP
listed: true
slug: http-source
description: 
index_title: HTTP
hidden: 
keywords: 
tags: 
---


## [Description](https://docs.mezmo.com/docs/http-pipeline-source#description)

You can configure any source to send data via a RESTful POST to the Memzo Pipeline.

{% callout type="success" title="Parsing Data after Ingestion" %}
When using the HTTP source, your content must be both encoded appropriately and packaged in way that enables it to be parsed after ingestion. You must also use a [auto$](/telemetry-pipelines/parse-processor) explicitly after ingestion in order to make use of any structured data. Structured formats, such as JSON, do not require additional parsing unless you want to further parse a specific value within the JSON.
{% /callout %}

You would typically use an HTTP request as a source when the specific source type you wish to send from is not supported.  For example, you may have a not well known open source application that you wish to process. As long as you're able to use a RESTful POST transport to send the data to an endpoint, you can send the data into the pipeline.

**All data sent to an HTTP endpoint must be parsed within the pipeline to extract the fields and act on it.** Once the data is parsed, you can use it for any subsequent desired use case, such as [remove](/telemetry-pipelines/drop-fields-processor) or [encrypt](/telemetry-pipelines/encrypt-fields-processor) any sensitive data before sending them to other tools for application performance monitoring, log analysis, or security information and event monitoring.

{% callout type="info" title="Use Buffering for Log Requests" %}
If you use an individual request per log, you will quickly exceed your network capacity, so we recommend using a buffering solution.
{% /callout %}

## [Configuration](https://docs.mezmo.com/docs/http-pipeline-source#configuration)

In the HTTP source configuration, use the pipeline data endpoint and configure the appropriate content type in your request. You must ensure that the Access key is included in the header with the configuration for `Authorization: <access key>` .

### [Mezmo Configuration Options](https://docs.mezmo.com/docs/http-pipeline-source#mezmo-configuration-options)

{% table %}

{% table %}
| Setting | Description | 
| ---- | ---- | 
| **Title** | A name for your source. | 
| **Description** | A short description of the source. | 
| **Decoding Method** | The decoding method to use to convert frames to data events\n\n\n\n\n\n\n\n**Note**: We recommend using Auto for convenience and to prevent potential errors in type mismatch | 
| **Access Key Management** | 1. Click **Create new key** to generate an access key.\n2. Enter a **Title** for the key.\n3. Click **Create**.\n\n\n\n\nMake sure to copy the Access Key and note the Ingestion URL, which should resemble `https://pipeline.mezmo.com/v1/<YOUR ROUTE ID>` .\n\n\n\n\n\n\n\nYou can include your Access key in any of the following headers for authentication:\n\n\n\n\n\n\n\n1. `Authorization: <YOUR_PIPELINE_INGEST_KEY>` \n2. `apikey: <YOUR_PIPELINE_INGEST_KEY>` | 
{% /table %}

{% /table %}

### Parsing and Subsequent Processing

- Always use a [auto$](/telemetry-pipelines/parse-processor) following your HTTP source to ensure the data in your payload is in a structured format.
- You may also need to use an [auto$](/telemetry-pipelines/unroll-processor) if your events are included in an array.

### Included Metadata

Note that you must explicitly turn on the metadata in the source to capture it.

Metadata recorded by the source is split into two types: the `header`  and `query`  parameters. Each of these types can include values based on the sender. Certain fields will be included typically, such as `ip`  and `user_agent` .

{% synced id="standard-metadata" %}
{% /synced %}

## Examples

### Reference Guides

The topic [auto$](/telemetry-pipelines/set-up-and-process-http-endpoint-data) up provides a basic example of how to set up your HTTP endpoint Source and typical Processors you would use.

### Basic Example for Sending Data to an HTTP Source

Let's set up an HTTP source and use `curl` to send in a sample payload with a set of key-value pairs.

1. Create a new pipeline.
2. Add an HTTP source to the graph with `text`  decoding.
3. Save the source, then generate an API key.
4. Save the API key somewhere safe, such as a password manager
5. Copy the HTTP URL endpoint. It should follow the format `https://pipeline.mezmo.com/v1/%YOUR PIPELINE ID%`
6. Deploy the pipeline with just the HTTP source. You cand ignore the warnings for missing connections.
7. Start a [tap](/telemetry-pipelines/view-pipeline-data) on the output of the HTTP source by clicking on the right end of it and pressing the play button.
    1. Leave the tap running

8. Open a terminal on your computer
9. Enter this `curl` command,  replacing the `%PIPELINE ID%` and the `%TOKEN%` with the information from your newly created pipeline

{% code %}
{% tab language="none" %}
curl -X POST -d 'msg=Hello_world' -H 'Authorization: &lt;YOUR_PIPELINE_INGEST_KEY&gt;' -d https://pipeline.mezmo.com/v1/&lt;YOUR ROUTE ID&gt;
{% /tab %}
{% /code %}

You should see the message payload `msg=Hello_world` show in the tap view after a few seconds as plain text with no color coding.

If you want to make the message into a useful structured data object, you could also use the [auto$](/telemetry-pipelines/parse-processor) with a key-value pair parse algorithm to turn it into a JSON formatted schema.

### Source Data Example with Metadata

Here's a payload representing an example of what the inbound HTTP payload looks like when including all of the metadata from `headers` and `query` parameters.

{% code %}
{% tab language="json" %}
{
"message": {
"availability_zone": "us-east-1b",
"event": {
"dest_ip": "10.1.3.81",
"dest_port": 17778,
"event_type": "netflow",
"flow_id": 694693483348034,
"netflow": {
"age": 0,
"bytes": 44,
"end": "2023-06-13T22:31:41.163906+0000",
"max_ttl": 242,
"min_ttl": 242,
"pkts": 1,
"start": "2023-06-13T22:31:41.163906+0000"
},
"proto": "TCP",
"src_ip": "205.210.31.133",
"src_port": 50813,
"tcp": {
"syn": true,
"tcp_flags": "02"
},
"timestamp": "2023-06-13T22:32:49.446239+0000"
},
"event_timestamp": "1686695569",
"firewall_name": "AWS-Network-Firewall-Multi-AZ-firewall"
},
"metadata": {
"headers": {
"accept": "*/*",
"accept-encoding": "gzip, deflate",
"connection": "keep-alive",
"content-length": "603586",
"host": "pipeline",
"user-agent": "python-requests/2.28.2",
"x-consumer-id": "68b52623-9642-4322-9e27-8218d8c7bb37",
"x-consumer-username": "p_1f799b82-53e2-11ee-a88d-26dab184329f",
"x-credential-identifier": "7c419a2c-ccf7-480b-9a9e-3fd94e3f6b28",
"x-forwarded-for": "76.253.171.67",
"x-forwarded-host": "pipeline.mezmo.it",
"x-forwarded-path": "/v1/1f799b82-53e2-11ee-a88d-26dab184329f",
"x-forwarded-port": "443",
"x-forwarded-proto": "https",
"x-kafka-key": "76.253.171.67",
"x-pipeline-capture-metadata": "true",
"x-pipeline-source-type": "http",
"x-real-ip": "76.253.171.67"
},
"query": {
"test": "parameter"
}
}
}
{% /tab %}
{% /code %}