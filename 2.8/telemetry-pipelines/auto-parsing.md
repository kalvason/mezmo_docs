---
type: page
title: Parse Shared Source Data
listed: false
slug: auto-parsing
description: 
index_title: Parse Shared Source Data
hidden: 
keywords: 
tags: 
---


There are two distinct types of telemetry logs: unstructured text lines or structured JSON events. Structured logs contain much more information than textual logs, and many of our processors require JSON events in order to to perform operations on them.

One of the ways you can convert unstructured logs to structured JSON logs is by using the [auto$](/telemetry-pipelines/parse-sequentially-processor). If you know the type of data that is expected in a Source, you can specify the appropriate parsers in the Processor.

Shared Sources make this process easier and more streamlined. The built-in automated parsing functionality classifies each incoming log line by event type, and adds metadata to identify the event type for the downstream processors. These event types are displayed under the Source, so that you can route each type to the appropriate Processor chain.

Auto-parsing will parse the first 1,000,000 lines. When automated parsing is running, the percentage donut shows what percentage of that total has been parsed.

**Event types found** shows the patterns [Data Profiler](/telemetry-pipelines/data-profiling) found in the data. You will also get an output, **Everything Else**, that will include lines that did not match any of the known log types.

{% image url="https://uploads.developerhub.io/prod/2KW7/oqz3ilg2d4adezbqxwv1hngi6bxlxp6z0l5img02cjsqokn7fphhmyvgvd6epggw.png" caption="The Event Types detected for each Shared Source" mode="full" height="274" width="1944" %}
{% /image %}

You can also **Stop** the analysis manually, or if you want the evaluation to start over, you can choose R**eset profile.**

You can toggle these outputs by editing the source in your pipeline. Outputs that are connected to a Processor or Destination may not be disabled, until that connection is removed. Disabling an output will send the data that would have matched to **Everything Else**.

{% image url="https://uploads.developerhub.io/prod/2KW7/zlqla6nnj9y8j0v7lwsw2hpper4xpuxz89qhhe5p502cbtqkt8qoth0j3rurw5wr.png" caption="Controls to enable or disable the output for a detected log type" mode="600" height="194" width="522" %}
{% /image %}