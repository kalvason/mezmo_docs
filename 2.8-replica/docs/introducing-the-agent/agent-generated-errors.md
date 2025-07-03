---
type: page
title: About Mezmo Agent Exclusion Rule: MEZMO Created - Exclude Agent-Generated Errors
listed: true
slug: agent-generated-errors
description: 
index_title: About Mezmo Agent Exclusion Rule: MEZMO Created - Exclude Agent-Generated Errors
hidden: 
keywords: 
tags: 
---


Starting in January 2023, an exclusion rule was added to some accounts.  Its purpose is to mitigate the impact of a bug in older versions of the Mezmo agent.

Most accounts use Mezmo's Agent to send logs to Mezmo's service.  The application for the agent can be installed in many different environments and is constantly monitoring for new log lines.  When the agent application is running, it generates log lines of its own.  In many cases, particularly with versions earlier than 3.x, its log lines are sent to the Mezmo service.  If there are problems with the agent, it can be useful to see these agent-generated logs.

Versions of the agent earlier than 3.x have a bug, whereby they sometimes generate a very large number of log lines, none of which contain useful information.  It is rare, affecting 1-2 accounts a month.  It can be avoided by upgrading to a version of the agent later than 3.x.

To prevent this problem for customers using older versions of the agent, we proactively added an exclusion rule that targets these "excessive" logs sent by the agent.  The rule was added only to accounts that send logs, as best we can determine, from versions of the agent earlier than 3.x.