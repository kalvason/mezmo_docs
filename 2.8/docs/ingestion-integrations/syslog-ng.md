---
type: page
title: Syslog-ng
listed: true
slug: syslog-ng
description: Get setup to start collecting, centralizing, monitoring, and analyzing your syslog-ng log files. Send log data from a variety of sources including syslog, rsyslog, AWS, JavaScript, JSON, Kubernetes, Docker, and more.
index_title: Syslog-ng
hidden: 
keywords: 
tags: 
---

You can stream RSyslog logs using TCP+TLS, TCP, and UDP, as well as through custom syslog ports. Mezmo accepts the Rsyslog default format, [RFC 5424](https://datatracker.ietf.org/doc/html/rfc5424) and [RFC 3164](https://datatracker.ietf.org/doc/html/rfc3164) for auto parsing.

{% callout type="info" title="LogDNA References in Code Examples" %}
In 2022, we changed the company name from LogDNA to Mezmo. However, the [IANA-approved Private Enterprise Number ](https://www.iana.org/assignments/enterprise-numbers/enterprise-numbers)(PEN), 48950, is still associated with the name LogDNA. We continue to use this name in our code examples for simplicity.
{% /callout %}

## Set Up Syslog-ng Log Ingestion

Follow the instructions in the Mezmo Web App to set up RSyslog log ingestion using your Mezmo syslog port and ingestion key.

1. Log in to the [Mezmo Web App](https://app.mezmo.com).
2. In the bottom section of the left-hand navigation, click **Help**.
3. Select **Add Log Sources**. 
4. Under **Via syslog**, click **syslog-ng.**
5. Follow the instructions to set up Syslog-ng log ingestion.

## Host Tags

Host tags let you group hosts automatically without having to explicitly assign a host to a group within the Mezmo web app.

Host tags follow the [syslog RFC-defined STRUCTURED-DATA format](https://tools.ietf.org/html/rfc5424#section-6.3.2) and require configuring the template line in `/etc/rsyslog.d/22-logdna.conf` to include the IANA-approved LogDNA [Private Enterprise Number (PEN)](https://www.iana.org/assignments/enterprise-numbers/enterprise-numbers), 48950. For example:

{% code %}
{% tab language="none" %}
$template LogDNAFormat,"<%PRI%>%protocol-version% %timestamp:::date-rfc3339% %HOSTNAME% %app-name% %procid% %msgid% [logdna@48950 key=\"YOUR-INGESTION-KEY-HERE\" tags=\"tag1,tag2\"] %msg%"
{% /tab %}
{% /code %}

This will send up lines from with the host tags `prod` and `web`, which would add this host to the prod and web tags.

{% callout type="info" title="Set keepalive in Syslog Forwarding Configuration" %}
If possible, we highly recommend setting up a keepalive inside your syslog forwarding configuration. This helps make sure that bad connections are properly terminated and re-initiated, and increases the reliability of log delivery. You can learn about rsyslog keepalive options [here](https://www.rsyslog.com/doc/v8-stable/configuration/modules/omfwd.html#keepalive).
{% /callout %}

## Configuration Examples

### Syslog-ng TCP+TLS with Custom Port Settings

{% code %}
{% tab language="none" %}
template LogDNAFormat { template("<${PRI}>1 ${ISODATE} ${HOST} ${PROGRAM} ${PID} ${MSGID} [logdna@48950 tags=\"ANY-TAG,COMMA-SEPERATED\"] $MSG\n"); ## Remove the "tags" if not being used above.`` template_escape(no);``};``destination d_logdna {`` tcp("syslog-a.logdna.com" port(CUSTOM-PORT-NUMBER)`` tls(peer-verify(required-untrusted) ca_dir("/etc/ld-root-ca.crt"))`` template(LogDNAFormat));``};``log {`` source(s_src);`` destination(d_logdna);``};``### END syslog-ng LogDNA logging directives ###
{% /tab %}
{% /code %}

### TCP with Custom Port Settings

{% code %}
{% tab language="none" %}
template LogDNAFormat { template("<${PRI}>1 ${ISODATE} ${HOST} ${PROGRAM} ${PID} ${MSGID} [logdna@48950 tags=\"ANY-TAG,COMMA-SEPERATED\"] $MSG\n"); ## Remove the "tags" if not being used above.`` template_escape(no);``};``destination d_logdna {`` tcp("syslog-a.logdna.com" port(CUSTOM-PORT-NUMBER)`` template(LogDNAFormat));``};``log {`` source(s_src); ### this could be (s_sys) for RedHat/Centos`` destination(d_logdna);``};``log {`` source(s_src);`` destination(d_logdna);``};``### END syslog-ng LogDNA logging directives ###
{% /tab %}
{% /code %}

### TCP+TLS Default Port

{% code %}
{% tab language="none" %}
template LogDNAFormat { template("<${PRI}>1 ${ISODATE} ${HOST} ${PROGRAM} ${PID} ${MSGID} [logdna@48950 key=\"YOURAPIKEY\"] $MSG\n");`` template_escape(no);``};`` ``destination d_logdna {`` tcp("syslog-a.logdna.com" port(6514)`` tls(peer-verify(required-untrusted) ca_dir("LOCATIONOFCERTIFICATE"))`` template(LogDNAFormat));``};`` ``log {`` source(s_src); ### this could be (s_sys) for RedHat/Centos`` destination(d_logdna);``};
{% /tab %}
{% /code %}

### TCP Default Port

{% code %}
{% tab language="none" %}
template LogDNAFormat { template("<${PRI}>1 ${ISODATE} ${HOST} ${PROGRAM} ${PID} ${MSGID} [logdna@48950 key=\"YOURAPIKEY\"] $MSG\n");`` template_escape(no);``};`` ``destination d_logdna {`` tcp("syslog-a.logdna.com" port(514)`` template(LogDNAFormat));``};`` ``log {`` source(s_src); ### this could be (s_sys) for RedHat/Centos`` destination(d_logdna);``};``log {`` source(s_src);`` destination(d_logdna);``};
{% /tab %}
{% /code %}

### UDP Default Port

{% code %}
{% tab language="none" %}
template LogDNAFormat { template("<${PRI}>1 ${ISODATE} ${HOST} ${PROGRAM} ${PID} ${MSGID} [logdna@48950 key=\"YOURAPIKEY\"] $MSG\n");`` template_escape(no);``};``destination d_logdna {`` udp("syslog-u.logdna.com" port(514)`` template(LogDNAFormat));``};``log {`` source(s_src); ### this could be (s_sys) for RedHat/Centos`` destination(d_logdna);``};``log {`` source(s_src);`` destination(d_logdna);``};`
{% /tab %}
{% /code %}