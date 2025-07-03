---
type: page
title: Grok Pattern Reference
listed: true
slug: using-grok-to-parse
description: 
index_title: Grok Pattern Reference
hidden: 
keywords: 
tags: 
---


Grok is a powerful tool for extracting structured data from unstructured text. Grok syntax is composed of reusable elements called G**rok patterns** that enable parsing for data such as timestamps, IP addresses, hostnames, log levels, and more.The prebuilt patterns make Grok easier to use than defining new regular expressions to extract structured data, especially for long text strings.

{% callout type="warning" title="Unique Mezmo Patterns for Grok" %}
Mezmo has some unique requirements for using Grok patterns, such as restricting the use of literals and regex between patterns, as described in the section on **Unique Mezmo Grok Patterns**, which also describes alternative shortcuts to use instead.
{% /callout %}

## Key Concepts for Using Grok

Grok patterns follow the syntax: `%{PATTERN TO MATCH:output label}`

- `PATTERN TO MATCH`: this is the pattern to match on
    - Many patterns are predefined and available for review within the [Logstash repository](https://github.com/hpcugent/logstash-patterns/blob/master/files/grok-patterns).
    - **Example**: `%{TIMESTAMP_ISO8601}` extracts an ISO 8601 timestamp
    - **Example**: `%{IP}` extracts any IPv4 or IPv6 value

- `output label`: the name of the key to use for the parsed data (optional)
    - While the `output label` is optional, if you don't specify a label, the extracted data is dropped and will not be included in the output
    - **Example:** `%{TIMESTAMP_ISO8601:timestamp}` extracts an ISO 8601 timestamp, and then outputs the result with the output label as `timestamp`:  `{"timestamp": "2022-09-27 18:00:00.000"}`

By combining multiple Grok patterns you can parse a single line of text and extract the relevant information into structured data.

## Unique Mezmo Grok Patterns

Standard Grok usage allows for characters between the pattern syntax. These can include literal characters, as well as regular expressions. **Mezmo does not allow any characters between Grok patterns other than** `\s,;:-`.

Instead, Mezmo recommends using one or more of the the patterns described here to aid in jumping over interstitial data. When you use these patterns  between recognized patterns, you will usually automatically span the appropriate characters.

{% table widths="163" %}

{% table %}
| Pattern | Usage | 
| ---- | ---- | 
| `%{GREEDYDATA}` | This pattern serves as an excellent starting point for building any Grok expression. This will match an entire line of data, or until you specify another expression to buffer it.\n\n\n\n\n\n\n\nThis pattern is often used for the remainder of any line not parsed. | 
| `%{DATA}` | This pattern uses a lazy loading with any character count from zero to many, until it is succeeded by another expression, or it reaches the end of the line.\n\n\n\n\n\n\n\nThis means you can use this pattern with other patterns to "bookend" a larger set of interstitial data. | 
{% /table %}

{% /table %}

Sometimes you will be unable to span the appropriate characters using these patterns. You can also employ the following patterns to aid in more specific advancement:

{% table %}

{% table %}
| Pattern | Usage | 
| ---- | ---- | 
| `%{SPACE}` | Use this pattern to explicitly jump over whitespace if needed. | 
| `%{NOTSPACE}` | This pattern is useful for skipping sets of characters between whitespaces. | 
| `%{WORD}` | This will match whole words within text. | 
| `%{QS}` or `%{QUOTEDSTRING}` | Use this pattern to extract sets of characters between quotes. | 
{% /table %}

{% /table %}

## Usage Examples

### Simple Log Line

Given this log line, parse it into the individual data fields:

`2022-12-23T18:33:21Z | WARN | User object with the id ’420’ was not found`

This example includes a timestamp, a log level, and a log message. We will tackle parsing this line iteratively to see the results as we go.

We can start with a `%{GREEDYDATA:message}` to get the whole line. Subsequent iterations add to the patterns to extract the individual values.


#### **Iteration 1**

**Pattern:** `%{GREEDYDATA:message}`

**Output:**

{% code %}
{% tab language="json" %}
{
"message":"2022-12-23T18:33:21Z | WARN | User object with the id ’420’ was not found"
}
{% /tab %}
{% /code %}


#### **Iteration 2**

Extract the timestamp from the beginning of the line, which is a standard ISO timestamp.

Note that we added a space between the timestamp pattern and greedy data. Spaces between patterns are treated as literals in Grok.

**Pattern:** `%{TIMESTAMP_ISO8601:timestamp} %{GREEDYDATA:message}`

**Output:**

This yields the `timestamp` as a separate field and the remainder of the message line in the `message` field

{% code %}
{% tab language="json" %}
{
"message":"| WARN | User object with the id ’420’ was not found"
"timestamp":"2022-12-23T18:33:21Z"
}
{% /tab %}
{% /code %}

**Iteration 3**

Now we need to get the `WARN` and assign it to the log level. This means we'll need to use an interstitial pattern that is not greedy, so we'll use `%{DATA}`.

**Pattern:** `%{TIMESTAMP_ISO8601:timestamp} %{DATA} %{GREEDYDATA:message}`

**Output:**

Unfortunately, because `%{DATA}` is a lazy pattern, the spaces between the pipes and the log level in combination with the `%{GREEDYDATA}` pattern means that Grok doesn't try to jump to the message. We don't get the desired result yet for the `level`  field. We need to help Grok manually jump over the vertical pipes.

{% code %}
{% tab language="json" %}
{
"message":"| WARN | User object with the id ’420’ was not found"
"timestamp":"2022-12-23T18:33:21Z"
}
{% /tab %}
{% /code %}

**Iteration 4 (Final)**

Let's use the `%{WORD}` pattern combined with the `%{DATA}` pattern to see if we can extract the `level` .

**Pattern:** `%{TIMESTAMP_ISO8601:timestamp} %{DATA} %{WORD:level} %{DATA} %{GREEDYDATA:message}`

**Output:**

Now we've got the full object and the pipes are dropped because they had no associated label defined.

{% code %}
{% tab language="json" %}
{
"level":"WARN"
"message":"User object with the id ’420’ was not found"
"timestamp":"2022-12-23T18:33:21Z"
}
{% /tab %}
{% /code %}

{% callout type="info" title="%(WORD) Instead of %(DATA)" %}
We could have also used the pattern `%{DATA}` instead of `%{WORD}` in this example. However, knowing log level was always a single word, we illustrated the `%{WORD}` pattern.
{% /callout %}

### Hypothetical for Embedded Metrics

Let's take an example where metrics are being included within a log line and need to be explicitly extracted.

{% code %}
{% tab language="none" %}
Mar 23 14:46:29 api-gateway-23 apigateway info GET 200 /api/transactions?offset=0&limit=999 18.580795ms
{% /tab %}
{% /code %}

**Iteration 1**

**Pattern:** `%{SYSLOGTIMESTAMP:timestamp} %{SYSLOGHOST:host} %{DATA:service} %{LOGLEVEL:level} %{WORD:method} %{NUMBER:response} %{GREEDYDATA:message}`

**Output:**

At first try, we can pull the timestamp, host, service, log level, method, and response quickly while greedy data captures the remainder. Next, we need to get the URI and the metric value we want at the end.

Note that the JSON view does not show escape characters that are present in the raw data.

{% code %}
{% tab language="json" %}
{
"host":"api-gateway-23",
"level":"info",
"method":"GET",
"message":"/api/transactions?offset=0&limit=999 18.580795ms",
"response":"200",
"service":"apigateway",
"timestamp":"Mar 23 14:46:29"
}
{% /tab %}
{% /code %}

**Iteration 2**

**Pattern**: `%{SYSLOGTIMESTAMP:timestamp} %{SYSLOGHOST:host} %{DATA:service} %{LOGLEVEL:level} %{WORD:method} %{NUMBER:response} %{URIPATH:path}%{URIPARAM:params} %{NUMBER:value}%{NOTSPACE:unit}`

**Output:**

We need to remove the path of the URI and the parameters separately as those are both within the string. That leaves only the value with the unit of milliseconds (ms) left.

The value is not an integer, but a floating point. The pattern for `NUMBER`  can be used to get the numeric values with the trailing decimals. This ensures we don't grab the `ms`  at the end. If we want to preserve the `ms`  as the units, we can use the `NOTSPACE`  option as it will grab alphanumeric characters.

**Note that we did not leave a space between the URI options or the NUMBER and NOTSPACE patterns because no space exists within the line.**

{% code %}
{% tab language="json" %}
{
"host":"api-gateway-23",
"level":"info",
"method":"GET",
"params":"?offset=0&limit=999",
"path":"/api/transactions",
"response":"200",
"service":"apigateway",
"timestamp":"Mar 23 14:46:29",
"unit":"ms",
"value":"18.580795"
}
{% /tab %}
{% /code %}

{% callout type="info" title="No Support for Number Data" %}
Currently Mezmo's grok patterns do not support the additional type capability for numbers and other data types, such as `%{NUMBER:field:int}`, where `int` represents the output format in the parsed data. You will need to add an additional processor to coerce the data into the appropriate format after parsing.
{% /callout %}

## Mezmo-supported Grok Patterns

This is not an exhaustive list. You can find additional pattern information in the **Other Resources** section if you need further reference.

### Custom Patterns

These patterns are specific to Mezmo and can be very useful in common scenarios involving extracting data from logs.

{% callout type="warning" title="Use Parse Processor to Separate Objects" %}
Many of these patterns will work for specific circumstances, but cases like `JSON_OBJECT` and `JSON_ARRAY` are not isolated to single objects within a string. They do not count the number of occurrences.

For example, if you have multiple JSON objects in a string, you would return both objects and the characters that are in between them. We recommend separating the objects using the [auto$](/telemetry-pipelines/parse-processor) prior to trying to use the `JSON_OBJECT` pattern to prevent the return of invalid JSON.
{% /callout %}

{% table %}

{% table %}
| Pattern | Expression | Usage | 
| ---- | ---- | ---- | 
| **ANY_CHAR** | `r#"."#` | Matches any **single** valid character. Useful for advancing by just one character until the next pattern. | 
| **CURLY_BRACKET** | `r#"{&#124;}"#` | Matches any single `{`  open or }  closed curly bracket. | 
| **DOUBLE_QUOTE** | `r#"""#` | Matches any single " double quote. | 
| **JSON_ARRAY** | `r#"\[.*\]"#` | Matches any embedded JSON array between square brackets.\n\n\n\n\n\n\n\nNote that this will match all arrays, not just one. If multiple arrays are present, separate them in a prior parse first. | 
| **JSON_OBJECT** | `r#"{.*}"#` | Matches any embedded JSON object between curly braces.\n\n\n\n\n\n\n\nNote that this will match all objects, not just one. If multiple objects are present, separate them in a prior parse first. | 
| **OPTIONAL_SENTENCE** | `r#"[\p{L},":;\s\-]*"#` | Matches any human readable sentence with UTF-8 characters that includes words, spaces, and punctuation, but is greedy | 
| **PERIOD_CHAR** | `r#"\."#` | Matches any single `.`  period character. | 
| **SENTENCE** | `r#"[\p{L},":;\s\-]+"#` | Matches any human readable sentence with UTF-8 characters that includes words, spaces, and punctation. | 
| **SINGLE_QUOTE** | `r#"'"#` | Matches any `'` single quote character. | 
| **SINGLE_SPACE** | `r#"\s"#` | Matches a single space.\n\n\n\n\n\n\n\nNote that this is different than the standard SPACE pattern, which is greedy and will return multiple spaces or tabs if they are present. | 
| **TAB** | `r#"\t"#` | Matches any tab character, which may be present in the form `\t` . | 
| **UTF8_WORD** | `r#"\p{L}+"#` |  | 
| **XML** | `r#"<[\w"=\s]+>.*<\/[\w\s]+>"#` | Matches any embedded XML object between .\n\n\n\n\n\n\n\nNote that this will match all objects, not just one. If multiple objects are present, separate them in a prior parse first. | 
{% /table %}

{% /table %}

### Common Patterns

These patterns are frequently used within Grok expressions.

{% callout type="info" title="Aliased and Combined Patterns" %}
Note that certain Grok patterns are aliases or a combination of other patterns. They can be used as shortcuts however for extracting more
{% /callout %}

{% table widths="0,296" %}

{% table %}
| Pattern | Expression | Usage | 
| ---- | ---- | ---- | 
| **USERNAME or USER** | `[a-zA-Z0-9._-]+` | Matches content that contains letters, digits, plus the characters `. _-.` | 
| **EMAILLOCALPART** | `[a-zA-Z][a-zA-Z0-9_.+-=:]+` | Matches the characters before the `@`sign in an email address. \n\n\n\n\n\n\n\nFor example, in the email address `user@mezmo.com` , the matched content is `user` . | 
| **EMAILADDRESS** | `%{EMAILLOCALPART}@%{HOSTNAME}` | Matches email addresses formats where the pattern is `<account_name>@<domain.com>`. | 
| **HTTPDUSER** | `%{EMAILADDRESS}&#124;%{USER}` | Matches either an email address or username. Especially useful for cases where usernames may be a mix of either type. | 
| **INT** | `(?:[+-]?(?:[0-9]+))` | Matches integer (whole) numbers. | 
| **BASE10NUM** | `(?<![0-9.+-])(?>[+-]?(?:(?:[0-9]+(?:.[0-9]+)?)&#124;(?:.[0-9]+)))` | Matches decimal numbers. | 
| **NUMBER** | `(?:%{BASE10NUM})` | Matches | 
| **BASE16NUM** | `(?<![0-9A-Fa-f])(?:[+-]?(?:0x)?(?:[0-9A-Fa-f]+))` | Matches hexadecimal numbers (0-9,A-F). | 
| **BASE16FLOAT** | `\b(?<![0-9A-Fa-f.])(?:[+-]?(?:0x)?(?:(?:[0-9A-Fa-f]+(?:.[0-9A-Fa-f]*)?)&#124;(?:.[0-9A-Fa-f]+)))\b` | Matches hexadecimal floating point numbers. | 
| **POSINT** | `\b(?:[1-9][0-9]*)\b` | Matches positive integers only | 
| **NONNEGINT** | `\b(?:[0-9]+)\b` | Matches non-negative integers including zero. | 
| **WORD** | `\b\w+\b` | Matches letters, digits, and underscores (_) separated by spaces. | 
| **NOTSPACE** | `\S+` | Matches any character that is not a whitespace character (spaces, tabs, line breaks). | 
| **SPACE** | `\s*` | Matches one or more of any whitespace character (spaces, tabs, line breaks) | 
| **DATA** | .`*?` | Matches between zero and unlimited times, as few times as possible, expanding as needed | 
| **GREEDYDATA** | .`*` | Matches zero or multiple characters until the end of the line | 
| **QS** or **QUOTEDSTRING** | ``(?&gt;(?&lt;!)(?&gt;"(?&gt;.&#124;[^"]+)+"&#124;""&#124;(?&gt;'(?&gt;.&#124;[^']+)+')&#124;''&#124;(?&gt;(?&gt;\\.&#124;[^\\ ]+)+`)&#124;``))`` | Matches content between quotes.\n\n\n\n\n\n\n\nNote that this pattern can return double quotes in the output, so `%{DATA}` is typically better to use. | 
| **UUID** | `[A-Fa-f0-9]{8}-(?:[A-Fa-f0-9]{4}-){3}[A-Fa-f0-9]{12}` | Matches any standard set of characters in a universally unique identifier () | 
{% /table %}

{% /table %}

## Other Resources

- The [Logstash repository](https://github.com/hpcugent/logstash-patterns/blob/master/files/grok-patterns) for supported Grok patterns.
- [Grokdebugger.com](https://grokdebugger.com), a site for building and testing Grok patterns.
- [Elastic tutorial](https://www.elastic.co/blog/slow-and-steady-how-to-build-custom-grok-patterns-incrementally) on using Grok.