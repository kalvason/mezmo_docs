---
type: page
title: Jan 25th, 2021 - LogDNA Web version 4.43.3
listed: true
slug: jan-25th-2021-logdna-web-version-4433
description: 
index_title: Jan 25th, 2021 - LogDNA Web version 4.43.3
hidden: 
keywords: 
tags: 
---



## Features and Enhancements

- Usage Quotas is a major new feature that allows users to control how much data their teams are storing in order to create predictable spend month-over-month, while still viewing, alerting on, and retaining the critical data. For more information, read the [Usage Quota documentation](https://docs.logdna.com/docs/usage-quotas).

- You can now define a default organization (account) so that when you log in to the LogDNA web application, you are automatically in your preferred organization. To do so, click the up-arrow in the bottom of the left navigation pane of the UI, next to the current organization. Then, in the list of organizations, hover over the one that you want to define as default, and select the checkbox icon that appears beside the organization's name.

## Fixed Issues

- Fixed an issue on the **Manage Team** &gt; **Groups** page where the Delete button was unresponsive on second and subsequent clicks. (LOG-8460])

- Fixed erroneous syntax for ingesting logs using syslog-ng in the documentation shown in the product UI. (SO-53)

- Fixed erroneous instructions for LogDNA Agent installation on CentOS 7 in the documentation shown in the product UI. (SO-57)

