---
type: page
title: Restore Log Data
listed: true
slug: data-restoration
description: Use the Mezmo Data Restoration feature to restore log data from your archives to search, review, and analyze.
index_title: Restore Log Data
hidden: 
keywords: 
tags: 
---

Mezmo's Log Data Restoration feature provides a way to re-ingest, or restore, archived logs from cold storage so you can [search and filter](/docs/search-and-filter) logs and in the Mezmo user interface. Restoration is useful for troubleshooting older bug tickets, as well as bringing up additional context from older logs beyond your retention period.

## Feature Notes

- Your account must have [log archiving](/docs/archiving) enabled to use the Log Data Restoration feature
- Mezmo supports restoration from [AWS S3 and Google Cloud Storage ](/docs/export-logs-to-external-storage)archives
- On [AWS S3](/mezmo-developer-docs/2.6/docs/export-logs-to-external-storage), object ownership needs to be set to [object writer](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-ownership-new-bucket.html#:~:text=Object%20writer%20(default))
- The Mezmo system requires **read** access to the stored logs
- By default, each restoration task will be ingested for the same period of time as your normal logs
- Data Restoration is included in [
the Community, Pro, and Enterprise plans
](https://www.mezmo.com/pricing)

## Create a New Log Data Restoration Task

1. Log in to [the Mezmo Web App](https://app.mezmo.com).
2. In the left-hand navigation, go to **Settings &gt; Archiving &gt; Log Data Restoration**. 
3. Click **New Restoration Task**.
Here you can name your task, select a time range for logs, and select the exact files to restore from that time period.
4. Click **Start** to begin the process of restoring logs.
Depending on the size of the restored logs, the task may take anywhere from 15 minutes to up to two ho

## View Restored Log Data

When your restoration task is complete, you can view and [search log content](/docs/searching-log-contents) in the same way as you would logs that were directly ingested. 

1. Log in to [the Mezmo Web App](https://app.mezmo.com/).
2. In the left-hand navigation, click the **Restored Tasks** icon.
3. Select a **Log Restoration Task** to view and search its contents.