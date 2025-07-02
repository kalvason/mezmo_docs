---
type: page
title: NGINX Ingress Controller Template
listed: true
slug: nginx-ingress-controller-template
description: 
index_title: NGINX Ingress Controller Template
hidden: 
keywords: 
tags: 
---



The Mezmo NGINX Ingress Controller Template provides you better observability into your infrastructure with NGINX Ingress Controller ([nginxinc/kubernetes-ingress](https://github.com/nginxinc/kubernetes-ingress)) logs. The Template includes pre-configured Views, Boards, Screens, and a [logging format](#nginx-ingress-controller-recommended-log-format-configuration) to get the most out of your logs. After configuring the Template, you can set up alerts on excessive HTTP 500's, graph response codes broken down by upstream service name, and more.

Interested in other templates? Browse the [full library of Mezmo Templates](https://app.Mezmo.com/manage/template-library).



{% image url="https://uploads.developerhub.io/prod/2KW7/vnla3s0spvnzetb74yjfh3mk6iq9a6ct6kbqvo2fn9v1rqjhbajzdibnxhu7wryp.png" caption="" mode="responsive" height="466" width="737" %}
{% /image %}



## What is the Mezmo NGINX Ingress Controller Template?

The Mezmo NGINX Ingress Controller Template provides users better observability into their infrastructure with NGINX Ingress Controller for Kubernetes (nginxinc/kubernetes-ingress) logs via pre-configured views, boards, and screens.  These customized dashboards and graphs help you quickly put Mezmo’s visibility tools to work. [Configure the template](https://app.Mezmo.com/manage/template-library/nginx-ingress-controller).



{% html %}
<a href="https://app.logdna.com/manage/template-library/nginx-ingress-controller">
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





{% callout type="info" title="Surfacing Additional Metadata" %}
To surface additional metadata in this Template such as upstream Kubernetes service name or response time, you'll need to set up our [recommended logging format](#nginx-ingress-controller-log-format-configuration).
{% /callout %}



### Views

1. HTTP 2XX
2. HTTP 5XX
3. HTTP 404 Errors
4. HTTP Forbidden/Unauthorized (401, 403)
5. HTTP Server Errors

- Includes 500's and NGINX error logs, if those error logs are using the default error log format.

### Boards

1. HTTP Response Codes and Errors

- Breakdown by App, Host, Request (Path), Client IP, and Upstream Kubernetes Service

2. 95th Percentile Response Times for Upstream and Total Time
3. Traffic Volume with Total Bytes and Requests

### Screens

1. Web Analytics, such as traffic trends, most popular pages, and referrers
2. Server Health, such as number of 500s by grouped by upstream service
3. Web Server Security, such as top 401 and 403 errors by IP Address

## NGINX Ingress Controller Log Format Configuration

To take full advantage of the the NGINX Ingress Controller Template with [nginxinc/kubernetes-ingress](https://github.com/nginxinc/kubernetes-ingress), users should add our recommended custom log format. If you're using the community version (`kubernetes/ingress-nginx`) [see the following section](#using-kubernetesingress-nginx). The custom log format exposes additional NGINX variables such as upstream service name and response times to further aid in debugging your infrastructure. Without this custom log format, parts of the Template will not be populated with data.

[See here](https://docs.nginx.com/nginx-ingress-controller/configuration/global-configuration/configmap-resource/) for more details on configuring NGINX via a ConfigMap resource. Log formats that deviate from this format or the default Apache Common or Combined log format will lead to incorrect data being populated in this Template.

Recommended log format configuration:



{% code %}
{% tab language="yaml" %}
log-format: 'verb="$request_method" request="$uri" response=$status clientip="$remote_addr" scheme="$scheme" bytes=$bytes_sent agent="$http_user_agent" referrer="$http_referer" request_time=$request_time upstream_response=$upstream_status upstream_response_time=$upstream_response_time upstream_service="$service" resource_name="$resource_name" resource_namespace="$resource_namespace" resource_type="$resource_type" http_host="$http_host" request_id="$request_id" time_date="$time_iso8601"'
log-format-escaping: 'json'
{% /tab %}
{% /code %}



Example ConfigMap (you'll need to modify this depending on your NGINX Ingress Controller setup):



{% code %}
{% tab language="yaml" %}
kind: ConfigMap
apiVersion: v1
metadata:
name: nginx-config
namespace: default
data:
log-format: 'verb="$request_method" request="$uri" response=$status clientip="$remote_addr" scheme="$scheme" bytes=$bytes_sent agent="$http_user_agent" referrer="$http_referer" request_time=$request_time upstream_response=$upstream_status upstream_response_time=$upstream_response_time upstream_service="$service" resource_name="$resource_name" resource_namespace="$resource_namespace" resource_type="$resource_type" http_host="$http_host" request_id="$request_id" time_date="$time_iso8601"'
log-format-escaping: 'json'
{% /tab %}
{% /code %}



## Using `kubernetes/ingress-nginx`

If you're not using the `nginxinc/kubernetes-ingress` but instead using the ingress version from `kubernetes/ingress-nginx` the out-of-the-box Template will still be compatible, but the extra Kubernetes metadata will not be parsed automatically so Template elements that require data like upstream service/response time will not be available.

To expose additional Kubernetes metadata to Mezmo, you can configure a custom [ConfigMap](https://kubernetes.github.io/ingress-nginx/examples/customization/custom-configuration/) and [log format](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/log-format/) in a similar manner to the recommended log format above.



