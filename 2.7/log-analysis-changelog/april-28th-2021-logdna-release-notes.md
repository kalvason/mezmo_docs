---
type: page
title: April 28th, 2021 - LogDNA Release Notes
listed: true
slug: april-28th-2021-logdna-release-notes
description: 
index_title: April 28th, 2021 - LogDNA Release Notes
hidden: 
keywords: 
tags: 
---



## LogDNA Web Application, version 4.93.10

### New Features and Enhancements
LogDNA is pleased to announce the following highlight of this release:
* The Browser Logger javascript code library and template, with pre-configured Views, Boards and Screens that you can customize and then configure alerts on browser errors and logs. The Browser Logger is the latest in a set of LogDNA Templates. For more information, refer to our documentation about [using LogDNA Templates](https://docs.logdna.com/docs/using-templates). [LOG-8117]

### Fixed Issues
* We modified our mailing address input field on the Billing area to change the State label to be “State, county, province, or region” when the address is not within the US. [LOG-9479].
* We fixed an issue where users who clicked a link into an area of the web application UI sometimes got a 401 error. This occurred if they were not logged in before clicking the link, or if their role was not authorized to view that area of the UI. Now, instead of getting a 401 error, authorized users users will be redirected to the login page, and unauthorized users will get a 404 error. [LOG-9469].

## LogDNA Agent

For the most recent release information about the LogDNA Agent, refer to [agent-specific Release Notes](https://docs.logdna.com/changelog).

## LogDNA Integrations

There are no external-facing changes to our LogDNA integrations in this release.

## LogDNA APIs

There are no external-facing changes to our LogDNA APIs in this release.

