---
type: page
title: OneLogin SAML Configuration
listed: true
slug: onelogin-saml-configuration
description: 
index_title: OneLogin SAML Configuration
hidden: 
keywords: 
tags: 
---

{% synced id="enteprisebanner" %}
{% /synced %}

## Get Your Mezmo Single Sign On URL

1. In your Mezmo app go to [**Settings &gt; Organization &gt; Security**](https://app.mezmo.com/manage/team-settings).
2. Go to **SAML Configuration** and copy the URL under **URL for the Single Sign On Service to Consume**.
3. Keep this URL available since it will be used in [Step 2: Configure OneLogin](https://app.developerhub.io/#step-2-configure-onelogin).

## Configure OneLogin

1. Log in to your instance of OneLogin.
2. Go to **Applications &gt; Applications**. Then click **Add App**.
3. In the search box, search for `SAML Custom Connector`. Select `SAML Customer Connector (Advanced)`.
4. Give the connector a name and then Save.
5. Select configuration from the menu in OneLogin.
6. Enter the Mezmo Single Sign On Service to Consume URL from [Get Your Mezmo Single Sign On URL](https://app.developerhub.io/#step-1-get-your-mezmo-single-sign-on-url), into `ACS (Consumer) URL Validator` and `ACS (Consumer) URL`.
7. Select **SSO** from the left menu.
8. Make sure the **SAML Signature Algorithm** is SHA-256 in the dropdown.

## SAML Configuration

1. In OneLogin, go to the **SSO** tab.
2. In the **More Actions** dropdown, select **SAML Metadata**. An XML file will download.
3. In your Mezmo app, go to **Settings &gt; Organization &gt; Security**.
4. Toggle **SAML Sign-in** to **On**.
5. In **SAML Configuration** upload the XML file downloaded.
6. Save and your OneLogin SSO is ready to go.