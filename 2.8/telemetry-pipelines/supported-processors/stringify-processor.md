---
type: page
title: Stringify Processor
listed: true
slug: stringify-processor
description: 
index_title: Stringify Processor
hidden: 
keywords: 
tags: 
---

## [Description](https://docs.mezmo.com/docs/string-pipeline-processor#description)

This processor renders any JSON object into a single string. You can only apply this processor to the entire event rather than fields within the event.

## [Use](https://docs.mezmo.com/docs/string-pipeline-processor#use)

This processor is used for cases when a subsequent processing step requires a string as input. This can include destinations such as Mezmo Log Analysis, or Processors such as the Encrypt processor.

The output of this processor takes any structured input event and outputs it as a text string.

## Example

{% table widths="434" %}
| Before | After | 
| ---- | ---- | 
| `{\n\n\n\n  "host": "localhost", \n\n`\n\n\n\n`"port": 3030,`\n\n\n\n`"public": "../public/",`\n\n\n\n`"paginate": {`\n\n\n\n`"default": 10,`\n\n\n\n`"max": 50`\n\n\n\n`},`\n\n\n\n`"mongodb": "mongodb://localhost:27017/api"`\n\n\n\n`}` | `{\n\n  "host": "localhost",\n\n  "port": 3030,\n\n  "public": "../public/",\n\n  "paginate": {\n\n    "default": 10,\n\n    "max": 50\n\n  },\n\n  "mongodb": "mongodb://localhost:27017/api"\n\n}` | 
|  |  | 
{% /table %}