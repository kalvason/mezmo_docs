---
type: page
title: Manage Access
listed: true
slug: manage-access
description: 
index_title: Manage Access
hidden: 
keywords: 
tags: 
---



Adding users to your Mezmo Organization allows you to share access to logs, views, alerts, and other Mezmo resources with other members of your team. This page will show you how to manage users as a Mezmo administrator, including how to add new users, assign permissions, and set global sign-in policies.
To see available security features, go to [**Settings &gt; Organization &gt; Security**](https://app.Mezmo.com/manage/team-settings).

## Access Control

By default, members who aren't assigned to any groups can see all logs. If this is set to `off`, then these members can't see any logs until they're assigned to a group. This only applies to users who are in the [Members](https://docs.mezmo.com/docs/how-to-manage-users) role and aren't assigned to any groups.

## Discoverability

Discoverability lets you control how users can find and join your organization.

- **Discover** - Members on the same domain can find and ask to join the organization. Discover is enabled by default.
- **Join** - Members on the same domain can join the organization without a request.

Your domain is determined by the email address you used when creating your Mezmo account. If you would like to add domains, please contact Mezmo support.

## Sign-in Policy

Sign-in policy determines which authentication methods members are allowed to use when signing into your Organization. These options are turned off by default. You can use:

- **SAML Sign-in** - Let members sign in using an identity provider such as Okta or OneLogin. Available for enterprise customers only. Learn how to set up [SAML SSO](https://docs.mezmo.com/docs/saml-sso#onelogin-setup).
- **Idle Logout** - Log members out after a period of inactivity. Available for all plans.
- **Redirect after logout** - Redirect members to an address after they logout. Available for all plans.

You can also control what logs members see by using [Role Based Access Control](https://docs.mezmo.com/docs/rbac).



