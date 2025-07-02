---
type: page
title: Syntax for Editing Pipeline Component Configuration Values
listed: true
slug: syntax-for-editing-pipeline-component-configuration-values
description: 
index_title: Syntax for Editing Pipeline Component Configuration Values
hidden: 
keywords: 
tags: 
---

When editing configuration values for Sources, Processors, or Destinations, you should be aware of using the proper syntax. There are four types of configuration values that each require their own syntax:

{% table widths="160,0" %}
| **Configuration Value** | **Description** | **Example** | 
| ---- | ---- | ---- | 
| **Data Fields** | A parsed field of an event, metadata associated to the event, or other types of data within the pipeline | `.hostname` refers to a hostname value that has been parsed from an object. | 
| **Data References** | Data being sent as a part of a destination configuration, which may be a field or a static value | You would use `{{ .hostname }}` to insert a hostname in an input field that might otherwise expect a static value. | 
| **Static Values** | Static values are typically used for comparison operations. | You would use the value `my string` for a string comparison, or the value `42` for a numeric comparison. | 
| **Event Metadata** | Values outside of the event, but related to the event itself | Hostname, IP address, and MAC address of where the event originated. Use the syntax `metadata.<some_location>.<field_name>` | 
{% /table %}

### Data Fields

Data fields are found in many processors. They are used when specifying fields within an object to use for conditional tests or transformation operations.

Data fields require a specific dot notation in order to define them. The dot notation uses periods as delimiters for the field levels.

### Special Characters

Characters allowed within the dot notation are **letters**, **numbers** and **underscores**. All other characters must be included between quotation marks `" "` if they are a part of the field key itself. For example, a key with a hyphen in it would be accessed via `."my-hyphen-field"` .

### Arrays

Arrays can be accessed anywhere in the data path via their index position, which is a zero-based integer. For example, `.my_array[1].prop` would access the second element of the array, and assuming it's an object, continue to retrieve the `prop` value.

#### Example

This example illustrates how to refer to the fields and values in this parsed event. This object would be the value of the `message` field of the event envelope, so all of its fields can be accessed starting with `.` or `message` .

{% code %}
{% tab language="json" %}
{
  "bytes": 22322,
  "datetime": "24/Jan/2023:18:54:09",
  "host": "127.219.215.140",
  "method": "DELETE",
  "protocol": "HTTP/1.1",
  "referer": "https://names.de/apps/deploy",
  "request": "/secret-info/open-sesame",
  "status": "300",
  "user-identifier": "meln1ks",
  "data": {
  	"extra-data": "mydata",
    "mixed_bag": {
      "int-array": [1, 2, 3],
      "objarray": [
        {
          "first-key": "hello"
        }
      ]
    }
	}
}
{% /tab %}
{% /code %}

Specific field references:

1. `.bytes` would return the numeric `22322`
2. `.host` would return the string value `127.219.215.140`
3. `message.method` or `.method` would return `DELETE`
4. `.data` would return the object `{ "extra-data": "mydata" }`
5. `.data.mixed_bag."int-array"[1]` would return `2`
6. `.data.mixed_bag.objarray.[0]."first-key"` would return hello

### [Templates](https://docs.mezmo.com/telemetry-pipelines/syntax-for-editing-pipeline-component-configuration-values#templates)

Data references, otherwise known as templates, are used to insert data fields within input values by surrounding a valid data field path within double curly braces,`{{ }}` . This can be useful for passing dynamic data through a pipeline, and the Pipeline UI should note which form fields support templating. Where applicable, the template can be an entire string such as `I found this value: {{.value}}` .

{% callout type="warning" title="Must Reference Simple Type" %}
Templates must reference a simple type. This is because templates are used in strings, and the values must allow string coercion. Using the example JSON above, `{{data}}` would be invalid, but `{{.data."extra-data"}}` is valid.
{% /callout %}

For example, in the case of sending data to Log Analysis via a Pipeline, the `hostname` field is a required value from the Log Analysis API. You could include a static hostname field if desired, but more likely you would want to use a data reference to identify a hostname that would come in from an event object.

#### Static Values

Static values used within an operator do not require any special notation or quotes. Any characters included for these operations will be considered a part of the value being used.

#### Metadata Fields

These fields include metadata coming from source collectors and from the HTTP edge, such as IP address of the host or collector which sent the event to the pipeline.

{% callout type="info" title="Metadata May Not be Available" %}
Note that depending on the source, metadata may or may not be available.
{% /callout %}

Data within the metadata set is outside of the event itself and can be referenced using the syntax `metadata.<field_name>`. Note there is no `.` before the metadata label because the data is above the message object within the event.

**Typically Available Fields**

Common types of metadata include query parameters, such as those used within the Mezmo Agent.

#### Examples for query parameters from Log Analysis

1. `metadata.query.app`
2. `metadata.query.ip`
3. `metadata.query.host`
4. `metadata.query.mac`
5. `metadata.query.tags`

#### Timestamp Field

Like `metadata` , the `timestamp` field sits outside of the message object. In some automated parsing sources we will try and extract the timestamp from the incoming event, but for the most part this timestamp will be set to the time we received the event. This timestamp can be modified with the [Set Timestamp Processor](https://docs.mezmo.com/telemetry-pipelines/set-timestamp-processor) or the [Script Processor](https://docs.mezmo.com/telemetry-pipelines/js-script-processor)

The `timestamp` field will be available as an ISO 8601 datetime format.