---
type: page
title: Archive Logs
listed: true
slug: archiving
description: 
index_title: Archive Logs
hidden: 
keywords: 
tags: 
---

Archiving is an automated function that exports your logs from Mezmo to an external storage provider. Once archiving is configured for your account, your logs will be exported to the storage provider on an hourly basis in a compressed JSON format `.json.gz`, with the associated metadata for each line preserved.  

- Only retained logs will be archived, meaning, for example, logs affected by exclusion rules would not be archived 
- The first time you configure archiving, your archived logs will typically appear within 12-24 hours, but will not include existing logs from the period before you enabled archiving

{% callout type="info" title="Supported Log Data Restoration Archives" %}
Mezmo's [Data Restoration](/docs/data-restoration) feature only supports restoring logs from [AWS S3 and Google Cloud Storage](/docs/export-logs-to-external-storage) archives.
{% /callout %}

## Hourly Archiving

- Hourly archives create 24+ Gzip JSON files per day. If there are no logs for an hour, then no files will be uploaded for that hour.
- Archives are expected to appear within 24 hours, but may take up to 72 hours for larger archives
- The file contents will stay the same as the daily archives, except now the file will be stored as `year=YYYY/month=MM/day=DD/<accountID>.<YYYY>-<MM>-<DD>.<HH>00.json.gz` ,where `HH` is hours in 24 hour format, for all providers. 
- If log lines are attributed or received 6 hours beyond the hour bucket the log line belongs to, subsequent archive files will be created in the name format of `<accountID>.<YYYY>-<MM>-<DD>.<HH>00.<NUMBER>.json.gz`, where `<NUMBER>` is an incrementing number starting from`1`, to prevent filename conflicts.
- Hourly archiving may create duplication of logs in the storage (1% of the time). You can tell if  a line has been duplicated if the lines have the same log line ID.

## Security

By default, Mezmo encrypts your archived data in transit, and requests server-side encryption where possible, including using x-amz-server-side-encryption upon upload of logs to S3.

## Related Topics

{% index-list %}
{% /index-list %}