---
type: page
title: Manage Usage
listed: true
slug: manage-usage
description: 
index_title: Manage Usage
hidden: 
keywords: 
tags: 
---


## Ways to Manage Usage

There are many ways to reduce and manage the amount of logging data used by your organization.

- [Exclusion Rules](https://docs.mezmo.com/docs/exclusion-rules) - Use Exclusion Rules to control what's stored.
- [Index Rate Alerts](https://docs.mezmo.com/docs/index-rate-alerts) - Track sudden spikes in logging and receive alerts if logs exceed a certain threshold.
- [Usage Quotas](https://docs.mezmo.com//docs/usage-quotas) - Specify the amount of log data to store. Create alerts once storage limits are reached.
- [Variable Retention Rules](https://docs.mezmo.com/docs/variable-retention) - Enterprise Only. Define how long logs are kept based on queries. These logs do not follow any other log retention rules set.
- Shut Off - Stop all incoming data.
- [Usage API](https://docs.mezmo.com/reference/about-the-usage-api) - Get information about your apps aggregated usage.

## Usage Dashboard

The [Usage Dashboard](https://app.Mezmo.com/manage/ingestion) provides an overview of how much data your organization is ingesting. It shows:

- Estimated usage for the given month.
- Breakdown of data ingested by day.
- Last Month in Days - Amount of data ingested in the past 30 days.
- Last month in Days, Trends - Shows the top sources, apps, and tags that create the most logs.


{% callout type="info" title="Data Available" %}
📘  The Usage Dashboard only shows data for the 50 most popular apps, sources, and tags each day.
{% /callout %}


## Last month in Days – Trends

The Last month in Days – Trends graph lets you show data in a stacked or unstacked view and compare the total usage.


{% image url="https://uploads.developerhub.io/prod/2KW7/3qerlzi0glb6vb0ghxfpovpe63bdp4fa88bq002jta3dsktzev45gp9s4q79bs80.jpg" caption="The Mezmo usage dashboard shows Last month in Days and Last month in Days – Trends." mode="responsive" height="704" width="500" %}
{% /image %}


### Stacked and Unstacked

Toggling Stacked to on, will stack the data lines on top of each other and display the sum of all visible sources. The graph will also be updated to show how each app, source, or tag compares to the total.


{% image url="https://uploads.developerhub.io/prod/2KW7/oh8phkvdifphv87fgvcjt8ktsx03qhhssa87vuagswdtztnetsklpaei3dt7ttnr.png" caption="The Unstacked graph shows the total number of log lines for each data source." mode="responsive" height="1080" width="1564" %}
{% /image %}



{% image url="https://uploads.developerhub.io/prod/2KW7/nbqx4se125em4862w0msj95fcjyr6tg6bytxombafj50c5aa5yzvknkvczct2a26.png" caption="The stacked graph shows sum of all logs compared to the visible sources. A new number representing the total is added when hovering over data sources." mode="responsive" height="1080" width="1564" %}
{% /image %}


## Log Data Restoration

Restoration is a way to bring back, or restore, archived logs from cold storage. You can search for this data in the Mezmo user interface. This is useful for finding old bugs and having more context from older logs. Learn more about [Data Restoration](https://docs.mezmo.com/docs/data-restoration).

## Email Digest

You can subscribe to a weekly or monthly digest breaking down your usage data for the given period.

## Usage Alerts

You can set up email alerts to notify you when you reach a percentage of the usage limit. The Usage Limit is the amount you want to use before getting an email alert. The Usage Limit only affects email alerts, and won't cause log ingestion to stop.

After defining a Usage Limit, add email recipients who will be notified when a certain usage percentage is reached. You can add as many email addresses as you need.

### How Usage Alerts Work

We send Usage Alerts at the end of your billing cycle. For example, if you get billed on the 15th of every month, our counter resets on the 16th to start a new cycle. If this isn't a billing date, such as accounts on a free trial, Mezmo will default to the account creation date.

If you have a contract, your custom billing date may not match our system's cycle start date.

To find out if your accounts custom billing date and the system's counter dates are aligned, please navigate to the Last month in Days – Usage chart, where the red ticker identifies the date your accounts billing cycle restarts.


{% image url="https://uploads.developerhub.io/prod/2KW7/8glsdux98p2l77g2yheyeoehqtx8av8tt08jvyoj74qczc3dhbcjdsvdkw184pp6.png" caption="The billing start date is identified by the red line in the Last month in Days graph." mode="responsive" height="682" width="1708" %}
{% /image %}


