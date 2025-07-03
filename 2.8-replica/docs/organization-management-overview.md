---
type: page
title: Organization Management Overview
listed: true
slug: organization-management-overview
description: 
index_title: Organization Management Overview
hidden: 
keywords: 
tags: 
---


When you create your Mezmo account, Mezmo automatically creates and assigns you to a new Organization. This Organization comes with a 30-day trial and an auto-generated [ingestion key](https://docs.mezmo.com/docs/ingestion-key) which you can use to send logs to Mezmo for storage and analysis.

You can be a member of many Organizations, but can only view one organization at a time. Your current active organization is shown at the bottom of the left-hand navigation pane in the web app. Click the name of the organization to open the **Manage Organizations** menu.

## Create an Organization

1. Click the organization name. Then **All Organizations** You'll see a list of all the organizations you're a member of.
2. Then click **Create a new organization**.

## Delete an Organization

Deleting an Organization will purge the Organization from Mezmo. This includes the Organization’s logs, billing data, and customizations. This is only available for administrators.

{% callout type="error" title="Not Reversible" %}
This action can't be reversed: This action can't be reversed. Make sure you want to delete your Organization before continuing.
{% /callout %}

1. Switch to the Organization in the Mezmo web app.
2. Navigate to **Settings &gt; Organization &gt; General**, then scroll down to **Deactivate Account**.
3. Click **Deactivate This Account**. Mezmo will prompt you to reenter your account ID for confirmation.

## Organization Ownership

Creating an Organization automatically makes you the owner of the Organization. Organization owners can invite users to join or make the Organization discoverable to certain users.

Learn more about [Setting Member Roles](https://docs.mezmo.com/2.8/docs/role-based-access-control).

## Join an Existing Organization

Mezmo allows you to join multiple Organizations. You can join or leave an organization by selecting the organization name and selecting Join or Leave.

## Manage an Organization

If you are an owner you have the ability to modify the Organization.

Click **Settings &gt; Organization &gt; General** in the web app to get started.

### Change the Organization Name

Changing the Organization name updates the display name of the Organization in Mezmo for all members.

### Change the Organization Owner

Changing the Organization owner passes ownership of the Organization to a different member. Once you do this, you will no longer have the ability to make changes such as changing the Organization name or deleting the Organization.

### Switching Between Organizations

If you are a member of multiple Organizations, you can switch between them in the Mezmo web app. Only one Organization can be viewable at a time.

The selected Organization is shown in the bottom left corner of the app. Click on the Organization name to open the Organization menu, then click on the name of the Organization that you want to switch to. The web app will refresh and bring you to the Organization’s log view.

### Set a Default Organization

For users with access to multiple organizations, you can specify the organization to open when you log in to Mezmo.

1. To set your default organization, click the upward arrow icon in the lower left of the application UI, beside the name of the organization you are currently in. The list of all organizations that you have access to appears.
2. Scroll up to the name of the organization that you want as your default, and hover your cursor over the name.
3. When a checkmark icon appears beside the name, click the arrow.

## API Keys

{% image url="https://uploads.developerhub.io/prod/2KW7/jpbuz19wyyb0412ncp5ktb0b1hd47wu657xynbx6279lfx6vuotfapylndkssh02.jpg" caption="How to set a default organization. Set the default org by hovering over the checkmark next to the organization name." mode="responsive" height="472" width="500" %}
{% /image %}

API keys (Ingestion Keys and Service Keys) are used to connect Mezmo to third-party applications and services, for ingesting log files and for API calls. Learn more about [Using Service and Ingestion Keys](https://docs.mezmo.com/docs/ingestion-key).