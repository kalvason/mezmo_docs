---
type: page
title: Custom Schedules for Alerts
listed: true
slug: custom-schedule-for-alerts
description: 
index_title: Custom Schedules for Alerts
hidden: 
keywords: 
tags: 
---



## About Custom Schedules for Alerts

Custom Schedules for Alerts allows you to define customized schedules for when and how you want to receive alerts. With Custom Schedules, you can configure Mezmo to send alerts only during business hours, and to specify different methods of how to alert you at different times of the day (e.g. Slack during the day, email at night).

To learn more about Alerts in general, and how to configure Alerts, [refer to the documentation](/docs/alerts#how-to-attach-an-alert-to-an-existing-view).

To enable the Custom Schedules feature, use the **Custom schedule** toggle in the Alert setup modal. Under the Custom schedule area there are several elements to help you define your schedule:

- **Timezone** - The timezone selector allows you to set the timezone of the custom schedule that you're setting up.
- **Counts from** - The graph displays the log line counts from the previous full day (i.e., starting at 12am) for reference. Greyed out sections show when your alert would be disabled by the custom schedule settings.
- **Active days** - Specify the days of the week that you want to receive alerts. Any days that are not selected are considered “blackout” periods, and no alerts will be sent.
- **Restrict to specific time** - Allows you to toggle if you would like to be alerted only on certain hours of the day. Toggling it off means the alert would be on for the entire day (24 hours) during active days. Toggling it on means the specified time would be applied for active days.

## Usage examples

There are several real-world examples of how our customers can use the Custom Alerts Schedule feature.

### Send _Weekend_ Alerts to Slack, _Weekday_ Alerts to PagerDuty

If you have an alert set up where it might not be important to respond on the weekend, but it is still important to have a record of alerts that fired (so that you can check back later on Slack), you can define multiple Alert notification channels, each with a custom schedule. Of course you can exchange Slack and PagerDuty for any alert integration and it would work just as well (ex. Jira via Webhooks and Email).

### Different Alert Thresholds for Different Times

If you run a service that has predictable daily or weekly changes in load and want your alerts to more closely monitor along those trends, you can use Custom Schedules to adjust your threshold based on the time of day. In this example we’ll set a more sensitive (i.e. lower) threshold during off-peak hours, and set a less sensitive (i.e. higher) threshold when demand is higher during peak hours. You can use multiple Alert channels with Custom Schedules to create more fine-tuned alert thresholds based on your usage patterns.

### Only during business hours

If your environments and business run on a "business hours only" schedule, you can schedule all alerts to only send notifications during workdays.



