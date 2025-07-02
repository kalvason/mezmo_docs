---
type: page
title: Syslog
listed: true
slug: syslog
description: Mezmo provides an integration to stream logs via Syslog using TCP and UDP
index_title: Syslog
hidden: 
keywords: 
tags: 
---

You can set up log ingestion from Syslog to Mezmo using both TCP and UDP. TCP and TCP+TLS are all supported on the same provisioned port. If you are using a custom port to send logs via UDP, please contact Mezmo support to provision the port. Consult your local Syslog man page for full configuration details.

## Set Up Syslog Log Ingestion

Follow the instructions in the Mezmo Web App to set up Syslog log ingestion using your Mezmo syslog port and ingestion key.

1. Log in to the [Mezmo Web App](https://app.mezmo.com).
2. In the bottom section of the left-hand navigation, click the **Add Log Sources** icon.
3. Under **Via syslog**, click **syslog**.
4. Follow the instructions to set up Syslog log ingestion.

We accept [RFC 5424](https://datatracker.ietf.org/doc/html/rfc5424) and [RFC 3164](https://datatracker.ietf.org/doc/html/rfc3164) for auto parsing Syslog.