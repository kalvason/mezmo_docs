---
type: page
title: Getting Started with the Mezmo Pipeline API
listed: true
slug: getting-started-with-the-mezmo-pipeline-api
description: 
index_title: Getting Started with the Mezmo Pipeline API
hidden: 
keywords: 
tags: 
---


## Create A New Pipeline

{% code %}
{% tab language="bash" title="Curl" %}
curl -X 'POST' \
'https://api.mezmo.com/v3/pipeline' \
-H 'accept: */*' \
-H 'Authorization: Token &lt;your_pipeline_service_key&gt;' \
-H 'Content-Type: application/json' \
-d '{
"title": "My API Pipeline",
"deploy_type": "saas",
"deployment_groups": [
]
}'
{% /tab %}
{% /code %}


#### Response

{% code %}
{% tab language="json" title="Curl" %}
{
"meta": {
"pk": "id",
"links": {
"self": {
"list": "/v3/pipeline",
"detail": "/v3/pipeline/{pipeline_id}"
},
"related": {
"source": {
"list": null,
"detail": "/v3/pipeline/{pipeline_id}/source/{source_id}"
},
"transform": {
"list": null,
"detail": "/v3/pipeline/{pipeline_id}/transform/{transform_id}"
},
"sink": {
"list": null,
"detail": "/v3/pipeline/{pipeline_id}/sink/{sink_id}"
}
}
},
"page": null
},
"data": {
"id": "&lt;your_pipeline_id&gt;",
"account_id": "&lt;your_account_id&gt;",
"partition_id": "gen1",
"title": "My API Pipeline",
"deploy_type": "saas",
"deployment_groups": [],
"config": {},
"created_at": "2024-10-28T20:33:56.251Z",
"updated_at": null,
"published_at": null,
"published_revision_id": null,
"origin": "ui",
"template": null
}
}
{% /tab %}
{% /code %}

This operation creates a new Mezmo Pipeline in your account. Think of this as a blank canvas. We will need to add sources, transforms, and destinations to make use of it. Take note of the "id" under "data" which will be your pipeline id. You will use this in future operations to edit and publish your pipeline.

## Add A Source

Now that you have a new pipeline created, it's time to add a Source to it, which defines where your data will be coming from into the pipeline. In this example, we will be creating an HTTP Source

{% code %}
{% tab language="bash" %}
curl -X 'POST' \
'https://api.mezmo.com/v3/pipeline/&lt;your_pipeline_id&gt;/source' \
-H 'accept: */*' \
-H 'Authorization: Token &lt;your_pipeline_service_key&gt;' \
-H 'Content-Type: application/json' \
-d '{
"type": "http",
"title": "My HTTP Source",
"description": "Data sent via agent on server",
"user_config": {
"capture_metadata": true,
"decoding": "auto"
}
}'
{% /tab %}
{% /code %}


#### Response

{% code %}
{% tab language="bash" %}
{
"meta": {
"pk": "id",
"type": "source",
"links": {
"self": {
"list": null,
"detail": "/v3/pipeline/{pipeline_id}/source/{source_id}"
},
"related": {
"pipeline": {
"list": "/v3/pipeline",
"detail": "/v3/pipeline/{pipeline_id}"
}
}
},
"page": null
},
"data": {
"durability_profile": null,
"access_keys": [],
"access_keys_user_provided": false,
"gateway_route_id": "c8b5911e-956e-11ef-a2a5-9aafefcf6cfb",
"id": "c8b5911e-956e-11ef-a2a5-9aafefcf6cfb",
"title": "My HTTP Source",
"description": "Data sent via agent on server",
"account_id": "&lt;your_account_id&gt;",
"pipeline_id": "&lt;your_pipeline_id&gt;",
"generation_id": 0,
"type": "http",
"deploy_type": "saas",
"user_config": {
"decoding": "auto",
"capture_metadata": true
},
"outputs": [
{
"id": "c8b5911e-956e-11ef-a2a5-9aafefcf6cfb",
"label": "Default"
}
]
}
}
{% /tab %}
{% /code %}

Take Note of data/id. We will be using this in later steps so that we can connect pipeline nodes together.

## Adding An Access Key

Now that we've created an HTTP Source, we need to add an access key to it so that only those authorized can send data to this endpoint. Grab the "gateway_route_id" from the response above as you'll use it in the next request.

{% code %}
{% tab language="bash" %}
curl --request POST \
--url https://api.mezmo.com/v3/pipeline/gateway-route/&lt;your_gateway_route_id&gt;/access-key \
--header 'Authorization: Token &lt;your_pipeline_service_key&gt;' \
--header 'Content-Type: application/json' \
--data '{
"type": "generated",
"title": "My Key"
}'
{% /tab %}
{% /code %}

### Response

{% code %}
{% tab language="bash" %}
{
"meta": {
"pk": "id",
"type": "access-key",
"links": {
"self": {
"list": null,
"detail": "/v3/pipeline/gateway-route/{gateway_route_id}/access-key"
},
"related": {
"gateway_route": {
"list": "/v3/pipeline/gateway-route",
"detail": "/v3/pipeline/gateway-route/{gateway_route_id}"
}
}
},
"page": null
},
"data": {
"key": "&lt;your_access_key&gt;",
"id": "e6a18050-9570-11ef-aabe-9aafefcf6cfb",
"account_id": "&lt;your_account_id&gt;",
"title": "My Key",
"gateway_route_id": "&lt;your_gateway_route_id&gt;",
"created_at": "2024-10-28T21:09:20.998Z"
}
}
{% /tab %}
{% /code %}

Success! Your access key has been generated under data/key and you can use this to start ingesting data! But first, let's add a transform to the pipeline to do something with the data coming in.

## Adding a Transform

For this example, we're going to add a Remove Fields transform that will remove a set of fields from each payload that is ingested into the pipeline. Note: We also need to add the ID of the source transform above into the "inputs" field to connect these two nodes. This means that immediately after ingesting through your HTTP source, it will start removing fields. Without this, the nodes will be disconnected.

{% code %}
{% tab language="bash" %}
curl --request POST \
--url https://api.mezmo.com/v3/pipeline/&lt;your_pipeline_id&gt;/transform \
--header 'Authorization: Token &lt;your_pipeline_service_key&gt;' \
--header 'Content-Type: application/json' \
--header 'User-Agent: insomnia/10.1.1' \
--data '{
"type": "drop-fields",
"title": "Remove my metadata",
"description": "Remove Field",
"user_config": {
"fields": [".my_meta"]
},
"inputs": [
"9c82e974-956f-11ef-bd42-9aafefcf6cfb"
]
}'
{% /tab %}
{% /code %}

### Response

{% code %}
{% tab language="bash" %}
{
"meta": {
"pk": "id",
"type": "transform",
"links": {
"self": {
"list": null,
"detail": "/v3/pipeline/{pipeline_id}/transform/{transform_id}"
},
"related": {
"pipeline": {
"list": "/v3/pipeline",
"detail": "/v3/pipeline/{pipeline_id}"
}
}
},
"page": null
},
"data": {
"id": "01ee81fe-95fe-11ef-8c9b-9aafefcf6cfb",
"title": "Remove my metadata",
"description": "Remove Field",
"account_id": "&lt;your_account_id&gt;",
"pipeline_id": "&lt;your_pipeline_id&gt;",
"generation_id": 0,
"type": "drop-fields",
"deploy_type": "saas",
"user_config": {
"fields": [
".my_meta"
]
},
"inputs": [
"9c82e974-956f-11ef-bd42-9aafefcf6cfb"
],
"outputs": [
{
"id": "01ee81fe-95fe-11ef-8c9b-9aafefcf6cfb",
"label": "Default"
}
]
}
}
{% /tab %}
{% /code %}

Great! Now we have a new transform created that is connected to our HTTP Source node. Next, let's send this data somewhere, like AWS. Take note of data/id in the response. We will be using this in the next step to connect this transform node to the destination of our choosing.

## Creating a Destination

Great! Now let's create a place for this data to go to. In this example, we've chosen to configure an S3 Destination.

{% code %}
{% tab language="bash" %}
curl --request POST \
--url https://api.mezmo.com/v3/&lt;your_pipeline_id&gt;/sink \
--header 'Authorization: Token &lt;your_pipeline_service_key&gt;' \
--header 'Content-Type: application/json' \
--header 'User-Agent: insomnia/10.1.1' \
--data '{
"type": "s3",
"user_config": {
"batch_timeout_secs": 300,
"ack_enabled": true,
"auth": {
"access_key_id": "123456",
"secret_access_key": "7891011"
},
"bucket": "my-s3",
"prefix": "/mezmo",
"encoding": "text",
"compression": "none",
"region": "us-east-1",
"file_consolidation": {
"enabled": false,
"process_every_seconds": 600,
"requested_size_bytes": 500000000,
"base_path": ""
}
},
"inputs": ["01ee81fe-95fe-11ef-8c9b-9aafefcf6cfb"]
}'
{% /tab %}
{% /code %}

### Response

{% code %}
{% tab language="bash" %}
{
"meta": {
"pk": "id",
"type": "sink",
"links": {
"self": {
"list": null,
"detail": "/v3/pipeline/{pipeline_id}/sink/{sink_id}"
},
"related": {
"pipeline": {
"list": "/v3/pipeline",
"detail": "/v3/pipeline/{pipeline_id}"
}
}
},
"page": null
},
"data": {
"id": "7f88617c-97b9-11ef-bdc8-9aafefcf6cfb",
"title": null,
"description": null,
"account_id": "&lt;your_account_id&gt;",
"pipeline_id": "&lt;your_pipeline_id&gt;",
"generation_id": 0,
"type": "s3",
"deploy_type": "saas",
"user_config": {
"auth": {
"access_key_id": "123456",
"secret_access_key": "7891011"
},
"bucket": "my-s3",
"prefix": "/mezmo",
"region": "us-east-1",
"encoding": "text",
"ack_enabled": true,
"compression": "none",
"batch_timeout_secs": 300,
"file_consolidation": {
"enabled": false,
"base_path": "",
"requested_size_bytes": 500000000,
"process_every_seconds": 600
}
},
"inputs": [
"01ee81fe-95fe-11ef-8c9b-9aafefcf6cfb"
]
}
}
{% /tab %}
{% /code %}

## Publishing The Pipeline!

{% code %}
{% tab language="bash" %}
curl --request POST \
--url https://api.mezmo.com/v3/pipeline/&lt;your_pipeline_id&gt;/publish \
--header 'Authorization: Token &lt;your_pipeline_service_key&gt;' \
--header 'User-Agent: insomnia/10.1.1'
{% /tab %}
{% /code %}


#### Response

{% code %}
{% tab language="bash" %}
{
"meta": {
"pk": "id",
"type": "pipeline",
"links": {
"self": {
"list": null,
"detail": "/v3/pipeline/{pipeline_id}/publish"
},
"related": {
"pipeline": {
"list": "/v3/pipeline",
"detail": "/v3/pipeline/{pipeline_id}"
},
"source": {
"list": null,
"detail": "/v3/pipeline/{pipeline_id}/source/{source_id}"
},
"transform": {
"list": null,
"detail": "/v3/pipeline/{pipeline_id}/transform/{transform_id}"
},
"sink": {
"list": null,
"detail": "/v3/pipeline/{pipeline_id}/sink/{sink_id}"
}
}
},
"page": null
},
"data": {
"id": "&lt;your_pipeline_id&gt;",
"account_id": "&lt;your_account_id&gt;",
"partition_id": "gen1",
"title": "My API Pipeline 3",
"deploy_type": "saas",
"config": {},
"created_at": "2024-10-28T20:49:35.547Z",
"updated_at": "2024-10-31T19:17:13.632Z",
"published_at": "2024-10-31T19:17:18.005Z",
"published_revision_id": "bea822cc-97bc-11ef-b6dd-9aafefcf6cfb",
"deployed_revision_id": null,
"loaded_revision_id": null,
"processing_status": "enabled",
"origin": "ui"
}
}
{% /tab %}
{% /code %}

And that's it! You've now published your first pipeline that you can send data into and out to S3! Stay tuned for part two for more advanced use cases, including removing/modifying nodes, reverting a pipeline version, pausing, and more.