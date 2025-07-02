---
type: page
title: May 11th, 2021 - LogDNA Release Notes
listed: true
slug: may-11th-2021-logdna-release-notes
description: 
index_title: May 11th, 2021 - LogDNA Release Notes
hidden: 
keywords: 
tags: 
---



## LogDNA Web Application, version 4.104.0

### New Features and Enhancements
LogDNA is pleased to announce the following highlight of this release:

- Webhooks enhancements: in this release we have added additional tokens, which enable you to customize exactly what content you want to extract from your logs and then include in your third-party service’s notifications. The following new tokens allow you to further customize the webhook body with specific information about the view or the matched lines that triggered the alert:
- `{{ url }}` The full URL of the View, with first matched line when possible
- `{{ query }}` The query of the View to which this alert is attached
- `{{ app }}` Single application included in the first line of the log
- `{{ host }}` Single host included in the first line of the log
- `{{ tag }}` Single tag included in the first line of the log
- `{{ line }}` The exact text of the first line of the log
- `{{ line_objects }}` Array of matched line objects
- `{{ first_line_object }}` First matched line object (the entire line)

Learn more in our [documentation](https://docs.logdna.com/docs/webhook-alert-integration) about using the LogDNA webhooks integrations.  [LOG-7857]

### Changes

- For contract customers, the Billing Overview page has changed to make it more clear that you do not change the plan from this page. A message now displays, stating that you should contact customer support because you might have additional incentives applied to your plan. [LOG-9449]

### Fixed Issues

- We fixed an issue where entering text into the search bar without pressing Enter to start the search, and then clicking the "Jump to" option in the Timeline incorrectly scoped the Timeline graph. [LOG-9586].
- Live tail behaviour fixed; when user scrolls up to view older files then back down view to newest files, live tail now automatically turns back on (if it was previously on).  [LOG-8948]
- When Usage Quotas are configured, the email addresses for all Admin users are automatically added as alert recipients. [LOG-9309]

## LogDNA Agent

For the most recent release information about the LogDNA Agent, refer to [agent-specific Release Notes](https://docs.logdna.com/changelog).

## LogDNA Integrations

There are no external-facing changes to our LogDNA integrations in this release.

## LogDNA APIs

There are no external-facing changes to our LogDNA APIs in this release.



