---
type: page
title: Mezmo Architecture Overview
listed: true
slug: concepts
description: 
index_title: Mezmo Architecture Overview
hidden: 
keywords: 
tags: 
---

Mezmo uses a microservice-based architecture to split different tasks into discrete and scalable units. These microservices can be organized into two roles: log ingestion, and log retrieval.

{% image url="https://uploads.developerhub.io/prod/2KW7/la72vtord56enossw5ovbkt24jgvc3ky666mvug6kr1rdp6ildt1x85wwhhgi704.png" mode="full" height="220" width="512" %}
{% /image %}

Logs sent from your log sources to Mezmo are received by one of many ingestion endpoints. These endpoints route each log to a message queue using a proprietary data pipeline. The message queues manage the delivery of logs to a number of worker pools, which process logs for use in various Mezmo services such as parsing, indexing, live tail, graphs, and alerts. Other microservices provide features such as hosting API endpoints, providing security and authentication, and maintaining log data stores.

## [Ingestion Services](https://docs.mezmo.com/docs/concepts#ingestion-services)

Ingestion services provide the backend components necessary to ingest, parse, index, and store logs. They receive logs sent by log-generating components, as well as fulfill requests for log data sent from other Mezmo services.

Logs arrive into the Mezmo infrastructure through ingestion endpoints, which route logs from your applications and systems to a proprietary message brokering service called Buzzsaw. Buzzsaw is a highly optimized and highly scalable brokering service designed specifically for log data.

Buzzsaw routes logs to worker pools, which consist of microservices performing specific actions such as parsing, generating graphs, and running alerts. It also sends logs to a cluster of nodes, which provides Mezmo's search and filtering functionality. Buzzsaw acts as a buffer between ingestion sources, worker pools, and nodes, ensuring that performance problems in any one service don't impact the performance of other services.

## [Retrieval Services](https://docs.mezmo.com/docs/concepts#retrieval-services)

Retrieval services provide the ability to access, view, and export log data. They act as the gateway between users and the Mezmo ingestion services and are responsible for actions such as responding to user requests, querying for saved log data, and live tailing logs.

The primary services provided by retrieval services are the user interfaces, which include the Mezmo Web App and REST API. Actions performed in the Mezmo Web App, command line interface (CLI), or REST API are received by these services and proxied to the relevant infrastructure services before returning the results to the user. These services also perform user authentication and enforce access controls.

Other retrieval services include features that export log data automatically, such as alerts and archives.