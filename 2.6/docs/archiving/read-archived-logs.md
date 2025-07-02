---
type: page
title: Read Archived Logs
listed: true
slug: read-archived-logs
description: 
index_title: Read Archived Logs
hidden: 
keywords: 
tags: 
---

Mezmo log files are exported and stored in zipped JSON Log files format. There are several tools you can use to re-ingest and parse the historical data in your archived logs, including the Mezmo Data Restoration feature, Amazon Athena, Google BigQuery, IBM SQL Query, and jq. 

## Mezmo Log Data Restoration

Log Data Restoration let you re-ingest, or restore, archived logs from cold storage so you can search the log data in the Mezmo user interface. Restoration is useful for troubleshooting older bug tickets, as well as bringing up additional context from older logs beyond your retention period. You can find more detailed information in the [Restore Log Data](/docs/data-restoration) topic. 

## Amazon Athena

Amazon Athena is a serverless interactive query service that can analyze large datasets residing in S3 buckets. You can use Amazon Athena to define a schema and query results using SQL. More information about Amazon Athena is available [i](https://aws.amazon.com/athena/)n [the AWS Athena documentation](https://aws.amazon.com/athena/).

## Google BigQuery

Google BigQuery is a serverless enterprise data warehouse that can analyze large datasets. You can find more information about Google Big Query in [the official documentation](https://cloud.google.com/bigquery/). 

## IBM SQL Query

[IBM SQL Query](https://www.ibm.com/cloud/sql-query) is a serverless data processing and analytics service for large volumes of data stored on IBM Cloud Object Storage. This [blog article](https://www.ibm.com/cloud/blog/analyze-mezmo-log-data-on-ibm-cloud-object-storage-using-ibm-cloud-sql-query) provides detailed information for using IBM SQL Query with Mezmo data in IBM Cloud.

## jq

jq is a handy command-line tool used to parse JSON data. Once your archive has been uncompressed, you can use jq to parse your archive log files. You can find more information about jq in [X](https://stedolan.github.io/jq/).