---
type: page
title: Feb 17th, 2021 - LogDNA Web version 4.50.2
listed: true
slug: feb-17th-2021-logdna-web-version-4502
description: 
index_title: Feb 17th, 2021 - LogDNA Web version 4.50.2
hidden: 
keywords: 
tags: 
---




## Features and Enhancements

- New users who are administrators of the organization are automatically subscribed to the monthly and weekly usage digest emails. Admins can opt-out of the digests. [LOG-8727]

## Fixed Issues
- We made a change to disable any associated usage quota exclusion rules whenever a user edits the values for either the daily or monthly usages values. This behavior prompts a reevaluation of the existing rules in terms of the newly edited values. Note that these are the usage quota triggered exclusion rules, which are separate and distinct from standalone exclusion rules. [LOG-8808]

- Fixed an issue where during import process, not all details of the attached view-specific alerts were imported properly. [LOG-8701]

## Support

If you have support-related questions about any of the above features or fixes, please reach out to us at [support@logdna.com](mailto:support@logdna.com).

