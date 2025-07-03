---
type: page
title: Set Up Mezmo Edge in Kubernetes
listed: true
slug: set-up-mezmo-edge-in-kubernetes
description: 
index_title: Set Up Mezmo Edge in Kubernetes
hidden: 
keywords: 
tags: 
---


Mezmo Edge is designed to run from within a Kubernetes cluster, but can also be alternatively be run within Docker Desktop.

## Requirements

To set up a Mezmo Edge Pipeline, you will need:

1. A Kubernetes cluster with WAN access.
2. (Recommended) Support for running Helm charts within the target cluster.

Helm charts automate the deployment of Mezmo Edge for simplified set up, but you can also choose to directly pull the Edge image and deploy it with other methods, such as `kubectl`.

{% callout type="info" title="Using Docker Desktop" %}
You can run Mezmo Edge using any existing Kubernetes cluster. If you do not have easy access to a cluster, you can alternatively try it out using the Docker Desktop app with Kubernetes enabled. Go to **Settings -&gt; Kubernetes  -&gt; Enable Kubernetes** in your Docker Desktop app to install the necessary dependencies.
{% /callout %}

## Install Mezmo Edge

### Add the Mezmo Helm Repository

Make sure the Mezmo repository is included to install the requirements.

{% code %}
{% tab language="bash" %}
helm repo add mezmo https://helm.mezmo.com
helm repo update
{% /tab %}
{% /code %}

### Define the Ports to Use

Each unique source you intend to send to Edge will need a single port. You can manually define which ports, but if not defined the default port range will be used.

{% callout type="info" title="Default Edge Ports" %}
The default Edge port range is 8000-8010.
{% /callout %}

### Run the Helm Chart Install Command

Run this Helm command to launch the Edge instance in your local cluster, replacing the port range your own preferred values. These ports will be used to expose ingestion connections for your local sources.

{% callout type="info" title="Obtaining a Service Key" %}
If you need a service key for your Edge instance, in your account go to **Settings** **&gt; Organization &gt; API keys** and find the Pipeline Service Key generation at the bottom of the page.
{% /callout %}

{% code %}
{% tab language="bash" %}
helm install edge mezmo/edge \
--set mezmoApiAccessKey=MY_PIPELINE_SERVICE_KEY
{% /tab %}
{% /code %}

## Create a Mezmo Edge Pipeline

Once Mezmo Edge has been installed and the ports are configured, you can create an Edge pipeline.

1. Log in to [the Mezmo Web App](https://app.mezmo.com/).
2. Go to **Pipelines** and click **New Pipeline**.
3. You will see an option to create either a SaaS or Edge Pipeline. Select **Edge**.
4. You will see the same Pipeline Map that you would use to build a SaaS Pipeline, but with additional options for Sources, and Rust-based regex syntax for the [Parse](/telemetry-pipelines/parse-processor), [Route](/telemetry-pipelines/route-processor), and [auto$](/telemetry-pipelines/filter-processor)s.
5. [Build and deploy ](/telemetry-pipelines/build-deploy-mezmo-pipeline)your Pipeline as you would for a SaaS Pipeline, and you can also use [Simulation Mode](/telemetry-pipelines/simulate-pipeline-data-flows) to test your Pipeline before deploying it.
6. Deploying the Pipeline will generate the Pipeline configuration, which will be pulled down by the satellite Edge instance and become a part of the Edge configuration. This can take up to 15 seconds to complete.
7. You can now send data to your Edge Pipeline through your local Kubernetes cluster service endpoint with this prefix and the value for the source port you set up in the previous step.

{% code %}
{% tab language="none" %}
edge.default.svc.cluster.local:&lt;source_port&gt;
{% /tab %}
{% /code %}

## Troubleshooting and Monitoring

If you have any issues with this endpoint, please review your Kubernetes network settings to make sure you have set the appropriate forwarding. You may need to check your services via `kubectl get services` to make sure the right service name is set.

{% callout type="warning" title="Sensitive Data Will be Visible in a Pipeline Tap" %}
If you are sending any sensitive data through your Edge Pipeline, it will be visible during a Pipeline Tap if you are inspecting nodes that do not have this data redacted. We recommend you test without sensitive data first, redact that data in your processing using the [auto$](/telemetry-pipelines/encrypt-fields-processor), and then use the Pipeline Tap p after it has been redacted.
{% /callout %}

You can monitor the data flow in your deployed Pipeline with [a Pipeline Tap](/mezmo-edge/tap-and-view-mezmo-edge-pipeline-data-on-premises) and  make any changes to the Pipeline architecture by clicking **Edit Pipeline**, and then deploying the edited Pipeline again.