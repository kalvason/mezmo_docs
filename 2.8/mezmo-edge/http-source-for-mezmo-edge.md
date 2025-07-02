---
type: page
title: HTTP Source for Mezmo Edge
listed: true
slug: http-source-for-mezmo-edge
description: 
index_title: HTTP Source for Mezmo Edge
hidden: 
keywords: 
tags: 
---

## Description

You can configure any source to send data via a RESTful POST to a Mezmo Edge Pipeline.

{% callout type="success" title="Parsing Data after Ingestion" %}
When using the HTTP source, your content must be encoded appropriately, and packaged in a way that enables it to be parsed after ingestion. Structured formats, such as JSON, do not require additional parsing unless you want to further parse a specific value within the JSON.
{% /callout %}

You would typically use an HTTP request as a Source when the type of Source you want to send data from is not supported. For example, you may want to send and process data from an uncommon open source application. As long as you're able to use a RESTful POST transport to send the data to an endpoint, you can send the data into the Pipeline.

## Configuration

This Source requires an allocated port that you will forward the data to. You must use a port that has been configured within your Edge instance during set up.

{% callout type="info" title="Default Edge Port Ranges" %}
The default Edge port range is 8000-8010, unless you modified it during set up.
{% /callout %}

### Configuration Options

{% table %}
| **Setting** | **Description** | 
| ---- | ---- | 
| **Title** | A name for your source. | 
| **Description** | A short description of the source. | 
| **Port** | The port number to listen on within the Edge instance. | 
{% /table %}

## Exposing for External Ingress 

{% callout type="warning" title="Prod Deployments" %}
It is highly recommended that a scalable load balancer be used like [Nginx](https://nginx.org).  The following is a simple example using the default LoadBalancer for your system which ignores TLS and the like.
{% /callout %}

A simple, non-prod method of exposing the HTTP Source to external ingress is to use the system default LoadBalancer.   

To do this we will create a load balancer service which exposes the port configured by the HTTP Source.

Sample Config: edge-load-balancer.yaml

{% code %}
{% tab language="yaml" %}
apiVersion: v1
kind: Service
metadata:
  name: edge-load-balancer
spec:
  ports:
  - name: http-source-1a
    port: <<HTTP_SOURCE_PORT>>
    protocol: TCP
    targetPort: <<HTTP_SOURCE_PORT>>
  selector:
    app.kubernetes.io/instance: <<EDGE_INSTANCE>>
    app.kubernetes.io/name: <<EDGE_NAME>>
  sessionAffinity: None
  type: LoadBalancer
{% /tab %}
{% /code %}

Replace `HTTP_SOURCE_PORT` with your configured port and `EDGE_INSTANCE` + `EDGE_NAME` with those found in your edge services description.  You can find your `instance` and `name` via a command like

{% code %}
{% tab language="bash" %}
kubectl get service EDGE_SERVICE_NAME -o yaml > tmp.yaml
{% /tab %}
{% /code %}

 Finally, apply to your cluster with the following command

{% code %}
{% tab language="bash" %}
kubectl apply -f edge-load-balancer.yaml
{% /tab %}
{% /code %}

You can now send data to the HTTP Source by routing data to `http://EXTERNAL_IP:HTTP_SOURCE``_PORT`.  Note th