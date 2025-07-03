---
type: page
title: Google Cloud PubSub
listed: true
slug: gcp-cloud-pubsub-destination
description: 
index_title: Google Cloud PubSub
hidden: 
keywords: 
tags: 
---

## Description

This destination enables you to send events to Google's Pub/Sub product.

## Configuration Options

{% table %}
| Option | Description | 
| ---- | ---- | 
| Encoding | Specifies how the data will be serialized before being stored. | 
| Project ID | The [Project Id](https://support.google.com/googleapi/answer/7014113?hl=en) of your GCP Account. | 
| Topic | The name of the topic to send messages. | 
| JSON Credentials | The Google Cloud [Service Account Key](https://cloud.google.com/iam/docs/keys-create-delete#creating). | 
{% /table %}