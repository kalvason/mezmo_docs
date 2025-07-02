---
type: page
title: Navigating the Dashboard
listed: true
slug: how-to-use-the-dashboard
description: 
index_title: Navigating the Dashboard
hidden: 
keywords: 
tags: 
---



After logging into the Mezmo web app, you will see the main logging dashboard. As long as `LIVE` is highlighted on the bottom right, you will see new log lines automatically show up and scroll to the latest.

## Here are the menus accessible on the log dashboard

- [Main Navigation menu (Far Left)](#main-navigation-menu-far-left)
- [Log Viewer menu (Top)](#log-viewer-menu-top)
- [Log Viewer Sidebar (Left)](#log-viewer-sidebar-left)
- [Log Navigation Bar (Bottom)](#log-navigation-bar-bottom)

Main Navigation Menu (Far Left)

On the left-hand bar, you can access Mezmo’s features through 4 main buttons:

- **Views** - Your "everything" view of your logs and is where you can manage saved views.
- **Boards** - Your collection of graphs.
- **Screens** - Your collection of screens.
- **Settings** - Your configurations and settings for Mezmo features such as alerts, archiving, billing, integrations, parsing, team, and more.

Other additional buttons:

- **View Finder** -  to quickly pull up a saved view or board or screen. You can also use this as a short cut to search logs no matter where you are in the Mezmo app.
- **Help Button** -  to access all of our How-To documentation. The “Logging Setup” is one of the most useful features because it readily gives you instructions on how to add your log source. Simply choose the type of your log source and ingest!
- **Toggle Sidebar Button** - to collapse the [log viewer sidebar menu](#log-viewer-sidebar-left) to give yourself more room to look at log lines.

## Log Viewer Menu (Top)

Find and access all saved views or filter view logs by `tags`, `sources`, `apps` or `log levels` using this menu bar.

The `⚡Everything` view is the one created by default when your account is created. When you click on the name of your current view, a menu appears to either save an `Unsaved View` as a new view or to edit the saved view. To learn how to create a view, update a view, attach an alert and more, refer to our [Views](/docs/views) documentation.

`All Tags`: When you [send logs](/docs/ingestion) to Mezmo you can add tags to your logs so that you can filter and display them here.

`All Sources`: When you click on this menu you will see all your hosts that are sending logs to Mezmo. You can search by host name and also mouse over the name to get more details about the host. When you select multiple hosts and apply the filter, you can click on Sources again to save this selection of hosts as a group with the button `Save as a group`.

`All Apps`: You can filter by logs from an app, container or file. Similar to above, you can select multiple apps to filter by and then return to this menu to group your selection.

`All Levels`: Each log line can indicate a log level and you can select the log levels you'd like to filter by or `N/A`.

## Log Viewer Sidebar (Left)

This is the sidebar between the main navigation menu and the live tail. Here you can create **categories** for all of your `Saved Views`, `Saved Boards`, `Saved Screens`, and `Settings` options.
At the very bottom, you can also view, join, and manage your organization, as well as quickly view your billing plan and the data usage for the month. Learn more here on [How to Manage Organizations](/docs/organization).

**How do you favorite views/boards/screens?**

- Simply hover you mouse over the name of your view/board/screen and click on the  ★

**How do you bulk manage categories of views/boards/screens?**

- Go to Settings -&gt; Categories OR hover over the `Views`(or `Boards`  or `Screens`) heading and click `Manage`
- Easily edit, add, drag and drop saved views/boards/screens into a desired `Category`.
- The views/boards/screens that do not have a category will be displayed under the label `Uncategorized`.

## Log Navigation Bar (Bottom)

This bottom bar is your go-to on how to [Search for Logs](/docs/search), [How to Jump to Timeframe](/docs/time), how you want the log lines to look, and how to enable `Live Tail` and `Timeline`.

There are 6 main components of this lower navigation bar (left to right):

- **Changing the Contrast** - Toggle between the light and dark themes for your log viewer.
- **Search box** - Use simple google-like syntax to search through your logs. This [quick reference](/docs/search) will also help you search like a pro. There is also a helper tool tip beside the search bar that gives you some help with the syntax as a quick reference. Searches are performed in conjunction with filters and time queries. Any specified timeframes, sources, apps, and log levels are respected in addition to the search query itself.
- **Jump to Timeframe** - Narrow down the logs to a specific timeframe within your retention time. This is great for troubleshooting an incident.  You can use both relative time, e.g. `an hour ago` and absolute time, e.g. `Oct 6 at 5pm` . Learn more on [How to Jump to Timeframe](/docs/time)
- **Log Viewer Tools** - Use this menu to format the log lines in the live tail. Everything you do here manipulates the log lines displayed in the app for display. It does not modify the log data in any way.
- highlight terms with a yellow and turquoise color
- search and replace terms, similar to [sed](https://en.wikipedia.org/wiki/Sed)
- formatting the line template
- dropping a marker on the screen
- disable or enable line-wrap
- persist these settings
- **Timeline**  - Toggle this button to show a histogram of number of occurrences of the log search results.
- use it as a convenient way to visualize your log events and determine time ranges of interest by inspecting patterns in your logging activity.
- see line count breakdowns in the search results across your entire retention period.
- use the Timeline capability to find out when an error message occurred, at what other times this same error message appeared, and if there was a pattern.



{% image url="https://uploads.developerhub.io/prod/2KW7/82adywckuq8x7s008h30prpb13ue87o5yix2xugus2uixpua6eax4jm4fhzq1qdo.gif" caption="" mode="responsive" height="363" width="443" %}
{% /image %}



- **Live Tail**  - The bottom right of Mezmo dashboard is the button you use to enable or disable `Live Tail`. When enabled, you get a real-time stream that is updated as soon as Mezmo receives new log data.



