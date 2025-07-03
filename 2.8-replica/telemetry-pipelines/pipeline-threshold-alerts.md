---
type: page
title: Set Threshold Alerts for Pipeline Data Volume
listed: true
slug: pipeline-threshold-alerts
description: 
index_title: Set Threshold Alerts for Pipeline Data Volume
hidden: 
keywords: 
tags: 
---


You can set alerts to notify you when the data ingress or egress for your Mezmo Telemetry Pipeline has reached threshold criteria for a specified period of time. You can also set how often you want to receive these alerts.

You can use the [auto$](/telemetry-pipelines/aggregate-processor) to set threshold alerts for specific events.

## Threshold Alert Types

There are three types of threshold alerts you can set for your data volume notification.

**Absolute:** An  Absolute threshold alert is based on the an absolute volume of ingress or egress data for the specified time range.

**Relative:** A Relative threshold alert is based on a set percentage of data volume above or below the time frame average.

**Absence:** An Absence threshold alert is based on a lack of ingress or egress data for the specified time range.

## Set a Threshold Alert

1. Log in to the [Mezmo Web App](https://app.mezmo.com).
2. Click **Pipelines**.
3. Select the Pipeline you want to set an alert for, then click **Alerts**.
4. Select either **Ingress** or **Egress** for the type of alert.
5. Select the **Threshold type** for the alert.
    1. For an **Absolute** threshold, enter the ingress or egress data volume to use as the basis for the alert, and the **Time frame**. For example, you could set the time frame to alert you if the data volume exceeds an absolute value within a period of 5 minutes.
    2. For a **Relative** threshold, enter the **Time frame**, and the **Percentage** above and below the average data volume for that time frame that will trigger an alert.
    3. For an **Absence** threshold, enter the **Time frame** during which an absence of data will trigger an alert.

6. Set the **Alert frequency**. This will determine how often the alert is sent when the threshold criteria are met.
7. Select a **Delivery method** for the alert.
8. Enter a **Name** for the alert.
9. Click **Create alert**.

You will see your Alert saved in the list of alerts for that Pipeline. You can toggle it **On** or **Off** as necessary. Click **Edit Alert** to make changes.