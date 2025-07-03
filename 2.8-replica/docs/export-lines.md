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
You can also export your log lines programmatically using the [Export API](https://docs.mezmo.com/log-analysis-api/ref#export).
{% /callout %}

1. Log in to the [Mezmo Web App](https://app.mezmo.com).
2. In the left-hand navigation, click **Views** and select the view where you want to search for log lines to export.
3. Enter a [search](/docs/search-and-filter) for the selected view.
4. Enter a time frame to apply to the search results.
5. In the **Unsaved View** menu, select **Export Log Lines.**
6. Select an option to prefer newer or older lines in case the export exceeds our line limit.
7. Click **Request Export**.

You will receive an email with a link to download your exported lines.

{% image url="https://uploads.developerhub.io/prod/2KW7/ee2vsnbujbv1pijr8hexvr61kg50sktwz2wkycdemknxin2h0v9drmkvaeokrbfp.png" caption="The Export lines option in the Unsaved View menu." mode="responsive" height="287" width="293" %}
{% /image %}

{% callout type="info" title="Export Limits" %}
The export log lines feature is only available under [the Professional and Enterprise plans](https://www.mezmo.com/pricing). Each plan includes an export limit, which is the number of parallel requests that you can make to the [Export API](https://docs.mezmo.com/log-analysis-api/ref#export) at one time. These limits are:

**Pro plans with 3 and 7 day retention periods**: 10K log lines per request

**Pro plans with 14 and 30 day retention periods**: 20K log lines per request

**Enterprise plans**: 20K log lines per request
{% /callout %}