---
type: page
title: Set Up System Cross-Domain Identity Management (SCIM)
listed: true
slug: system-cross-domain-identity-management
description: 
index_title: Set Up System Cross-Domain Identity Management (SCIM)
hidden: 
keywords: 
tags: 
---

{% synced id="enteprisebanner" %}
{% /synced %}

## What is SCIM

**System for Cross-domain Identity Management** (SCIM) is a set of application-level protocols that use JSON, REST, and several different authentication methods to automate the task of account provisioning. Using SCIM you can provision/de-provision user accounts in Mezmo via your identity providers, such as Okta and Azure.

## How SCIM works with Enterprise Accounts and Child Orgs

Mezmo's implementation of SCIM allows you to map Groups in your IDP with Child Organizations in Mezmo.  It also maps users in your IDP to users in Mezmo.  Assignments of these users to groups in your IDP will be reflected by Mezmo assigning these users to the matching Org.

## General Setup

To utilize SCIM, you will need to obtain an Enterprise Service Key.  You can find this in the  **Access Management** section of the Mezmo Web App in your **Enterprise Dashboard**.  You will need this key, as well as our SCIM endpoint:

`https://api.mezmo.com/v1/enterprise/scim`

## Support

While our SCIM endpoint was built to SCIM 2.0 specifications, we have only tested it with the following IDPs.  You may use other IDPs, but we cannot guarantee support for untested providers.

Please note that while we support group sync, we do not support creation and deletion of groups.

## Okta

1. Log into to your Okta Admin Console
2. Create an App Integration (skip this step if you have already done this):Follow the steps in our [Okta SAML instructions](https://docs.mezmo.com/2.8/docs/okta-saml-setup)

### Enable SCIM Provisioning

1. Go into your Mezmo App Integration.
2. Go to **General** and click **Edit** in **App Settings.**
3. Under **Provisioning**, choose **SCIM** and click **Save**,

### Configure Provisioning Settings

1. In the Memzo App Integration, go to **Provisioning**, and under **SCIM connection**, click **Edit**.
2. For  **SCIM connector base URL** enter `https://api.mezmo.com/v1/enterprise/scim`
3. For **Unique identifier field for user** enter `userName.`
4. Under **Supported provisioning actions,**  select all options.
5. For **Authentication Mode,**  choose **HTTP Header.**
6. In the field labeled **Bearer,**  enter your enterprise token.
7. Click **Test Connector Configuration**. 
8. Assuming everything succeeds, click **Save.**

### Configure **To App** settings

1. Click **Edit** next to **Provisioning to App.**
2. Select all options except **sync password.**
3. Click **Save**.

### Set Up Initial Connection of Users/Groups

1. In the **Import** tab, click **Import Now.**
2. If required, choose a method to reconcile users. 

### Set Up Links between Okta and Mezmo Groups

1. Create a group and assign **App Mezmo** to this group (you may have already done this if you are using Mezmo SAML).
2. In the Mezmo Application, click**Push Groups**, then click the gear configuration icon. 
3. Clear the option **Rename app groups to match group name in Okta.**
4. Choose **Push Groups**, then **By Name**.
5. Find the group you created.
6. Clear the option  **Push group memberships immediately.**
7. Choose **Link group** and choose the Mezmo account you want to sync.
8. Click **Save**.
9. Assign people to groups as necessary.

### Activate Groups

- In the  Mezmo App, go to **Push Groups**.
- Under **Push Status**,  choose **Activate group push.**

Provisioning in Mezmo should start shortly. You can find errors and status  under **Reports, System Log.**

For additional information please consult [Okta Documentation](https://help.okta.com/en-us/content/topics/apps/apps_app_integration_wizard_scim.htm).

## Microsoft Azure Entra ID (formerly Active Directory)

In Azure Portal, go to your **Entra ID** instance.  

### Set Up SCIM as a New Enterprise Application

1. Click **Enterprise applications** and then **New application**.
2. Click **Create your own application**.
3. Enter **Mezmo SCIM**, then click **Create**.
4. Once this application is created, click **Provisioning**. 
5. Click  **Get Started**. 
6. Click **Connect Your Application** under **Create Configuration** section
7. Under section **Admin Credentials** enter:

- 
    - For **Tenant URL**, enter: `https://api.mezmo.com/v1/enterprise/scim?aadOptscim062020`
    - For **Secret token** enter your enterprise token.

- Click **Test Connection** and then **Create**. 

### Configure Group Mappings

1. Go to **Provisioning &gt; Attribute Mapping (Preview)**, and click **Provision Microsoft Entra ID Groups.**
2. Make sure there is **Matching precedence** set to  **1** for **displayName a**ttribute  to allow Entra matches its groups with Mezmo groups (Child orgs)
3. Under **Target Object Actions,** clear the **Create** and **Delete** options and click **Save.**

{% callout type="info" title="Groups provisioning" %}
In order to make groups provisioning work properly, Microsoft Entra group names must match Mezmo account (Child orgs) names. For example, if your Mezmo child org name is "Department", then your Microsoft Entra group name should be "Department". 

Any users assigned to this group on the Entra side will be synced with the corresponding account (Child org) on the Mezmo side.
{% /callout %}

### Configure User Mappings

1. Go to **Provisioning &gt; Attribute Mapping (Preview)**, and click **Provision Microsoft Entra ID Users.**
2. Under section **Attribute Mappings** remove all attributes except:
    - userName
    - active
    - displayName
    - emails[type eq "work"].value
    - name.givenName
    - name.familyName
    - name.formatted

3. Edit attribute **userName** by replacing **Source attribute** from **userPrincipalName** to **mail**.  Mezmo assumes **userName** is a unique user ID which must be the user's email address.
4. Click **Save.**

### Choose Groups to Sync

1. Under **Mezmo SCIM**, click **Users and groups**.
2. Click **Add user/group.**
3. Choose the group(s) you want to sync and click **select.**
4. Click **Assign**

### Start Provisioning

1. Under **Mezmo SCIM,** click **Provisioning** then again **Provisioning**.
2. Set **Provisioning Status** to **On.**
3. After this setting SCIM provisioning should start automatically with a default 40 minutes interval.

Provisioning in Mezmo should start shortly. You can find errors and status on the **Mezmo SCIM Provisioning Overview** page and **Monitor** section in **Mezmo SCIM -&gt; Provisioning**.

For additional information check out the [Azure Documentation](https://learn.microsoft.com/en-us/entra/architecture/sync-scim).