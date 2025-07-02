---
type: page
title: Script Execution Processor
listed: true
slug: js-script-processor
description: 
index_title: Script Execution Processor
hidden: 
keywords: 
tags: 
---

## Description

This Processor enables you to use a subset of JavaScript to transform your data, which can significantly simplify your Pipeline map.You can combine multiple actions like filtering, dropping, mapping, and casting inside of a single script.

{% callout type="info" title="Limited Command Execution" %}
This processor has specific limitations on command execution, as described in the section on **Known Limitations**.
{% /callout %}

## Configuration

{% table %}
| Option | Description | 
| ---- | ---- | 
| `Script` | The JavaScript code to transform your data | 
{% /table %}

{% code %}
{% tab language="javascript" title="Example" %}
function processEvent(message, metadata, timestamp, annotations) {
  if (message.total_users > 5) {
    return message
  }
  
  return null // Drop it
}
{% /tab %}
{% /code %}

### Main Function

With the JavaScript processor you can define a single function to encapsulate the logic for processing an event. This function can be named whatever you want, but  by default is called `processEvent`. This function has up to three arguments that you can declare positionally, by any name.

{% table widths="145" %}
| Parameter | Description | 
| ---- | ---- | 
| `message` | This is a reference to the actual message that flows through this processor | 
| `metadata` (optional) | The metadata associated with the event | 
| `timestamp`\n\n(optional) | The timestamp associated with this event.  In some automated parsing sources we will try and extract the timestamp from the incoming event, but for the most part this timestamp will be set to the time we received the event. | 
| `annotations` (optional) | The annotations object for the event. In scenarios where you have created a [Data Profile](/telemetry-pipelines/data-profiling), classification information such as event type, message type, and total bytes will be present. | 
{% /table %}

The function must return a value on all paths. The returned object (modified, replaced, or otherwise) becomes the message downstream. Returning `null` causes the message to be dropped (no event is propagated). Modified metadata is propagated with the message.

### Global Functions

These functions are available to use on any respective value. At this time, these are the only supported global operations. There is no support for global objects like `Math`, `Array`, `Map`, or `Set`, except for `Object`, `JSON` and `Date` objects.

{% table widths="252" %}
| Function | Description | 
| ---- | ---- | 
| `Date.now()` | Returns the number of milliseconds elapsed since the [epoch](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date#the_epoch_timestamps_and_invalid_date), which is defined as the midnight at the beginning of January 1, 1970, UTC. | 
| `Date.parse(date_string, unit)` | Parses a string representation of a date, and returns and returns the number of milliseconds elapsed since the [epoch](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date#the_epoch_timestamps_and_invalid_date). It defaults to `null` when parsing fails.\n\n\nUnit indicates the scale of units to return (`seconds`, `milliseconds` or `nanoseconds`) and defaults to `milliseconds`. | 
| `new Date()` | Returns a timestamp representing the time of processing of this script. | 
| `new Date(date_string)` | Parses `date_string` to produce a timestamp.  The following formats are supported - ISO8601, W3C, Apache, nginx:\n\n\n`%+`\n\n\n\n`%Y-%m-%d %T%.f%#z`\n\n\n`%Y-%m-%d %T%.f`\n\n\n`%d/%b/%Y:%T%.f %z`\n\n\n\n`%Y/%m/%d %T%.f`\n\n\n\n`%Y/%m/%d %T%.f#z` | 
| `JSON.parse(json_string)` | Parses a JSON string into a JS type. It defaults to `null` when parsing fails. | 
| `JSON.stringify(value)` | Converts a JavaScript value to a JSON string. You should use this for converting any JSON object, instead of the `toString()` method. | 
| `Object.entries(value)` | Returns an array of property key-value pairs of the spedified object. It returns an empty array when the provided value is not an object, or `null`. | 
| `Object.keys(value)` | Returns an array of property keys of the provided object. It returns an empty array when the provided value is not an object or `null`. | 
| `parseInt(value)` | Attempts to parse the data as an integer and returns the integer. It defaults to `0`when it fails. | 
| `parseFloat(value)` | Attempts to parse the data as a float and returns the float. It defaults to `0.0`when it fails. | 
| `parseGrok(value, pattern)` | Parses the `value` using [a grok pattern](https://www.elastic.co/blog/do-you-grok-grok).\nNote that only these literals are supported between expression:`\s,;:-` | 
| `toString()` | Casts an object to a string. Returns an empty string for null values. | 
{% /table %}

{% code %}
{% tab language="javascript" %}
function processEvent(event) {
  if (parseInt(event.myProperty) == 1 || parseFloat(event.myProperty2) == 2.1) {
  	return event.myProperty.toString()
  }
}
{% /tab %}
{% /code %}

### Comparison Operators

This processor supports all basic comparison operators that are defined in JavaScript.

{% table %}
| Operator | Description | 
| ---- | ---- | 
| &gt; | Greater Than | 
| &gt;= | Greater Than or Equal To | 
| &lt; | Less Than | 
| &lt;= | Less Than or Equal To | 
| == or === | Equal.  **Note**: This has strict type checking whether it's defined as `==` or `===` | 
| != or !== | Not Equal. **Note**: This has strict type checking whether it's defined as `==` or `===` | 
{% /table %}

### Arithmetic Operators

An arithmetic operator takes numerical values as their operands and returns a single numerical value.

{% table widths="279" %}
| Operator | Description | 
| ---- | ---- | 
| + | Addition | 
| - | Subtraction | 
| * | Multiplication | 
| / | Division | 
{% /table %}

### String Operations

String operations supported follow the standard Javascript conventions.

{% table %}
| Operator | Description | 
| ---- | ---- | 
| + | Concatenates two strings together | 
| .endsWith(substring) | Checks whether a string ends with `substring.` | 
| .startsWith(substring) | Checks whether a string starts with `substring.` | 
| .at() | Retrieve an character at the specific index from a string (more readable) | 
| .charAt() | Retrieve an character at the specific index from a string | 
| .indexOf() | Return the first index of a value in a string | 
| .lastIndexOf() | Return the last index of a value in a string | 
| .length | Returns the number of characters in a string\n\n\n\n_Note that to avoid collisions with a field name of_ `.length`_the function checks to ensure that field does not exist first. If it does, it will return the value of the field, not the computed length._ | 
| .padEnd() | Adds additional specified characters to the end of a string | 
| .padStart() | Adds additional specified characters to the beginning of a string | 
| .repeat() | Returns a new string with a number of copies of the original string | 
| .slice() | Extracts the specified portion of the string by index, defaulting to the end of the string if only one index is specified | 
| .substring() | Extracts a specified portion of the string between the indexes given | 
| .toLowerCase() | Changes all string characters to lower case letters | 
| .toUpperCase() | Changes all string characters to upper case letters | 
| .trim() | Removes whitespaces from both sides of the string | 
| .trimEnd() | Removes whitespaces from the end of the string | 
| .trimStart() | Removes whitespaces from the beginning of the string | 
{% /table %}

### Function-Scoped Variables

Variables can be defined and used inside of the main `processEvent` function. To use one, define a variable with the `let`  keyword.

{% code %}
{% tab language="javascript" %}
let myVar = 1
{% /tab %}
{% /code %}

### Deleting Attributes

Attributes can be deleted from an object by assigning `undefined` .

{% code %}
{% tab language="javascript" %}
message.attr = undefined
{% /tab %}
{% /code %}

## Examples

### Filter Events

{% code %}
{% tab language="javascript" title="Filter Event" %}
// Fitering an event	
function processEvent(message, metadata, timestamp, annotations) {
  if (message.code == 102) {
    return message // Pass the event through
  }

  return null // Drop it
}
{% /tab %}
{% /code %}

### Adding Properties to an Event

{% code %}
{% tab language="javascript" title="Add property to event" %}
// Simple assignment
function processEvent(message, metadata, timestamp, annotations) {
  if (message.sample === 'something') {
    message.newProperty = 'ITS_SOMETHING'
  }
  return message
}
{% /tab %}
{% /code %}

### Removing Properties from an Event

{% code %}
{% tab language="javascript" title="Remove property from event" %}
// Remove property from event
// Set the value to null on a property or subset of properties to remove it from the message
function processEvent(message, metadata, timestamp, annotations) {
  message.total = null
  message.summary.description = null
  return message
}
{% /tab %}
{% /code %}

### Parsing Numbers

{% code %}
{% tab language="javascript" title="Parsing" %}
// Using parseInt and parseFloat
function processEvent(message, metadata, timestamp, annotations) {
  message.total = parseInt(message.dollars) + parseFloat(message.change)
  return message
}
{% /tab %}
{% /code %}

### Convert To String

{% code %}
{% tab language="javascript" title="Convert to String" %}
// Using toString()
function processEvent(message, metadata, timestamp, annotations) {
  message.total = message.total.toString()
  return message
}
{% /tab %}
{% /code %}

### Counting the Number of Bytes in a Message

This example shows how you can compute the size of the event payload using combined functions. This returns the amount of the size in bytes by assuming that each character is 1 byte (8 bit ASCII characters).

{% code %}
{% tab language="json" %}
// Count the number of characters to determine payload size
function processEvent(message, metadata, timestamp, annotations) {
	const my_string = JSON.stringify(message) // convert the payload to a string
  message.size = message.length // return the number of characters
  return message
}
{% /tab %}
{% /code %}

### Working with Strings

{% code %}
{% tab language="javascript" title="Convert to String" %}
// Using toString()
function processEvent(message, metadata, timestamp, annotations) {
  message.total = message.total.toString()
  if (message.total.endsWith('88')) {
      message.tags.clearance = 1
  } 
  if (message.total.startsWith('9')) {
      message.tags.premium = 1
  }
  message.displayTotal = '$' + message.total + ' USD'
  return message
}
{% /tab %}
{% /code %}

### Working with Arrays

{% code %}
{% tab language="javascript" title="Array manipulation" %}
function processEvent(message, metadata, timestamp, annotations) {
  const filtered_tags = []
  // Iterate using for...of
  for (const tag of message.tags) {
    if (tag.startsWith('my-tag-')) {
      	// Add elements to an existing array with push()
        filtered_tags.push(tag)
    } 
  }
  message.tags = filtered_tags
  return message
}
{% /tab %}
{% /code %}

## Known Limitations

This processor was not intended to implement the full JavaScript language, but was developed with event manipulation in mind only. For this reason, it has some limitations:

- Only one function can be used to encapsulate all of the logic (helper functions aren't supported)
- Accessing Array items is only supported with literal values (numbers)
- Only JavaScript ES5 syntax is supported
- Error handling is not supported via try/catch
- Mixing data types with binary expressions results in a no-op