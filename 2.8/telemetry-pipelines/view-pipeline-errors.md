---
type: page
title: View Pipeline Errors
listed: true
slug: view-pipeline-errors
description: 
index_title: View Pipeline Errors
hidden: 
keywords: 
tags: 
---

## Error Indicators

If an error is generated during the processing of data in your Pipeline, a red indicator will appear next to the name of the Pipeline, as well as on the node where the processing error occurs. Hover your mouse over the indicator on the node for more information about the error. The [auto$](/telemetry-pipelines/error-code-reference) contains more information about the specific types of errors for each Processor. 

{% image url="https://uploads.developerhub.io/prod/2KW7/avtop0omzu48t7wuec41zjsqxayex55jspe0tg1xlg3fshgnqdr58c48wntcsnxk.jpg" caption="This screenshot shows the error indicators for the OTEL-Replay Pipeline and the Parse Processor." mode="600" height="321" width="825" %}
{% /image %}

## View Error History

You can view the errors for any Pipeline by accessing its **Error History**. 

1. Log in to the [Mezmo Web App](https://app.mezmo.com). 
2. Click **Pipelines** in the Admin Panel. 
3. Under **Deployed Pipelines**, click the arrow next to the Pipeline you want to view to open the **Pipeline Menu**. 
4. Click **Error History**. You will see a list of errors in order by **Timestamp,** along with information about the type, the affected node, and the error message.   You can also search errors using character and term matching. 

{% image url="https://uploads.developerhub.io/prod/2KW7/3fye3anp5vhbzmi39w6va5nadgykhojx79vjikcosqhwqy440p058gexilyjaqub.png" caption="An example error" mode="600" height="345" width="990" %}
{% /image %}

## View Log Lines for Errors

You can view the specific log lines that have caused errors. 

1. Open  the **Error History** for the Pipeline.
2. Click the arrow next to the error to view the log line that caused the error. 

{% image url="https://uploads.developerhub.io/prod/2KW7/rcn1l4kp71n82zo0m64l7ynst9l5zl1r6txrx1jt1t9ol7esm1ug0062oxzejssp.png" caption="The log line associated with the error" mode="responsive" height="549" width="1085" %}
{% /image %}

## Error Retention

- Pipeline error logs are retained for 10 days.  A scheduled task runs every 12 hours and deletes logs that are over 10 days old. 
- If a repeat error occurs, only the timestamp is updated , and the additional log entries are not retained