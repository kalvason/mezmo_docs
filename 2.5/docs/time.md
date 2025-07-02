---
type: page
title: Jumping to Timeframe
listed: true
slug: time
description: 
index_title: Jumping to Timeframe
hidden: 
keywords: 
tags: 
---



This topic covers how to use the **Jump to timeframe** input box located at the bottom of the page in the Mezmo web app.



{% callout type="info" title="Note" %}
keep in mind that time queries are performed in conjunction with filters and search. Any specified search queries, sources, apps, and log levels are respected in addition to the timeframe itself.
{% /callout %}



## Jump to time

To jump to a point in time in your logs, type the desired day and time in the **Jump tp timeframe** field.



{% code %}
{% tab language="none" %}
today at 11am
{% /tab %}
{% /code %}



This will take you to your log lines at 11 am today, in your local time.

## Set a timeframe

To set a timeframe for your logs, type two different dates and times separated by `to`.



{% code %}
{% tab language="none" %}
last fri 4:30p to 11/12 1 AM
{% /tab %}
{% /code %}



This will show all logs between last Friday at 4:30 PM and November 12 at 1 AM.

## Caveats

You can only search as far back as your plan's retention allows.



