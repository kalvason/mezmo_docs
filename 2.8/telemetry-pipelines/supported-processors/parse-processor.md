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

You can create multiple parsing operations that will be performed in sequential order. This enables a stream of multiple logs to be separated without needing to build complex logic. If the first operation successfully parses all the incoming data, the Processor will exit to the next Pipeline component. 

## Configuration

There are two options for configuring the Parse processor.

{% table widths="" %}
| Option | Description | Example | 
| ---- | ---- | ---- | 
| Field | The JSON field to parse. Leave blank for the entire message. | `.msg` | 
| Parser | The type of parser to use. | CSV | 
{% /table %}

## Parser Options

{% table widths="" %}
| Parser | Description | 
| ---- | ---- | 
| Common Log | Also known as NCSA Common log format**.**\n\n\n\nThis format is the basis for Apache Common Log and will work for Apache logs (not Apache Error logs however). | 
| CSV | This formats comma separated values and makes the individual rows accessible as events where the key values within the parsed data are labeled with the columns. | 
| Grok Pattern | This parser allows a user to define [a grok expression](https://www.elastic.co/blog/do-you-grok-grok) for parsing unstructured data based on a desired output format.\n\n\nNote that the following literals are allowed between expressions, but otherwise you should use %{DATA} and %{GREEDYDATA} for data between expressions.\n\n\n\nAllowed literal characters:`\s,;:-` | 
| JSON | This accepts any JSON that came in as a text string to make it explicitly JSON.\n\n\n\nNote that you might also need to use this if JSON is embedded within a message, such as inside of a syslog event. | 
| Integer | Converts a string number into a numeric value.\n\n\n\nThis can be used to parse hexadecimal, octal, and binary numbers into a base 10 format. | 
| Query String | Takes any appended values from URL query parameters, meaning anything after the `?` and parses them according to HTML character encoding | 
| Regex Expression | This allows the user to enter a custom regular expression to be used in matching text within an unstructured text or line.\n\n\n\n**Note that this is a special feature that must be turned on by request.** Please try to use grok first as it is often a faster and safer way to extract data from unstructured text. | 
| URL | Separates a URL into the individual components. | 
| Tokens | This parser separates a string of words based on the contained whitespace and text references.\n\n\n\n- Text delimited by whitespace\n- Text delimited by double quotes: `".."`\n- Text delimited by square brackets: `[..]`\n\n\nNote that the quotes and brackets can be escaped with a backslash (`\).` | 
| User Agent | This parser provides a best effort approach towards user agent identifiers, such as for browsers. It breaks the text of the user agent string into an object that can be subsequently used for processing. | 
| Key/Value | This parser can be applied towards any text that includes a separated set of delimiters against a string. It includes:\n\n\n\n1. A key delimiter - the character that separates the key and the value\n2. The field delimiter - the character that separates the key / value pairs\n\n\nThis can be useful for `logfmt` and other types of data that are within a string, but have a defined delimiter. | 
| Timestamp | This parser allows you to define a parsing expression to be used against timestamp strings that are ingested within logs.\n\n\n\nTimestamp parsing expressions are evaluated based on the [strftime format](strftime format). Common preset expressions are included for ease of use. | 
{% /table %}

## AI Pattern Matching

{% synced id="beta-banner" %}
{% /synced %}

The Parse Processor includes an AI feature that can generate a regular expression to use in parsing based on a sample of log data. 

1. Use the PIpeline Tap feature to collect a few sample logs that you want to parse in the pipeline, then paste the sample into the Sample log lines window. 
2. Click **Find Patterns**, and the AI assistant will generate the regex for that data sample. 
3. When you click **Select Patterns**, the regular expressions will be copied to the Expression field of the Parse processor. You can test and tweak these expressions in the Parse processor as necessary.

{% callout type="info" title="Remove Sensitive Data from Sample Log Lines" %}
Mezmo uses a 3rd party LLM for generating regular expressions. Only your sample log lines are sent to a 3rd party LLM over API, please scrub any sensitive or user identifying data from your samples.
{% /callout %}

{% image url="https://uploads.developerhub.io/prod/2KW7/9irdtqrk0r0hign7advsulsb0j0uv5pqc5c4p306zm1odpooill2jm0cura2x29w.png" caption="The AI pattern recognition interface for the Parse Process" mode="responsive" height="1158" width="1128" %}
{% /image %}

## Examples

### Common Log

#### Input

{% code %}
{% tab language="none" %}
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

### Grok Pattern Example 1

#### Input

{% code %}
{% tab language="none" %}
220.181.108.96 - - [13/Jun/2021:21:14:28 +0000] "GET /blog/geekery/xvfb-firefox.html HTTP/1.1" 200 10975 "-" "Mozilla/5.0 (compatible; Baiduspider/2.0; +http://www.baidu.com/search/spider.html)"
{% /tab %}
{% /code %}

{% callout type="info" title="Literals and RegEx Values Not Supported" %}
Key items to note is that Mezmo does not support literals or regex values between grok patterns. This means that you will need to use the `%{DATA}` and `%{GREEDYDATA}` in replacing the literal characters.

You may still use a literal space %{SPACE} in between patterns and `%{NOTSPACE}` expressions in cases where the %{DATA} or %{GREEDYDATA} go to far.
{% /callout %}

**Pattern used**

{% code %}
{% tab language="none" %}
%{IPORHOST:clientip} %{USER:ident} %{USER:auth}%{DATA}%{HTTPDATE:timestamp}%{DATA}%{WORD:verb} %{DATA:request} %{WORD}%{DATA}%{NUMBER:httpversion}%{DATA}%{POSINT:status} %{NUMBER:bytes} %{QS:referrer} %{QS:agent}
{% /tab %}
{% /code %}

#### Output

{% code %}
{% tab language="json" %}
{
  "agent":"Mozilla/5.0 (compatible; Baiduspider/2.0; +http://www.baidu.com/search/spider.html)"
  "auth":"-"
  "bytes":"10975"
  "clientip":"220.181.108.96"
  "httpversion":"1.1"
  "ident":"-"
  "referrer":"-"
  "request":"/blog/geekery/xvfb-firefox.html"
  "status":"200"
  "timestamp":"13/Jun/2021:21:14:28 +0000"
  "verb":"GET"
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