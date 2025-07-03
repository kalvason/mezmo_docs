---
type: page
title: Parse Sequentially Processor
listed: true
slug: parse-sequentially-processor
description: 
index_title: Parse Sequentially Processor
hidden: 
keywords: 
tags: 
---


## Description

The Parse Sequentially Processor enables you to set up multiple parsers for a single node.  The Processor will attempt to parse the data starting with the first parser in the list.  If there is a match, the remaining parsers will not be evaluated,  and the line will be parsed with the matched parser.

## Configuration

{% table %}

{% table %}
| Option | Description | 
| ---- | ---- | 
| Field | The field to parse | 
| Target Field | The field into which the parsed value should be inserted. Leave blank to insert the parsed data into the original field. | 
| List of Parsers | The parsers to use for the defined field. The Processor will attempt to match the parsers to the defined field, and the first parser that matches will be used. See the [auto$](/telemetry-pipelines/parse-processor) for the list of Parsers you can use and their details. | 
{% /table %}

{% /table %}

{% image url="https://uploads.developerhub.io/prod/2KW7/dkq53ic0ttxpa6bqoytw2jjk6cn69znqhjla5h5tobgsavx4ra3ebixrp2h14h2n.png" caption="This screenshot shows the configuration of the Parse Sequentially Processor with an Unmatched and Apache Log Parser options." mode="300" height="173" width="256" %}
{% /image %}