---
type: page
title: VictorOps Alert Integration
listed: true
slug: victorops-alert-integration
description: 
index_title: VictorOps Alert Integration
hidden: 
keywords: 
tags: 
---

The VictorOps alert integration enables users to easily trigger incidents in VictorOps based off of log data in Mezmo.

## Integrating with VictorOps

1. On the alerts creation page, select the VictorOps logo. 
2. Define the alert properties.

{% image url="https://uploads.developerhub.io/prod/2KW7/q11205ke8dtbj6ca7ac2xis1ahhc0qz251n0r6o9ik4ejzef9y7xacyqe4541gt3.png" mode="responsive" height="645" width="1350" %}
{% /image %}

To retrieve the URL to notify go to Integrations -&gt; REST -&gt; URL to notify and input the url up to the final / into the URL to notify section of the Mezmo VictorOps alert integration.

{% image url="https://uploads.developerhub.io/prod/2KW7/q11205ke8dtbj6ca7ac2xis1ahhc0qz251n0r6o9ik4ejzef9y7xacyqe4541gt3.png" mode="responsive" height="645" width="1350" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/2KW7/n58it379sc4ab6s9eetlt6k6nwmhuak3xkn0hrv9eh5xbxsr6snfr7zd1h3cfbl8.png" mode="responsive" height="1800" width="2880" %}
{% /image %}

For the routing key, go to Settings -&gt; Routing Key. More information on routing keys can be found [here](https://help.victorops.com/knowledge-base/routing-keys/#:~:text=%3E%3E%20Routing%20Keys.-,Creating%20Routing%20Keys%20in%20VictorOps,Escalation%20Policy%20for%20a%20team).

{% image url="https://uploads.developerhub.io/prod/2KW7/q11205ke8dtbj6ca7ac2xis1ahhc0qz251n0r6o9ik4ejzef9y7xacyqe4541gt3.png" mode="responsive" height="645" width="1350" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/2KW7/n58it379sc4ab6s9eetlt6k6nwmhuak3xkn0hrv9eh5xbxsr6snfr7zd1h3cfbl8.png" mode="responsive" height="1800" width="2880" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/2KW7/ycuy16zetyd7oeddvzm4041rx9fx51o1q6dxzgnxbkxw0b1ywg84h2ggr6g91fh2.png" mode="responsive" height="1000" width="1600" %}
{% /image %}

After clicking test alert from the Mezmo alert UI, you will now see incidents in VictorOps!

{% image url="https://uploads.developerhub.io/prod/2KW7/q11205ke8dtbj6ca7ac2xis1ahhc0qz251n0r6o9ik4ejzef9y7xacyqe4541gt3.png" mode="responsive" height="645" width="1350" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/2KW7/n58it379sc4ab6s9eetlt6k6nwmhuak3xkn0hrv9eh5xbxsr6snfr7zd1h3cfbl8.png" mode="responsive" height="1800" width="2880" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/2KW7/ycuy16zetyd7oeddvzm4041rx9fx51o1q6dxzgnxbkxw0b1ywg84h2ggr6g91fh2.png" mode="responsive" height="1000" width="1600" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/2KW7/pi62qhs52cg6mdled9j12nqbo1jinqjlieh3muflk1fohzdbtvmm68w7qcs4x57u.png" mode="responsive" height="1800" width="2880" %}
{% /image %}

**Note:** When creating a new Routing Key, changes may take up to 10 minutes to propagate on the VictorOps side. If you don't see an alert show up in the VictorOps dashboard, please try again in 10 minutes.