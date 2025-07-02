---
type: page
title: Mezmo Glossary
listed: true
slug: mezmo-glossary
description: An introduction to Mezmo terms
index_title: Mezmo Glossary
hidden: 
keywords: 
tags: 
---




Below is a list of Mezmo terms found in our product. If there are any other terms that require more context, please email our support team.

[**Agent**](introducing-the-agent)
The Mezmo agent is a program that reads log files from the computer/server it is installed on and uploads the log data to your Mezmo account.

**[Alerts](alerts)**
Alerts send out alert notifications to the specified alert channel(s) whenever a log line appears in that alert's associated view.

**[Alert channels](alerts)**
These are specific places where alerts will show up. Mezmo supports integrations with email, Slack, Webhook, PagerDuty, OpsGenie, Datadog, VictorOps, HipChat and AppOptics.

**[Apps](filters#filters)**
An app can represent a log file, program or container. Typically, log lines within an app are inherently similar.

**[Archiving](archiving)**
Archiving is an automatic function that exports your logs from Mezmo to an external source. Archived logs are in JSON format and preserve metadata associated with each line.

**[Boards](graphs)**
A board is a named collection of graphs. All boards are located in the Boards List and may contain any number of graphs.

**[Categories](views#categories)**
Categories serve as ways to group similar views together, similar boards together and similar screens together.

**[Custom parsing](custom-parsing)**
Mezmo allows you to define your own parsing rules with a custom parsing template to apply to your ingested logs.

**Everything (Views)**
Default View to see every log coming into Log Viewer without any search queries or filters.

**[Exclusion Rules](excluding-log-lines)**
These specific rules can be set to exclude unnecessary logs and save on data ingested.

**[Export API](https://docs.mezmo.com/reference#v1export-1)**
Sends a cURL request with specified log lines to be emailed to the user and additional parameters.

**[Export Configuration](how-to-replicate-mezmo-configurations#to-export-configurations)**
Mezmo allows users to export their account configurations (Views, Alerts, Boards, Screens, Exclusion rules and Parsing templates) in a JSON file to be uploaded in another account.

**[Exporting Log Lines](export-lines)**
Exporting log lines provides you with a local copy of specific log lines. Log lines are exported in JSON line format (.jsonl) and are emailed to your Mezmo user email address.

**[Extract and Aggregate Fields](extract-and-aggregate-fields)**
This feature lets you extract, view, and export fields from log lines that have already been indexed. Unlike the custom log parser, this feature allows you to parse out additional fields ad-hoc from your historical logs without having to re-ingest them.

**Fields**
Fields are specific properties of logs that contain information such as an id, class, group, stream, etc.

**[Graphs](graphs)**
A graph is a visual representation of your parsed log data over time. For each graph, you can adjust the name, color, and dataset filter.

**[Groups](rbac)**
Groups are a collection of Members with specific, customizable access permissions where every user in the group shares the same permissions. Only users with the role of “Member” can be added to a group.

**[Histograms (under graphs)](graphs#breakdowns)**
Found under each graph, histograms show a breakdown of the data by plot and ENV/HOST/APP.

**[Import Configuration](how-to-replicate-mezmo-configurations#to-import-configurations)**
Mezmo allows users to import their account configurations (Views, Alerts, Boards, Screens, Exclusion rules and Parsing templates) from a JSON file downloaded from another account.

**[Ingestion API](https://docs.mezmo.com/v1.0/reference#logsingest)**
Sends a cURL request with log lines in JSON format as payload to be ingested by Mezmo.

**[Jump to timeframe](time)**
Next to the search field, this is used to filter the search results to a certain block of time.

**[Line context](context#accessing-context)**
Each log line can be parsed to show its raw data in a formatted manner with fields like the app, source and file.

**[Live Tail (Log Viewer)](how-to-use-the-dashboard#log-navigation-bar-bottom)**
Real time visibility into logs coming in — a toggle setting in Log Viewer.

**Log Format**
Customize the size of text in Log Viewer as well as the line formatting and ordering of fields for each line. Found under User Preferences.

**[Log Levels](filters#filters)**
Log Levels are a property of log lines and include (but are not limited to) INFO, DEBUG, and ERROR. Log levels are automatically parsed from log lines using standard log level detection and common patterns.

**[Log Viewer](how-to-use-the-dashboard)**
UI for surfacing logs being ingested, filterable by tags, data sources, app sources and log levels.

Metadata
Information about the log line itself rather than the specific information present in the log.

**[Raw Lines](store-and-show-raw-lines)**
See the log in its entirety, in its original format. You can enable saving and viewing raw lines for your account.

**[Roles](rbac)**
Roles are predefined titles that have default privileges. Mezmo supports 4 types of roles: Owner, Admin, Member and Read.

**[Screens](screens)**
Screens let you create detailed customized dashboards using your log data. Screens provide several configurable widgets, which display aggregate metrics about logs over a given period of time. You can use Screens to visualize overall log volume, key performance metrics (KPIs), and more.

**[Search](search)**
Located in Log Viewer, Mezmo search supports Google-like search syntax to find logs.

**[Sources](filters#filters)**
A source can be a host, computer, virtual machine, or Heroku app. Source metadata such as IP address or OS may be displayed with the source.

**[Stack Lines](graphs)**
Graphs with multiple plots can show the plots’ values aggregated together.

**Starred**
Label given to Views, Boards and Screens — if something is starred, then it will be prominently featured first in the sidebar.

**[Tags / Host Tags](introducing-the-agent#how-do-i-use-host-tags)**
Host tags allow you to group hosts automatically into dynamic host groups without having to explicitly assign a host to a group within the Mezmo web app.

**[Timeline (Log Viewer)](how-to-use-the-dashboard#log-navigation-bar-bottom)**
Available as a toggle in Log Viewer, Timeline gives a frequency histogram depicting the counts of logs from the search query.

**User Profile**
Shows your name and allows you to change your password. Found under User Preferences.

**Viewer Style**
Customize between Light Mode and Dark Mode as well as choose a particular theme for your Log Viewer. Found under User Preferences.

**Viewer Options**
Customize particular settings for your Log Viewer, including muted DEBUG statement colors and timestamp display formats. Found under User Preferences.

**[Viewer Tools (Log Viewer)](how-to-use-the-dashboard#log-navigation-bar-bottom)**
Toggle available in Log Viewer that allows you to customize how logs are shown in your Log Viewer. Specifically, this feature allows you to highlight particular terms, search and replace with regex and mark particular lines.

**[Views](views)**
Views are saved shortcuts to a specific set of filters and search queries. You can see the list of views in the Views pane on the left.

**Whitelist Domains**
List domains that will be permitted to make CORS requests to Mezmo servers.

**[Widgets](screens#adding-widgets)**
Widgets are independently configured controls used to analyze and present log data. They are the building blocks for screens.





