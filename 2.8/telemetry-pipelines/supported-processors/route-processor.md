---
type: page
title: Route Processor
listed: true
slug: route-processor
description: 
index_title: Route Processor
hidden: 
keywords: 
tags: 
---


## [Description](https://docs.mezmo.com/docs/route-pipeline-processor#description)

With the Route processor, you can separate events from a single stream into multiple streams. This allows you to choose the next processor or destination to which an event is sent.

## [Use](https://docs.mezmo.com/docs/route-pipeline-processor#use)

A typical use of this processor would be to route processed log data to different destinations, for example sending one set of log events to storage, and another to Mezmo Log Analysis.

## [Configuration](https://docs.mezmo.com/docs/route-pipeline-processor#configuration)

The Route processor determines where to send the log data based on a conditional statement applied to a specified field. The format of this conditional statement is: `Field (comparison operator) Value`. You can add conditions including AND and OR, as well as nested expressions. A Route Processor can contain multiple conditional statements.

{% callout type="info" title="Value is Case Insensitive by Default" %}
The filter terms you enter for **Value** are treated as case-insensitive by default. Click the button next to the **Value** field to activate case-sensitivity.
{% /callout %}

## Interactive Demo

The topic [auto$](/practioner-guide-data-optimization/pipeline-module--route) contains an interactive demo for using the Route Processor to combine data from multiple sources and send it along specific Pipeline branches for processing, along with a tutorial for experimenting with demo data.

## Exclusivity

The routes are not in a sequential order of operation. Any conditional expression that matches sends a copy of the matching event through to the subsequent step.

If you want to make the routes exclusive, make that you create the conditions to oppose sending events down multiple paths if needed.

## [Operators and Conditions](https://docs.mezmo.com/docs/route-pipeline-processor#operators-and-conditions)

Logical conditions are used to determine when a specific event qualifies for sending on to a subsequent step. Each condition uses a source field, operator, and potentially an evaluation to return a true-false result.

### Comparison Operators

{% table %}

{% table %}
| Operator | Description | 
| ---- | ---- | 
| Equals | Compares the values for equivalency. \n\n\n\n\n\n\n\nThe specified value can be a number or a string. | 
| Not Equals | Compares the values for non-equivalency. \n\n\n\n\nThe specified value can be a number \n\n\n\nor a string. | 
| Greater Than | If the specified field value is greater, this returns true. \n\n\n\n\n\n\n\nThis comparison only works for numeric values. | 
| Greater Than or Equal | If the specified field value is greater or equivalent, this returns true. \n\n\n\n\n\n\n\nThis comparison only works for numeric values. | 
| Less Than | If the specified field value is less than, this returns true. \n\n\n\n\n\n\n\nThis comparison only works for numeric values. | 
| Less Than or Equal | If the specified field value is less than or equivalent, this returns true. \n\n\n\n\n\n\n\nThis comparison only works for numeric values. | 
{% /table %}

{% /table %}

### Contents Operators

{% table %}

{% table %}
| Operator | Description | 
| ---- | ---- | 
| Not Contains | This operator looks for a specified string to not exist anywhere within the value of the field. | 
| Contains | This operator looks for a specified string to exist anywhere within the value of the field. | 
| Exists | Returns true if the specified field exists regardless of the value. | 
| Not Exists | Returns true if the specified field does not exist regardless of the value. | 
| Is IP in CIDR Range | Route events based on their IPv4 or IPv6 range | 
{% /table %}

{% /table %}

### [Type Operators](https://docs.mezmo.com/docs/route-pipeline-processor#type-operators)

{% table %}

{% table %}
| **Operator** | Description | 
| ---- | ---- | 
| Is Array | Checks if the field contains an array | 
| Is Boolean | Checks if the field contains a Boolean value | 
| Is Empty | Checks if the field is empty | 
| Is Null | Checks if the field value is null | 
| Is Number | Checks if the field contains a number | 
| Is Object | Checks if the field is an object | 
| Is String | Checks if the field value is a string | 
{% /table %}

{% /table %}

### [String Operators](https://docs.mezmo.com/docs/route-pipeline-processor#string-operators)

{% table widths="485,0,0" %}

{% table %}
| **Operator** |  |  |  | 
| ---- | ---- | ---- | ---- | 
| Ends with |  |  |  | 
| Starts with |  |  |  | 
{% /table %}

{% /table %}

## [Example](https://docs.mezmo.com/docs/route-pipeline-processor#examples)

{% table %}

{% table %}
| Conditional Statement | Result | 
| ---- | ---- | 
| `IF transaction.result equal success`\n\n\n\n\n\n\n\n`AND transaction.total_price is_greater_or_equal_to 0` | Checks the fields `transaction.result`and `transaction.total_price`for the values shown, and if a match is found, sends that data to the Encryption Processor chain. | 
| `IF transaction.result equal fail`\n\n\n\n\n\n\n\n`AND transaction.total_price not 0` | Checks the fields `transaction.result`and `transaction.total_price`for the values shown, and if a match is found, sends that data to the Encryption Processor chain. | 
{% /table %}

{% /table %}