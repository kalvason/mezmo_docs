---
type: page
title: Importing and Exporting Configurations
listed: true
slug: importing-and-exporting-organization-configurations
description: 
index_title: Importing and Exporting Configurations
hidden: 
keywords: 
tags: 
---



You can export your configuration for an organization as a JSON file, then import the file to another organization. You can export:

- [Views](https://docs.mezmo.com/docs/views)
- [Boards](https://docs.mezmo.com/docs/graphs)
- [Alerts](https://docs.mezmo.com/docs/alerts)
- [Exclusion rules](https://docs.mezmo.com/docs/excluding-log-lines)
- [Parsing Templates](https://docs.mezmo.com/docs/custom-parsing)

## When To Use Import and Export

- **Replicate existing account configurations**. Use the existing account configuration for multiple new Mezmo accounts. This makes them easier to manage, support, and keeps things consistent.
- **Move configurations** from staging to production.
- **Restore account configuration** using the Import option. This will return the configurations to a saved state and overwrite any existing configurations.

## Feature Notes

- The file is exported as a JSON file
- Administrator privileges are required to use this feature
- You can export from the same account and replace in the same account. You can't add to and from the same account. This prevents accidental duplication of views, alerts, and other configurations in the same account.
- Importing the same config file twice to one account will create duplicates of every configuration that was originally exported to the file,  except for categories.
- You can't export alerts without also exporting the views they're attached to. You can export views without alerts.
- To stop multiple team members from overwriting each other's work, there is a 10 minute wait between import attempts to the same account.
- If an exported configuration file is modified in any way, the import will fail due to a failed checksum action
- The configuration file doesn't expire, so you can keep a copy to restore your settings if your account's configuration ever needs to be restored
- No log data is exported

## Export Configurations

1. Go to [**Settings &gt; Organization &gt; Export**](https://app.Mezmo.com/manage/export-config). By default any configurations you have set are selected. Clear the selection for any you don't want to export.
2. For each type of configuration, click the arrow beside the type to display the full list. Use the arrow to drill down into the categories and view the configuration.
3. For views, you can select whether to also export any alert that's attached to the view.
4. The values shown in the parentheses indicate the total counts of configurations of that type.
5. Click **Export**.
6. A JSON file with the selected configurations downloads to your local machine. The name of the file is prepended with `mezmo-config`.

## Import Configurations

1. Go to [**Settings &gt; Organization &gt; Import**](https://app.Mezmo.com/manage/import-config).
2. Upload your JSON configuration file.
3. Once the file is uploaded, choose **Add** or **Replace**.
4. Add to existing configuration
5. Replace existing configuration. **This is irreversible**.
6. Click **Import**.
7. The Import Configuration page reloads, and displays information about the before and after states, including the types and numbers of configurations that were imported.



{% callout type="info" title="Info" %}
📘 Refresh the application: You'll need to refresh the browser to see the new configurations.
{% /callout %}



## Restore Account Configuration

To restore account configuration, store a copy of your exported JSON file and choose **Replace existing configuration**.



