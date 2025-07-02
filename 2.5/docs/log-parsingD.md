---
type: page
title: Auto-Parsing Logs
listed: false
slug: log-parsingD
description: 
index_title: Auto-Parsing Logs
hidden: 
keywords: 
tags: 
---



Mezmo can intelligently detect log types, parse them to display optimally, and more importantly index them in a way that makes keyword [search](/docs/search) fast and easy to use. [Custom parsing rules](/docs/custom-parsing) can be [configured for any proprietary formats](https://www.mezmo.com/blog/custom-log-parsing) as well.

## Supported Types

Mezmo automatically parses the following log line types:

- [Akamai](/docs/akamai-cloud-monitor-logs)
- Ansible
- Apache Common Log Format
- Apache Combined Log Format
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
- Nginx Error Log Format
- PostgreSQL
- Redis
- Ruby/Rails
- Syslog
- Tomcat
- Windows Events

### JSON Parsing

As long as the log message ends in a }, your JSON object will be parsed, even if the JSON object does not span the entire message. If you do not want your JSON object to be parsed, you can simply append an additional character after the ending } such as . a period.

If your JSON contains a `message` field, that field will be used for display and search in the log viewer. We also parse out (and override any existing) log levels if you include a level field.

### Reserved fields

For JSON parsed lines, Mezmo uses a number of reserved fields to keep track of specific types of data. Please note that using the following reserved fields in your root JSON object will result in an underscore (_) prepended to those fields inside the context menu (e.g. internally status is stored as _status). However, you can still search normally inside our web app without being aware of this storage behavior (e.g. you can still just search status:200 as we will automatically search both status and _status). For reference, common reserved fields can be found below:

- _source
- _type
- _tag
- auth
- bytes
- connect
- method
- namespace
- path
- pod
- request
- response
- service
- space
- status
- timestamp
- user

If you are using custom log formats, you can create a custom parsing template to tell Mezmo's parsing engine how to parse your log lines. Refer to the [documentation](/docs/custom-parsing) to learn more.

## Line components

Nearly all log line strings contain the three components below.

### Timestamp

The Mezmo code libraries and agent automatically provide a timestamp that is based on the time that Mezmo ingests the log. If there is also included in the log line a timestamp from when the log was written, it will get parsed and you can view it by [expanding the section](/docs/context). The written-time timestamp is not used further by our system. LogNDA generated timestamps follow the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format. If you have further questions about timestamps, [contact us](mailto:support@mezmo.com).

### Log Level

Log level typically follows timestamp and is automatically parsed. We look for common formats, such as a timestamp followed by a separator followed by the log level. Common log levels include:

- CRITICAL
- DEBUG
- EMERGENCY
- ERROR
- FATAL
- INFO
- SEVERE
- TRACE
- WARN

### Message

Message is a string that represents the core descriptive component of a log line and is usually preceded by timestamp and level. A message typically contains a mixture of static and variable substrings and allows for easy human interpretation. For example:



{% code %}
{% tab language="none" %}
User myemail@email.com requested /API/accountdetails/
{% /tab %}
{% /code %}



## Source information

Source information metadata is also ingested alongside the log line and is displayed in the All Sources menu in the web app.

### Hostname

A hostname is the name of the source of the log line, and is automatically picked up by the Mezmo agent as well as syslog-based ingestion. However, a host must be specified when submitting lines via the [REST API](/docs/code-libraries)(/reference,api) or [code libraries].

### Tags

A tag can be used to group lines and more than one tag can be applied to a given line. Tags show up under the All Tags menu in the web app. Tagging is supported by both the Mezmo agent as well as custom-template supported syslog-based ingestion, such as [rsyslog](/docs/rsyslog) or [o[syslog-ng](/docs/syslog-ng). At the time of writing, only source tags are currently supported, but more types are planned.

### Other information

Other optional source information can be specified, such as

- IP address
- MAC address

The above information is automatically picked up by the Mezmo agent and can be specified for the [REST API](/reference#api). The Mezmo agent also picks up some instance metadata, such as instance type.

## Application information

In addition to source information, app information is also ingested. The Mezmo agent automatically parses the app name as the filename (e.g. error.log) while syslog-based ingestion uses the [syslog-generated APP-NAME tag](https://tools.ietf.org/html/rfc5424#section-6.2.5). For the [REST API](/reference#api) and code libraries, the app name must be specified.

## Metadata

Metadata is a field reserved for custom information associated with a log line. Sending metadata is currently supported by the [Ingest API](https://docs.mezmo.com/reference/logsingest#metadata), as well as our [Node.JS](https://github.com/mezmo/nodejs), and [Python](https://github.com/mezmo/python) code libraries.



