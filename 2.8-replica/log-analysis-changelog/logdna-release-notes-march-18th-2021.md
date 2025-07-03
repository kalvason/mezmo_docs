---
type: page
title: LogDNA Release Notes, March 18th, 2021
listed: true
slug: logdna-release-notes-march-18th-2021
description: 
index_title: LogDNA Release Notes, March 18th, 2021
hidden: 
keywords: 
tags: 
---



## LogDNA Web Application, version 4.67.2

### Changes

- Our web application UI now provides a way for customers to enter a full billing address. When logging in, Owners and Admins of an organization will see a one-time pop-up message asking that they add their billing address. Owners and Admins will receive a follow-up email about this change. [LOG-7821]

### Fixed Issues

- Improved search results return speed; decreasing the max delay for recursive searching resulted in a moderately faster search response in the web application UI. [LOG-9116]
- We modified the placement of the **Edit** icon's tooltip on the  Boards page of the UI to display beneath the icon. Previously, the tooltip displayed to the left of the icon and obscured the board name. [LOG-8759]
- Our "in-app" documentation (which displays in the web application) about adding a log source now accurately shows that we deprecated support for Kubernetes 1.8 and earlier versions.  [LOG-8745]

## LogDNA Agent

For the most recent release information about the LogDNA Agent, refer to [agent-specific Release Notes](https://docs.logdna.com/changelog).

## LogDNA Integrations

There are no external-facing changes to our LogDNA integrations in this release.

##LogDNA APIs

There are no external-facing changes to our LogDNA APIs in this release.

