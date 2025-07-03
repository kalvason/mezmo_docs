---
type: page
title: Web Server Template
listed: true
slug: web-server-template
description: 
index_title: Web Server Template
hidden: 
keywords: 
tags: 
---


The Mezmo Web Server Template enables you to immediately receive valuable data from HTTP web servers via pre-configured Views, Boards, and Screens.

Browse the[ full library of Mezmo Templates](https://app.Mezmo.com/manage/template-library).

## Views

Views are saved shortcuts to a specific set of filters and search queries. Using views, the Web Server template can track server errors and alert you when they occur.

To set up alerting, we recommend attaching presence alerts to the "HTTP Server Error" view and absence alerts to the "HTTP 200" view to be alerted on excessive errors, or insufficient successful traffic. Check out the topic [](/docs/add-alerts-to-views) for more information.

- HTTP Server Errors (Recommended to Presence Alert on) - includes 500's and all NGINX or Apache error logs, if those error logs are using the default error log format
- HTTP Success (200) (Recommended to Absence Alert on)
- HTTP 404 Errors
- HTTP Forbidden/Unauthorized (401, 403)

## Boards

Boards are collections of graphs. Using boards, you can track trends with response codes and understand how they fluctuate over time at a glance. Drill down using subplots to see which host or path is generating the most errors. Check out the topic [](/docs/visualize-log-data-with-graphs) for more information.

- HTTP Response Codes and Errors
- Breakdown by App, Host, Request (Path), Client IP, and Referrer
- Traffic Volume with Total Bytes and Requests

## Screens

Screens are collections of customized dashboards that can display data in various forms. Using screens, you can see top 401 and 403 requests by IP address in the last hour, day, and week. See the topics [auto$](/docs/use-screens-and-widgets-to-monitor-log-data) and [](/docs/web-analytics-screen) for more information.

- Web Analytics, such as traffic trends, most popular pages, and referrers
- Server Health, such as count of 200 and 500's on time shifted graphs
- Web Server Security, such as top 401 and 403 errors by IP Address