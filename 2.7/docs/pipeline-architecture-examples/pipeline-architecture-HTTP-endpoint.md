---
type: page
title: Pipeline Architecture: Set Up and Process HTTP Endpoint Data
listed: true
slug: pipeline-architecture-HTTP-endpoint
description: 
index_title: Pipeline Architecture: Set Up and Process HTTP Endpoint Data
hidden: 
keywords: 
tags: 
---

This topic describes how to set up an HTTP endpoint as a Pipeline Source, and then process and inspect the endpoint data before sending it to a destination, such as [auto$](/docs/amazon-s3-storage-pipeline-destination), or [auto$](/docs/mezmo-log-analysis-pipeline-destination).

## Source

### Set Up the HTTP Endpoint Source

1. Log in to [the Mezmo Web App](app.mezmo.com).
2. In the left-hand menu, click **Pipelines**. This will open the **Edit Pipeline** interface.
3. In the left-hand navigation, click **+ New Pipeline**.
4. For the Pipeline **Name**, enter `HTTP Inspect`, then click **Save**.
5. In the **Source** column of the Pipeline Map, click **Add**, then select **HTTP Source**. 

#### HTTP Source Configuration Settings

After you add the HTTP Source to your Pipeline Map, click the node to open the configuration settings. 

{% table %}
| Setting | Value | 
| ---- | ---- | 
| **Title** | A name for your source. | 
| **Description** | A short description of the source. | 
| **Decoding Method** | `.json` | 
| **Access Key Management** | 1. Click **Create new key** to generate an access key. \n2. Enter a **Title** for the key. \n3. Click **Create**.\n\n\nMake sure to copy the Access Key and note the Ingestion URL, which should resemble `https://pipeline.mezmo.com/v1/%YOUR PIPELINE ID%.`You will need to provide this information in the next step. | 
{% /table %}

Click **Update** to finish configuring the HTTP endpoint, and then click **Deploy Pipeline**.

{% callout type="success" title="Ignore \"Unconnected Node\" Warnings" %}
You will probably see a message warning you of unconnected nodes in your Pipeline. You can safely ignore these at this step of building your Pipeline.
{% /callout %}

### Send Test Data to Your Source

Now that you've deployed your pipeline, the next step is to send data into it via the Ingestion Endpoint. This example uses a basic cURL command to send test data to the endpoint, but you could also use an API tool like Postman if you prefer. 

Before you send the data, you should use a [Pipeline Tap](/docs/view-and-sample-pipeline-data) monitor the HTTP source and make sure it is receiving data. 

1. Hover your cursor over the right side of the HTTP Source node until it turns blue. 
2. Click the blue edge of the node to open the **Pipeline Tap**. 
3. Set the **Log Events** to **20**, and click **Play**. A loading animation will begin to play, but you won't see any data yet. 
4. Open a terminal to send cURL commands, and enter this command, entering your Access Key and Ingestion Endpoint from the previous step as shown.  

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

## Processors

Now that you've got your pipeline accepting data, the next step is to start adding additional processors to it. There are many ways you can [auto$](/docs/process-pipelin-data), but for this example you will use the [auto$](/docs/remove-fields-pipeline-processor) to remove a specific field. This is a typical use case if you want to send data to a storage location like Amazon S3 to reduce the amount or type of data you store, or if you want to send a limited amount of data to a tool like Mezmo Log Analysis. 

1. In the **Processors** column of the Pipeline Map, click **Add**. 
2. Select the **Remove Fields Processor.**
3. Provide a **Title** and **Description** for the node, like `Sensitive Data` and  `Drop sensitive data fields`. 
4. For **Fields**, enter `.sensitive`. In this case, the `.` notation is used to designate that the configuration object is a field. You can find more information in [auto$](/docs/syntax-for-editing-pipeline-component-configuration-values) for how to designate fields, sub-fields, and string and numeric values. 
5. **Save** the Processor. 
6. To connect the Processor and Source, hover your cursor over the right side of the until a blue circle appears, then click the circe and draw a Connector between the Source and Processor. 
7. Click **Deploy Pipeline**. You can again ignore the **Unconnected Node** warning.  
8. Open the Pipeline Tap window for the Processor.
9. Go back to your cURL terminal and send this command:

{% code %}
{% tab language="bash" %}
$ curl -H "Content-Type: application/json" \
       -H "Authorization: %YOUR TOKEN HERE%" \
       -X POST \
       -d '{"Hello": "World", "sensitive": "data","was": "here"}' \
       https://pipeline.mezmo.com/v1/%YOUR PIPELINE ID%
{% /tab %}
{% /code %}

In the Pipeline Tap window you should see ``{"Hello":"World","was":"here"}`.```

## Destinations

Now that you've set up an HTTP endpoint source and a Processor, you could send the processed data to any number of [Destinations](/docs/set-up-pipeline-destinations) depending on your specific use case.