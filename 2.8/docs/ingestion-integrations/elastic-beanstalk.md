---
type: page
title: AWS Elastic Beanstalk
listed: true
slug: elastic-beanstalk
description: Learn how to get setup to start collecting, monitoring, and analyzing your elb logs for easy, centralized log management.
index_title: AWS Elastic Beanstalk
hidden: 
keywords: 
tags: 
---

For the best user experience, we recommend logging into the [Mezmo web app](https://app.Mezmo.com/) and following the account-tailored add log source instructions. You may also follow the more generic instructions below

Copy the configuration for your version of the Mezmo agent into into a .config file in your Elastic Beanstalk app's .ebextensions directory.

Before redeploying your Elastic Beanstalk app, be sure to insert your [Mezmo Ingestion Key](https://app.Mezmo.com/manage/api-keys) and specify any custom directories you want the Mezmo agent to monitor.

## Mezmo Agent v2

{% code %}
{% tab language="yaml" %}
files:
  "/etc/yum.repos.d/logdna.repo":
    mode: "000644"
    owner: root
    group: root
    content: |
      [logdna]
      name=logdna packages
      baseurl=https://assets.logdna.com/el6/
      enabled=1
      gpgcheck=1
      gpgkey=https://assets.logdna.com/logdna.gpg

  "/home/ec2-user/logdna.sh":
    mode: "000755"
    owner: root
    group: root
    content: |
      #!/bin/bash
      rpm --import https://assets.logdna.com/logdna.gpg
      yum -y install logdna-agent
      systemctl start logdna-agent
      systemctl enable logdna-agent

  "/etc/logdna.env":
    mode: "000644"
    owner: root
    group: root
    content: |
      LOGDNA_INGESTION_KEY=YOURAPIKEY
      LOGDNA_TAGS=TEST

commands:
  1_install_agent:
    command: "/home/ec2-user/logdna.sh"
  2_enable_agent:
    command: "systemctl restart logdna-agent"
{% /tab %}
{% /code %}