---
type: page
title: 3 - Build the OTel Demo Source
listed: true
slug: 4---profile-log-data
description: 
index_title: 3 - Build the OTel Demo Source
hidden: 
keywords: 
tags: 
---

{% synced id="workshop-need-help" %}
{% /synced %}

This workshop uses an OpenTelemetry Demo with expanded logs that you will connect to the shared sources you created in the previous step. In this step you will clone the repo, modify the config, and then build the OTel demo.

1. Run `git clone https://github.com/braxtonj/opentelemetry-demo` into a local folder. 
2. In the local folder, modify the `mezmo-otel-config-extras.yml` file with the endpoints and access keys of the shared sources you created in the previous step.  
3. To build the OTel demo source, run `sh run.sh`. This will build the demo and deploy it to `localhost:8080`.

{% callout type="info" title="15 Minutes to Build" %}
It can take up to 15 minutes for the demo to build and deploy, so you may want to to take a break before proceeding with the rest of the tutorial.
{% /callout %}

##