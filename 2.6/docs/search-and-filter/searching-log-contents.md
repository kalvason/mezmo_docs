---
type: page
title: Search Log Contents
listed: true
slug: searching-log-contents
description: 
index_title: Search Log Contents
hidden: 
keywords: 
tags: 
---

Mezmo provides advanced capabilities for searching the contents of your logs. In this topic you'll find detailed information about search operators with examples of search queries, using Time Search, and how to work with special characters in your search queries. 

## Queries, Terms, and Operators

A **query** or **search** is composed of **terms** and **operators**.  

In this example **query**, ClassCastException OR NullPointerException:

- `ClassCastExceptionand` and `NullPointerException` are **terms**
- **OR** is an operator

## Simple Search

The simplest type of search is a single term string search. This will return all log lines with the word `healthcheck` in them.

{% code %}
{% tab language="bash" %}
healthcheck
{% /tab %}
{% /code %}

## Search Operators

{% callout type="info" title="Capitalize Operators" %}
`AND` and `OR` are case sensitive and must be capitalized.
{% /callout %}

### NOT Operator

To perform a simple exclude search, prepend a dash `-`  to exclude results with that word. 

This example will return all log lines that **do NOT** contain the word `healthcheck`.

{% code %}
{% tab language="bash" %}
-healthceck
{% /tab %}
{% /code %}

### AND Operator

**Implicit AND**

Any whitespace between terms is implicitly interpreted as `AND`. 

For example, the query `file does not exist` will return any log containing all four words, regardless of their order. To search for the exact phrase, surround it in double quotes, `"file does not exists"` . Learn more in [auto$](/docs/searching-log-contents).

{% callout type="info" title="List Exception" %}
The only exception is when using lists, which treat whitespace as a part of the search term. Learn more in [auto$](/docs/searching-log-contents).
{% /callout %}

**Explicit AND**

You can also add AND as an operator to your search query to explicitly combine terms.

This example query will look for the word `healthcheck` AND log lines that **do not** contain the word `successful`.

{% code %}
{% tab language="bash" %}
healthcheck AND -successful
{% /tab %}
{% /code %}

### OR Operator

Specifying the **OR** operator returns results with either term. 

This example query will return all log lines that contain the word `healthcheck` or contain the word `ping.`

{% code %}
{% tab language="bash" %}
healthcheck OR ping
{% /tab %}
{% /code %}

### Chained Operators

You can chain operators together for specific searches. See the section Order of Operators for more information on the order of operator execution. 

This query example will return lines with `healthcheck`, then lines that **do not** have the word `successful` or `ping`.

{% code %}
{% tab language="bash" %}
healthcheck -successful OR ping
{% /tab %}
{% /code %}

### Grouping

Use parentheses to explicitly specify operator precedence for your search terms, Queries in parenthesis are executed first. 

This will search in the Mezmo app and exclude log line containing success or waiting.

{% code %}
{% tab language="bash" %}
app:memo -("success" OR "waiting")
{% /tab %}
{% /code %}

### Order of Operations

Search query operations are executed in this order:

1. `( )` Grouping
2. `-` Not
3. `OR`
4. `AND` or implicit white space between terms

The query  `me myself OR I` is equivalent to  `me AND (myself OR I)` since **OR** operators have higher precedence than **AND** operators. 

The query `(me myself) OR I` is equivalent to `(me AND myself) OR I` since grouping operators have higher precedence than OR operators.

All remaining operators are at the same precedence as the grouping operators.

## Time Search

You can search for logs that were generated during specific or broad time frames in the **Jump to Timeframe** area in the log **View**. You can use both text and numeric values, For example:

- `last friday`
- `yesterday 1pm`
- `5:4am`
- `2/24 2:30pm`

## Special Characters

### Escaping Special Characters

Put words in parenthesis to escape special characters such as white space. Unless escaped, terms are combined by whitespace and use AND to search. 

This query example will look for `403 Forbidden` and `login:`

`"403 Forbidden" login`

### Symbols

By default, all symbols in queries are matched exactly. 

In this example, the query will return all logs that contain the term `%VARIABLE%` :

`%VARIABLE%`

## Filter Logs

Filters can be found on the [Views page](https://app.logdna.com/logs/view) in your Mezmo app.

- **Tags -** A tag can be used to group lines and more than one tag can be applied to a given line.
- **Source -**  Contains a list of your logging sources. A source can be a host, computer, virtual machine, or Heroku app. Source metadata such as IP address or OS may be displayed with the source.
- **App** - Contains a list of logging buckets. An app can represent a log file, program or container. Typically, log lines within an app are inherently similar.
- **Level** - Contains a list of parsed log levels, such as `INFO`, `DEBUG`, or `ERROR`. Log levels are automatically parsed from log lines using standard log level detection and common patterns.

### Use Filters

To use filters, click on the desired filter drop-down menu and tick the checkboxes of the entries you are interested in. Selecting more than one checkbox within a filter will include log lines that belong to any of the selected entries. Selecting checkboxes in more than one filter, such as selecting 1 app and 1 source, will return log lines that match both that app and that source.

- Selected entries within such as selecting two sources, use OR
- Selected entries across filters such as selecting a source and an app, use AND

If you select two sources, `host1` and `host2` , then select two apps, `website` and `react_app` . Log lines matching these conditions will be returned. 

{% code %}
{% tab language="bash" %}
(host1 AND website) OR (host1 AND react_app) OR (host2 AND website) OR (host2 AND react_app).
{% /tab %}
{% /code %}