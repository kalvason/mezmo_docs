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



Quickly unlock insights and gain visibility into Heroku with Mezmo Views, Boards, and Screens templates. Interested in other templates? Browse the [full library of Mezmo Templates](https://app.Mezmo.com/manage/template-library).



{% image url="https://uploads.developerhub.io/prod/2KW7/rtynfwoeqep226alxzkrzx0s0wipjbzzy4dbshxmezr92v7ms0ejx9cv9nyp5dcd.png" caption="" mode="responsive" height="466" width="736" %}
{% /image %}



## What is the Mezmo Heroku Template?

The Heroku Template can get you started whether it’s alerting on your app crashing, viewing HTTP 500 trends, graphing 95th percentile of response times and more. The Heroku Template leverages both the [Heroku platform error codes](https://devcenter.heroku.com/articles/error-codes) as well as router and [system logs](https://devcenter.heroku.com/articles/logging#types-of-logs) emitted by default.



{% html %}
<a href="https://app.logdna.com/manage/template-library/heroku">
  <button class="brand-btn" style="margin: 32px 0;">
    Configure Template
  </button>
</a>
<style>        
  .brand-btn {
    padding: 8px 16px;
    height: 44px;
    background: #DB0A5B;
    border: 1px solid #DB0A5B;
    box-shadow: 0px 4px 16px rgba(225, 54, 120, 0.4);
    border-radius: 3px;
    color: #FBE8F0;
    text-shadow: 0px 1px 0px rgba(0, 0, 0, 0.3);
    font-weight: 600;
    font-size: 16px;
    cursor: pointer;
  }
</style>
{% /html %}





{% image url="https://uploads.developerhub.io/prod/2KW7/tkoflgx67bb7z9xvfutc9ugig2a41lfqhl6e9n07d57m79xr7564xobsrs628enk.png" caption="A board included in the template showing HTTP response code trends broken down by endpoint." mode="responsive" height="865" width="1386" %}
{% /image %}



## Included in the Heroku Template

### Views

1. All Heroku HTTP Errors
2. All Heroku Runtime Errors
3. App Crashed (Recommended to [Alert](https://docs.mezmo.com/docs/alerts) On)
4. Deployments
5. HTTP 2XX’s
6. HTTP 5XX’s
7. HTTP Forbidden or Unauthorized
8. Memory Quota Exceeded
9. Request Timeout

### Boards

1. Web Server Status

- Volume of HTTP Response Codes Over Time
- 95th Percentile of Connection/Service Response Times
- Cumulative Response Bytes

2. Errors

- Frequency of App Crashes
- Frequency of Request Timeouts
- Frequency of All HTTP Errors
- Frequency of all Heroku Runtime Errors

### Screens

1. Server Overview

- Day Over Day Total Request Volume
- Day Over Day Total 5XXs
- Top response codes
- Top dynos with 5XXs
- 95th Percentile Service Response over last day
- Day over Day Total Bytes Sent

2. Server Security

- Top 10 IPs Hitting 401/403s
- Day Over Day 401/403s Request Volume
- Week Over Week 401/403 Request Volume
- Number of 429 Requests
- Number of 401/403 Requests
- Number of 200 Requests

### Custom Parsing

1. Parsing deployment hash and initiating user into `deploy_user` and `deploy_version`

_Have any feedback or thoughts on our Template Library? [Join our forum](https://community.mezmo.com/) and let us know!_



