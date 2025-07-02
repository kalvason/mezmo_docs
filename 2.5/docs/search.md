---
type: page
title: Searching Your Logs
listed: true
slug: search
description: Learn how to use the Search Box located at the bottom of the page in the Mezmo web app. Mezmo is the easiest, fastest cloud log management software.
index_title: Searching Your Logs
hidden: 
keywords: 
tags: 
---


Before we begin, keep in mind that searches are performed in conjunction with filters and time queries. Any specified timeframes, sources, apps, and log levels are respected in addition to the search query itself.

A query is parsed into a series of terms and operators. A term can be a single word - **quick** or **brown** - or a phrase, surrounded by either double or single quotes - **"quick brown**" - which allows escaping operators and spaces. Unless escaped, terms are split by whitespace and consecutive numbers and letters are split into separate terms.

## Simple search

The simplest type of search is a single term string search.

By default, when you type a term you want to see in your results, Mezmo performs a prefix search.


{% code %}
{% tab language="bash" %}
healthcheck
{% /tab %}
{% /code %}


This will return all log lines with the word "healthcheck" in them.

## Exclude (NOT)

To perform a simple exclude search, prepend a dash to exclude results with that word.


{% code %}
{% tab language="bash" %}
-healthcheck
{% /tab %}
{% /code %}


This will return all log lines that do not contain the word `healthcheck`.

## Compound search

Multiple search terms and operators can help you quickly find a specific set of log lines. Please note that the AND and OR operators are case sensitive and must be entirely capitalized.

### AND operator

By default, multiple search terms are AND'd together.


{% code %}
{% tab language="bash" %}
healthcheck -successful
{% /tab %}
{% /code %}


This will return all log lines that contain the word `healthcheck` and do not contain the word `successful`

### OR operator

Specifying the OR operator returns results with either term.


{% code %}
{% tab language="bash" %}
healthcheck OR ping
{% /tab %}
{% /code %}


This will return all log lines that contain the word `healthcheck` or contain the word `ping`.

### Chained operators

By default, adjacent terms are AND'd together first.


{% code %}
{% tab language="bash" %}
healthcheck -successful OR ping
{% /tab %}
{% /code %}


This will return all log lines with the word `healthcheck` and **not** the word `successful`, as well as all log lines with the word `ping` in it.

### Parentheses

To explicitly specify operator precedence for your search terms, use parentheses.


{% code %}
{% tab language="bash" %}
healthcheck (-successful OR ping)
{% /tab %}
{% /code %}


This will return all log lines with the word `healthcheck` and without the word `successful`, as well as all log lines with the word `healthcheck` and with the word `ping`.

### Order of Operations

The order of operations are listed below:

- Grouping (...)
- Not -
- Or OR
- And AND or implicit white space between terms

This query `me myself OR I` is equivalent to  `me AND (myself OR I)` since OR operators have higher precedence than AND operators

Whereas the query `(me myself) OR I` is equivalent to `(me AND myself) OR I` since grouping operators have higher precedence than OR operators.

All remaining operators are at the same precedence as the grouping operators.

## Field search

For parsed log lines, you can specify a value for a given field in that log line.

### Default Behavior

By default, this is what Mezmo will assume about your search queries unless specified:

- All terms are case insensitive
- Prefix search is performed (searches for the beginning portion of the term)
- If no field is specified, the entire raw line is searched
- If the field is specified, only the field is searched

### Quick Reference of Field Search Operators


{% table %}
| Query | Behavior | Log line matches with | 
| ---- | ---- | ---- | 
| level:error | Prefix match, case insensitive | Error, error, errors | 
| level:=error | Prefix match, case sensitive | error, errors | 
| level:==error | Term match, case insensitive | error, Error | 
| level:===error | Term match, case sensitive | error | 
| level:[warning,error] | List of prefix matches, case insensitive | warning, Warning, Warnings, error, ERROR, errors, | 
| level:===[warning,error] | List of term matches, case sensitive | warning, error | 
| level:* | Checks if the field exists | All lines that contain the field level | 
{% /table %}

### Parsing

When a log line is parsed, you can search directly for a specific field value. We currently automatically parse the following types of log lines:

- [Akamai](/docs/akamai-cloud-monitor-logs#how-akamai-logs-are-parsed)
- Ansible
- Apache
- Aptible
- AWS CloudWatch
- AWS ELB
- AWS ECS
- AWS S3
- Cron
- Docker Swarm
- Docker Cloud/Compose
- GitHub
- Golang
- HAProxy
- Heroku
- HTTPD
- IIS Log
- JSON
- Logfmt
- LogSpout
- Rancher
- MongoDB
- Nagios
- Nginx
- PostgreSQL
- Redis
- Ruby/Rails
- Syslog
- Tomcat
- Windows Events

### JSON Parsing

As long as the log message ends in a `}`, your JSON object will be parsed, even if the JSON object does not span the entire message. If do not want your JSON object to be parsed, you can simply append an additional character after the ending `}` such as `.` a period.

If your JSON contains a `message` field, that field will be used for display and search in the log viewer. We also parse out (and override any existing) log levels if you include a `level` field.

### Root level field search

To search for a field with a particular value, use a colon to separate the field and value.


{% code %}
{% tab language="none" %}
response:404
{% /tab %}
{% /code %}


This will return all parsed log lines with the field `response` with a value of `404`.

### Nested field search

To search for a nested field, use periods to separate each nested field.


{% code %}
{% tab language="none" %}
user.id:12345
{% /tab %}
{% /code %}


This will return all log lines containing the following key value structure `{ "user": { "id": 12345 }}`

### Filters

Using the same field search syntax, you can also set filters directly in the search bar.


{% code %}
{% tab language="none" %}
host:myawesomehost -app:mycoolapp
{% /tab %}
{% /code %}


This will return all log lines that originate from the source `myawesomehost` and not from the app `mycoolapp`.

### Metadata

With the [REST API](/reference#api) or [Node.js library](https://www.npmjs.com/package/@mezmo/logger), you can upload a metadata object as part of a log line's context. To search for field values contained in the metadata object, use the `meta` prefix.


{% code %}
{% tab language="none" %}
meta.status_code:404
{% /tab %}
{% /code %}



{% callout type="info" title="Info" %}
When searching it is important to remember not to leave a space between the `field:` and then search term. For example
{% /callout %}


This will return results is `meta.weather.monday` has any entries for `rain`


{% code %}
{% tab language="none" %}
meta.weather.monday:rain
{% /tab %}
{% /code %}


This will not


{% code %}
{% tab language="none" %}
meta.weather.monday: rain
{% /tab %}
{% /code %}


This will return all log lines containing the context object with the following key value structure `{ "status_code": 404}`

## Field comparison operators

We support the following comparison operators for numeric parsed fields:


{% code %}
{% tab language="none" %}
* =
* <
* >
* <=
* >=
{% /tab %}
{% /code %}


### Field comparison search

To search for parsed fields matching comparison operators, use a colon followed by the comparison operator.


{% code %}
{% tab language="none" %}
response:>=400
{% /tab %}
{% /code %}


This will return all log lines with the field `response` with values greater than or equal to 400.

### Compound field comparison search

To form a compound field search query using comparison operators, use a colon followed by parentheses.


{% code %}
{% tab language="none" %}
response:(>=400 <500 -404)
{% /tab %}
{% /code %}


This will return all log lines with the field `response` with values greater than or equal to 400, less than 500, and not 404.

### Case-sensitive field search

To search for a case-sensitive parsed field, use a colon followed by an equal sign (=).


{% code %}
{% tab language="none" %}
name:=camelCasedName
{% /tab %}
{% /code %}


This will return all log lines with the field `name` with the case-sensitive string value `camelCasedName`.

### Existence field search

To search for the existence of a parsed field, use a colon followed by the asterisk (*).


{% code %}
{% tab language="none" %}
user:*
{% /tab %}
{% /code %}


This will return all log lines that have a value for the `user` field.

### Term match field search

By default, we perform a prefix search for all string fields. To search for an term match for a field value, use `==`.


{% code %}
{% tab language="none" %}
name:==bob
{% /tab %}
{% /code %}


This will return all lines with the exact name field value of `bob`, and will not match `bobby`.

### Term match case-sensitive field search

By default, we perform a prefix search for all string fields. To search for an exact match for a field value, use `===`.


{% code %}
{% tab language="none" %}
name:===Bob
{% /tab %}
{% /code %}


This will return all lines with the exact name field value of `Bob`, and will not match `bob` or `Bobby`.

## Special characters

There are a few behaviors for special characters to be aware of.

### Spaces

Due to the implicit AND'ing behavior described in the [Compound Search](#compound-search) section, searching for strings with spaces in them requires quotes.


{% code %}
{% tab language="none" %}
"job failed"
{% /tab %}
{% /code %}


This will only return log lines with the exact case-insensitive phrase `job failed`.


{% callout type="warning" title="When using lists, make sure not to add space or symbols when you separate the terms." %}
level:[warning,error] will behave as expected.
level:[warning, error] will search for entries of the field level which have "warning" or " error" with space included.
level:[warning,(error)] will search for entries of the field level which have "warning" or "(error)" with parenthesis included.
{% /callout %}


### Symbols

By default, if you include a symbol in your query, we will match your query exactly.


{% code %}
{% tab language="none" %}
%VARIABLE%
{% /tab %}
{% /code %}


This will return all log lines with `%VARIABLE%` in them.

### Colons

Since the colon is a reserved character for field search, quotes are required when searching for strings with colons in them.


{% code %}
{% tab language="none" %}
"response:"
{% /tab %}
{% /code %}


This will return all log lines with the string `response:` in them.

## Caveats

### Search Query Warnings

This warning `Unsupported visualizations query: symbols` is displayed whenever any symbols are used in a query, i.e. . / , +, etc. There is no issue with your query and search results. The warning shows up to let you know that the query was performed without the symbols to populate the  [Graphs](/docs/graphs) or [Timeline Graphs](https://mezmo.com/blog/log-timeline-its-about-time/). Additionally, to search for symbols such as + or - in your logline, they need to be wrapped with quotes (e.g. '+').

### Camel cased words and case sensitivity

When logs lines are stored and indexed in Elasticsearch, compound words with internal capitalization like `SyntaxError` get split up into separate words, `Syntax` and `Error`. This means that performing a search (defaults to case insensitive) for `syntaxerror` may not return lines containing that term because it was not stored that way. You will need to query for 'SyntaxError' to match the original form in this case.

