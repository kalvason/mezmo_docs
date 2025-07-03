---
type: page
title: LogDNA Release Notes, March 9th 2021
listed: true
slug: logdna-release-notes-march-9th-2021
description: 
index_title: LogDNA Release Notes, March 9th 2021
hidden: 
keywords: 
tags: 
---





[LogDNA Web Application](https://docs.logdna.com/changelog/logdna-release-notes-march-9th-2021#logdna-web-application-version-4610)
[LogDNA Agent](https://docs.logdna.com/changelog/logdna-release-notes-march-9th-2021#logdna-agent)
[LogDNA Ingestion Integrations](https://docs.logdna.com/changelog/logdna-release-notes-march-9th-2021#logdna-ingestion-integrations)
[LogDNA APIs](https://docs.logdna.com/changelog/logdna-release-notes-march-9th-2021#LogDNA-APIs)

---
## LogDNA Web Application, version 4.61.0

### Changes
* The option of embedding a view in a website or elsewhere outside of the LogDNA application was deprecated as of February 22, 2021. You cannot create or update an embedded view. On March 29th, 2021, embedded views will be disabled and removed. For more information, please refer to our [blog](https://logdna.com/blog/sunsetting-embedded-views/). [LOG-8667]

### Fixed Issues

* Usage Quotas: we fixed the alert recipients dropdown for both email and Slack, which was displaying in too large a format across the UI. [LOG-9010]
* On Boards, a missing pop-up for editing/hiding/deleting a specific plot for a board has been fixed. [LOG-8999]

## LogDNA Agent

For the most recent release information about the LogDNA Agent, refer to [agent-specific Release Notes](https://docs.logdna.com/changelog).

## LogDNA Ingestion Integrations

- LogDNA now integrates with Pino. The pino-logdna "transport" tool was built to facilitate Pino-based logging from Node.js applications. In addition to transporting logs from Pino to LogDNA for in-depth analysis, monitoring, and storage, pino-logdna provides numerous options for configurations such as controlling the flush limits, backoff times, and searching metadata. If you are interested in contributing to this project, our repository is on [GitHub](https://github.com/logdna/pino-logdna). You can also find pino-logdna listed in the Transports section of the official [Pino site](https://getpino.io/#/docs/transports?id=pino-logdna).

##LogDNA APIs

- There are currently no external-facing changes to our LogDNA APIs.

