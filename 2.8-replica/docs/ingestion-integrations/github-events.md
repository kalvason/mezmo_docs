---
type: page
title: GitHub Events
listed: true
slug: github-events
description: Mezmo provides an integration to stream, aggregate, and gain insights from the GitHub Events API
index_title: GitHub Events
hidden: 
keywords: 
tags: 
---





The Mezmo integration for GitHub Events lets you collect information associated with GitHub events, like the repository where an event occurred or the user who triggered the event. The Mezmo integration for GitHub events monitors these GitHub Event types by default:

- PushEvent
- CreateEvent
- DeleteEvent
- Commit
- CommentEvent
- ReleaseEvent
- ForkEvent
- PullRequest
- EventPull
- RequestReview
- CommentEvent

You also have options to include Extended Repository Events, Issues Events, and Deployment Events.

## Set Up GitHub Event Logging

1. Log in to the [Mezmo Web App](http://app.mezmo.com).
2. Go to **Settings &gt; Integrations &gt; GitHub**.
3. Click **Connect to GitHub**.
If prompted, sign in to GitHub.
4. Click **Authorize Application**.
5. Select the GitHub repositories that you want to monitor.
6. Select any optional event types that you want to monitor for your repository.




{% callout type="info" title="Viewing GitHub Events" %}
If you select the GitHub source in the **All Sources** filter, you can see all GitHub events that were sent to Mezmo. You can also filter by specific repositories in **All Apps &gt; Repositories** .
{% /callout %}






