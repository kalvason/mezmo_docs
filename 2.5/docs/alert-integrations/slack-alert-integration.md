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



The Slack alert integration enables users to easily integrate Slack alerts on log data with their Slack workspace. See [documentation](/docs/views) for more on the process on creating a view and attaching an alert.

After attaching an alert and selecting view-specific alerts- Mezmo provides you with several options for third-party integrations and one of these is Slack:



{% image url="https://uploads.developerhub.io/prod/2KW7/zdfdv0e8l36ne4wyl72wlpdtqbzft52fch0roswpl1n8v2nb1kj8pihb8bb0uxlh.png" caption="" mode="responsive" height="1800" width="2880" %}
{% /image %}



After clicking on Slack- a window pops up with options for test alerts, presence and absence alerting.

Test alerts allow the user to check whether the third party integration is working, presence alerts send alerts to the third party integration after a criteria is met (i.e. 5 or more matches within 30 seconds) and [absence alerts](https://www.mezmo.com/blog/logdna-absence-alerting) sends an alert when there are fewer log lines than anticipated.

The user can select the Slack channel for sending alerts, the color of the message, the type of alerting, and the number of matches and seconds after which to send the alert.



{% image url="https://uploads.developerhub.io/prod/2KW7/zdfdv0e8l36ne4wyl72wlpdtqbzft52fch0roswpl1n8v2nb1kj8pihb8bb0uxlh.png" caption="" mode="responsive" height="1800" width="2880" %}
{% /image %}





{% image url="https://uploads.developerhub.io/prod/2KW7/fidugtiflu7tisp5xh5b4ztwpypehvqhbv41fgqjr88qxl56gntksz9l3emhjs9d.png" caption="" mode="responsive" height="1408" width="1380" %}
{% /image %}



An example of setting up presence match alerting with Slack- containing the log source, the number of matched lines as well as the log-lines:



{% image url="https://uploads.developerhub.io/prod/2KW7/zdfdv0e8l36ne4wyl72wlpdtqbzft52fch0roswpl1n8v2nb1kj8pihb8bb0uxlh.png" caption="" mode="responsive" height="1800" width="2880" %}
{% /image %}





{% image url="https://uploads.developerhub.io/prod/2KW7/fidugtiflu7tisp5xh5b4ztwpypehvqhbv41fgqjr88qxl56gntksz9l3emhjs9d.png" caption="" mode="responsive" height="1408" width="1380" %}
{% /image %}





{% image url="https://uploads.developerhub.io/prod/2KW7/p5f7eehzwaf8lvombgz6t8r3p4z550kyc4s957ejy2dp011mbyjwcjtoren7pusn.png" caption="" mode="responsive" height="1315" width="1210" %}
{% /image %}



## Delete Your Integration

1. Log in to the Mezmo Web App.
2. Go to **Settings &gt; Integrations**.
3. Select your Slack integration to open its **Settings** page.
4. Click the **X** next to the channel you want to delete.
5. Click **Yes, delete** in the confirmation dialog to remove the channel.



