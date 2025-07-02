---
type: page
title: Required Schema for Mezmo Log Analysis Destination
listed: true
slug: required-schema-for-mezmo-log-analysis-destination
description: 
index_title: Required Schema for Mezmo Log Analysis Destination
hidden: 
keywords: 
tags: 
---

If you choose to restore data to the [Mezmo Log Analysis Destination](/telemetry-pipelines/mezmo-destination), it must conform to the schema shown in this topic.

{% callout type="info" title="Schema for Message Property" %}
This schema is what appears in the `message` property within the Pipeline.  The contents of `message`  is what is sent to the archive.
{% /callout %}

## Primary Fields

{% table widths="129" %}
| Field Name | Description | 
| ---- | ---- | 
| `_line` | (required) This is the content of the log line to be displayed in the collapsed line viewer. | 
| `_ts` | (required) The epoch timestamp. | 
| `_logtype` | Helps lineviewer decide which renderer to use when line is expanded. \n\n\n\n Valid values are `customapp`, `json`, `meta`, `combinedapachelog`, `commonapachelog`, `github`, `mongo3log`, `redis3log`, `heroku_line`, `heroku_router` | 
| `level` | Indicates the level of severity and it displayed in the collapsed line. | 
| `_label` | JSON Object containing the key and values of labels appearing as yellow chips under LABELS in expanded view. | 
| `_tag` | JSON Object containing the key and values of tags appearing as purple chips under TAGS in expanded view. | 
| `_rawline` | This is usually the entire raw line.  If set is displayed just above line identifiers. | 
| `_meta` | JSON Object of metadata fields and values.  If `_logtype` is meta, these values will be displayed in a special section at the top of the expanded view. | 
{% /table %}

## Line Identifier Display Names for Fields

This table shows the display name for fields as they appear in the **Line Identifiers** expanded view. 

{% table widths="147" %}
| Field | Line Identifiers Display Name | 
| ---- | ---- | 
| `_host` | Also known as `Source`. Displayed as a chip in **Line Identifiers**, and in the color orange in the collapsed line view. | 
| `_app` | Displayed as `App` in Line Identifiers, and in the color blue in the collapsed line view. | 
| `_file` | `File` | 
| `org` | `Organization` | 
| `env` | `Env` | 
| `dyno` | `Dyno` | 
| `pod` | `Pod` | 
| `container` | `Container` | 
| `namespace` | `Namespace` | 
| `node` | `Node` | 
| `containerid` | `Container ID` | 
| `k8sclusterkey` | `Cluster` | 
{% /table %}

## Line Metadata Display Names for Fields

This table shows the display name for fields in the Line Metadata expanded view. 

{% table widths="" %}
| Field | Line Metadata Display Name | 
| ---- | ---- | 
| `mezmo_line_size` | `Line size (bytes)` | 
{% /table %}

## Custom Fields

Additional fields and objects will be displayed at the top of expanded view as long as `_logtype` is either `meta` or `json.`

## Example Minimum Required JSON

{% code %}
{% tab language="json" %}
{
    "_line": "this is the line 1", 
    "_ts": 1714498430000
}
{% /tab %}
{% /code %}

## Example of More Complex JSON

{% code %}
{% tab language="json" %}
{
    "_host": "mezmo",
    "_ingester": "Mezmo/0.34.2-custom- (x86_64-unknown-linux-gnu,debug=full)",
    "_label": {
        "app": "metallb",
        "component": "speaker",
        "controller-revision-hash": "86c95794fd",
        "pod-template-generation": "1"
    },
    "_logtype": "json",
    "_file": "speaker",
    "_line": "2024-05-13T00:06:10.997763284Z stdout F {\"caller\":\"speakerlist.go:271\",\"level\":\"info\",\"msg\":\"triggering discovery\",\"customObj\": {\"SomeField\": \"Some value\" \"anotherfield\": \"a value\"}}",
    "_rawline": "2024-05-13T00:06:10.997763284Z stdout F {\"caller\":\"speakerlist.go:271\",\"level\":\"info\",\"msg\":\"triggering discovery\",\"customObj\": {\"SomeField\": \"Some value\" \"anotherfield\": \"a value\"}}",
    "_ts": 1715734305158,
    "_app": "speaker",
    "_meta": {
        "Image Name": "quay.io/metallb/speaker",
        "Tag": "v0.13.12"
    },
    "message": "stdout F {\"caller\":\"speakerlist.go:271\",\"level\":\"info\",\"msg\":\"triggering discovery\",\"op\":\"memberDiscovery\",\"ts\":\"2024-05-13T00:06:10Z\"}",
    "caller": "speakerlist.go:271",
    "level": "info",
    "customObj": {
        "SomeField": "Some value",
        "anotherfield": "a value"
    }
}
{% /tab %}
{% /code %}