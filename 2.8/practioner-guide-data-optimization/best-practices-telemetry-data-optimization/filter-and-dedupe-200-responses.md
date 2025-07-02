---
type: page
title: Dedupe 200 Responses
listed: true
slug: filter-and-dedupe-200-responses
description: 
index_title: Dedupe 200 Responses
hidden: 
keywords: 
tags: 
---

Telemetry data contains a large volume of redundant information. For example, 200 codes are indicators of successful transactions, but are so common that they can overwhelm other, more meaningful data, like 4xx and 5xx status codes that indicate system anomalies. At the same time, there are requirements to maintain records of these transactions, so they can't simply be dropped from the data stream. With the [auto$](/telemetry-pipelines/dedupe-processor) you can remove duplicate fields from a defined number of events to reduce the noise in your telemetry data. This processor will emit the first matching record of the set of records that are being compared.