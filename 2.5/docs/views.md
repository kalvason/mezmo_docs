---
type: page
title: Creating Views
listed: true
slug: views
description: 
index_title: Creating Views
hidden: 
keywords: 
tags: 
---



Views are saved shortcuts to a specific set of filters and search queries. You can see the list of views in the Views pane on the left.
If this is your first time using Mezmo, you will only see the default Everything view, which shows you all log lines.

## Categories

Categories can be created and chosen to group your `views` (or `boards` or `screens`).  As a default, when you save a new view, It will save it under a category named `UNCATEGORIZED` unless it's specified. Views are unique within Mezmo but you can have more than one categories for each view.

Go to `Settings` &gt; `Categories` to easily edit, add, drop and drag your views into different categories.

## Creating a view

1. Set the sources, apps, and/or log level filters as well as perform any search queries to get desired set of log lines.
2. Click the `Unsaved View` button at the top and select `Save as New View/Alert`.
3. Name your new view, and hit `Save`. At this step, you can also choose the option to either create a new `category`, or you can choose an existing category from the list for the view.

## Alerts and Views

Alerts can only exist with a saved view. Send out alert notifications to the specified alert channel(s) whenever a log line appears in that alert's associated view. A bell icon is also displayed to the right of the view name to indicate that this view has an alert attached to it.  Learn how to set-up [Alerts](/docs/alerts).

## Export Lines in this view

You can export the lines found within any view by selecting `Export Lines` and specifying a time range. A compressed .jsonl file is sent to your email when your export is ready.

### Update a view

As you add additional filters to your view, you can update your view to include it. For example if you only want to see logs from a specific source, you can select that and then click on `Update view` to save it.

You can also choose `View Properties` to add a description to the View and also specify how the lines can be displayed.

## Managing views

A number of options are available to help you manage your views.

### Accessing a view

Your newly created views will appear in the views pane on the left under the categories that it belongs to and will persist even after you log out. To see the log lines, as well as the filter and search options associated with a view or alert, simply expand the category and click on the name of that view. If you have more than twelve (12) views, you can use the View Finder feature in the Views pane on the left to search for a particular view. You can use the `Find View` top search bar in the view pane or press ⌘K on your keyboard to find a particular view.

### Deleting a view

1. Click on the name of the view you wish to delete in the views pane on the left.
2. Click the name of the view in the drop-down menu at the top, and select `Delete`.
3. A confirmation prompt will appear. Click the red `Delete` button to confirm the deletion of the view.

Deleting view will remove it completely from the system. If the view exists in multiple categories, it will disappear from each one. If you want to delete your view from a category, go to Manage Views page. Deleting a view will also delete any attached alerts.

### Duplicating a view

1. Expand the category and click on the name of the view you wish to edit in the views pane on the left.
2. Click the name of the view in the drop-down menu at the top, and select `Save as New View/Alert`.
3. Name your view, optionally attach any desired alerts, and click `Save`.

You can also use this method to attach an alert to an existing view.

### Editing a view

1. Expand the category and click on the name of the view you wish to edit in the views pane on the left.
2. Click the name of the view in the drop-down menu at the top, and select `Edit View Properties`.
3. Optionally enter a new name for that view in the `Rename View` text box.
4. Optionally configure a custom line template for that view. For more details, see [Understanding Custom Line Templates](#understanding-custom-line-templates).
5. Click the green `Save` button.

The changes made in the view can be seen in all the categories of the view.

### Starring a view

This will add the view into the Starred section on top of the view pane.

1. Expand the Category and click on the Star icon on the left side of the view name.

### Unstarring a view

1. In the Starred section, hit the Star icon on the left side of the view name you wish to un-star.

### Creating a category

1. Click `Manage` under the views pane.
2. Click `Add a Category` button under the categories section.
3. Enter the name of the category and click `Add`.

### Adding a view to a category

1. Click `Manage` under the views pane.
2. Select an existing view under All Views section and Drag&Drop to the desired category on the categories section on the right.

### Deleting a category

1. Click `Manage` under the views pane.
2. Find the category under the categories section and hit delete appears on the right to the category name.

Deleting a category does not delete the views associated with the category.

### Attaching an alert

1. Click the name of the existing view you wish to attach an alert to.
2. Click the name of the existing view in the drop-down menu at the top, and select `Attach an Alert`.

### Edit alert

1. Click the name of the existing view with an alert you wish to edit the alert of.
2. Click the name of the existing view in the drop-down menu at the top, and select `Edit alert`.

### Detaching an alert

1. Click the name of the existing view with an alert you wish to detach the alert from.
2. Click the name of the existing view in the drop-down menu at the top, and select `Detach an Alert`.

### Embedding a view



{% callout type="warning" title="Warning" %}
This option is being deprecated as of February 22, 2021. After that date, you cannot create or update an embedded view. On March 29th, 2021, embedded views will be disabled and removed. For more information, please refer to [https://mezmo.com/blog/sunsetting-embedded-views/](https://mezmo.com/blog/sunsetting-embedded-views/).
{% /callout %}



1. Click the name of the existing view you wish to embed.
2. Click the name of the existing view in the drop-down menu at the top, and select `Embed this View`.

For detailed information on embedded views, see the Embedded Views guide.

### Organizing views

By default, views are arranged in the alphabetical order. You can star your views and re-order them by clicking and dragging the left side of a view. While all categories and views are shared across the entire organization, the content and order of the starred views section can be personalized by each user.

## Understanding custom line templates

Located under Edit View Preferences, custom line templates allow you to configure how your logline messages are displayed in that view. **Custom line templates do not change the way your log lines are parsed or searched, only the way they are displayed in that specific view**.

For example, if I have a view that displays log lines with the following message:



{% code %}
{% tab language="none" %}
user 1234 requested endpoint /api/endpoint
{% /tab %}
{% /code %}



And contains the following field metadata:



{% code %}
{% tab language="none" %}
{
meta: {
first_name: Jane
last_name: Doe
}
}
{% /tab %}
{% /code %}



If I use the following custom line template:



{% code %}
{% tab language="none" %}
{{_meta.first_name}} {{_meta.last_name}}, aka $@
{% /tab %}
{% /code %}



This will display log messages in that view in this format:



{% code %}
{% tab language="none" %}
Jane Doe, aka user 1234 requested endpoint /api/endpoint
{% /tab %}
{% /code %}



When you configure a custom line template, you can use any field data available to you for that line, including the line itself, represented as `$@`. For JSON, you can use the field name directly to reference the field value like this: `{{first_name}}` or prefixing it with an underscore like `_meta` if it is a [reserved field](https://docs.mezmo.com/docs/ingestion#reserved-fields).

Please keep in mind that field elements and static text in a custom line template cannot be searched as normal substrings since they are for display only. All field data must still be searched in the following format: `field:value`. For more details on our search syntax, check out our [search guide](/docs/search).



