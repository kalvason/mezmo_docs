---
type: page
title: Monitor Pipeline Data Volume
listed: true
slug: monitor-data-pipelines
description: 
index_title: Monitor Pipeline Data Volume
hidden: 
keywords: 
tags: 
---

On your Pipelines dashboard, you can monitor the volume of data flowing through your Pipelines, including the aggregated Ingress and Egress metrics for all Pipelines. You can also view volume metrics for each of your Sources and Destinations, and aggregated Ingress and Egress metrics for all Sources and Destination.

## [Access the Monitoring Dashboard](https://docs.mezmo.com/docs/monitor-log-data-pipelines#access-the-monitoring-dashboard)

1. Log into the [Mezmo Web App](https://app.mezmo.com/).
2. In the left-hand navigation, click the **Pipelines** icon.
3. Click **Dashboard**.
4. Adjust the time-span for the metrics you want to view by selecting an option from the **Time** menu in the upper-right corner of the dashboard. All metrics on the dashboard will adjust for the selected time period.

## [Aggregated Ingress and Egress](https://docs.mezmo.com/docs/monitor-log-data-pipelines#aggregated-ingress-and-egress)

The **Ingestion/Egress by Volume** chart at the top of the dashboard shows the total ingress and egress for all of your Pipelines. You can drag your cursor along the top of the chart to view the metrics for a specific point in time relative to your selected time period.

## [Top 10 Sources and Destinations](https://docs.mezmo.com/docs/monitor-log-data-pipelines#top-10-sources-and-destinations)

Below the I**ngestion/Egress by Volume** chart are two charts showing the **Top 10 Sources** and **Top 10 Destinations**, by bytes, for the selected time period. Hover your cursor over the bar that represents each source or destination to see the number of bytes for that specific source or destination.

## [Aggregated Egress](https://docs.mezmo.com/docs/monitor-log-data-pipelines#aggregated-egress)

Next to the charts for Top 10 Sources and Destinations is circle graph showing the **Aggregated Egress** for all Pipeline Destinations, with the circle divided in proportion to the egress to each Destination. 

## [All Pipelines](https://docs.mezmo.com/docs/monitor-log-data-pipelines#all-pipelines)

Below the **Top 10 Sources** and **Destinations** and **Aggregated Egress** charts is a listing of all deployed Pipelines, along with the number of sources and destinations, and the Ingress and Egress statistics, for each Pipeline. You can click the **Name** of any Pipeline to view its **Total Ingress** and **Total Egress by Volume**, as well as the architectural schematic for the Pipeline. Click **Edit pipeline** if you want to make any changes to the architecture. After you edit the Pipeline and deploy the changes, click **Monitor deployed pipeline** to view the impact of your changes.

## [Sources](https://docs.mezmo.com/docs/monitor-log-data-pipelines#sources)

Click **Sources** under **Dashboard** to view a list of all sources, the names of their associated Pipelines, and the Ingress volume for each. Click a Source to view it in the context of the Pipeline architecture schematic. You can also vie the **Total Ingress** for all sources, and the **Total Sources** used in all your Pipelines.

## [Destinations](https://docs.mezmo.com/docs/monitor-log-data-pipelines#destinations)

Click **Destination** under **Dashboard** to view a list of all sources, the names of their associated Pipelines, and the Egress volume for each.Click a Destination to view it in the context of the Pipeline architecture schematic. You can also vie the **Total Egress** for all sources, and the **Total Destinations** used in all your Pipelines.

## [Video Overview](https://docs.mezmo.com/docs/monitor-log-data-pipelines#video-overview)

{% video videoId="821073643" provider="vimeo" %}
{% /video %}