---
type: page
title: Introduction: Telemetry Data Optimization with Mezmo Pipelines
listed: true
slug: data-optimization-introduction
description: 
index_title: Introduction: Telemetry Data Optimization with Mezmo Pipelines
hidden: 
keywords: 
tags: 
---


## A Day in the Life of an SRE: Too Much Data, Man!

Today's applications are composed of a multitude of components and micro-services within a "stack," each of which generates its own telemetry data. This results in an overwhelming volume of data to store and analyze. In many cases, this data is sent directly to observability tools, but lacks the optimization necessary to turn it from raw data to useful information. Worse yet, much of this data is not inherently useful and only contributes to "data bloat" that results in high costs for storage and observability tools.

## Mezmo's Approach to Data Optimization

Mezmo's approach to the problem of too much data is to provide you with the means to first understand your data, optimize it for your observability tools and storage solutions, and derive new insights into your systems. In our own analysis of typical data samples from sources such as Kubernetes, we have identified specific processing techniques for optimizing and reducing the volume of telemetry data, developed Processor components to match these techniques, and created features that enable you to understand and interact with your data in stream.

## In This Guide

In this guide you'll find:

- A [deep dive into the five techniques of data optimization](/practioner-guide-data-optimization/optimize-your-observability-data-in-five-steps) and their relationship to Mezmo Telemetry Pipeline Processors
- The [summary results and key findings](/practioner-guide-data-optimization/analysis-data-reduction-techniques) from our research into telemetry data optimization
- A set of [auto$](/practioner-guide-data-optimization/reference-architectures-for-data-optimization-pipelines) so you can learn how to create Pipelines for your own use cases