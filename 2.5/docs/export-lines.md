---
type: page
title: Export Log Lines
listed: true
slug: export-lines
description: 
index_title: Export Log Lines
hidden: 
keywords: 
tags: 
---

This topic describes how to export a local copy of your log lines. Exported files are saved in [JSON line format](http://jsonlines.org/)`.jsonl`, and emailed to your Mezmo user email address. 

{% callout type="info" title="Export API" %}
You can also export your log lines programmatically using the [auto$](/2.5/export-api/ref).
{% /callout %}

1. Log in to the [Mezmo Web App](https://app.mezmo.com). 
2. In the left-hand navigation, click **Views** and select the view where you want to search for log lines to export. 
3. Enter a [search query](/docs/search) for the selected view. 
4. Enter a [time frame](/docs/time) to apply to the search results.
5. In the **Unsaved View** menu, select **Export Log Lines.**
6. Select an option to prefer newer or older lines in case the export exceeds our line limit.
7. Click **Request Export**. 

You will receive an email with a link to download your exported lines.

{% callout type="info" title="Export Limits" %}
The export log lines feature is only available under [the Professional and Enterprise plans](https://www.mezmo.com/pricing). Each plan includes an export limit, which is the number of parallel requests that you can make to the [auto$](/2.5/export-api/ref) at one time. These limits are:

**Pro plans with 3 and 7 day retention periods**: 10K log lines per request

**Pro plans with 14 and 30 day retention periods**: 20K log lines per request

**Enterprise plans**: 20K log lines per request
{% /callout %}