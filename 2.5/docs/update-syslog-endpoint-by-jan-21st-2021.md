---
type: page
title: Update Syslog Endpoint by Jan 21st, 2022
listed: true
slug: update-syslog-endpoint-by-jan-21st-2021
description: 
index_title: Update Syslog Endpoint by Jan 21st, 2022
hidden: 
keywords: 
tags: 
---



## Action Required for All Syslog-UDP Users

We’ve enabled a new Syslog endpoint to our service that’s devoted to accepting UDP traffic only. The new endpoint is called syslog-u.mezmo.com.

Currently, both TCP and UDP traffic is accepted at the endpoint syslog-a.mezmo.com.  **Starting on January 21st, 2022, all UDP traffic must be sent to the new endpoint syslog-u.mezmo.com**. After this date, logs sent over UDP to the older endpoint will be silently dropped.

If you have devices sending logs over UDP to Mezmo today, please configure them to point at the new endpoint, syslog-u.logdna.com, before January 21st, 2022.

In order to determine if your Mezmo account is using UDP over Syslog, Rsyslog, and Syslog-ng, you can search for these strings:

- For Syslog: `_ingester:syslog-UDP`
- For Rsyslog: `_ingester:syslog-UDP`
- For Syslog-ng: `_ingester:syslog-UDP`

Please re-configure them to point at the new endpoint, syslog-u.logdna.com, before January 21st, 2022.

Any traffic sent over TCP is unaffected by this change and can continue to be sent to the older endpoint, syslog-a.logdna.com.

Any further questions, please email [support@mezmo.com](mailto:support@mezmo.com)



