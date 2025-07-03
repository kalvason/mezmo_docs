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


The Mezmo NGINX Ingress Controller Template provides you better observability into your infrastructure with NGINX Ingress Controller ([nginxinc/kubernetes-ingress](https://github.com/nginxinc/kubernetes-ingress)) logs. The Template includes pre-configured Views, Boards, Screens, and a [logging format](#nginx-ingress-controller-recommended-log-format-configuration) to get the most out of your logs. After configuring the t emplate, you can set up alerts on excessive HTTP 500's, graph response codes broken down by upstream service name, and more.

### Views

Views are saved shortcuts to a specific set of filters and search queries. You can also add Alerts to views to notify you when specific conditions are met. Check out the topic [](/docs/add-alerts-to-views) for more information.

- HTTP 2XX
- HTTP 5XX
- HTTP 404 Errors
- HTTP Forbidden/Unauthorized (401, 403)
- HTTP Server Errors - includes 500's and NGINX error logs, if those error logs are using the default error log format.

### Boards

Boards are collections of graphs. Using boards, you can track trends with response codes and understand how they fluctuate over time at a glance. Drill down using subplots to see which host or path is generating the most errors. Check out the topic [](/docs/visualize-log-data-with-graphs) for more information.

- HTTP Response Codes and Errors
- Breakdown by App, Host, Request (Path), Client IP, and Upstream Kubernetes Service
- 95th Percentile Response Times for Upstream and Total Time
- Traffic Volume with Total Bytes and Requests

### Screens

Screens are collections of customized dashboards that can display data in various forms. See the topic [auto$](/docs/use-screens-and-widgets-to-monitor-log-data) for more information.

- Web Analytics, such as traffic trends, most popular pages, and referrers
- Server Health, such as number of 500s by grouped by upstream service
- Web Server Security, such as top 401 and 403 errors by IP Address

## NGINX Ingress Controller Log Format Configuration

To take full advantage of the the NGINX Ingress Controller Template with [nginxinc/kubernetes-ingress](https://github.com/nginxinc/kubernetes-ingress), you should add our recommended custom log format. The custom log format exposes additional NGINX variables such as `upstream service name` and `response times` to further aid in debugging your infrastructure. Without this custom log format, parts of the template will not be populated with data.

[The NGINX documentation](https://docs.nginx.com/nginx-ingress-controller/configuration/global-configuration/configmap-resource/) contains more details on configuring NGINX via a ConfigMap resource. Log formats that deviate from this format or the default Apache Common or Combined Log Format will lead to incorrect data being populated in this template.

### Recommended Log Format Configuration

{% code %}
{% tab language="yaml" %}
log-format: 'verb="$request_method" request="$uri" response=$status clientip="$remote_addr" scheme="$scheme" bytes=$bytes_sent agent="$http_user_agent" referrer="$http_referer" request_time=$request_time upstream_response=$upstream_status upstream_response_time=$upstream_response_time upstream_service="$service" resource_name="$resource_name" resource_namespace="$resource_namespace" resource_type="$resource_type" http_host="$http_host" request_id="$request_id" time_date="$time_iso8601"'
log-format-escaping: 'json'
{% /tab %}
{% /code %}

### Example ConfigMap

You may need to modify this depending on your NGINX Ingress Controller setup.

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

## Configuration for Community Version

If you're using the ingress version from `kubernetes/ingress-nginx,`the default template will still be compatible, but the extra Kubernetes metadata will not be automatically parsed. This means that template elements that require data like upstream service/response time will not be available.

To expose additional Kubernetes metadata to Mezmo, you can configure a custom [ConfigMap](https://kubernetes.github.io/ingress-nginx/examples/customization/custom-configuration/) and [log format](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/log-format/) that is similar to the default log format shown in the previous section.