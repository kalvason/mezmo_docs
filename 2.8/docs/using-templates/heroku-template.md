---
type: page
title: Heroku Template
listed: true
slug: heroku-template
description: 
index_title: Heroku Template
hidden: 
keywords: 
tags: 
---


The Heroku Template is a collection of Views, Boards, and Screens that enable you to set alerts on your app crashing, view HTTP 500 trends, graph 95th percentile of response times and more. The Heroku Template leverages both the [Heroku platform error codes](https://devcenter.heroku.com/articles/error-codes) as well as router and [system logs](https://devcenter.heroku.com/articles/logging#types-of-logs) emitted by default.

Browse the[ full library of Mezmo Templates](https://app.mezmo.com/manage/template-library).

### Views

Views are saved shortcuts to a specific set of filters and search queries. You can also add Alerts to views to notify you when specific conditions are met. Check out the topic [](/docs/add-alerts-to-views) for more information.

1. All Heroku HTTP Errors
2. All Heroku Runtime Errors
3. App Crashed (recommended to Alert on)
4. Deployments
5. HTTP 2XX’s
6. HTTP 5XX’s
7. HTTP Forbidden or Unauthorized
8. Memory Quota Exceeded
9. Request Timeout

### Boards

Boards are collections of graphs. Using boards, you can track trends with response codes and understand how they fluctuate over time at a glance. Drill down using subplots to see which host or path is generating the most errors. Check out the topic [](/docs/visualize-log-data-with-graphs) for more information.

**Web Server Status**

- Volume of HTTP Response Codes Over Time
- 95th Percentile of Connection/Service Response Times
- Cumulative Response Bytes

**Errors**

- Frequency of App Crashes
- Frequency of Request Timeouts
- Frequency of All HTTP Errors
- Frequency of all Heroku Runtime Errors

### Screens

Screens are collections of customized dashboards that can display data in various forms. See the topic [auto$](/docs/use-screens-and-widgets-to-monitor-log-data) for more information.

**Server** **Overview**

- Day Over Day Total Request Volume
- Day Over Day Total 5XXs
- Top response codes
- Top dynos with 5XXs
- 95th Percentile Service Response over last day
- Day over Day Total Bytes Sent

**Server Security**

- Top 10 IPs Hitting 401/403s
- Day Over Day 401/403s Request Volume
- Week Over Week 401/403 Request Volume
- Number of 429 Requests
- Number of 401/403 Requests
- Number of 200 Requests

## Custom Parsing

Parsing deployment hash and initiating user into `deploy_user` and `deploy_version.`