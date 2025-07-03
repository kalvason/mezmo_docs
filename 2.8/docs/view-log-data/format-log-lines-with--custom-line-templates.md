---
type: page
title: Format Log Lines with  Custom Line Templates
listed: true
slug: format-log-lines-with--custom-line-templates
description: 
index_title: Format Log Lines with  Custom Line Templates
hidden: 
keywords: 
tags: 
---

You can use custom line templates to format the lines in the log viewer to make it easier for you to identify specific information that is of interest to you. 

1. Select an existing View or [auto$](/docs/create-and-edit-views).
2. Select **Edit View Properties.**
3. In the **Custom %LINE Template** area, enter your template.

## Display PID, Program, and Log Source

If you have log lines that look similar to the example, you can decide to display the information in a more easily parsed format.

{% image url="https://uploads.developerhub.io/prod/2KW7/e5cpcsho4qptzqgn9afgbl28uehi79it2b7ahj5jhpbcjogxzajoxezdosygj4l6.png" caption="Images of log lines from Viewer." mode="300" height="1060" width="770" %}
{% /image %}

1. Enter `PID: {{pid}} | Program: {{program}} | Log Source: {{logsource}}` into Custom %LINE Template area.
2. You logs should now look like:

{% code %}
{% tab language="bash" %}
Aug 8 11:29:03 samir-Debian-10 daemon.log PID: 468 | Program: logdna-agent | Log Source: ip-12-34-5-67
{% /tab %}
{% /code %}

## Use Reserved Fields

[Reserved fields](/docs/log-parsing) are marked by an underscore. 

If your data resembles: 

{% code %}
{% tab language="bash" %}
user 1234 requested endpoint /api/endpoint
{% /tab %}
{% /code %}

And contains this field metadata:

{% code %}
{% tab language="json" title="JSON" %}
{
	meta: {
		first_name: Jane,
		last_name: Doe
	}
}
{% /tab %}
{% /code %}

Enter `{{_meta.first_name}} {{_meta.last_name}}, aka $@`  into Custom %LINE Template area. Using `$@`  will reference the original line.

This will display log messages in that view in this format:

{% code %}
{% tab language="bash" %}
Jane Doe, aka user 1234 requested endpoint /api/endpoint
{% /tab %}
{% /code %}

## Return as JSON

You can format your data to return as JSON.

{% code %}
{% tab language="json" %}
{"index": {{query.index}}, "size": {{query.size}}, "ignore_unavailable": {{query.ignore_unavailable}}, "track_total_hits": {{query.track_total_hits}}, "body": {"query": {{query.body.query}}, "sort": {{query.body.sort}}, "aggs":{{query.body.aggs}}}}
{% /tab %}
{% /code %}

### Formatted Log Line Example

{% code %}
{% tab language="json" %}
Aug 8 12:49:20  xxxx-xxxx-xxxxxxxxx-xxxx  apiinternal info  {"index": ["*:logline.*"], "size": 0, "ignore_unavailable": true, "track_total_hits": true, "body": {"query": {
  "bool": {
    "must": [
      {
        "range": {
          "_ts": {
            "gte": 1659976890001,
            "lte": 1659977360647
          }
        }
      },
      {
        "bool": {
          "should": [
            {
              "term": {
                "_app": "localhost"
              }
            }
          ]
        }
      }
    ]
  }
}, "sort": {
  "_lid": {
    "order": "desc"
  }
}, "aggs":{
  "metrics": {
    "date_histogram": {
      "field": "_ts",
      "interval": "30s"
    }
  }
}}}
{% /tab %}
{% /code %}