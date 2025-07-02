---
type: page
title: Mezmo Log Ingestion Methods
listed: true
slug: ingestion
description: Mezmo offers a variety of methods to ingest logs, including the Mezmo Agent, Mezmo CLI, a client-side logger, logging platform integrations, code libraries, and a REST API
index_title: Mezmo Log Ingestion Methods
hidden: 
keywords: 
tags: 
---

**Ingestion** refers to the process of formatting and uploading log data from external sources like hosts, applications, and cloud-based logging services. In the process of ingesting log data, Mezmo also parses the information in the log lines following  [automatic](/docs/log-parsing)  and [custom rules](/docs/parse-logs-with-custom-templates) to make it available for searching, and for use in data analysis.

## Mezmo Ingestion Methods

Mezmo provides several methods for ingesting log data.

#### Mezmo Agent

You can install [the Mezmo Logging Agent](https://docs.mezmo.com/docs/introducing-the-agent)  directly on the host where your logs are generated, and it will maintain a persistent, HTTPS-encrypted connection to the Mezmo ingestion servers. You can deploy the Mezmo Agent on Linux, Windows, macOS, Kubernetes, and OpenShift systems.

#### Mezmo Command Line Interface (CLI)

With [the Mezmo CLI](/docs/mezmo-cli)  you can live tail and filter log line data. The Mezmo CLI is available for Windows, Linux, and macOS.

#### Mezmo Client-Side Logger

Built on the Mezmo Node.js library, the [Mezmo client-side logger](https://docs.mezmo.com/docs/client-side-logging) sends logs from your client-side JavaScript applications to Mezmo's ingestion servers.

#### Platform Integrations

Mezmo has developed [integrations](https://docs.mezmo.com/docs/ingestion-integrations) to send logs directly from several popular logging platforms, including Akamai Cloud Monitor, AWS CloudWatch, Docker, Heroku, and varieties of Syslog.

#### Code Libraries

There are both Mezmo supported and community [Code Libraries](/docs/code-libraries)  available for sending logs directly from applications built in Go, Python, Ruby, Rust, Android, and iOS.

#### REST API

You can use the [Mezmo API](https://docs.mezmo.com/log-analysis-api/ref) to send log lines to Mezmo, as well as programmatically manage starting and stopping ingestion.

## Troubleshooting and Tips

For tips and troubleshooting information for the Mezmo Agent and other ingestion methods, check out the [Mezmo Log Analysis Support Knowledge Base](https://supportkb.mezmo.com).