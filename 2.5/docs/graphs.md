---
type: page
title: Creating Boards & Graphs
listed: true
slug: graphs
description: 
index_title: Creating Boards & Graphs
hidden: 
keywords: 
tags: 
---


If you want to learn more about the difference between boards vs. screens, click [here](/docs/boards-vs-screens).

## Terminology

- **Graph**: A set of queries or _plots_ visualized over time. It can be visualized as a line graph, a histogram, or a pie graph.
- **Board**: A collection of graphs and breakdowns
- **Plot**: A single query plotted on a graph. Learn more [here](/docs/graphs#managing-plots).
- **Breakdown**: A graph visualized as a histogram or a pie graph. It is essentially a distribution of field values for a set of plots in a graph. Learn more [here](/docs/graphs#breakdowns).
- **Filter**: A query used to refine results for plots Learn more [here](/docs/graphs#filters).
- **Screens**: A dashboard of configurable widgets to display metrics about your logs to view list of the widgets available in this view. Learn more [here](/docs/screens).

## Boards

A board is a named collection of graphs. List of all your boards can be found in the [Log-viewer sidebar] (/how-to-use-the-dashboard) on the left. Changes made to a board are automatically saved. Similar to views, all of your users have access to all boards in your account.

### Managing a board

- **Create a board**: Click the `New Board`
- **Duplicate a board**: Click on the board you want to duplicate. Then click `Duplicate Board`
- **Delete a board**:  Click the `Delete` at the top of the board
- **Filter a board**: Click the `funnel icon` at the top of the board and type query to filter all plots on all graphs in this board
- **Time Range**: Click into the `time duration field` on the top right to present a time range.
- **Live**: Used to display live data in your graphs
- _* Favorite Boards_: Mouse over Mouse over the board in the menu bar to reveal the `star` icon

## Graphs

A graph is a visual representation of your parsed log data over time. You can only create a graph after you have created a board.  For each graph, you can adjust the name, color, and dataset filter. Each data point coincides with a log line so you can click-in to understand where that datapoint is coming from.

### Creating a graph

1. Create a new board by selecting the `+ New Board` button.
2. Click the `+Add Graph` button at the bottom of the page.
3. Choose a plot or query system field to visualize on the graph.
4. For string fields, count is the only possible metric for plotting values . However, for numeric fields, you can choose counts, min, max, average, sum, diff, or select percentiles. For more details, see [Understanding Metrics](/docs/graphs#understanding-metrics).
5. Optionally filter your dataset using our google-like [search syntax](/docs/search). For numeric fields, you can find filtering under `Advanced Filtering`.
6. Click the `+Add a Graph` button.
7. Congratulations! You made your first graph!

### Add another plot to a graph

1. Under the graph, click the `+Add Plot` button
2. Select a field to plot
3. Optionally select a value or apply an advanced filter
4. Click the `Save` button to add the new plot to graph
5. Change the line color by clicking on the colored icon beside the plot value

### Managing a graph

At the top of the graph you can modify the following properties (from left to right)

- **Name a graph**: Click `pencil icon` to edit the name
- **Operation function**: Choose a metric used to plot the data (eg. count, max/min, average etc.). Learn more [here](/docs/graphs#understanding-metrics).
- **Stack Lines**: Place multiple lines together. on the same graph as a percentage of all other line values.
- **Filter a graph**: Click the funnel icon and type a query to add a filter to all plots in the graph
- **Duplicate a graph**: Click the `two overlapping squares` icon
- **Delete a graph**: Click the `trash` icon
- **Reorder a graph**: Click the up or down arrow to reorder a graph's position within the board
- **Change line colors** - Under the graph, click the colored circle beside the variable name

### Interacting with a graph

There are a number of ways to interact with a graph to gleam meaningful information.

- Mouse over a graph to see the value of each plot at that point in time
- Click a point in the graph and select the `Show Logs` button to jump to those logs
- Click and drag on a graph to select an area to zoom in on

### Managing plots

All the plots are listed underneath their corresponding graph to the right of the line color used to represent that plot.

- Click on the downward arrow next to a plot to **Edit**, **Delete**, or **Hide** a plot
- Click on the circle next to a plot to change that plot's line color
- Learn how to add more plots [here](/docs/graphs#add-another-plot-to-a-graph)

## Breakdowns

A breakdown are essentially a _histograph_ or _pie graph_ view of your main graph. It is a cross-sectional field value distribution of the aggregated plots in your graph. For example, to see the distribution of request values for the HTTP response codes on a graph, create a breakdown for that graph on the request field.

### Adding a breakdown to a graph

1. Locate a graph you wish to create a breakdown for.
2. Expand the downward arrow under the center of the graph
3. Select a breakdown type (e.g. histogram)
4. Choose a field to distribute values on (e.g. request)
5. Click the `Add Breakdown` button

### Adding another breakdown to a graph

1. Locate a graph you wish to create another breakdown for
2. Expand the downward arrow under the center of the graph
3. Click the + Add button on the right
4. Select a breakdown type (e.g. histogram)
5. Choose a field to distribute values on (e.g. verb)
6. Click the **Add Breakdown** button

### Interacting with a breakdown

There are a number of ways to interact with a breakdown to gleam meaningful information.

- Mouse over a breakdown bar to view the values for that bar
- If there is more than one breakdown for a graph, click on the left and right arrows in the top left of the breakdown to rotate through the breakdowns for that graph. You can also click on the circles at the bottom to select the position of a particular breakdown in the carousel

### Deleting a breakdown from a graph

1. Locate a graph you wish to delete
2. Expand the downward arrow under the center of the graph
3. If there is more than one breakdown for this graph, use the arrows in the top left to rotate to the desired breakdown
4. Click the `X` delete button on the right

### Filters

A filter is a refined query that can be applied to a plot, graph, or board

- **Plot filter**: A refined query only applied to that plot. Depending on the plotted field, it may be located under the Advanced Filtering option for that plot (see [Managing Plots](#managing-plots) for more details).
- **Graph filter**: A refined query applied to all plots on that graph. Click the funnel icon in the top left of the graph to set a graph filter.
- **Board filter**: A refined query applied to all plots in all graphs on that board. Click the text box next to the funnel icon on the top left of the board to set a board filter.

## Understanding metrics

A metric is an aggregate function that transforms a graphed dataset in a particular way. While you can graph any parsed field, only numeric fields can utilize the full list of metric functions. All metric functions only apply to data that contains the selected field and matches the applied dataset filter.

- **Counts**: Counts the number of lines in each interval. This is the only metric function that can be applied to string fields.
- **Min**: Returns the lowest value for each interval.
- **Max**: Returns the highest value for each interval.
- **Average**: Returns the average value for each interval
- **Cumulative**: Returns the sum of values for each interval
- **Diff**: Returns the largest difference between values for each interval
- **Percentiles**: Returns the Nth percentile of a set of values for each interval. You can choose from the 75th, 85th, 95th, and 99th percentile presets.


{% image url="https://uploads.developerhub.io/prod/2KW7/9ohsdfslvoc400jtd9px2iv6vf0ehw2o22mhver416ausx8hvvoqn1k66jc98ee2.png" caption="" mode="responsive" height="449" width="1317" %}
{% /image %}


