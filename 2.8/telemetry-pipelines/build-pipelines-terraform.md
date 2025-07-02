---
type: page
title: Build a Mezmo Telemetry Pipeline with Terraform
listed: true
slug: build-pipelines-terraform
description: 
index_title: Build a Mezmo Telemetry Pipeline with Terraform
hidden: 
keywords: 
tags: 
---


{% callout type="info" title="Beta" %}
This feature is in Beta development.
{% /callout %}

## Introduction

[Terraform](https://developer.hashicorp.com/terraform/intro)  is an infrastructure-as-code tool from Hashicorp that lets you define, create, and manage resources using a code-based approach. Mezmo has implemented a Terraform provider that gives you the ability to build and manage your telemetry data Pipelines with Terraform.  This makes managing your pipelines easier and simpler by allowing you to:

- Store your Pipelines as code
- Version your Pipelines in your source control
- Have multiple users collaborate on Pipelines outside of a user interface
- Quickly and easily replicate Pipelines

## Getting Started

You will need:

1. A Pipeline Service Key. Create a new Pipeline Service Key by accessing Settings &gt; API Keys &gt; Pipeline Service Keys.
2. A [local Terraform installation](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)  for your system

Once have these items, you can add the [Mezmo Terraform provider](https://registry.terraform.io/providers/mezmo/mezmo/latest)  by referencing the provider in any TerraForm project using this code:

{% code %}
{% tab language="yaml" %}
terraform {
required_providers {
mezmo = {
source = "registry.terraform.io/mezmo/mezmo"
version = "4.3.0"
}
}
}

provider "mezmo" {
# Configuration options
auth_key = "&lt;YOUR TOKEN&gt;"
}
{% /tab %}
{% /code %}

{% callout type="info" title="Start with a New Terraform Project" %}
Unitll you are comfortable working with Mezmo Terraform for Pipelines, we recommend you start a new Terraform project for your Pipelines that is separate from any existing Terraform installations you may have.
{% /callout %}

You will need to add the configuration option for your pipeline service key to authenticate and use the Terraform provider API. Use the `auth_key = "<YOUR TOKEN>"`  configuration option in the provider configuration object as shown here:

{% code %}
{% tab language="yaml" %}
provider "mezmo" {
auth_key = "&lt;YOUR TOKEN&gt;"
}
{% /tab %}
{% /code %}

## Your First Terraform Pipeline

Now that you've installed the Mezmo Terraform provider, you can generate Pipelines directly within your account based on the generated Pipeline service key. In the public repository on [github.com/mezmo](https://github.com/mezmo/terraform-provider-mezmo/tree/main/examples), you will find examples of Pipelines and other resources you can use to get started.

{% callout type="info" title="Separate files for Providers, Sources, Destinations, Pipelines, and Variables" %}
We are showing the example in a single file, but we generally recommend splitting it out into individual files for your providers, sources, destinations, pipelines, and variables.
{% /callout %}

This is is a simple placeholder example you can try out,  which will then reflect in your environment.

{% code %}
{% tab language="yaml" title="" %}
terraform {
required_providers {
mezmo = {
source = "registry.terraform.io/mezmo/mezmo"
}
}
required_version = "&gt;= 1.1.0"
}

provider "mezmo" {
auth_key = "&lt;YOUR TOKEN&gt;"
}

resource "mezmo_pipeline" "pipeline1" {
title = "My Terraform pipeline"
}

resource "mezmo_http_source" "source1" {
pipeline_id = mezmo_pipeline.pipeline1.id
title       = "My HTTP source"
description = "This receives data from my webhook"
decoding    = "json"
}

resource "mezmo_http_source" "shared_source" {
pipeline_id      = mezmo_pipeline.pipeline1.id
title            = "A shared HTTP source"
description      = "This source can be used across pipelines"
decoding         = "json"
gateway_route_id = mezmo_http_source.source1.gateway_route_id
}

resource "mezmo_sample_processor" "processor1" {
pipeline_id = mezmo_pipeline.pipeline1.id
title       = "My second sample processor"
description = "Let's sample some data while keeping other events intact"
inputs      = [mezmo_http_source.shared_source.id]
rate        = 100
always_include = {
field        = ".my_app_id"
operator     = "greater"
value_number = 10
}
}
{% /tab %}
{% /code %}

Once you've created your example,  run:

{% code %}
{% tab language="bash" %}
terraform init
terraform plan
{% /tab %}
{% /code %}

Terraform will examine the local state and compute the necessary changes to enact your configuration. The `plan` command does not execute the configuration changes, but computes how they would be enacted. Practically this means that Terraform will list the changes to apply. You should see an output similar to this example:

{% code %}
{% tab language="bash" %}

## mezmo_http_source.shared_source will be created
+ resource "mezmo_http_source" "shared_source" {
+ capture_metadata = false
+ decoding         = "json"
+ description      = "This source can be used across pipelines"
+ gateway_route_id = (known after apply)
+ generation_id    = (known after apply)
+ id               = (known after apply)
+ pipeline_id      = (known after apply)
+ title            = "A shared HTTP source"
}

# mezmo_http_source.source1 will be created
+ resource "mezmo_http_source" "source1" {
+ capture_metadata = false
+ decoding         = "json"
+ description      = "This receives data from my webhook"
+ gateway_route_id = (known after apply)
+ generation_id    = (known after apply)
+ id               = (known after apply)
+ pipeline_id      = (known after apply)
+ title            = "My HTTP source"
}

# mezmo_pipeline.pipeline1 will be created
~ resource "mezmo_pipeline" "pipeline1" {
~ created_at = (known after apply)
~ id         = (known after apply)
~ title      = "My Terraform pipeline"
}

# mezmo_sample_processor.processor1 will be created
~ resource "mezmo_sample_processor" "processor1" {
+ always_include = {
+ field        = ".my_app_id"
+ operator     = "greater"
+ value_number = 10
}
~ description    = "Let's sample some data while keeping other events intact"
~ generation_id  = (known after apply)
~ id             = (known after apply)
~ inputs         = [
+ (known after apply),
]
~ pipeline_id    = (known after apply)
~ rate           = 100
~ title          = "My second sample processor"
}

Plan: 4 to add
{% /tab %}
{% /code %}

Verify that the `plan` returns the expected changes. If this is your first Pipeline, it will list creation of all of the resources.

Once you're ready to deploy your Terraform Pipeline, use the `apply` command. This command results in the execution of the computed changes between your Terraform file and your environment. You will have to confirm you want to make the changes to your environment.

{% code %}
{% tab language="bash" %}
terraform apply
{% /tab %}
{% /code %}

{% callout type="success" title="You Did It!" %}
You've just created your first Terraform pipeline! However, be aware the Pipeline is not deployed automatically. You will need to l[og into the the Mezmo Web App](https://app.mezmo.com) to test and deploy your Pipeline.
{% /callout %}

Once you've created your first Pipeline, we recommend studying the documentation [found in our repository ](https://github.com/mezmo/terraform-provider-mezmo/tree/main/docs/resources) to learn more about the available resources, including Sources, Processors, and Destinations.

{% callout type="warning" title="\"State\" and Editing Terraform Pipelines in the Mezmo User Interface" %}
**State** is an important concept in Terraform. Terraform assumes that you will only manage your resources via Terraform itself. This means if you edit your configuration anywhere else than Terraform, you risk getting out of sync with the state of your resources. If you try to edit your Pipelines in the Mezmo UI, a similar issue can occur, because your resources may become out of sync with your Terraform state. This can lead to unexpected behavior. For this reason, we've restricted editing Pipelines created by Terraform in the UI. This way you can view and reference the Pipelines in the UI, but limit the risk of having unexpected changes because of the Terraform state. .
{% /callout %}

## Other Resources

- [The Mezmo Terraform repo on Github](https://github.com/mezmo/terraform-provider-mezmo/tree/main)
- [How to install Terraform](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)
- [Terraform and the concept of state](https://developer.hashicorp.com/terraform/language/state)