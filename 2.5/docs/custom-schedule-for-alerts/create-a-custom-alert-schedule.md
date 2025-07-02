---
type: page
title: Create a Custom Schedule for Alerts
listed: true
slug: create-a-custom-alert-schedule
description: 
index_title: Create a Custom Schedule for Alerts
hidden: 
keywords: 
tags: 
---



## How to define a custom schedule for an alert

You can enable a custom schedule for:

- Preset alerts (a pre-defined, standalone alert that can be applied to any view)
&gt;To add a custom schedule to an existing Preset alert, go to **Settings** -&gt; **Alerts** and either edit an existing Preset alert, or create a new Preset alert. Then follow the steps below.
- View-specific alerts (an alert that is created and attached to a particular view)
&gt;To add a custom schedule to a View-specific alert, open the View to which you want to attach the alert, click the down arrow to the right of the View name to open the drop-down menu, and then select **Attach an alert** from the drop-down menu. If you want to edit an existing alert, select **Edit Alert** from the drop-down list. Then follow the steps below.

The following steps are for working with custom schedules for alerts. Refer to our documentation for more information about creating [alerts](https://docs.mezmo.com/docs/alerts#how-to-attach-an-alert-to-an-existing-view) and [preset alerts](https://docs.mezmo.com/docs/alerts#how-to-configure-a-preset-alert-template).

1. On the Alert modal, click the **Custom schedule** option to toggle it "on."



{% image url="https://uploads.developerhub.io/prod/2KW7/pyiyyvne9v3n0yox9dr27rl41sbk6apvk6dh2h8i0g0t2etcctfvs94iwf74trux.jpg" caption="" mode="responsive" height="1380" width="756" %}
{% /image %}



2. Select the **Timezone** for the alert. This is the timezone to which the custom schedule applies.
3. Select the **Active Days** to specify which days of the week you want to receive the alert.
4. Optionally, you can **Restrict to specific times**  the hours of the day that you want to receive alerts. You can choose to not receive alerts in the evening, for example.


{% callout type="info" title="Info" %}
Note that the graph will dynamically reflect your selections, with the gray areas showing the times during which you will not receive alerts.
{% /callout %}




{% callout type="info" title="Time to take effect" %}
As with all Mezmo alerts, it might take up to 15 minutes after an alert is created or modified for it to take effect.
{% /callout %}





