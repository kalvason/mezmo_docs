---
type: page
title: Alerts Overview
listed: true
slug: alerts
description: Learn about the various ways you can create alerts, view alerts, and receive alerts and notification integrations in Mezmo, the easiest, fastest cloud log management and analysis software.
index_title: Alerts Overview
hidden: 
keywords: 
tags: 
---



The purpose of this page is to describe the various alert notification integrations Mezmo has to offer.

Alerts send out alert notifications to the specified notification channel(s) whenever a log line with specific content appears in that alert's associated View. A bell icon is also displayed to the right of the View name to indicate that this View has an alert attached to it. While most alerts are for a specific View (known as a **_view-specific alert_**), you can also define a **preset**. A preset is an alert template that you can attach to any number of views.

## Types of Alerts

There are two types of alerts you can set on a view.

- **Presence** Alerts notify you when there are more than the number of matches of your query within a set time frame.
- **Absence** Alerts notify you when your logs start showing fewer lines than what is expected. This is useful when you want to be alerted for inactivity in your system. To avoid excessive alerts, absence alerts notifications are paused after 24 hours of not receiving logs and should reset after receiving new logs on a particular view.

## Conditions for Alerts

You can configure any of the following conditions for an alert:

_Time frequency:_ Specify how often to trigger an alert. Valid values are: 30 seconds, 1 minute, 5 minutes, 15 minutes, 30 minutes, 1 hour, 6 hours, 12 hours, 24 hours. 25 hours

_Log lines counter:_ Specify the number of log lines that match the view's filtering and search criteria. When the number of log lines is reached, an alert is triggered. You can decide whether both conditions are checked or only one. If both conditions are set, an alert is triggered when any of the thresholds is reached.

For example, you can configure an alert that is triggered after 30 seconds, or when a 1000 log lines that match the view's filtering and search criteria are collected.

## Notification channels

You can configure multiple alert notification channels. Valid channels are: `email`, `Slack`, `PagerDuty`, `Webhook`, `OpsGenie`, `Datadog`, `AppOptics`, `VictorOps`, and `Sysdig`.

Also check out our video on how to save a view to create alerts:



{% video videoId="JpGoXO4cI9Q" provider="youtube" %}
{% /video %}



## Alert Integrations



{% table %}
| Integration | Configuration Details | 
| ---- | ---- | 
| **Email** | You can configure one or more email addresses. | 
| **Slack** | You can configure a slack channel to deliver alerts to. | 
| **Webhook** | You can configure a webhook URL. | 
| **Pagerduty** | You can configure connection details to your PagerDuty system, and select a service.\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n_Manager level permissions required_ | 
| **OpsGenie** | You can configure the API key to connect to your OpsGenie system. \n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n_The US OpsGenie endpoint is used by default.  If using the EU OpsGenie endpoint is required please reach out to [support@mezmo.com](mailto:support@mezmo.com)._ | 
| **Datadog** | You can configure the API key to connect to your Datadog system. | 
| **AppOptics/Librato** | You can configure the API key to connect to your AppOptics/Librato system. | 
| **VictorOps** | You can configure the URL to notify when an alert is triggered, the routing key, and an alert type. Valid alert types are: info, warning, critical. | 
{% /table %}

{% callout type="info" title="Time to take effect" %}
Allow up to 15 minutes after an alert is created or modified for it to take effect.
{% /callout %}



## How to create a view

1. Perform any search queries and set the sources, apps, and/or log level filters to create the desired conditions you'd like to set an alert on.
2. Click the `Unsaved View` button in the top left and select `Save as New View/Alert`.
3. Name your new view and select a category for it.  An alert can also be attached here, with the instructions below.

## How to attach an alert to an existing view

1. Click the arrow icon beside the name of an existing view to display the drop-down menu.
2. Select **Attach an alert** from the drop-down menu.
3. Select a preset alert or build your own. You can send an email, Slack, Webhook, Pager Duty, OpsGene, Datadog, AppOptics/Librato, VictorOps alert. It is also possible to send alerts to multiple channels by clicking the plus button above the alert channel options until you have added the desired number of alert channels.
4. Set your threshold alerting parameters (e.g. alert immediately when the 20th match appears within 5 minutes, alert at the end of 5 minutes when 20 or more matches appear).
5. Configure your [alert notification channels](/docs/alerts#notification-channels).
6. Click **Save Alert**.

**Note:** There may be a delay of up to 2 minutes before the alert takes effect.

You can define one or more notification channels to a view-specific alert. You can mute alerts. You can detach alerts from a view.

## How to configure a preset (alert template)

1. Select the `Settings` icon in the main menu
2. Select `Alerts`.
3. Select `Add a preset alert`.
4. Choose a notification channel.
5. Define the threshold conditions.
Select a time frequency. For example, 12 hours.
Enter the number of log lines after which you want the alert to trigger.
Select whether you want both conditions to be checked or just one.
6. Add the details for the notification channel that you have chosen.
For example, for the email notification channel, add one or more recipients, and optionally a time zone.
7. Click `Save alert`.

## How to delete a preset (alert template)

Complete the following steps to delete a preset:

1. Select the `Settings` icon in the main menu
2. Select `Alerts`.
3. Hover the mouse over the edit button of the preset that you want to delete. The delete option shows.
4. Select `Delete`.
5. Confirm that you want to delete the preset. Click `Delete`.

## How to mute alerts

When receiving email alerts, there is an option in the email to mute the alert for the time period desired. Clicking on one of the links in the UI (shown below) will redirect you to alerts settings.



{% image url="https://uploads.developerhub.io/prod/2KW7/v9zkpqu46sdcgsdmsdzw64h30m7k8f42kib81ni573w7u6fwkw8d5h933ecf24cm.png" caption="" mode="responsive" height="46" width="352" %}
{% /image %}





