---
type: page
title: Alert Message
listed: true
slug: alert-message-destination
description: 
index_title: Alert Message
hidden: 
keywords: 
tags: 
---

## Description

You can use this Destination to send alert messages to a selected service, such as Slack, PagerDuty, or a Webhook. This is helpful if there are particular events or metrics that process through your Pipeline that should trigger further action for you or your team.

## Configuration

### Configuration Options

{% table %}
| Option | Description | 
| ---- | ---- | 
| End-to-End Acknowledgment | Sends an end-to-end acknowledgement for the alert message. | 
| URI | The full URI  of the service that you want to send the alert message to. This should include the protocol and host, but can also include the port, path, and any other valid part of a URI. | 
| Service | The message service to send the alert to. Options include Slack, PagerDuty, and WebHook. There are additional configuration parameters depending on the Service chosen (See below). | 
| Window Seconds | The time frame during which the number of events (set by the **Threshold**) is permitted. | 
| Threshold | The number of events allowed over the given time window set by **Window Seconds** (default: 1). | 
{% /table %}

## When Service is Set to Slack or Webhook

**Prerequisite for Slack**: Setup an [incoming webhook](https://api.slack.com/messaging/webhooks) within your Slack organization and use the webhook URL as the URI config above. 

{% table widths="170" %}
| Option | Description | 
| ---- | ---- | 
| Message Text | The text to send to the Service. Note: This currently does not support message templates. | 
{% /table %}

## When Service is Set to PagerDuty

{% table widths="170" %}
| Option | Description | 
| ---- | ---- | 
| Summary | A brief text summary of the event, used to generate the summaries/titles of any associated alerts. The maximum permitted length of this property is 1024 characters. Note: This currently does not support message templates. | 
| Severity | The perceived severity of the status the event is describing with respect to the affected system.  (info, warning, error, critical). | 
| Source | The unique location of the affected system, preferably a hostname or FQDN. | 
| Routing Key | This is the 32 character Integration Key for an integration on a service or on a global ruleset. | 
| Event Action | The event action associated with the alert (trigger, acknowledge, resolve). | 
{% /table %}