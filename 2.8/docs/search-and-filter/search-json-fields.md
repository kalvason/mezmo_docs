---
type: page
title: Search Log Fields
listed: true
slug: search-json-fields
description: 
index_title: Search Log Fields
hidden: 
keywords: 
tags: 
---

Mezmo provides several capabilities for searching fields in your logs. In this topic you'll find information on nested field searches, searching by field comparison, searching for the existence of fields, and general and exact term field searches.

## Access Search

1. Log in to [app.mezmo.com](https://app.developerhub.io/app.mezmo.com).
2. In the **Search** box at the bottom of the log viewer, enter your search terms.
3. Select the **Timeframe** that you want to search.
4. Select if you want to search **Live** log data, or historical.
5. In the **Viewer Tools** menu, enter any text you want highlighted in the search results.

{% image url="https://uploads.developerhub.io/prod/2KW7/q5q8p8eyjd4bq756unsdf9u3rpt97p9tgcjgkxj5cc8gh4i4nrf86pvt3au7ivl1.png" caption="Search bar in the Mezmo Web App" mode="responsive" height="88" width="1678" %}
{% /image %}

## JSON Field Search

To search for a field with a particular value, use a colon to separate the field and value. 

This example will return all parsed log lines with the field `response` with a value of `404`. 

{% code %}
{% tab language="bash" %}
response:404
{% /tab %}
{% /code %}

### Nested Field Search

To search for a nested field, use periods to separate each nested field. 

This example will return all log lines containing the key:value structure `{ "user": { "id": 12345 }}.`

{% code %}
{% tab language="bash" %}
user.id:12345
{% /tab %}
{% /code %}

## Filters

Using the same field search syntax, you can also set filters directly in the search bar. 

This example will return all log lines that originate from the source `myawesomehost` and not from the app `mycoolapp`.

{% code %}
{% tab language="bash" %}
host:myawesomehost -app:mycoolapp
{% /tab %}
{% /code %}

## Metadata

With the REST API or Node.js library, you can upload a metadata object as part of a log line's context. To search for field values contained in the metadata object, use the `meta` prefix.

This example will return all log lines containing the context object with the key:value structure `{ "status_code": 404}.`

{% code %}
{% tab language="bash" %}
meta.status_code:404
{% /tab %}
{% /code %}

## Field Comparison Operators

For parsed fields with a numeric value, we support the following operators:

{% code %}
{% tab language="bash" %}
* =
* <
* >
* <=
* >=
{% /tab %}
{% /code %}

To search for parsed fields matching comparison operators, use a colon followed by the comparison operator. 

{% code %}
{% tab language="bash" %}
response:>=400
{% /tab %}
{% /code %}

## Compound Field Comparison Search

To form a compound field search query using comparison operators, use a colon followed by parentheses.

This example will return all log lines with the field `response` with values greater than or equal to `400`, less than `500`, and not `404`.

{% code %}
{% tab language="bash" %}
response:(>=400 <500 -404)
{% /tab %}
{% /code %}

## Case-Sensitive Field Search

To search for a case-sensitive parsed field, use a colon followed by an equal sign `=`. 

This example will return all log lines with the field `name` with the case-sensitive string value `camelCasedName`.

{% code %}
{% tab language="bash" %}
name:=camelCasedName
{% /tab %}
{% /code %}

## Existence Field Search

To search for the existence of a parsed field, use a colon followed by the asterisk `*.`

This example will return all log lines that have a value for the `user` field.

{% code %}
{% tab language="bash" %}
user:*
{% /tab %}
{% /code %}

## Term Match Field Search

To search for a term match for a field value, use `==`. 

This example will return all lines with the exact name field value of `bob`, and will not match `bobby`.

{% code %}
{% tab language="bash" %}
name:==bob
{% /tab %}
{% /code %}

## Term Match Case-Sensitive Field Search

Prefix search is set by default for all string fields. To search for an **exact** match for a field value, use `===`. 

This example will return all lines with the exact name field value of `Bob`, and will not match `bob` or `Bobby`.

{% code %}
{% tab language="bash" %}
name:===Bob
{% /tab %}
{% /code %}

## Line Size Search

You can search for log lines by size by using the `mezmo_line_size` field annotation. This example will return lines with a line-size greater than 4000 bytes.

{% code %}
{% tab language="bash" %}
_mezmo_line_size:>4000
{% /tab %}
{% /code %}

You can create a search based on the size of specific log line by clicking the **Line size** value in the Log Viewer.

{% image url="https://uploads.developerhub.io/prod/2KW7/meed8nskqjlz26dlrmjvrdufw3gtwx8ertdnphip55ep8kk03wgo1j3b1ptusvvh.png" mode="responsive" height="88" width="282" %}
{% /image %}

You can also create graphs based on `mezmo_line_size` as described in [auto$](/docs/create-a-graph).

## Colons

Since the colon is a reserved character for field search, quotes are required when searching for strings with colons in them. 

This example will return all log lines with the string `response:` in them.

{% code %}
{% tab language="bash" %}
"response:"
{% /tab %}
{% /code %}

## Combining Operators

You can combine operators to make your search more specific. This searches first for logs scanned from`/var/log/syslog` or that contain the word `ERROR`, then limits the results to `node1.`

{% code %}
{% tab language="bash" %}
source:node1 AND (file:/var/log/syslog OR ERROR)
{% /tab %}
{% /code %}

This searches logs where the value stored in the status field is greater than 100 and less than 503.

{% code %}
{% tab language="bash" %}
status:(>100 AND <= 503)
{% /tab %}
{% /code %}

## Lists

Any whitespace between search terms is automatically interpreted as AND. For example, searching warning error returns logs containing both warning and error. The only exception is when using lists, which treat whitespace as a part of the search term. For example, searching `message:[file, exists]` will only search for instances of exists that are preceded by a space. Some other examples:

- `level:[warning,error]` will return as normal.  
- `level:[warning, error]`with a space between warning and error, will search for entries of the field level which have "warning" or " error" with space included.
- `level:[warning,(error)]` will search for entries of the field level which have "warning" or "(error)" with parenthesis included.