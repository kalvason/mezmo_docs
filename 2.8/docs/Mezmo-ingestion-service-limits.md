---
type: page
title: Mezmo Ingestion Service Limits
listed: true
slug: Mezmo-ingestion-service-limits
description: This topic describes the size and length limitations for log and log line components such as body size, app name length, log level, and tags
index_title: Mezmo Ingestion Service Limits
hidden: 
keywords: 
tags: 
---









{% table %}

{% table %}
| Log or Log Line Component | Size Limit | 
| ---- | ---- | 
| Body | 10MB\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\nThis is the server-enforced maximum body size. Ingestion clients may further reduce this | 
| Message | 16KB | 
| Metadata | 32KB | 
| Hostname length | 256 characters\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\nDomains within hostnames are truncated. FQDN settings available upon request. | 
| App Name length | 512 characters | 
| Log Level | 80 characters | 
| Tags | 80 characters | 
| Depth of nested fields | 3 | 
| Number of unique fields | Typically 500 per day | 
{% /table %}

{% /table %}

