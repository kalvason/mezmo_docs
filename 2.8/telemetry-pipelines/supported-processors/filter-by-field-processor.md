---
type: page
title: Filter by Field Processor
listed: true
slug: filter-by-field-processor
description: 
index_title: Filter by Field Processor
hidden: 
keywords: 
tags: 
---

{% callout type="error" title="Deprecated" %}
This Processor has been deprecated. You should use the [auto$](/telemetry-pipelines/filter-processor) instead, which offers the ability to use multiple conditional statements for filter criteria.
{% /callout %}

## [Description](https://docs.mezmo.com/docs/filter-by-field-pipeline-processor#description)

The Filter by Field processor allows events to pass based on the presence of a specific key-value pair. Events that return `true` for the comparison operands are forwarded.

## [Use](https://docs.mezmo.com/docs/filter-by-field-pipeline-processor#use)

You can use this processor to drop events that may not be meaningful, or to reduce the total amount of data forwarded to a subsequent processor or destination. This can be useful, for example, for dropping events that may be DEBUG level and not needed for long term storage, or metrics that are zero and should not need to be recorded.

## [Configuration](https://docs.mezmo.com/docs/filter-by-field-pipeline-processor#configuration)

This processor uses a key and comparison operator to determine if a specific event should be forwarded. Comparison operations are primarily targeted at numeric values, though string comparison is supported in the **equal to** and **not equal to** operators**.**

There are three options to configure for this processor.

{% table %}
| Option | Description | Example | 
| ---- | ---- | ---- | 
| **Field** | The field you want to apply the filter to. | .`foo` | 
| **Operator** | The type of operator to use for the filter. | `greater` | 
| **Value** | The value for the operator to use. | `10` | 
{% /table %}

{% callout type="info" title="Values are Case Insensitive by Default" %}
The filter terms you enter for **Value** are treated as case-insensitive by default. Click the button next to the **Value** field to activate case-sensitivity.
{% /callout %}

## [Operators](https://docs.mezmo.com/docs/filter-by-field-pipeline-processor#operators)

### Contents Operators

{% table %}
| **Operator** | **Description** | **Example** | 
| ---- | ---- | ---- | 
| **Contains** | Accepts string values. Will drop the record if it does not contain the value in the string. | `bar` | 
| **Exists** | Drops the record if the field exists |  | 
| **Not Exists** | Drops the record if the field does not exist |  | 
{% /table %}

### String Operators

{% table %}
| **Operator** | **Description** | **Example** | 
| ---- | ---- | ---- | 
| **Ends With** | The contents of a given field ends with. | `bar` | 
| **Starts With** | The contents of a given field starts with. | `foo` | 
{% /table %}

### Comparison Operators

{% table %}
| **Operator** | **Description** | Example | 
| ---- | ---- | ---- | 
| **Greater** | Accepts only numeric values. | `10` | 
| **Greater or Equal** | Accepts only numeric values. | `10` | 
| **Less** | Accepts only numeric values. | `10` | 
| **Less or Equal** | Accepts only numeric values. | `10` | 
| **Equal** | Accepts both numeric and string values.  Does a string comparison on non string fields. | `bar` | 
| **Not Equal** | Accepts both numeric and  string values.  Does a string comparison on non string fields. | `bar` | 
{% /table %}

### Type Operators

{% table widths="0,477" %}
| Operator | Description | Example | 
| ---- | ---- | ---- | 
| **Is Array** | Drops the record if the field is not an array. | `[ "foo", "bar" ]` | 
| **Is Boolean** | Drops the record if the field is not a boolean. | `true` | 
| **Is Empty** | Drops the record if the field does not contain an empty string, array or object. | `""` | 
| **Is Null** | Drops the record if the field is not null. | `null` | 
| **Is Number** | Drops the record if the field is not a numeric. | `123.45` | 
| **Is Object** | Drops the record if the field is not an object. | `{ "foo": "bar" }` | 
| **Is String** | Drops the record if the field is not a string. | `"This is foo bar"` | 
{% /table %}

## Examples

### Filter Greater

#### Before

{% code %}
{% tab language="json" %}
{ "foo": 10 }
{ "foo": 20 }
{ "foo": "25" }
{ "foo": "bar" }
{% /tab %}
{% /code %}

#### Filter Options

{% table %}
| Option | Value | 
| ---- | ---- | 
| **Field** | `.foo` | 
| **Operator** | `greater` | 
| **Value** | `10` | 
{% /table %}

#### After

{% code %}
{% tab language="json" %}
{ "foo": 20 }
{% /tab %}
{% /code %}

### Filter Equals

#### Before

{% code %}
{% tab language="json" %}
{ "foo": 10 }
{ "foo": 20 }
{ "foo": "10" }
{ "foo": "bar" }
{% /tab %}
{% /code %}

#### Filter Options

{% table %}
| Option | Value | 
| ---- | ---- | 
| **Field** | `.foo` | 
| **Operator** | `equal` | 
| **Value** | `10` | 
{% /table %}

#### After

{% code %}
{% tab language="json" %}
{ "foo": 10 }
{ "foo": "10" }
{% /tab %}
{% /code %}

### Filter Contains

#### Before

{% code %}
{% tab language="json" %}
{ "foo": "setting the bar high." }
{ "foo": "setting the bar low." }
{ "foo": "below the BAR." }
{ "foo": "driving around town." }
{% /tab %}
{% /code %}

#### Filter Options

{% table %}
| Option | Value | 
| ---- | ---- | 
| **Field** | `.foo` | 
| **Operator** | `contains` | 
| **Value** | `10` | 
| **Case Sensitive** | `On` | 
{% /table %}

#### After

{% code %}
{% tab language="json" %}
{ "foo": "setting the bar high." }
{ "foo": "setting the bar low." }
{% /tab %}
{% /code %}

### Filter is Empty

#### Before

{% code %}
{% tab language="json" %}
{ "foo": "setting the bar high." }
{ "foo": "" }
{ "foo": null }
{ "foo": {} }
{ "foo": { "bar": "baz"} }
{ "foo": [] }
{ "foo": [ "bar" ] }
{% /tab %}
{% /code %}

#### Filter Options

{% table %}
| Option | Value | 
| ---- | ---- | 
| **Field** | `.foo` | 
| **Operator** | `is_empty` | 
{% /table %}

#### After

{% code %}
{% tab language="json" %}
{ "foo": "" }
{ "foo": {} }
{ "foo": [] }
{% /tab %}
{% /code %}

### Filter Debug Data

In some cases, log data streams include extraneous data such as Debug level information. These would normally not be needed in the production monitoring stream and can be discarded.

This example uses the `log level` field as a filtering operator to drop anything with a `DEBUG` value.

#### Before

{% code %}
{% tab language="json" %}
[{
"timestamp": "2022-12-23T12:34:56Z",
"level": "error",
"message": "There was an error processing the request",
"request_id": "1234567890",
"user_id": "abcdefghij"
},
{
"timestamp": "2022-12-23T12:34:56Z",
"level": "info",
"message": "User logged in",
"user_id": "abcdefghij",
"user_agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36"
},
{
"timestamp": "2022-12-23T12:34:56Z",
"level": "debug",
"message": "Server starting",
"server_id": "abcdefghij",
"start_time": "2022-12-23T12:30:00Z"
}]
{% /tab %}
{% /code %}

#### Filter Options

{% table %}
| Option | Value | 
| ---- | ---- | 
| **Field** | `.level` | 
| **Operator** | `not_equal` | 
| **Value** | `debug` | 
{% /table %}

#### After

{% code %}
{% tab language="json" %}
[{
"timestamp": "2022-12-23T12:34:56Z",
"level": "error",
"message": "There was an error processing the request",
"request_id": "1234567890",
"user_id": "abcdefghij"
},
{
"timestamp": "2022-12-23T12:34:56Z",
"level": "info",
"message": "User logged in",
"user_id": "abcdefghij",
"user_agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36"
}]
{% /tab %}
{% /code %}