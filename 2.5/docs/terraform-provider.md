---
type: page
title: Terraform Provider for Mezmo
listed: true
slug: terraform-provider
description: 
index_title: Terraform Provider for Mezmo
hidden: 
keywords: 
tags: 
---



## About the Terraform Provider for Mezmo

[Mezmo](https://mezmo.com) is a centralized log management platform. The Terraform provider from Mezmo allows organizations to manage Views and Alerts programmatically via Terraform commands.  With the Terraform provider, which utilizes our [Mezmo Configuration API](ref:getting-started-with-the-configuration-api), you can automate deployments of Views and Alerts to your Mezmo environment.

Read the full documentation on the official  [Terraform site](https://registry.terraform.io/providers/logdna/logdna/latest). If you are interested in contributing to this project, the source is in [GitHub](https://github.com/logdna/terraform-provider-logdna).

## Scenarios for Using the Terraform Provider

One use case for the Terraform provider is if you need to quickly spin up multiple Alerts on Views in several Kubernetes clusters and you need them to all be exactly the same. You can use Terraform to create and deploy the Alerts. Automation like this helps reduce the risk of error and speeds the process.

Other use cases include:

- As a developer, I want to replicate a set of Views/Alerts with minor tweaks from a base template in the same or different account.
- I want to manage my infrastructure and infrastructure SaaS apps (ex. PagerDuty, Sysdig, etc.) including Mezmo from the same toolset.
- As a SRE manager, I want all changes to a critical set of views/alerts to be code reviewed so that my workflow and alerting doesn’t get disrupted by accident, and mistakes can be quickly undone.

## Example

This example code for creating a new View and Alert is in [HCL (Hashicorp Configuration Language)](https://www.terraform.io/docs/configuration/syntax.html).



{% code %}
{% tab language="none" %}
terraform {
required_providers {
logdna = {
source = "logdna/logdna"
version = "1.0.0"
}
}
}
# Configure the LogDNA Provider
provider "logdna" {
servicekey = <your_service_key_goes_here>
}

resource "logdna_view" "my_view" {
apps     = ["app1", "app2"]
categories = ["Demo1", "Demo2"]
hosts    = ["host1", "host2"]
levels   = ["fatal", "critical"]
name     = "Email PagerDuty and Webhook View-specific Alerts"
query    = "test"
tags     = ["tag1", "tag2"]

email_channel {
emails          = ["test@mezmo.com"]
immediate       = "false"
operator        = "absence"
terminal        = "true"
timezone        = "Pacific/Samoa"
triggerinterval = "15m"
triggerlimit    = 15
}

pagerduty_channel {
immediate       = "false"
key             = <your_service_key_goes_here>
terminal        = "true"
triggerinterval = "15m"
triggerlimit    = 15
}

webhook_channel {
bodytemplate = jsonencode({
hello = "test1"
test  = "test2"
})
headers = {
hello = "test3"
test  = "test2"
}
immediate       = "false"
method          = "post"
terminal        = "true"
triggerinterval = "15m"
triggerlimit    = 15
url             = "https://yourwebhook/endpoint"
}
}
{% /tab %}
{% /code %}





{% callout type="info" title="Info" %}
Your service key can be generated or retrieved from the Mezmo web application. Navigate to  **Settings &gt; Organization &gt; API Keys**.
{% /callout %}





{% callout type="warning" title="Warning" %}
Note that if you create a new View using Terraform, but then delete the View by using the Mezmo Dashboard UI and _not_ Terraform, then Terraform will not be aware of the deletion and displays an `Error: Resource Not Found` message. 
For more information about handling "_deletion drift_" refer to our full documentation on the official  &lt;a href="[https://registry.terraform.io/providers/logdna/logdna/latest/docs"](https://registry.terraform.io/providers/logdna/logdna/latest/docs&quot;) target="_blank"&gt;Terraform site&lt;/a&gt;.
{% /callout %}





{% callout type="warning" title="Warning" %}
Be aware that running `terraform plan` and/or `terraform apply` may not display the full delta of possible changes, if TF is not aware of all existing Mezmo resources.
{% /callout %}





