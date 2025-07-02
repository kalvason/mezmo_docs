---
type: page
title: Rsyslog
listed: true
slug: rsyslog
description: Mezmo provides an integration to stream logs via RSyslog using TCP+TLS, TCP, and UDP
index_title: Rsyslog
hidden: 
keywords: 
tags: 
---

You can stream RSyslog logs using TCP+TLS, TCP, and UDP, as well as through custom syslog ports. Mezmo accepts the Rsyslog default format, [RFC 5424](https://datatracker.ietf.org/doc/html/rfc5424) and [RFC 3164](https://datatracker.ietf.org/doc/html/rfc3164) for auto parsing.

## Set Up RSyslog Log Ingestion

Follow the instructions in the Mezmo Web App to set up RSyslog log ingestion using your Mezmo syslog port and ingestion key.

1. Log in to the [Mezmo Web App](https://app.mezmo.com).
2. In the bottom section of the left-hand navigation, click the **Add Log Sources** icon.
3. Under **Via syslog**, click **rsyslog**.
4. Follow the instructions to set up RSyslog log ingestion.

## Host tags

Host tags let you group hosts automatically without having to explicitly assign a host to a group within the Mezmo web app.

Host tags follow the [syslog RFC-defined STRUCTURED-DATA format](https://tools.ietf.org/html/rfc5424#section-6.3.2) and require configuring the template line in `/etc/rsyslog.d/22-logdna.conf` to include the IANA-approved Mezmo [Private Enterprise Number (PEN)](https://www.iana.org/assignments/enterprise-numbers/enterprise-numbers), 48950. For example:

{% code %}
{% tab language="none" %}
$template LogDNAFormat,"<%PRI%>%protocol-version% %timestamp:::date-rfc3339% %HOSTNAME% %app-name% %procid% %msgid% [logdna@48950 key=\"YOUR-INGESTION-KEY-HERE\" tags=\"tag1,tag2\"] %msg%"
{% /tab %}
{% /code %}

This will send up lines from with the host tags `prod` and `web`, which would add this host to the prod and web tags.

{% callout type="success" title="Set keepalive in RSyslog Forwarding Configuration" %}
If possible, we highly recommend setting up a keepalive inside your rsyslog forwarding configuration. This helps make sure that bad connections are properly terminated and re-initiated, and increases the reliability of log delivery. You can learn about rsyslog keepalive options [here](https://www.rsyslog.com/doc/v8-stable/configuration/modules/omfwd.html#keepalive).
{% /callout %}