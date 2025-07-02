---
type: page
title: Reduce Processor
listed: true
slug: reduce-processor
description: 
index_title: Reduce Processor
hidden: 
keywords: 
tags: 
---

## [Description](https://docs.mezmo.com/docs/reduce-pipeline-processor#description)

The Reduce processor takes multiple log input events and combines them into a single log event based on specified criteria.

## [Use](https://docs.mezmo.com/docs/reduce-pipeline-processor#use)

Reduce will combine many events into one over a window of time. **Only root-level properties are reduced**, so nested objects are not supported. Note that you could use the [auto$](/docs/flatten-field-pipeline-processor) if you want to reduce the nesting of the event.

You can configure how fields are "merged" on a per-field basis. If you don't specify the merge strategy, the **default** merge strategy for each reduced event follows this pattern:

- **String fields** - The first value is kept while successive ones are discarded
- **Number fields** - The values are summed, and that result becomes the value of the field
- **Date fields** - The first date is kept, and the last one will be placed in a new field suffixed by `_end`

**Dates**

Most Pipeline dates will be serialized. You can tell Reduce how to parse your dates by using `date_formats` to specify the location of any date fields, and their [expected format](https://docs.rs/chrono/0.4.23/chrono/format/strftime/index.html#specifiers).

Examples:

- A '`datestamp'` field in ISO format; Like 2023-01-02T16:56:15.387Z"`{ field: 'datestamp', format: '%Y-%m-%dT%H:%M:%S.%3fZ'}`
- A field named `'epoch'` that has either an integer or string `{ field: 'epoch', format: '%s'}`

Dates will be returned in the same data type that they were submitted. For example, an epoch date that comes in as `epoch: 1671134262` will be returned as integer epochs, while `epoch: '1671134262'` will be returned as string epochs.

## [Configuration](https://docs.mezmo.com/docs/reduce-pipeline-processor#configuration)

There are three options to configure for this processor. Note that two of these can have any number of values specified.

{% table %}
| Option | Description | Example | 
| ---- | ---- | ---- | 
| **Duration** | The total window of time over which to run the reduction | `3000ms (default)` | 
| **Group By** | The incoming event fields to group. If none are specified, all events are combined. | `.level` | 
| **Merge Strategy** | Determines how the contents of a specified field will be treated when added to the combined event. |  | 
{% /table %}

### [Merge Options](https://docs.mezmo.com/docs/reduce-pipeline-processor#merge-options)

The merge options define how the fields will be combined. Note that certain strategies require numeric values in order to function.

{% table %}
| Option | Description | Required Input Type | 
| ---- | ---- | ---- | 
| **Array** | Append each value to an array. | Array | 
| **Concatenate** | Concatenate each string value and separate with a space. | String | 
| **Concatenate New Line** | Concatenate each string value and add to a new line. | String | 
| **Discard** | Discard all values except the first one detected. | Any | 
| **Flat Unique** | Create a flattened array of all unique values. | Any | 
| **Longest Array** | Keep the longest array detected. | Array | 
| **Maximum** | Keep the largest numeric value detected. | Numeric | 
| **Minimum** | Keep the smallest numeric value detected. | Numeric | 
| **Retain** | Discard every value except the last one detected.\n\n\n\nUse this option to coalesce values by not retaining null. | Any | 
{% /table %}