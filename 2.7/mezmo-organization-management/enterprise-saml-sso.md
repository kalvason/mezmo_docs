---
type: page
title: Enterprise SAML SSO Configuration
listed: true
slug: enterprise-saml-sso
description: 
index_title: Enterprise SAML SSO Configuration
hidden: 
keywords: 
tags: 
---

{% synced id="enteprisebanner" %}
{% /synced %}

## Set Up SAML Login

1. Go to [**Settings &gt; Organization &gt; Security**](https://app.mezmo.com/manage/team-settings).
2. Toggle **SAML Sign-in** to on.
3. You can either configure SAML manually or upload the XML service provider metadata.

## Setting the URL

There are two URLs for SAML configuration:

- Single Sign On URL
- URL for the Single Sign On Service to Consume or SAML Assertion Consumer Service (ACS) URL

Your IDP will specify which URL is needed. You only need one of the URLs.

## Manual Configuration

If your IDP doesn't offer an XML file for download, you can enter the information manually. You'll need to provide:

- **Identity provider sign-in URL** - This URL users use when they enter their domain email address.
- **X.509 certificate** - The security `.pem` file.
- You'll also need to enter Mezmo information into your provider.
    - **IdP Entity ID -** Set this to `https://app.mezmo.com` or the domain you are using for the app. This value is also known as Identifier.
    - **SP Entity ID -** Set this value to `logdna-saml/<accountID>`. This value is also known as IdP Audience or Audience URI.
    - **ACS URL -** Set this value to`https://app.mezmo.com/auth/saml-consume/<accountID>`. This value is also known as Sign-On URL.

## Provider Instructions

- [Okta SAML Setup](/docs/okta-saml-setup)
- [OneLogin SAML Setup](/docs/onelogin-saml-setup)

## Service Provider Metadata

Most service providers will have an XML data file containing the SAML information. The file should include the following:

- EntityDescriptor
- IDPSSODescriptor
- KeyDescriptor
- KeyInfo
- X509Certificate
- NameIDFormat
- SingleSignOnService