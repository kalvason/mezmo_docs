---
type: page
title: Build and Deploy a Mezmo Telemetry Pipeline
listed: true
slug: build-deploy-mezmo-pipeline
description: 
index_title: Build and Deploy a Mezmo Telemetry Pipeline
hidden: 
keywords: 
tags: 
---


Building a Pipeline involves three basic steps:

1. Set up a [Pipeline Source](/telemetry-pipelines/set-up-pipeline-sources).
2. Set up a [Pipeline Destination](/telemetry-pipelines/set-up-pipeline-destinations).
3. Add [Processors](/telemetry-pipelines/set-up-pipeline-processors) to manage and transform your Pipeline data.

## [Build a Telemetry Data Pipeline](https://docs.mezmo.com/docs/build-and-deploy-a-log-data-pipeline#build-a-log-data-pipeline)

1. Log into [the Mezmo Web App](https://app.mezmo.com/).
2. In the left-hand menu, click **Pipelines**. This will open the **Edit Pipeline** interface.
3. In the left-hand navigation, click **+ New Pipeline**.
4. Enter a name for the Pipeline, then click **Save**.
5. In the **Sources** column of the pipeline schematic, click **Add**.
6. Select the Pipeline Source you want to use, and enter the configuration information.
7. In the **Destinations** column, click **Add**.
8. Select the Destination for your Pipeline log data, and enter the configuration information.
9. To connect your Source and Destination, click the right edge of your Source, and when the blue circle appears, drag the connector from the Source to the Destination until the Destination tile turns blue.
10. After you connect the Source and Destination, click the connector and the **Insert Node** dialog will open.
11. Select **Insert Node** and choose the Processor you want to apply to that Pipeline segment.

Repeat these steps until you have added all the Sources, Destinations, and Processors for your Pipeline.

## [Deploy the Pipeline and View the Data](https://docs.mezmo.com/docs/build-and-deploy-a-log-data-pipeline#deploy-the-pipeline-and-view-the-data)

When you have completed your Pipeline architecture, you need to deploy it for data to begin flowing.

1. In the **Pipelines** section, select the Pipeline you want to deploy.
2. Click **Deploy Pipeline**.
3. When the Pipeline is deployed and active, you will see a panel above the Pipeline that displays the amount of data that is flowing through the Pipeline.
4. To view the data that is flowing between segments of the Pipeline, insert a [Pipeline Tap](/telemetry-pipelines/view-pipeline-data)

After a Pipeline is deployed, you can continue to [edit it](/telemetry-pipelines/edit-a-pipeline).

## Pipeline Demos and Tutorials

These topics provide an overview of the demo Pipelines that are included in the Mezmo Web App, as well as tutorials for for typical Processor configuration use cases. The tutorials include an overview of the "Pipette" and the Processor configurations, an interactive demo that shows how the data is transformed as it moves along the Processor chain, and step-by-step instructions to build a version of the Pipette using [auto$](/telemetry-pipelines/demo-logs-source) and the [auto$](/telemetry-pipelines/blackhole-destination) Destination, as well as how to connect your own Source and Destination.

- [auto$](/telemetry-pipelines/pipeline-architecture-for-kubernetes-data-optimizationzlz)
- [auto$](/practioner-guide-data-optimization/pipeline-module--route)
- [auto$](/practioner-guide-data-optimization/pipeline-module--security-and-compliance)
- [auto$](/practioner-guide-data-optimization/pipeline-example--convert-200-events-to-metrics)