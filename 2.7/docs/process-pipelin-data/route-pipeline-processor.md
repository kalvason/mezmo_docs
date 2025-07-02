---
type: page
title: Route Processor
listed: true
slug: route-pipeline-processor
description: 
index_title: Route Processor
hidden: 
keywords: 
tags: 
---

## Description

With the Route processor, you can separate events from a single stream into multiple streams. This allows you to choose the next processor or destination to which an event is sent.

## Use

A typical use of this processor would be to route processed log data to different destinations, for example sending one set of log events to storage, and another to Mezmo Log Analysis. 

## Configuration

The Route processor determines where to send the log data based on a conditional statement applied to a specified field. The format of this conditional statement is: `Field (comparison operator) Value`. You can add conditions including AND and OR, as well as nested expressions. A Route Processor can contain multiple conditional statements.

## Operators and Conditions

Logical conditions are used to determine when a specific event qualifies  for sending on to a subsequent step. Each condition uses a source  field, operator, and potentially an evaluation to return a true-false  result.

### Comparison Operators

{% table %}
| Operator | Description | 
| ---- | ---- | 
| Equals | Compares the values for equivalency. \n\n\n\nThe specified value can be a number or a string. | 
| Not Equals | Compares the values for non-equivalency. \n\n\nThe specified value can be a number \n\nor a string. | 
| Greater Than | If the specified field value is greater, this returns true. \n\n\n\nThis comparison only works for numeric values. | 
| Greater Than or Equal | If the specified field value is greater or equivalent, this returns true. \n\n\n\nThis comparison only works for numeric values. | 
| Less Than | If the specified field value is less than, this returns true. \n\n\n\nThis comparison only works for numeric values. | 
| Less Than or Equal | If the specified field value is less than or equivalent, this returns true. \n\n\n\nThis comparison only works for numeric values. | 
{% /table %}

### Contents Operators

{% table %}
| Operator | Description | 
| ---- | ---- | 
| Contains | This operator looks for a specified string to exist anywhere within the value of the field. | 
| Exists | Returns true if the specified field exists regardless of the value. | 
| Not Exists | Returns true if the specified field does not exist regardless of the value. | 
{% /table %}

### Type Operators

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

### String Operators

{% table widths="485,0,0" %}
| **Operator** |  |  |  | 
| ---- | ---- | ---- | ---- | 
| Ends with |  |  |  | 
| Starts with |  |  |  | 
{% /table %}

## Examples

The topic [auto$](/docs/pipeline-architecture--encrypt--drop--and-route-data-to-amazon-s) provides an example of using the Route Processor to send data containing credit card information through a series of Encrypt Processors before storing it in an Amazon S3 bucket. The conditional statements shown here are from that example, and use comparison operators to identify transaction information. 

{% table %}
| Conditional Statement | Result | 
| ---- | ---- | 
| `IF transaction.result equal success`\n\n\n\n`AND transaction.total_price is_greater_or_equal_to 0` | Checks the fields `transaction.result`and `transaction.total_price`for the values shown, and if a match is found, sends that data to the Encryption Processor chain. | 
| `IF transaction.result equal fail`\n\n\n\n`AND transaction.total_price not 0` | Checks the fields `transaction.result`and `transaction.total_price`for the values shown, and if a match is found, sends that data to the Encryption Processor chain. | 
{% /table %}