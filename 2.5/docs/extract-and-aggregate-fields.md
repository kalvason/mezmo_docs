---
type: page
title: Extracting and Aggregating Fields
listed: true
slug: extract-and-aggregate-fields
description: 
index_title: Extracting and Aggregating Fields
hidden: 
keywords: 
tags: 
---



## Extracting and Aggregating Fields

How to extract and aggregate additional fields from indexed logs using Mezmo, the easiest, fastest cloud log management and analysis software.

The extract and aggregate fields feature lets you extract, view, and export fields from log lines that have already been indexed. Unlike the custom log parser, this feature allows you to parse out additional fields ad-hoc from your historical logs without having to re-ingest them. The extracted fields are presented in tabular format, which you can view in the Mezmo web app or export to a CSV file.

If you want to custom parse out a field from existing logs (post ingested logs), you can extract the field that you want to aggregate with this feature. Once the custom parsing template is set up, the parsing rules will apply to existing logs that have already been ingested. You can modify the custom parsing rules until you extract the desired field. Custom and existing parsed fields can be aggregated to give insights (metrics) to help the user further diagnose the issue.

## Accessing the Extract Fields Screen

To access the Extract Fields screen, open the Mezmo web app and select the log line that you want to extract additional fields from. Open the line’s [context menu](/docs/context) and click on the **Extract Fields** button.



{% image url="https://uploads.developerhub.io/prod/2KW7/inxf197xl7p9u5ezgmj94cfhpi5qtfdr0p6ttp4pjui5dbdywj9409xxdagili6a.png" caption="" mode="responsive" height="154" width="1245" %}
{% /image %}



## Using the Extract Fields Screen

The Extract Fields screen is where you create and verify your parsing template, select the log lines that you want to extract from, perform the extraction, and view the results.

When you first open the screen, the **Reference line** text box displays the log line that you selected in the event viewer. This provides a reference line for testing your parsing template. The actual log lines to be parsed are determined by the **Query** and **Time range** fields.



{% image url="https://uploads.developerhub.io/prod/2KW7/inxf197xl7p9u5ezgmj94cfhpi5qtfdr0p6ttp4pjui5dbdywj9409xxdagili6a.png" caption="" mode="responsive" height="154" width="1245" %}
{% /image %}





{% image url="https://uploads.developerhub.io/prod/2KW7/w6gojq7he0ckwehuppk065ounwzpnp7av5ekr6v6f1wu85h78w9p5vd92kndisxr.png" caption="" mode="responsive" height="1206" width="1043" %}
{% /image %}



To exit this screen, click the X in the top-right corner of the screen.

## Creating and Performing an Extraction

To create and run an extraction:

1. Use the **Parsing templates** control to define the [parsing template](/docs/custom-parsing#parsing-operators) that will be used to parse the log line. You can use the same [parsing operators](/docs/custom-parsing#parsing-operators) as in the custom log parser. You can also use the *_Parsing result *_field to verify the output of your template.
2. Select which (if any)** auto-parsed fields** you wish to include in the result. These are fields that Mezmo automatically parsed from the log line when ingesting it. Note that selecting an auto-parsed field will limit your results to log lines containing that field.
3. Specify a **time range** to query log lines.
4. Use the **Query** box to enter or refine the [search query](/docs/search) that will be used to retrieve logs.
5. Click **Run** to perform the extraction.

Once the extraction is finished, callouts detailing the run will appear next to the run button. The first callout shows the total number of log lines processed (and whether you reached a limit on the number of lines that can be processed), and the second callout shows the percentage of processed logs that were parsed by your template. You can hover the mouse over either callout to view additional details, including any warnings or errors.



{% image url="https://uploads.developerhub.io/prod/2KW7/inxf197xl7p9u5ezgmj94cfhpi5qtfdr0p6ttp4pjui5dbdywj9409xxdagili6a.png" caption="" mode="responsive" height="154" width="1245" %}
{% /image %}





{% image url="https://uploads.developerhub.io/prod/2KW7/w6gojq7he0ckwehuppk065ounwzpnp7av5ekr6v6f1wu85h78w9p5vd92kndisxr.png" caption="" mode="responsive" height="1206" width="1043" %}
{% /image %}





{% image url="https://uploads.developerhub.io/prod/2KW7/72ehlk5roogymb55dsctcbddyelw7u8g6ifbk5d3af8e8ua5zwpkxldxlu5umpis.png" caption="" mode="responsive" height="40" width="265" %}
{% /image %}



## Viewing the Results

Once your run finishes, the results will appear in a table at the bottom of the screen. This includes the name and value of the field(s) extracted by your template, the auto-parsed fields you selected, and a Count column showing the number of logs containing the field values.

You can sort the results by clicking on any column name. You can also rearrange the columns by dragging and dropping a column name in the** Aggregated fields** box. To display the count as a percentage of the total queried log count, click the % **instead of count** button at the top of the table.

## Downloading the Results

To download the table as a CSV file, click the Download CSV button.



