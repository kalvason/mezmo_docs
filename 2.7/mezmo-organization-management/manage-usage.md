---
type: page
title: Manage Usage Quotas
listed: true
slug: manage-usage
description: 
index_title: Manage Usage Quotas
hidden: 
keywords: 
tags: 
---

Usage Quotas enables developers and technical teams to see and set alarms for all important logs. This allows account administrators to manage how much data their teams are storing. The goal is to store all critical logs while staying under the monthly storage budget.

These configuration options allows for fine-grained control, providing a range of options such as:

- [Stop the storage](https://app.developerhub.io/#stop-log-storage) of all incoming logs once a certain quota is met.
- [Reduce the volume](https://app.developerhub.io/#reduce-the-volume-of-logs) of logs that are stored using filters, while still being able to stop logs once a quota is met.
- [Create alerts](https://app.developerhub.io/#alert-only) to notify you that your usage quota threshold is met.

## Stop Log Storage

When you reach your monthly or daily log limit, stop storing them. Logs that aren't stored don't add to your bill, but you can still see live tailing and get alerts.

1. Go to [**Settings &gt; Usage &gt; Usage Quotas**](https://app.mezmo.com/manage/usage-quotas).
2. Click **Edit Usage Quotas**.
3. Set the **Daily Usage Quota** and **Monthly Usage Quota** using GB, TB, or MB.
4. Choose if you want to discard logs with the daily or monthly quota is met. You can also choose to discard the logs daily and monthly once the quotas are reached.
5. Click **Apply** to save changes.

## Reduce the Volume of Logs

Triggered Exclusion Rules let you be more specific in what you filter out, so you don't reach the usage quota value as quickly. This way, you can focus on the important log data.

For example, if you set a Daily Usage Quota threshold at 2GB, and set the percentage at 50%, then at 1GB the system will start applying the triggered exclusion rule and no longer retain logs from the specified sources, apps, or queries.

You can use this approach to keep certain logs out of storage, but still see them and set alerts.

1. Go to [**Settings &gt; Usage &gt; Usage Quotas**](https://app.mezmo.com/manage/usage-quotas).
2. Click **Edit Usage Quotas**.
3. Set the Daily Usage Quota and Monthly Usage Quota using GB, TB, or MB.
4. Don't check either of the discard logs boxes.
5. Click **Apply**.
6. Go to **Triggered Exclusion Rules** and select Daily or Monthly. You can also configure both.
7. On the **Apply this rule at:** percentage selector, use your cursor to select and drag the marker to the percentage point you want. This percentage indicates at what percentage point of your pre-defined Daily or Monthly Usage Quota you want to start applying the triggered exclusion rule.
8. Set the exclusion rules based on Sources, Apps, and Query. You can use one or more of these filters. One filter is required.
9. Select Discard matching log lines if you want to stop retaining logs as soon as the specified percentage is met.
10. Select Preserve for Live Tail and Alerting, If you want to stop retaining all logs as soon as the specified percentage is met, but you do want to still have ingested logs appear in live tail and be able to set alerts on them.
11. Click **Apply** to save changes.

{% callout type="info" title="Exclusion Rule Limit" %}
Each account can only have five daily and monthly Triggered Exclusion Rules.
{% /callout %}

{% callout type="info" title="Archived Logs" %}
Logs not excluded by rules or quotas won't be archived
{% /callout %}

## Alert Only

You can choose to only send alerts when the quota is met. This option stores all logs and sends alerts when the quota is met or edited.

1. Go to [**Settings &gt; Usage &gt; Usage Quotas**](https://app.mezmo.com/manage/usage-quotas).
2. Click **Edit Usage Quotas**.
3. Set the Daily Usage Quota and Monthly Usage Quota using GB, TB, or MB.
4. Don't check either of the discard logs boxes.
5. Click Apply.
6. On the Setup page, in the Alert recipients area, specify the notification channels and the recipients.
7. Don't add a Discard Rule.
8. You can also create a [triggered exclusion rule](https://app.developerhub.io/#reduce-the-volume-of-logs), and receive an alert specifically based on the defined rules in addition to the alert for when you reach the overall usage quota.

## Remove Usage Rules

To remove rules, make sure to set all daily and monthly limits to 0. Then toggle the Usage Quotas off.

## Feature Notes

- If a quota value is set lower than what has already been consumed and sent to storage, all incoming logs after the rule has been set will be discarded.
- If you change your Daily or Monthly Usage Quotas, it will automatically turn off all the discard rules associated with that quota. For example, if you have a Monthly quota of 100GB and three Daily discard rules based on that quota, changing the Monthly quota to anything other than 100GB will turn off those rules. We do this to prevent changes that could result in logs not being retained. So, after you make the update, check that the discard rules are still what you want.