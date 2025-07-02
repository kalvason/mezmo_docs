---
type: page
title: March 4th, 2021 - LogDNA Web version 4.58.3
listed: true
slug: march-2nd-2021-logdna-web-version-4583
description: 
index_title: March 4th, 2021 - LogDNA Web version 4.58.3
hidden: 
keywords: 
tags: 
---






{% callout type="info" title="Note" %}
This page was modified on March 8th to remove two items from the **Fixed Issues** section. Those two fixes have not yet been released. They are:
- Usage Quotas: we fixed the alert recipients dropdown for both email and Slack, which was displaying in too large a format across the UI. [LOG-9010]
-  On Boards, a missing pop-up for editing/hiding/deleting a specific plot has been fixed. [LOG-8999]
{% /callout %}



## Features and Enhancements

- Import and Export account configurations: we have enhanced our Import/Export Configuration feature to allow users to selectively import and export specific views, boards, alerts, exclusion rules, and parsing templates. You can export the selected configurations into a JSON file, and then import this file to either a different LogDNA account to recreate your configurations across different accounts, or to the same account at a later date, to restore an account. To learn more, read our [documentation about this feature](https://docs.logdna.com/docs/importing-and-exporting-organization-configurations). [LOG-8937]

- We are pleased to announce a new community forum, at [https://community.logdna.com](https://community.logdna.com/)! This forum is a spot for all of us to have conversations and ask questions about LogDNA, including our open-source projects and the product itself. We welcome product feedback, requests for general help, or discussions. [LOG-8804]

## Fixed Issues

- We fixed an issue where the pop-up text displayed when a user clicks on certain portions of a log line was flickering or absent. [LOG-6359]

- Changed the cursor type for when a user hovers over a board to a regular pointer cursor instead of a text cursor. [LOG-8758]

- We improved the feedback mechanism used to display information for Kubernetes-based log lines by separating the statistics call from the line-context call. Now you will see the line context show up quickly while we are still retrieving the Kubernetes stats.  [LOG-8900]

- Usage Quotas: we fixed an issue where the status text for daily and monthly exclusion rules was not updated after toggling off the rule (either manually or after changing quota amounts). [LOG-8673]

## Support

If you have support-related questions about any of the above features or fixes, please reach out to us at [support@logdna.com](mailto:support@logdna.com).

