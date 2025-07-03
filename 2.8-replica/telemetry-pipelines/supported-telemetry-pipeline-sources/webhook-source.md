---
type: page
title: Webhook (WebSub)
listed: true
slug: webhook-source
description: 
index_title: Webhook (WebSub)
hidden: 
keywords: 
tags: 
---


## Description

This source provides a way to accept RESTful Webhook messages using the WebSub protocol for verification.

## Configuration

This source corresponds to the [WebSub specification](https://www.w3.org/TR/websub/). All that is needed for this processor is the signing key to use to verify the payload with the HMAC digest.

### Configuration Options

{% table %}

{% table %}
| Option | Description | 
| ---- | ---- | 
| Signing key | This is the key used for the HMAC signature to verify the sender. | 
{% /table %}

{% /table %}