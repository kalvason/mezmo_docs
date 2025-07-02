---
type: page
title: Tap and View Mezmo Edge Pipeline Data on Premises
listed: true
slug: tap-and-view-mezmo-edge-pipeline-data-on-premises
description: 
index_title: Tap and View Mezmo Edge Pipeline Data on Premises
hidden: 
keywords: 
tags: 
---


The SaaS version of Mezmo Telemetry Pipelines includes a  [Data Tap feature](/telemetry-pipelines/view-pipeline-data)  feature that enables you to view the flow of data  through your Pipeline, and to confirm that the Processors are transforming and formatting the data as expected. This functionality is also available tapping remotely deployed Mezmo Edge instances. However, some organizations prefer to disable remote tapping to avoid the possibility  of sensitive data leaving their network. In this case, you  can leverage similar functionality in the  `vector tap` CLI, or GraphQL , to view the data for your local Edge Instance, without having to send any data to the Mezmo Web App.

## Set Up Vector Tap with Mezmo Edge

The easiest way to get access to `vector tap` is to use a command line interface to connect to  a running Edge node, which will have built-in `vector tap` connectivity and tools.

### List Edge Nodes


{% code %}
{% tab language="none" %}
kubectl get pods -l app.kubernetes.io/name=edge
{% /tab %}
{% /code %}


### Connect to a Named Node


{% code %}
{% tab language="none" %}
kubectl exec -it <pod name> -- bash
{% /tab %}
{% /code %}


If `exec` is not available to your user in the cluster,  you can use `vector tap` from any host with network connectivity to the cluster.

### List Services


{% code %}
{% tab language="none" %}
kubectl get svc -l app.kubernetes.io/name=edge
{% /tab %}
{% /code %}


### Forward the API Port


{% code %}
{% tab language="none" %}
kubectl port-forward <service name> 8686
{% /tab %}
{% /code %}


## Tap Edge Data

### View Data for All Nodes

You can use the `vector tap` to view data from combinations of node outputs in the Pipeline. The basic method is to view data at the output of every node:


{% code %}
{% tab language="none" %}
vector tap
{% /tab %}
{% /code %}


### View Data for a Specific Node

To view the data stream for a specific Pipeline component, you need to provide the `component id`:


{% code %}
{% tab language="none" %}
vector tap <component id>
{% /tab %}
{% /code %}


If tapping remotely is explicitly disabled by your administrator, the **Tap** button in the UI will prompt you with the exact `vector`  command to tap that node:


{% image url="https://uploads.developerhub.io/prod/2KW7/qtv4nklxsqmfuyqk2bjq822dkl0iyp03akr2ctbldy3aozuo5ycz6tv0wk4i6h8n.png" caption="Prompt for the vector command to tap the selected node" mode="300" height="632" width="744" %}
{% /image %}


Click the copy/clipboard button to copy the command, which can be executed on the container or locally (with port forwarding active as described above).

Alternatively, if port forwarding is active, you can click the **Vector GraphQL playground** link. This will open a new window that is connected to the GraphQL instance. The subscription query will be pre-populated with the selected node query, as shown in this screenshot:


{% image url="https://uploads.developerhub.io/prod/2KW7/l2d72jt8qpyskdetca6s6o27qyrl4hjd0tpytx27kfprinq1dwr2z4ka6bdiizux.png" caption="Using `outputEventsByComponentIdPatterns` to inspect data for the http source shown in the first example of this topic" mode="600" height="1112" width="2216" %}
{% /image %}


### Manually Constructing a Custom Tap

You can find the component id by viewing the Pipeline in the Mezmo Web App. Right-click on the component in the Pipeline Map, then click **inspect**.


{% image url="https://uploads.developerhub.io/prod/2KW7/cxnux4taxrj9j0sfrocnhfq5xoq36cphpzltq7d7m3iiwmcpmycs8ujdeiuj8s71.jpg" caption="Use **Inspect** to find the component ID" mode="300" height="329" width="244" %}
{% /image %}


This will open the **Dev Tools** window, which will display a sub div of the component. Find `data-nodeid`, which will the UUID of the component.


{% image url="https://uploads.developerhub.io/prod/2KW7/ntlehgsyzt3pf5r6h3xyul6o57952ka20z4is310fi21ktkuaufpovcs2q8hn2tv.png" caption="The `data-nodeid`for the component highlighted in blue" mode="responsive" height="156" width="720" %}
{% /image %}


Enter the UUID of the component with wildcard characters and quotes:


{% code %}
{% tab language="none" %}
vector tap "*9c0b419c-bee9-11ee-b560-520afa0d7a83*"
{% /tab %}
{% /code %}


This method can return multiple components, as seen in this example. This shows both the raw message exiting the component, as well as the same message after further processing.


{% code %}
{% tab language="none" %}
{"asdf":"fdsa","source_type":"http_server","timestamp":"2024-02-27T20:51:25.386608710Z"}
{"message":{"asdf":"fdsa","timestamp":"2024-02-27T20:51:25.386608710Z"},"metadata":{"headers":{"accept":"*/*","content-length":"16","content-type":"application/x-www-form-urlencoded","host":"localhost:8010","user-agent":"curl/7.74.0"},"query":null},"timestamp":"2024-02-27T20:51:25.386608710Z"}
{% /tab %}
{% /code %}


By including the component type, shown in this example as `http`, you can tap just the component itself:


{% code %}
{% tab language="none" %}
vector tap "*http*9c0b419c-bee9-11ee-b560-520afa0d7a83*"
{% /tab %}
{% /code %}


This will display only the raw message that exits the component:


{% code %}
{% tab language="none" %}
{"asdf":"fdsa","source_type":"http_server","timestamp":"2024-02-27T20:57:56.435666086Z"}
{% /tab %}
{% /code %}


You can find a list of all component types that you can tap in the **Component Types** section in this topic.

### View Data for a Component with Multiple Outputs


#### View the Data for All Outputs

To view the data through the various transformations of a component with multiple outputs, like the [auto$](/telemetry-pipelines/route-processor), use the `route` command with the UUID of the component.


{% code %}
{% tab language="none" %}
vector tap "*route*304b4ee2-d5a1-11ee-9cf9-12129877dec6*"
{% /tab %}
{% /code %}


This will display the data for each output of the component:


{% code %}
{% tab language="none" %}
{"message":{"asdf":"asdf","timestamp":"2024-02-27T21:12:00.422454671Z"},"metadata":{"headers":{"accept":"*/*","content-length":"16","content-type":"application/x-www-form-urlencoded","host":"localhost:8010","user-agent":"curl/7.74.0"},"query":null},"timestamp":"2024-02-27T21:12:00.422454671Z"}
{"message":{"asdf":"asdf","timestamp":"2024-02-27T21:12:00.422454671Z"},"metadata":{"headers":{"accept":"*/*","content-length":"16","content-type":"application/x-www-form-urlencoded","host":"localhost:8010","user-agent":"curl/7.74.0"},"query":null},"timestamp":"2024-02-27T21:12:00.422454671Z"}
{% /tab %}
{% /code %}



#### View the Data for a Single Output

To view the data for only one of the components outputs, you will need to use the child node ID. As with the node id, you can find the child ID node by using the Dev Tools to inspect the child node ID.


{% image url="https://uploads.developerhub.io/prod/2KW7/fokn3su7qfkk3s3ocie1433wla4cya6u5rsjh0koynl1atxrk5m8xa1epa8amzic.png" caption="The child nodes of a parent multi-output component" mode="responsive" height="62" width="720" %}
{% /image %}


Hover over the line containing the child node id, and the corresponding route in the Web App interface will be highlighted. You can use this to make sure you are selecting the correct child node id.


{% image url="https://uploads.developerhub.io/prod/2KW7/r43p9onfckbryjng7q4pmxes2yxyubkaj0afv7ccklqpeuantorenkqqrjggmy7d.png" caption="" mode="300" height="718" width="720" %}
{% /image %}


The syntax of the child `data.nodeid` is of the form `<component id>.<route id>`. Separate the two ids with an asterisk and add quotations to the full sting:


{% code %}
{% tab language="none" %}
vector tap "*304b4ee2-d5a1-11ee-9cf9-12129877dec6*c534e85e*"
{% /tab %}
{% /code %}


This will display the output for that specific route:


{% code %}
{% tab language="none" %}
{"message":{"asdf":"asdf","timestamp":"2024-02-27T21:36:04.122741881Z"},"metadata":{"headers":{"accept":"*/*","content-length":"16","content-type":"application/x-www-form-urlencoded","host":"localhost:8010","user-agent":"curl/7.74.0"},"query":null},"timestamp":"2024-02-27T21:36:04.122741881Z"}
{% /tab %}
{% /code %}


## Using GraphQL

If you prefer, you can use the GraphQL Playground to inspect Edge Pipeline data.

Follow the instructions for connecting Vector to your Edge instance described in the first section. After completing the step for Port Forwarding, use you browser to navigate to:

[http://localhost:8686/playground](http://localhost:8686/playground)


{% image url="https://uploads.developerhub.io/prod/2KW7/2psoy3ab00uquyqmyvkdd2g710sbgfb3dgt0px5t4z7xs9f7c24mt6lcsxelek0m.png" caption="The GraphQL Playground" mode="responsive" height="359" width="720" %}
{% /image %}


Obtain the component IDs as described in the previous section, and then use the`outputEventsByComponentIdPatterns` to inspect the component.


{% image url="https://uploads.developerhub.io/prod/2KW7/l2d72jt8qpyskdetca6s6o27qyrl4hjd0tpytx27kfprinq1dwr2z4ka6bdiizux.png" caption="Using `outputEventsByComponentIdPatterns` to inspect data for the http source shown in the first example of this topic" mode="responsive" height="1112" width="2216" %}
{% /image %}


This code sample shows the component ID within the `outputsPatterns` field:


{% code %}
{% tab language="none" %}
subscription {
      events: outputEventsByComponentIdPatterns(
        outputsPatterns: ["*http*9c0b419c-bee9-11ee-b560-520afa0d7a83*"],
        inputsPatterns: [],
        limit: 100) {
        ... on Log {
          type: __typename
          timestamp
          metadata: userMetadata
          message: json(field: ".message")
        }
      }
    }
{% /tab %}
{% /code %}


## Component Types Available for Inspection


{% table %}
| Source Type | Processor Type | Destination Type | 
| ---- | ---- | ---- | 
| azure-event-hub | clustering | alert-message | 
| demo-logs | compact-fields | azure-blob-storage | 
| fluent | decrypt-fields | blackhole | 
| host-metrics | dedupe | clickhouse | 
| http | drop-fields | cloudwatch-logs | 
| kafka | encrypt-fields | cloudwatch-metrics | 
| kubernetes-logs | filter | datadog-logs | 
| mezmo-agent | flatten-fields | datadog-metrics | 
| open-telemetry-logs | js-script | elasticsearch | 
| open-telemetry-metrics | map-fields | gcp-cloud-monitoring | 
| open-telemetry-traces | mask-pii | gcp-cloud-operations | 
| splunk-hec | parse-sequentially | gcp-cloud-pubsub | 
| syslog | parse | gcp-cloud-storage | 
|  | reduce | honeycomb-logs | 
|  | route | http | 
|  | sample | indexed-search | 
|  | stringify | kafka | 
|  | unroll | kinesis-firehose | 
|  | vrl | kinesis-streams | 
|  |  | loki | 
|  |  | mezmo | 
|  |  | new-relic | 
|  |  | prometheus-remote-write | 
|  |  | pulsar | 
|  |  | redis | 
|  |  | s3 | 
|  |  | splunk-hec-logs | 
|  |  | sqs | 
|  |  | sumo-logic-logs | 
|  |  | sumo-logic-metrics | 
|  |  | vector | 
{% /table %}

## Disabling Tap from the Edge Helm Configuration

To disable tap from the Edge itself, simply edit the `statefulset` and set two environment variables to `https://localhost`.  This will cause the vector pod to emit error logs when it cannot fetch tasks, but otherwise functionality of the Edge instance is not affected other than to prevent data egress to the SaaS Control Plane from within an environment.


{% code %}
{% tab language="none" %}
# edit the statefulset
kubectl edit sts/edge
{% /tab %}
{% /code %}



{% image url="https://uploads.developerhub.io/prod/2KW7/kogoi8i0le3why6n9bkoi7tv9qr8lz7gbxizfhqvz335pwv240lt29dc455exa35.png" caption="" mode="full" height="81" width="571" %}
{% /image %}


