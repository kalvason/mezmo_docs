---
type: page
title: Windows Security Template
listed: true
slug: windows-security-template
description: 
index_title: Windows Security Template
hidden: 
keywords: 
tags: 
---


The Windows Security Template enables you to quickly gain insights into excessive login attempts, audits on cleared logs, or anomalous access patterns. Set up alerts to monitor when unexpected events happen. or use our dashboards to get constant visibility into the access patterns of your servers.

Browse the[ full library of Mezmo Templates](https://app.mezmo.com/manage/template-library).

## NXLog Requirement and Configuration

The Windows Security Template requires NXLog to be set up to collect security event logs. Uncomment the line `<Select Path='Security'>*</Select>` in your NXLog config file and restart NXLog to apply changes. The [](/docs/nxlog-for-windows) ingestion integration topic contains more information on setting up NXLog. The Windows Security Template will not work with other integrations such as FluentD.

## Views

Views are saved shortcuts to a specific set of filters and search queries. You can also add Alerts to views to notify you when specific conditions are met. Check out the topic [](/docs/add-alerts-to-views) for more information.

- 1102 / Audit log cleared
- 4616 / System time was changed
- 4624 / Successful account log on
- 4625 / An account failed to log on
- 4634 / An account logged off
- 4720 / User account created
- 4725 / Disabled account
- 4740 / Locked account
- 4946 / Firewall exception added
- 5025 / Windows Firewall stopped

### Boards

Boards are collections of graphs. Using boards, you can track trends with response codes and understand how they fluctuate over time at a glance. Drill down using subplots to see which host or path is generating the most errors. Check out the topic [](/docs/visualize-log-data-with-graphs) for more information.

- Windows Server Activity
- Events Count by Channel
- Failed Logins
- Successful Logins

### Screens

Screens are collections of customized dashboards that can display data in various forms. See the topic [auto$](/docs/use-screens-and-widgets-to-monitor-log-data) for more information.

- Security log events daily and weekly trends
- Distribution of log events by event id
- Distribution of log on events by user name
- Total successful and failed authentications per week
- Total log events per week