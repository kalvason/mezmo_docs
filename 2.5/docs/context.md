---
type: page
title: Viewing Log Context
listed: true
slug: context
description: 
index_title: Viewing Log Context
hidden: 
keywords: 
tags: 
---



This guide covers how to use the context menu associated with each log line in the Mezmo web app. The purpose of the context menu is to provide you additional details about a particular log line.

## Accessing context

To open the context menu:

1. Mouse over the desired log line.
2. Click on the grey triangle to the left of the log line.

## Viewing context

The context menu contains several components.

### Log type

On the left, the type of log is displayed. By default, this is `TEXT`, but if the log line was parsed, it will display the log line type, such as `JSON`. For a full list of of parsed log line types, see the [Parsing section of the Search guide](/docs/search#parsing).

### Log message

In the center of the context menu, the log line contents are displayed without the timestamp, source, app, or level. If this log line was parsed, the parsed fields are typically nicely formatted as well.

### View in context

At the top of the context menu there is a `View in context` button. This will open a modal displaying your log line in the context of other log lines from that host, app, or both.

### Copy to clipboard

This copies the log line contents as displayed inside the context menu. By default, this will copy the formatted line.



{% image url="https://uploads.developerhub.io/prod/2KW7/raqy2o1djx03xcwxfmg1i5m5bv8nigzzdtowbgjmjik0tz1m6eu66z2gy47tus1k.png" caption="" mode="responsive" height="278" width="1693" %}
{% /image %}



From the above screenshot, the formatted log line in your copy buffer would look like this:



{% code %}
{% tab language="none" %}
<head><title>404 Not Found</title></head>
{% /tab %}
{% /code %}



However, if you [configure your account to store and show raw lines](/docs/store-and-show-raw-lines), you will have the option to copy the raw line as well.



{% image url="https://uploads.developerhub.io/prod/2KW7/raqy2o1djx03xcwxfmg1i5m5bv8nigzzdtowbgjmjik0tz1m6eu66z2gy47tus1k.png" caption="" mode="responsive" height="278" width="1693" %}
{% /image %}





{% image url="https://uploads.developerhub.io/prod/2KW7/975xkhmtga8trjni0ktb0nsj11e0h8z9kvpdc1nmkvjl7fe98fgj5b327pjcau30.png" caption="" mode="responsive" height="279" width="1695" %}
{% /image %}



From the above screenshot, the raw log line in your copy buffer would look like this:



{% code %}
{% tab language="none" %}
{"log":"\u003chead\u003e\u003ctitle\u003e404 Not Found\u003c/title\u003e\u003c/head\u003e\r\n","stream":"stdout","time":"2020-05-08T05:40:30.995632532Z"}
{% /tab %}
{% /code %}



### Share this line

This menu lets you share your line via a login-protected link or via a secret gist.

## Context Color Legend

The different colors of the expanded log context represent different types of data. Below is the mapping of colors to both the individual tokens as well as the indentifiers/tags/labels:



{% image url="https://uploads.developerhub.io/prod/2KW7/raqy2o1djx03xcwxfmg1i5m5bv8nigzzdtowbgjmjik0tz1m6eu66z2gy47tus1k.png" caption="" mode="responsive" height="278" width="1693" %}
{% /image %}





{% image url="https://uploads.developerhub.io/prod/2KW7/975xkhmtga8trjni0ktb0nsj11e0h8z9kvpdc1nmkvjl7fe98fgj5b327pjcau30.png" caption="" mode="responsive" height="279" width="1695" %}
{% /image %}





{% image url="https://uploads.developerhub.io/prod/2KW7/pjs2ip2iyg4e16xrzbnnt6johq5xc7rbgexoy65oo90uupqyr2b3nx4iqmwrkdak.png" caption="" mode="responsive" height="646" width="699" %}
{% /image %}



Please note that the exact color depends on your Viewer Theme.



