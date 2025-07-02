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



Quickly unlock insights and gain visibility into your HTTP web server on Mezmo with pre-defined templates for views, boards, and screens. Interested in other templates? Browse the[ full library of Mezmo Templates](https://app.Mezmo.com/manage/template-library).



{% image url="https://uploads.developerhub.io/prod/2KW7/ro1yla1z20m3jka32l56qu9qap5g0x747kkomud0e3eu7ntjkpqfoconx275snkg.png" caption="" mode="responsive" height="770" width="1264" %}
{% /image %}



## What is the Mezmo Web Server Template?

The Mezmo Web Server Template allows users to immediately receive valuable data from HTTP web servers via pre-configured views, boards, and screens.  These customized dashboards and graphs help you quickly put Mezmo’s visibility tools to work. Whether you are a new or experienced Mezmo user, the Web Server Template is beneficial for both setting a foundation of Mezmo’s tools and learning how to further expand your current visibility.  Getting insights out of your logs has never been easier.



{% html %}
<a href="https://app.Mezmo.com/manage/template-library/web-server">
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



##  What is in the Web Server Template?

The Web Server Template consists of a collection of pre-configured [Views](/docs/views), [Boards](/docs/boards-vs-screens), and [Screens](/docs/screens). To learn more about these visibility tools and their specific use cases, click on the respective links above. Detailed below are the specific HTTP web server logs that the template analyzes.

### Views

1. HTTP Server Errors
    1. Include 500's and all NGINX or Apache error logs, if those error logs are using the default error log format.

2. HTTP Success (200)
3. HTTP 404 Errors
4. HTTP Forbidden/Unauthorized (401, 403)

### Boards

1. HTTP Response Codes and Errors
    1. Breakdown by App, Host, Request (Path), Client IP, and Referrer

2. Traffic Volume with Total Bytes and Requests

### Screens

1. Web Analytics, such as traffic trends, most popular pages, and referrers
2. Server Health, such as count of 200 and 500's on time shifted graphs
3. Web Server Security, such as top 401 and 403 errors by IP Address

## How do I use the Web Server Template?

The Web Server Template provides detailed dashboards and graphs to easily visualize your HTTP web servers.  Here are some example use cases of the many helpful insights your Web Server Template will provide.

Views

Receive alerts when server errors occur or when traffic goes below normal. _(Alerts require additional setup)_



{% image url="https://uploads.developerhub.io/prod/2KW7/njf2a9rzjz4n6ye2aonm697dkg4oha9r03gbpuyjck9p2dzq7b7iuogxrb2yd98u.png" caption="" mode="responsive" height="824" width="1812" %}
{% /image %}



Views are saved shortcuts to a specific set of filters and search queries.  Using views, the Web Server template can track server errors and alert you when they occur.

To set up alerting, we recommend attaching presence alerts to the "HTTP Server Error" view and absence alerts to the "HTTP 200" view to be alerted on excessive errors, or insufficient successful traffic. Learn more about setting up alerts in [our alert guide](https://docs.mezmo.com/docs/alerts#how-to-create-an-alert).

## Boards

Visualize and monitor HTTP response codes to pinpoint web traffic drop-offs or error spikes.



{% image url="https://uploads.developerhub.io/prod/2KW7/0ya6on8dto3sukauchtn6b7nqmh84tkyd99zm6ddo8m2wj2290i65lr8w2g9hh7u.png" caption="" mode="responsive" height="1662" width="2016" %}
{% /image %}



Boards are collections of graphs.  Using boards, you can track trends with response codes and understand how they fluctuate over time at a glance. Drill down using subplots to see which host or path is generating the most errors.

## Screens

Understand threats to your web servers and identify IPs that may be mounting an attack on your services.



{% image url="https://uploads.developerhub.io/prod/2KW7/8vtxigl3dm4a4ampxfdiuzq31lr4bg76slv4sz1ia8kwrpp10p2tnuu31rv39oez.png" caption="" mode="responsive" height="1106" width="1970" %}
{% /image %}



Screens are collections of customized dashboards that can display data in various forms.  Using screens, you can see top 401 and 403 requests by IP address in the last hour, day, and week.

### Web Analytics

Analyze traffic trends and the most popular content being requested.



