---
type: page
title: Getting Started with Mezmo
listed: true
slug: mezmo-quick-start-guide
description: Mezmo is the easiest centralized log management software. Learn about logging, how to get started, and how to maximize our log collection, monitoring, retention, alerting, and analysis features.
index_title: Getting Started with Mezmo
hidden: 
keywords: 
tags: 
---

## Welcome Future Mezmoers!

Welcome to Mezmo!  Mezmo’s easy, blazing fast system allows you to collect, monitor, parse, live tail, graph, and analyze logs with clear visualizations and smart alerting all within minutes.

In this quick start guide, we will walk you through the following steps to get you onboarded as smoothly as possible:

## Step 1: Set up Your Account and Create an Organization

1. Click **Sign Up** on the [Mezmo website](https://mezmo.com/sign-up/).
You will be automatically enrolled into a 14-day free trial.
2. Your organization is an independent workspace where you can access and configure your logs, add members, change billing plan, and manage other aspects of your account. Once you create an organization, you will be given an auto-generated ingestion key, which you can use to send in logs. The topic [](/docs/organization) contains more information about setting up your organization. 

## Step 2: Add A Log Source

1. Next, choose the ingestion logging source.  Mezmo offers a variety of  [ingestion methods](/docs/ingestion), including the  [auto$](/docs/introducing-the-agent) and the [Ingestion API](/2.5/log-analysis-api/ref#ingest). You can install the Mezmo Agent on Kubernetes, Openshift, Linux, Windows, and MacOS, and you can take a look at our source code on [GitHub](https://github.com/logdna/logdna-agent-v2). You can also take a deeper dive into [ingestion](/docs/ingestion) here.
2. Each organization can have multiple ingestion sources. To add an ingestion source, [log in to the Mezmo Web App](app.mezmo.com).
3. In the left-hand navigation of the Web App, just below your user profile avatar, click **Add Log Sources.**
4. Select the log source you want to use, and follow the  setup instructions. Note that your ingestion key is automatically added to the code examples. 

You can find more information about ingestion sources in the topic [auto$](/docs/ingestion-integrations).

## Step 3: Parse Logs

As your logs are ingested into Mezmo, they are [automatically parsed into components](/docs/log-parsingD) that are instantly viewable and actionable. You can also create [your own custom parsing templates](/docs/custom-parsing) . 

## Step 4: Add Team Members

Start inviting team members to view the logs flowing into your new organization! 

1. In the Mezmo Web App, go to **Settings &gt; Organization &gt; Members**.
2. Follow the instructions in [](/docs/how-to-manage-users) to add users to your organization.
3. Set the [Role-Based Access Controls (RBAC)](/docs/rbac) for your members.
4. Create [](/docs/groups) for your members to set access to specific log data. 

## Step 5: Search Your Logs

Mezmo Log Search provides [advanced search methods and syntax](/docs/search) to find critical data in your logs, as well as the ability to search by [date/time and timeframe](/docs/working-with-the-timeline-visualization) . 

## Step 6: Create Views and Alerts

Once you've searched your logs, you can [save the results as a View](/docs/views). A view is like a bookmark for your log lines, so you can easily save them and review them as many times as you want. You can also [add Alerts to your views](/docs/alerts) to notify you and your team when certain conditions are met. Mezmo has [Alert integrations](/docs/alert-integrations) for many popular platforms, including DataDog, Slack, and PagerDuty. 

## Step 7: Set Up Exclusion Rules and Spike Protection

Mezmo provides several cost control features to protect against unexpected spikes in log data volume, including:

[Exclusion Rules](https://docs.mezmo.com/docs/excluding-log-lines) that help you filter out log data that you don’t need to store, which can help you manage storage costs and focus your analysis on data that contains meaningful information.

[Usage Quotas](https://docs.mezmo.com/docs/usage-quotas) allow you to set hard and soft limits on ingestion, and set additional Exclusion Rules to ensure that you aren’t going over budget while still getting the log data you need.

[Index Rate Alerts ](https://docs.mezmo.com/docs/index-rate-alerts)use historical trends to notify you when there are unexpected volume-based spikes in log data, and provides insights into where they are happening.

## Step 8: Set Up Archiving

Mezmo stores your log data for a certain period of time, based on which plan you are on (the free trial plan stores logs for 14 days). Enabling [Archiving](/docs/archiving) ensures that once the retention period has concluded, your log data will be [automatically exported to your long-term object storage](/docs/export-logs-to-external-storage) (for example, S3) for continued access. Additionally, enabling Archiving allows you to easily bring log data back into the Mezmo UI via our [](/docs/data-restoration) feature.

## Step 9: Create Boards and Graphs

[Boards](/docs/graphs) are similar to Views, but instead of containing log line data, contain graphs that present metrics about your log data. Graphs are especially useful for application monitoring and data visualization, and provide their own controls for filtering and refining log data. 

## Step 10: Change Plan

Once your 14 day trial is over, you can still use Mezmo on a free plan but your logs will no longer be retained. If you would like to retain your logs for 7, 14, or 30+ days, you can go to `Settings` &gt; `Billing` &gt; `Overview` to select one of our paid plans. Compare all our pay-per-usage [pricing](https://mezmo.com/pricing/) model here.

Now that you've followed these steps to set up Mezmo and start working with your logs, you're ready to start mining your logs for information and insights to accelerate your operational success!