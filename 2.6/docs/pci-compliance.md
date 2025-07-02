---
type: page
title: PCI Compliance
listed: true
slug: pci-compliance
description: 
index_title: PCI Compliance
hidden: 
keywords: 
tags: 
---




The Payment Card Industry Data Security Standard (PCI DSS) establishes protections for credit cardholder data, including how it’s stored and accessed. This means that a significant portion of the standard—specifically, Requirement 10—governs auditing and logging your applications and systems.

Complying with these regulations may seem daunting, but we’re here to help. As a PCI Level 1 Service Provider, we take compliance very seriously. We developed this guide to summarize your requirements for creating and managing log data.

Note that this is not a legal document, but a guide to help you understand your potential obligations. Always check with your legal team before making any changes to your logging procedures or infrastructure.

## What PCI Means for Logging

Logs are one of your primary tools in monitoring and auditing systems containing sensitive cardholder data. While logs may not directly contain cardholder data, they do contain critical information about the operation, state, and contents of systems that handle cardholder data. Implementing a PCI compliant logging strategy therefore involves:

- Generating logs that can be used to audit systems
- Logging data that allows you to trace user activity on these systems
- Storing these logs securely and restricting access to authorized individuals

Requirement 10 addresses these directly, but Requirements 3 and 12 also impact log data. We’ll explain each of these requirements and their sub-requirements in more detail.

## Requirement 3: Protect stored cardholder data

Requirement 3 explains how cardholder data should be secured using techniques such as encryption, masking, and truncation. While logs most likely won’t contain cardholder data, you shouldn’t rule out the possibility. If a credit card number was accidentally leaked in a log file, it could result in significant penalties.

To avoid this, any sensitive data that gets logged should be hashed or masked to avoid leaks. A common method involves using regular expressions to scan each log event and replace matches with a masked value. For example, if you use Fluentd, the [record_transformer plugin ](https://docs.fluentd.org/filter/record_transformer)will replace a specific field with a different value that you specify.

### Requirement 10: Monitor access to network resources and cardholder data

Requirement 10 outlines the necessary practices for auditing, monitoring, and alerting on user access to sensitive systems and data. It oversees the collection of log data, its contents, how it should be stored, how long it should be retained, and more. The goal is to ensure that any action can be traced back to a specific user or process.

Let’s look at each requirement in more detail:

**Requirement 10.1** requires that all access logs be linked to an individual user. Your logs should create an audit trail that can be traced from a particular event back to the user who initiated it. This means storing contextual user data in your logs, such as usernames or user IDs.

**Requirements 10.2** and **10.3** list the types of events and associated data to collect in order to fully audit your systems. You will need to log any valid or invalid attempts to access cardholder data, any actions performed by a privileged account, access or changes to your logs and logging mechanisms, changes to identification or authentication mechanisms, and changes to system-level objects (such as databases or stored procedures).

To create a complete audit trail, each log event should include a timestamp, the type of event and whether it succeeded, user identification, where the event occurred, and what component(s) it affected. Mezmo includes much of this data when logging from the agent or a code library, but more contextual data (like user IDs, event types, and successes or failures) may need to be added to your logging calls.

**Requirement 10.5** enforces secure, unalterable audit trails. Mezmo prevents any modifications to your log data after ingestion, centralizes and encrypts your logs, and provides comprehensive authentication measures and role-based access control (RBAC) to prevent access from unauthorized users.

**Requirements 10.6 & 10.8** involve regularly reviewing logs for suspicious activities and component failures (Requirement 10.8 only applies to service providers). PCI DSS allows for automated systems to be used in place of manual reviews, and with Mezmo alerts you can monitor your logs 24/7. If a security alert fires, make sure to follow up with your team to make sure the issue is investigated and addressed according to your organization’s security policies.

**Requirement 10.7** specifies that at least the past 3 months of log data is immediately available for analysis. To increase your Mezmo retention period to 3 months (90 days) or more, please contact us. (Standard retention times are 7, 14, and 30 days.) The 10.7 requirement also specifies one year or more of cold log data for auditing purposes. To meet both the requirements for the past 3 months and the cold storage of 1 year, you can configure Mezmo to automatically generate nightly log archives and send them to your encrypted cloud storage bucket.

## Requirement 12: Maintain an information security policy

PCI DSS requires organizations to main a security policy explaining how employees, contractors, and consultants is expected to treat cardholder data. While this requirement isn’t directly related to logging, logging can help with compliance.

**Requirement 12.5.2** requires that security alerts are not only monitored, but distributed to the appropriate parties so that they can respond to the alert. For example, if an alert indicates a systems failure, this might involve exporting logs to the Ops team so that they can troubleshoot the affected system. These alerts and the individual(s) responsible for responding to them should be included in your incident response plan, according to Requirement 12.10.5

*_Requirement 12.8 *_defines your relationship with any service providers who might affect the security of cardholder data. This includes Mezmo. While we are committed to complying with PCI DSS, it’s your responsibility to perform due diligence (Requirement 12.8.3) and ensure that we are PCI DSS compliant at least once per year (Requirement 12.8.5).

## How Mezmo Supports PCI DSS Compliance

Mezmo is committed to protecting your data. We have been audited by an independent PCI Qualified Security Assessor (QSA) and certified as a PCI Level 1 Service Provider. If you have any questions about compliance, please[ contact us](https://www.mezmo.com/contact-us).





