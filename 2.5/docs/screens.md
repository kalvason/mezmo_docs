---
type: page
title: Creating Screens
listed: true
slug: screens
description: 
index_title: Creating Screens
hidden: 
keywords: 
tags: 
---



Learn how to use Screens to display metrics and log activity in Mezmo, the easiest, fastest cloud log management software.

Mezmo Screens let you create detailed customized dashboards using your log data. Screens provide several configurable widgets, which display aggregate metrics about logs over a given period of time. You can use Screens to visualize overall log volume, key performance metrics (KPIs), and more.

To access Screens, open the Mezmo web app and select the Screens icon from the left-hand bar.



{% image url="https://uploads.developerhub.io/prod/2KW7/zx902w8ad9tac6ah1gecnuhzu4eyvf34dpob411en6au1qs7bnevwz9aij8qj250.png" caption="" mode="responsive" height="247" width="146" %}
{% /image %}



## Creating a Screen

From the Screens page, click “New Screen” in the top-left corner to open a blank Screen. From here you can add widgets and change the background color. You can also adjust the layout of the Screen by changing the aspect ratio, or by rotating the Screen 90 degrees.

## Adding Widgets

Widgets are independently configured controls used to analyze and present log data. Mezmo provides four different widget types:

- Count displays a single aggregate number.
- Gauge displays a count out of a minimum and maximum value using a gauge indicator.
- Table displays a horizontal bar chart with logs grouped by a selectable field.
- Time Shifted Graph displays a layered line graph comparing values over two different time periods (for example, log volume today vs. log volume yesterday).

To add a widget, click the “Add Widget” button in the top-left corner:



{% image url="https://uploads.developerhub.io/prod/2KW7/2r2clpqy24qz9cd6gzrgkx1fafpfulspsfia175ma8ezg4tbuvd8i8fbtkdouw4y.png" caption="" mode="responsive" height="682" width="1094" %}
{% /image %}



## Editing Widgets

After selecting a widget, you can modify its properties using the sidebar on the right side of the screen. The sidebar consists of four sections: Data, Duration, Data Format, and Appearance. Note that the contents of each section may vary depending on the type of widget selected.

## Changing the Data Source

The Data section specifies the data that is used to populate the widget including log fields, filters, and aggregate operations. By default, the data source uses all log lines. To filter the data to certain log lines, enter a filter in the “Add optional filter” text box.

For the Table and Time Shifted Graph widgets, you will also need to select a field to group events by. You can do this by selecting the widget and selecting a log field using the “Group By” combo box.



{% image url="https://uploads.developerhub.io/prod/2KW7/lkra7vgh3w5iu3f13t0c4jkzswbwuh1mk9tcb80e33a17sc766d8g41tto4mx59g.png" caption="" mode="responsive" height="202" width="235" %}
{% /image %}



## Changing the Time Period (Duration)

The Duration section sets the period of time that the widget will display data for. For example, the Count widget defaults to “Last 1 Day,” which aggregates all log lines ingested over the past day. The Time Shifted Graph widget requires two time periods: one for each line plot.



{% image url="https://uploads.developerhub.io/prod/2KW7/o761buq5ltqelv1coko6rymeiiqtlw5h6unn6ze93ra71soya5v3kj7kfdzj2ljv.png" caption="" mode="responsive" height="106" width="235" %}
{% /image %}



## Changing the Data Format

The Data Format section changes how data is displayed. The options available vary depending on the type of widget selected. For example, with Table widgets, you can specify the number of rows shown and the order by which rows are sorted.

For most widgets, you can change the formatting of large numbers. Count and Gauge widgets allow you to change the label used for the aggregate number.



{% image url="https://uploads.developerhub.io/prod/2KW7/imyt87l8d7jh3ffulsinpp6tra0re6mvykijr9q4thwb7m3zo592ma9ne5w6xkn4.png" caption="" mode="responsive" height="171" width="235" %}
{% /image %}



## Changing the Appearance

The Appearance section changes the look and feel of the widget. The Count, Gauge, and Time Series Graph widgets allow you to set a custom label. The Gauge widget allows you to set minimum and maximum values that the aggregate value is measured against.



{% image url="https://uploads.developerhub.io/prod/2KW7/vqbi2sx9ria6t17j4liq1x5o9ft5t8ld3wradfxuunq951gpej38vvlkxjkdt73v.png" caption="" mode="responsive" height="239" width="235" %}
{% /image %}



## Moving and Resizing Widgets

To move a widget, click and drag in the widget’s title bar. To resize a widget, select the widget, then click and drag on the handles located around the corners and edges of the widget.

## Deleting a Widget

To delete a widget, select the widget you wish to delete, click on the menu in the top-right corner of the widget, then select “Delete.”

## Managing Screens

To open an existing Screen, select the Screen name from the “Screens” list on the left-hand side.

## Saving a Screen

To save an open Screen, click on the “Save Screen” button in the top-right corner. Enter a name for the Screen, then optionally select or enter a category to save it under. If no category is given, the Screen will be listed under “Uncategorized.”

## Deleting a Screen

To delete a Screen, open it from the Screens list, expand the “Save Screen” menu, then click “Delete Screen.”

## Duplicating a Screen

To duplicate a Screen, open the Screen that you wish to duplicate, expand the “Save Screen” menu, then click “Duplicate Screen.” Enter a new name and category for the Screen, then click “Save.”



