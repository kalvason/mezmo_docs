---
type: page
title: Slack Alert Integration
listed: true
slug: slack-alert-integration
description: 
index_title: Slack Alert Integration
hidden: 
keywords: 
tags: 
---

The Slack alert integration enables users to easily integrate Slack alerts on log data with their Slack workspace. 

After attaching an alert and selecting view-specific alerts- Mezmo provides you with several options for third-party integrations and one of these is Slack:

{% image url="https://uploads.developerhub.io/prod/2KW7/chu14e8ddw8xd6jj13zzdd9rgigx0phz26qm7594v89ins0j1zr2zftmg9l3mb1n.png" mode="responsive" height="882" width="1844" %}
{% /image %}

After clicking on Slack- a window pops up with options for test alerts, presence and absence alerting.

Test alerts allow the user to check whether the third party integration is working, presence alerts send alerts to the third party integration after a criteria is met (i.e. 5 or more matches within 30 seconds) and [absence alerts](https://www.mezmo.com/blog/logdna-absence-alerting) sends an alert when there are fewer log lines than anticipated.

The user can select the Slack channel for sending alerts, the color of the message, the type of alerting, and the number of matches and seconds after which to send the alert.

{% image url="https://uploads.developerhub.io/prod/2KW7/1t5p6632bk0fwfa50bh88qcclujfsnnn0rt52blc3qo8x69gvfqzmqwljha5s3o0.png" mode="responsive" height="787" width="608" %}
{% /image %}

An example of setting up presence match alerting with Slack- containing the log source, the number of matched lines as well as the log-lines:

{% image url="https://uploads.developerhub.io/prod/2KW7/53c493fkckomrhw4do6580z0rp3twd6dqz98omkzje42kmm4d2it8md20jo0xgog.png" mode="responsive" height="548" width="858" %}
{% /image %}

## Delete Your Integration

1. Log in to the Mezmo Web App.
2. Go to **Settings &gt; Integrations**.
3. Select your Slack integration to open its **Settings** page.
4. Click the **X** next to the channel you want to delete.
5. Click **Yes, delete** in the confirmation dialog to remove the channel.