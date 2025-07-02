---
type: page
title: Working with the Timeline Visualization
listed: true
slug: working-with-the-timeline-visualization
description: 
index_title: Working with the Timeline Visualization
hidden: 
keywords: 
tags: 
---



## About the Timeline

The Mezmo Timeline is an important tool for visualizing patterns and trends in log lines within a user-specified timeframe. By default, the Timeline displays a visualization of the most recent 60 minutes worth of log lines.

You can use your cursor to click in the Timeline and "zoom in" (or scope in) to a specific time range in the timeline (even down to seconds). The log lines selected by scoping in are loaded in the Log Viewer, the main pane of the application UI, allowing you to more closely inspect the lines and look for repeated errors or other patterns.

After inspecting the selected log lines, you can then either reselect a subset of the selected area to scope even further in to a shorter timeframe, or zoom back out to a wider frame by selecting an option from the  **Time scale** drop-down list.

### Main use cases

- View the counts of logs that match a specific query to understand how often the same error or action is occurring in a timeframe of interest.
- Debug issues that occurred during a specific timeframe (i.e. when a known state change happened) in order to do root cause analysis (RCA).
- Determine exactly when a certain error or issue first started occurring.

### Considerations

- The reset button (the circular arrow to the right of **Time scale** field) takes you back to the default timeline, showing the visualization of the last 60 minutes of log lines.
- Note that when the Log Viewer is in 'live tail' mode, the timeline graph is a few minutes behind the Log Viewer display.
- As you select a specific period of time in the Timeline via clicking or dragging, As you select will populate the  [**Jump to timeframe**](https://docs.mezmo.com/docs/time) field. This field is always the "source of truth" for what is loaded into the Log Viewer. You can overwrite the auto-populated value in the field to use the **Jump to timeframe** independently of the timeline visualization "scope in" functionality.
- Using the "Time scale" selector will not change the **Jump to timeframe** field, it will only zoom in and out the data displayed in the Timeline to allow for graphing time scales independent of the Log Viewer.
- As you "scope in" each bar in the timeline represents 15 minutes.

## Using the Timeline Visualization

Review the following sections for step-by-step instructions.

The timeline is by default displayed on the right vertical pane of the Mezmo application UI.



{% image url="https://uploads.developerhub.io/prod/2KW7/sggt1mhs33u7goys3o5rqm3fj0w6ryoaqyqveeqnfhh8rwi6b9zlredks1l3fig8.jpg" caption="" mode="responsive" height="903" width="323" %}
{% /image %}



If you do not see the timeline, use the **expand left** icon in the upper right of the compressed timeline to display the full timeline.



{% image url="https://uploads.developerhub.io/prod/2KW7/sggt1mhs33u7goys3o5rqm3fj0w6ryoaqyqveeqnfhh8rwi6b9zlredks1l3fig8.jpg" caption="" mode="responsive" height="903" width="323" %}
{% /image %}





{% image url="https://uploads.developerhub.io/prod/2KW7/m555d3knmmt7uvi1ncclpbzd8xer8yhh3614qjto1qksf4ghmztqd4tbie1tadsv.jpg" caption="" mode="responsive" height="539" width="236" %}
{% /image %}



### How to zoom in to a specific range

To zoom in (scope in) to a smaller time frame than the default of 60 minutes, use one of the two options:

- Place your cursor in the timeline, click to select, and then drag up or down the timeline to select a time frame
- Click the downward arrow beside the **Time scale** field to display the drop-down list, and then select a predefined time scale (range).

After you "scope in" to a specific range,  the whole timeline redraws to show only the specific time scale that you selected, and the log lines for the selected period display in the Log Viewer.

Optionally, you can scope in yet further in that selected time scale to see an even more granular set of log lines in the viewer. You can not use the **Time scale** selector to zoom in further than your current time frame selection.

### How to zoom back out to wider range

To zoom back out to a broader time scale, click the downward arrow beside the **Time scale** field to display the drop-down list, and then select a predefined time scale (range).

Note that the time scale you select from the drop-down list represents a superset; that is, a larger period of time that covers _both before and after_ the time scale that you originally zoomed in on.

For example, if your original time scale that you zoomed in on was 10 minutes, and then you select **30 minutes** as your new "zoom back out" time scale, you will see log lines for: the 10 minutes preceding your selected 10 minutes, your selected 10 minutes (shown within the **bracket**), plus the following 10 minutes.

This allows you to examine the time frame immediately preceding and following the time of your original interest.



{% image url="https://uploads.developerhub.io/prod/2KW7/sggt1mhs33u7goys3o5rqm3fj0w6ryoaqyqveeqnfhh8rwi6b9zlredks1l3fig8.jpg" caption="" mode="responsive" height="903" width="323" %}
{% /image %}





{% image url="https://uploads.developerhub.io/prod/2KW7/m555d3knmmt7uvi1ncclpbzd8xer8yhh3614qjto1qksf4ghmztqd4tbie1tadsv.jpg" caption="" mode="responsive" height="539" width="236" %}
{% /image %}





{% image url="https://uploads.developerhub.io/prod/2KW7/ztk4lnkks42qqn920hx49sfx85jyneylenv7ycezsynp298zjyozx6zutycqr7tx.jpg" caption="" mode="responsive" height="1320" width="886" %}
{% /image %}



To have your Log Viewer "zoom out" as well, click and drag a larger time range in the Timeline and click "Scope in" to change the Log Viewer's time frame.

Optionally, you can choose to zoom further out by again selecting a broader time range from the **Time scale** drop-down list. Or you can click the reset icon to dismiss your original selection (shown in the brackets) and return to the default of 60 minutes.



