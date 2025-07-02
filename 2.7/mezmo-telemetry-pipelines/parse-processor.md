---
type: page
title: Parse Processor
listed: true
slug: parse-processor
description: 
index_title: Parse Processor
hidden: 
keywords: 
tags: 
---

## [Description](https://docs.mezmo.com/docs/parse-pipeline-processor#description)

With the Parse processor you can take incoming data of a known format and convert it into a parsed set of values prior to subsequent processing.

## [Use](https://docs.mezmo.com/docs/parse-pipeline-processor#use)

The primary use case is for parsing logs sent to the HTTP endpoint. The labeled sources in the user interface are already parsed automatically.

## [Configuration](https://docs.mezmo.com/docs/parse-pipeline-processor#configuration)

There are two options for configuring the Parse processor.

{% table %}
| Option | Description | Example | 
| ---- | ---- | ---- | 
| Field | The JSON field to parse. Leave blank for the entire message. | `.msg` | 
| Parser | The type of parser to use. | CSV | 
{% /table %}

## Parser Options

{% table %}
| Parser | Description | 
| ---- | ---- | 
| Common Log | Also known as NCSA Common log format**.**\n\n\n\nThis format is the basis for Apache Common Log and will work for Apache logs (not Apache Error logs however). | 
| CSV | This formats comma separated values and make the individual rows accessible as events where the key values within the parsed data are labeled with the columns. | 
| JSON | This accepts any JSON that came in as a text string to make it explicitly JSON.\n\n\n\nNote that you might also need to use this if JSON is embedded within a message, such as inside of a syslog event. | 
| Integer | Converts a string number into a numeric value.\n\n\n\nThis can be used to parse hexadecimal, octal, and binary numbers into a base 10 format. | 
| Query String | Takes any appended values from URL query parameters, meaning anything after the `?` and parses them according to HTML character encoding | 
| URL | Separates a URL into the individual components. | 
| Tokens | This parser separates a string of words based on the contained whitespace and text references.\n\n\n\n- Text delimited by whitespace\n- Text delimited by double quotes: `".."`\n- Text delimited by square brackets: `[..]`\n\n\nNote that the quotes and brackets can be escaped with a backslash (`\).` | 
| User Agent | This parser provides a best effort approach towards user agent identifiers, such as for browsers. It breaks the text of the user agent string into an object that can be subsequently used for processing. | 
| Key/Value | This parser can be applied towards any text that includes a separated set of delimiters against a string. It includes:\n\n\n\n1. A key delimiter - the character that separates the key and the value\n2. The field delimiter - the character that separates the key / value pairs\n\n\nThis can be useful for `logfmt` and other types of data that are within a string, but have a defined delimiter. | 
| Timestamp | This parser allows you to define a parsing expression to be used against timestamp strings that are ingested within logs.\n\n\n\nTimestamp parsing expressions are evaluated based on the [strftime format](strftime format). Common preset expressions are included for ease of use. | 
{% /table %}

## Examples

### Common Log

#### Input

{% code %}
{% tab language="json" %}
91.227.35.153 - - [13/Feb/2023:23:23:03 +0000] "POST /js210dbc20e85d2c543d2cba57379ad20 HTTP/1.1" 200 9021
{% /tab %}
{% /code %}

#### Output

{% code %}
{% tab language="json" %}
{
  "host": "91.227.35.153",
  "message": "POST /js210dbc20e85d2c543d2cba57379ad20 HTTP/1.1",
  "method": "POST",
  "path": "/js210dbc20e85d2c543d2cba57379ad20",
  "protocol": "HTTP/1.1",
  "size": 9021,
  "status": 200,
  "timestamp": "2023-02-13T23:23:19Z"
}
{% /tab %}
{% /code %}

### Timestamp

#### Input

`Sat Jul 23 02:16:57 2005`

#### Output

`2005-07-23T02:16:57Z`

### User Agent

#### Input

`Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:109.0) Gecko/20100101 Firefox/109.0`

#### Output

{% code %}
{% tab language="json" %}
browser:{
  family:"Firefox"
  version:"109.0"
}
device:{
  category:"pc"
}
os:{
  family:"Mac OSX"
  version:"10.15"
}
{% /tab %}
{% /code %}