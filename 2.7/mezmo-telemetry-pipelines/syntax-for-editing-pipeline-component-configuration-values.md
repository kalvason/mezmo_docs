---
type: page
title: Syntax for Editing Pipeline Component Configuration Values
listed: true
slug: syntax-for-editing-pipeline-component-configuration-values
description: 
index_title: Syntax for Editing Pipeline Component Configuration Values
hidden: 
keywords: 
tags: 
---

When editing configuration values for Sources, Processors, or Destinations, you should be aware of using the proper syntax. There are three types of configuration values that each require their own syntax:

{% table widths="160,0" %}
| **Configuration Value** | **Description** | **Example** | 
| ---- | ---- | ---- | 
| **Data Fields** | A parsed field of an event, metadata associated to the event, or other types of data within the pipeline | `.hostname` refers to a hostname value that has been parsed from an object. | 
| **Data References** | Data being sent out as a part of a destination configuration, which may be a field or a static value | You would use `{{ .hostname }}` to insert a hostname in an input field that might otherwise expect a static value. | 
| **Static Values** | Static values are typically used for comparison operations. | You would use the value `my string` for a string comparison, or the value `42` for a numeric comparison. | 
{% /table %}

## [Data Fields](https://docs.mezmo.com/docs/syntax-for-editing-pipeline-component-configuration-values#data-fields)

Data fields are found in many processors. They are used when specifying fields within an object to use for conditional tests or transformation operations.

Data fields require a specific dot notation in order to define them. The dot notation uses periods as delimiters for the field levels.

Characters allowed within the dot notation are **letters**, **numbers** and **underscores**. All other characters must be included between quotation marks `" "` if they are a part of the field key itself.

#### Example

This example illustrates how to refer to the fields and values in this parsed event.

{% code %}
{% tab language="json" %}
{
  "bytes": 22322,
  "datetime": "24/Jan/2023:18:54:09",
  "host": "127.219.215.140",
  "method": "DELETE",
  "protocol": "HTTP/1.1",
  "referer": "https://names.de/apps/deploy",
  "request": "/secret-info/open-sesame",
  "status": "300",
  "user-identifier": "meln1ks",
  "data": {
  	"extra-data": "mydata"
	}
}
{% /tab %}
{% /code %}