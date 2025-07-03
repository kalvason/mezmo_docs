---
type: page
title: Set Up and Test an HTTP Endpoint Source
listed: true
slug: set-up-and-process-http-endpoint-data
description: 
index_title: Set Up and Test an HTTP Endpoint Source
hidden: 
keywords: 
tags: 
---


This topic describes how to set up an HTTP endpoint as a Pipeline Source, and then process and inspect the endpoint data before sending it to a destination, such as [Mezmo Log Analysis](/docs/about-mezmo-log-analysis), or [auto$](/telemetry-pipelines/s3-destination).

## [Source](https://docs.mezmo.com/docs/pipeline-architecture-HTTP-endpoint#source)

### [Set Up the HTTP Endpoint Source](https://docs.mezmo.com/docs/pipeline-architecture-HTTP-endpoint#set-up-the-http-endpoint-source)

1. Log in to [the Mezmo Web App](https://docs.mezmo.com/app.mezmo.com).
2. In the left-hand menu, click **Pipelines**. This will open the **Edit Pipeline** interface.
3. In the left-hand navigation, click **+ New Pipeline**.
4. For the Pipeline **Name**, enter `HTTP Inspect`, then click **Save**.
5. At the bottom of the Pipeline map, click the **Add** **Source** button, then select **HTTP Source**.


#### HTTP Source Configuration Settings

After you add the HTTP Source to your Pipeline Map, click the node to open the configuration settings:

{% table %}

{% table %}
| Setting | Value | 
| ---- | ---- | 
| **Title** | A name for your source. | 
| **Description** | A short description of the source. | 
| **Decoding Method** | `.json` | 
| **Access Key Management** | 1. Click **Create new key** to generate an access key.\n2. Enter a **Title** for the key.\n3. Click **Create**.\n\n\n\n\nMake sure to copy the Access Key and note the Ingestion URL, which should resemble `https://pipeline.mezmo.com/v1/%YOUR PIPELINE ID%.`You will need to provide this information in the next step. | 
{% /table %}

{% /table %}

Click **Update** to finish configuring the HTTP endpoint, and then click **Deploy Pipeline**.

{% callout type="success" title="Ignore \"Unconnected Node\" Warnings" %}
You will probably see a message warning you of unconnected nodes in your Pipeline. You can safely ignore these at this step of building your Pipeline.
{% /callout %}

### [Send Test Data to Your Source](https://docs.mezmo.com/docs/pipeline-architecture-HTTP-endpoint#send-test-data-to-your-source)

Now that you've deployed your pipeline, the next step is to send data into it via the Ingestion Endpoint. This example uses a basic cURL command to send test data to the endpoint, but you could also use an API tool like Postman if you prefer.

Before you send the data, you should use a [Pipeline Tap](/telemetry-pipelines/view-pipeline-data) monitor on the HTTP source and make sure it is receiving data.

1. Click the **Tap** button on the **HTTP source**.
2. A loading animation will begin to play and it will say "Waiting for events to arrive", but you won't see any data yet.
3. Open a terminal to send cURL commands, and enter this command, entering your Access Key and Ingestion Endpoint from the previous step as shown.

{% code %}
{% tab language="bash" %}
$ curl -H "Content-Type: application/json" \
-H "Authorization: %YOUR TOKEN HERE%" \
-X POST \
-d '{"Hello":"World"}' \
https://pipeline.mezmo.com/v1/%YOUR PIPELINE ID%
{% /tab %}
{% /code %}

When the command executes, you should see a `{"status":"ok"}` response in your terminal, and `Hello World` appear in your Pipeline Tap.

## [Processors](https://docs.mezmo.com/docs/pipeline-architecture-HTTP-endpoint#processors)

Now that you've got your pipeline accepting data, the next step is to start adding additional processors to it. There are many ways you can process log data, but for this example you will use the [auto$](/telemetry-pipelines/drop-fields-processor) to remove a specific field. This is a typical use case if you want to send data to a storage location like Amazon S3 to reduce the amount or type of data you store, or if you want to send a limited amount of data to a tool like Mezmo Log Analysis.

1. Start by clicking on **Edit Pipeline** if you're not already in this view.
2. To add a processor, click the **Add Processor** button at the bottom of the pipeline map.
3. Select the **Remove Fields Processor.**
4. Provide a **Title** and **Description** for the node, like `Sensitive Data` and `Drop sensitive data fields`.
5. For **Fields**, enter `.sensitive`. In this case, the `.` notation is used to designate that the configuration object is a field. You can find more information in [auto$](/telemetry-pipelines/pipeline-event-data-model) on how to designate fields, sub-fields, and string and numeric values.
6. **Save** the Processor.
7. To connect the Processor and Source, hover your cursor over the right side of the until a blue circle appears, then click the circe and draw a Connector between the Source and Processor.
8. Click **Deploy Pipeline**. You can again ignore the **Unconnected Node** warning.
9. Open the Pipeline Tap window for the Processor.
10. Go back to your cURL terminal and send this command:

{% code %}
{% tab language="bash" %}
$ curl -H "Content-Type: application/json" \
-H "Authorization: %YOUR TOKEN HERE%" \
-X POST \
-d '{"Hello": "World", "sensitive": "data","was": "here"}' \
https://pipeline.mezmo.com/v1/%YOUR PIPELINE ID%
{% /tab %}
{% /code %}

In the Pipeline Tap window you should see ````{"Hello":"World","was":"here"}'` ``.

## [Destinations](https://docs.mezmo.com/docs/pipeline-architecture-HTTP-endpoint#destinations)

Now that you've set up an HTTP endpoint source and a Processor, you could send the processed data to any number of [Destinations](/telemetry-pipelines/set-up-pipeline-destinations) depending on your specific use case.