---
type: page
title: PagerDuty Auto-resolve Settings
listed: true
slug: pagerduty-auto-resolve
description: 
index_title: PagerDuty Auto-resolve Settings
hidden: 
keywords: 
tags: 
---



## About auto-resolving PagerDuty incidents

With auto-resolution, you can configure settings to automatically resolve PagerDuty incidents based on the number of log lines that show up in the associated view during the specified time frame, rather than manually resolving incidents in the PagerDuty application. When a PagerDuty alert channel has auto-resolution settings configured and the conditions are met to auto-resolve the incidents, all incidents that were triggered from the associated PagerDuty alert channel will be resolved.

For example, say you have a View that you use to look for specific incoming log lines. This might be a View that filters for a certain error type of log, so if you get more than 10, you consider that a problem that should be looked into. You attach an alert to the View for when 10 or more log lines are ingested and configure the alert to notify the PagerDuty app to create an incident when it happens.

With PagerDuty auto-resolve, you can further specify that if fewer than 10 log lines come in within a certain time frame, you want PagerDuty to auto-resolve any previous incidents that were triggered (within the specified timeframe) by the alert, and move them to the “Resolved” area on the PagerDuty application UI.

The auto-resolve settings are found at the bottom of the Alert modal for creating PagerDuty alerts.



{% image url="https://uploads.developerhub.io/prod/2KW7/bzuu8jf9eypplb7yf6fbgvp516wfyaijvtet91zpu1a5kv3mxa17eqqw70tpufu9.png" caption="" mode="responsive" height="1948" width="1408" %}
{% /image %}



## How to configure auto-resolution for PagerDuty incidents

1. On the [Alert modal](https://docs.mezmo.com/docs/alerts#how-to-attach-an-alert-to-an-existing-view), click the **Auto-resolve incidents** option to toggle it "on."
2. Specify the two conditions for the trigger to auto-resolve:

- the number of log lines to appear
- the timeframe within which that number of log lines appears

3. Click **Save Alert**.



{% callout type="info" title="Notes:" %}
- The auto-resolve option recognizes if the alert is a Presence alert (e.g. alert me when this specific type of log line appeared) or an Absence alert (e.g. alert me if this specific type of log line did NOT appear). Subsequently, the auto-resolve feature will look for "fewer than" the specified numbers of lines for a Presence alert, while for an Absence alert the auto-resolve functionality uses a "more than" value to trigger auto-resolution.
- A recommendation for auto-resolution is to use the same number and time interval that was defined for the alert itself.  Though each use case could be different; some users might want to auto-resolve incidents very quickly, while others may be more conservative and wait until a larger number of log lines come in.
- There may be a delay of several minutes before the alert takes effect.
{% /callout %}





