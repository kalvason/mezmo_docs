---
type: page
title: Okta SAML Setup
listed: true
slug: okta-saml-setup
description: 
index_title: Okta SAML Setup
hidden: 
keywords: 
tags: 
---

{% synced id="enteprisebanner" %}
{% /synced %}

## Step 1: Get Your Mezmo Single Sign On URL

1. In your Mezmo app go to [**Settings &gt; Organization &gt;** **Access Management**.](https://app.Mezmo.com/manage/team-settings)
2. Go to **SAML Configuration** and copy the URL under **URL for the Single Sign On Service to Consume**.
3. Keep this URL available since it will be used in the next step.

## Step 2: Configure Okta

1. In Okta go to **Applications &gt; Applications**.
2. Click **Create App Integration**.
3. In the window, choose **SAML 2.0**.
4. Fill out **General Settings**.
5. In the next window, enter the **URL for the Single Sign On Service to Consume** from the previous step.
6. Make sure **Recipient URL and Destination URL** are checked.
7. Set the **Audience URI (SP Entity ID)** to your account ID at the end of your URL. For example, `https://app.mezmo.com/auth/saml-consume/<AccountID>`. You can leave the rest of the options as is.
8. Fill out step 3 Feedback.

{% image url="https://uploads.developerhub.io/prod/2KW7/ze8x3es39lnukk3jwqz6vlmvat5kv6w2um3a2r48zp05ipxf07wpmqko71bg19jc.png" mode="responsive" height="282" width="1042" %}
{% /image %}

## Step 3: SAML Configuration

1. In Okta, on the settings page, click the button; **View SAML setup instructions**.
2. If not already done, in Mezmo, select **configure manually**.
3. Copy the **Identity Provider Single Sign-On URL** in Okta to **Identity provider sign-in URL** in Mezmo.
4. Download the **X.509 Certificate** from Okta and upload it to Mezmo.
5. Save your config in Mezmo.
6. You can also copy and save the XML data on Okta under **Optional** and upload it to Mezmo.