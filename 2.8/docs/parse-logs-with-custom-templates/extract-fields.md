---
type: page
title: Extract Fields
listed: true
slug: extract-fields
description: 
index_title: Extract Fields
hidden: 
keywords: 
tags: 
---


Extract fields lets you parse additional fields from your historical logs without re-ingesting them. Extracting fields is used as needed and does not change how the logs are seen in the Log Viewer.

1. To Extract fields, select the line you want to extract in the Viewer, then click **Extract Fields**. This will take you to the Extract Fields screen.

{% image url="https://uploads.developerhub.io/prod/2KW7/vgylnp9aefwenfkfs8s8odza5lt29tzorgucjro7vl6267fw1ulj8t9wiih0aqht.png" caption="Click a log line to reveal the extract fields functionality" mode="responsive" height="252" width="1632" %}
{% /image %}

1. Check the reference line is correct. This is what your parsing will be based on.
2. Choose an extractor type to parse the information needed.
3. Select the auto parsed fields to include. Selecting an auto-parsed field will limit your results to log lines containing that field.
4. Set the time range. The time range is limited based on your plans retention.
5. Enter the query to further refine what logs will be returned.
6. Once you run the query, you'll be able to see the results in a table at the bottom of the screen.

    1. The Processed callout shows the total number of log lines processed and if you reached a limit on the number of lines that can be processed
    2. The Matched callout shows the percentage of processed logs that were parsed by your template. You can hover either callout to view additional details, including any warnings or errors.

7. You can also sort the columns and drag the column names to sort them.
8. Download the results as a CSV.

{% callout type="success" title="Custom Parsing" %}
If you need to parse your logs before they are ingested, create a Custom Parsing Template.
{% /callout %}