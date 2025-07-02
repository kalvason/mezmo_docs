---
type: page
title: Filtering Logs
listed: true
slug: filters
description: This guide shows you how to use filter log events using source, app, and level filters.
index_title: Filtering Logs
hidden: 
keywords: 
tags: 
---



This guide covers how to use the source, app, and level filters located at the top of the page in the [Mezmo web app](https://app.mezmo.com/).



{% video videoId="XQk4Ket49_4" provider="youtube" %}
{% /video %}



Before we begin, keep in mind that filters are applied in conjunction with search and time queries. Any specified search queries and timeframes are respected in addition to the filters themselves.

## Filters

- **Source** contains a list of your logging sources. A source can be a host, computer, virtual machine, or Heroku app. Source metadata such as IP address or OS may be displayed with the source.
- **App** contains a list of logging buckets. An app can represent a log file, program or container. Typically, log lines within an app are inherently similar.
- **Level** contains a list of parsed log levels, such as `INFO`, `DEBUG`, or `ERROR`. Log levels are automatically parsed from log lines using standard log level detection and common patterns.

## Behavior

To use filters, click on the desired filter drop-down menu and tick the checkboxes of the entries you are interested in. Selecting more than one checkbox within a filter will include log lines that belong to any of the selected entries. Selecting checkboxes in more than one filter, such as selecting 1 app and 1 source, will return log lines that match both that app and that source.

For example, if I select two sources, `Oprah` and `Colbert`, and then select two apps, as `iMessage` and `Snapchat`, I will be returned all log lines matching the following conditions:
(`Oprah` AND `iMessage`) OR (`Oprah` AND `Snapchat`) OR (`Colbert` AND `iMessage`) OR (`Colbert` AND `Snapchat`).

Summary:

- Selected entries within a filter are OR'd
- Selected entries across filters are AND'd

## Categories

The sources and apps filters include categories to help organize your sources and apps. For the sources filter, the categories are hosts, groups, and inactive hosts. For the apps filter, the categories are groups, apps, and files. You may see additional categories in the future.

## Search

For the sources and apps filters, you can use the built-in search bar inside the filter menu. For example, if one of your sources was named 'Madonna', searching 'mdon' under Sources would return 'Madonna' as one of the results. Search results are also categorized by type.

## Groups

Within the apps and sources filter, you can create groups that represent a set of sources or apps. To create a group:

1. Click on either the source or app filter, and then select the create new group option at the top of the drop-down menu.
2. Name your group.
3. Select the set of sources or apps you would like to associate with this group.
4. Click the green save button at the bottom of the modal.

When you select the group in the source or app filter, it will return all log lines matching any of the entries within that group.

## Dynamic Groups

Dynamic groups allow your hosts to automatically manage their dynamic group membership. To configure your hosts to automatically add themselves to dynamic groups ensure you are using the Mezmo agent to collect your logs. See the [host tags section of the Mezmo Agent article](/docs/introducing-the-agent#how-do-i-use-host-tags) or the [host tags section of the rsyslog article](/docs/rsyslog#host-tags) for configuration details.

## Metadata

If you mouse over an entry, depending on which category, additional details may be displayed. For example, under the Sources filter in the host section, mousing over an entry may show the IP address, operating system, and other details.



