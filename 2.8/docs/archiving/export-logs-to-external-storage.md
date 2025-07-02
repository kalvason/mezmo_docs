---
type: page
title: Export Logs to External Archive Storage
listed: true
slug: export-logs-to-external-storage
description: 
index_title: Export Logs to External Archive Storage
hidden: 
keywords: 
tags: 
---


Mezmo supports exporting logs to external storage providers, including AWS S3, Azure Blob Storage, Digital Ocean Spaces, Google Cloud Storage, IBM Cloud Object Storage, and OpenStack Swift. This topic provides information on configuring both your storage provider and Mezmo Archiving.

## AWS S3

To export your logs to an S3 bucket, make sure that you have an AWS account with access to S3. If you need to create a new S3 bucket for log storage, follow the instructions in the [AWS S3 Getting Started Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/GetStartedWithS3.html).

**Add Mezmo as a Grantee for Your S3 Bucket Access Control List**

To set up log archiving for your bucket, follow the AWS instructions for [Using the S3 console to set ACL permissions for a bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/managing-acls.html#:~:text=Using%20the%20S3%20console%20to%20set%20ACL%20permissions%20for%20a%20bucket). In those instructions, follow the steps “To grant access to another AWS account” and use this canonical ID for Mezmo:

{% code %}
{% tab language="none" %}
659c621e261e7ffa5d8f925bbe9fe1698f3637878e96bc1a9e7216838799b71a
{% /tab %}
{% /code %}

Enable these permissions for Mezmo:

- `Objects List`
- `Objects Write`
- `Bucket ACL Read`
- `Bucket ACL Write`

{% callout type="info" title="Additional Permissions for Log Data Restoration Feature" %}
To use the [Restore Log Data](/docs/data-restoration) feature, `Object Ownership` should be set to `Object Writer`  in the S3 bucket.
{% /callout %}

**Configure Mezmo**

1. In the [Mezmo web app](https://app.mezmo.com), navigate to **Settings &gt; Archiving &gt; Manage**.
2. Toggle **Enable Logging** to **On**.
3. In the **Provider** menu, select **AWS S3**.
4. Enter the name of your S3 bucket, and then click **Save**.

## Azure Blob Storage

To export your logs to Azure Blob Storage, make sure that you have an Azure account with access to storage accounts.

1. [Create a Storage Account](https://docs.microsoft.com/en-us/azure/storage/storage-create-storage-account) on Microsoft Azure.
2. Once created, select your storage account, then, under **Settings** click **Access Keys**.
3. Create a key if you do not already have one.
4. In the [Mezmo web app](https://app.mezmo.com), navigate to **Settings &gt; Archiving &gt; Manage**.
5. Toggle **Enable Logging** to **On**.
6. In the **Provider** menu, select **Azure Blob**.
7. Under **Settings** , enter your **Account Name** and **Account Key**, and then click **Save**.

## Digital Ocean Spaces

To export your logs to Digital Ocean Spaces, make sure that you have a Digital Ocean account with access to storage.

1. Create a new space (or use an existing one) in [Digital Ocean Spaces](https://cloud.digitalocean.com/spaces).
2. Create a new spaces access key in [Digital Ocean Applications & API](https://cloud.digitalocean.com/settings/api/tokens). Make sure to save the access key and secret key.
3. In the [Mezmo web app](https://app.mezmo.com), navigate to **Settings &gt; Archiving &gt; Manage**.
4. Toggle **Enable Logging** to **On**.
5. In the **Provider** menu, select **Digital Ocean Spaces**.
6. Under **Settings**, input your **Space Name**, **Endpoint**, **AccessKey**, and **SecretKey**, and then click **Save**.

You can find your region in your spaces URL. For example`https://my-mezmo-bucket.nyc3.digitaloceanspaces.com` has the region `nyc3`.

## Google Cloud Storage

To export your logs to Google Cloud Storage, make that you have a Google Cloud Platform account and project with access to storage.

1. Make sure that [Google Cloud Storage JSON API](https://console.cloud.google.com/apis/library/storage-api.googleapis.com/) is enabled.
2. Create a new bucket (or use an existing one) in [Google Cloud Storage](https://console.cloud.google.com/storage/).
3. Update the permissions of the bucket and add a new member `archiver@logdna-internal-oauth.iam.gserviceaccount.com` with the role of `Storage Admin`.
4. In the [Mezmo web app](https://app.mezmo.com), navigate to **Settings &gt; Archiving &gt; Manage**.
5. Toggle **Enable Logging** to **On**.
6. In the **Provider** menu, select **Google Cloud**.
7. Under **Settings**, enter your **ProjectId** and **Bucket**, and then click **Save**.

## IBM Cloud Object Storage

To export your logs to IBM Cloud Object Storage Archiving, make sure that you have an IBM Cloud account with access to storage.

1. Create a new object storage service (or use an existing one) in [IBM Cloud Object Storage](https://console.bluemix.net/catalog/services/cloud-object-storage).
2. Create a new bucket (or use an existing one) in your service for Mezmo dump files.
3. In the [Mezmo web app](https://app.mezmo.com), navigate to **Settings &gt; Archiving &gt; Manage**.
4. Toggle **Enable Logging** to **On**.
5. In the **Provider** menu, select **IBM Cloud Object Storage**.
6. Under **Settings**, enter your **Bucket**, **Public Endpoint**, **API Key**, and **Instance ID**, and then click **Save**.

## OpenStack Swift

To export your logs to OpenStack Swift, make sure that you have an OpenStack account with access to Swift.

1. Set up Swift by following [the instructions](https://www.swiftstack.com/docs/cookbooks/swift_usage/auth.html#v2-auth) in the Swift documentation.
2. In the [Mezmo web app](https://app.mezmo.com), navigate to **Settings &gt; Archiving &gt; Manage**.
3. Toggle **Enable Logging** to **On**.
4. In the **Provider** menu, select **OpenStack Swift**.
5. Under **Settings**, enter your **Username**, **Password**, **Auth URL**, **Tenant Name**, and a date for **Expire After**, then click **Save**.