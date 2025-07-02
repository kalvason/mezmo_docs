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

## Mezmo Agent v1




{% code %}
{% tab language="yaml" %}
files:
  "/home/ec2-user/logdna.sh" :
    mode: "000777"
    owner: root
    group: root
    content: |
      #!/bin/sh
      rpm --import https://repo.logdna.com/logdna.gpg
      echo "[logdna]
      name=LogDNA packages
      baseurl=https://repo.logdna.com/el6/
      enabled=1
      gpgcheck=1
      gpgkey=https://repo.logdna.com/logdna.gpg" | sudo tee /etc/yum.repos.d/logdna.repo
      yum -y install logdna-agent
      logdna-agent -k INSERT_KEY_HERE # this is your unique Ingestion Key
      # /var/log is monitored/added by default (recursively), optionally add more dirs here (remove # to uncomment the line)
      #logdna-agent -d /path/to/your/logs
      # --hostname allows you to pass your env hostname/appname to LogDNA, optionally you can change this to whatever you want (remove # to uncomment the line below)
      #logdna-agent --hostname `{"Ref": "AWSEBEnvironmentName" }`
      # -t option allows you to tag the host/app with the existing host/app name, optionally you can change this to whatever you want (remove # to uncomment the line below)
      #logdna-agent -t `{"Ref": "AWSEBEnvironmentName" }`
      chkconfig logdna-agent on
      service logdna-agent start
commands:
  01_install_logdna:
    command: "/home/ec2-user/logdna.sh"
  02_restart_logdna:
    command: "service logdna-agent restart"
{% /tab %}
{% /code %}




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






