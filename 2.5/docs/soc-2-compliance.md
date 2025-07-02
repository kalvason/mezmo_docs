---
type: page
title: SOC 2 Compliance
listed: true
slug: soc-2-compliance
description: 
index_title: SOC 2 Compliance
hidden: 
keywords: 
tags: 
---




More and more industries are turning towards cloud computing services as a way to process more data at lower costs. However, organizations that handle sensitive data need assurance from service providers that their data will be strongly protected. While regulations like [HIPAA](/docs/hipaa-compliance) and [the GDPR](/docs/gdpr-compliance) create strict rules for specific industries and regions, there is no single federal law enforcing data protection in the U.S. To fill this gap, many service providers including Mezmo offer Service Organization Controls (SOC) 2 compliance, which describes the policies and practices that a provider has in place for protecting customer data.

In this guide, we’ll explain how you can use Mezmo to become and remain compliant with SOC 2. This document does not provide legal advice, but is a general purpose guide to help you identify and understand your potential obligations. Always check with your legal team before making any changes to your operations.

## Background Information on SOC and SSAE

SOC is neither a regulation or a standard, but a report that describes an organization’s internal controls over data managed on behalf of their users. It stems from the Statement on Standards for Attestation Engagements (SSAE), which is an auditing standard for service providers (called _service organizations_) and maintained by the American Institute of Certified Public Accounts (AICPA). SSAE requires service organizations to describe the systems, controls, and processes that they have in place for protecting and maintaining the integrity of data belonging to their customers (called _user entities_).

To comply with SSAE, a service organization is audited by a third party CPA. The CPA reviews the organization’s controls over data and documents their findings in a SOC report. SOC 1 reports describe these controls and how they could affect a user entity’s financial reporting capabilities. SOC 2 reports, on the other hand, describe how the service organization handles all types of data, not just data related to its user’s finances.

SOC 1 and SOC 2 reports come in two types:

- **Type I** reports describe the service organization’s controls at a particular point in time. This shows that the controls in place are properly designed.
- **Type II** reports describe the effectiveness of the organization’s controls over a period of time. These are generally preferred, since they indicate that the controls are most likely in place and working as intended every day.

### Trust Services Criteria

SOC 2 reports are based on a set of criteria called the Trust Services Criteria (TSC). These criteria outline how the organization was evaluated and reported on. These criteria fall into five categories: security, availability, processing integrity, confidentiality, and privacy. We’ll explain each of these categories in greater detail and show how logs can help you meet the criteria in each category.

## How Logs Factor into SOC 2 Compliance

The purpose of a SOC 2 Type II report is to show that your systems and processes operated securely over a period of time. This means having the ability to monitor your infrastructure, identify unusual events or security incidents, and troubleshoot problems. Logs play a vital role in this process, since they store highly detailed records of infrastructure operations and events over a period of time. This makes them ideal for reviewing and auditing both current and past operations.

Note that the quoted passages in this section are from the official [Trust Services Criteria Publication](https://www.aicpa.org/content/dam/aicpa/interestareas/frc/assuranceadvisoryservices/downloadabledocuments/trust-services-criteria.pdf) from the AICPA.

### Security

Security involves protecting information and systems “against unauthorized access, unauthorized disclosure of information, and damage to systems that could compromise the availability, integrity, confidentiality, and privacy of information or systems and affect the entity’s ability to meet its objectives.” Strong security controls protect data—and the systems that handle this data—from being accessed or modified by an unauthorized entity. Security is the only category required for SOC 2 compliance.

A vital use of logs is monitoring for security events. This can include user logins, software modifications, changes to system settings and processes, and changes to your organization’s network. Many critical security events are already logged by the operating system; for example, the “auth.log” file found in most Linux distributions records all login attempts and any administrator-initiated actions, making it essential for monitoring system-level access.

Security events must be monitored for signs of suspicious activity. With Mezmo, you can use [alerts](/docs/alerts) to continuously scan incoming logs and send a notification if an anomaly is detected. For instance, if a user logs into a server containing sensitive data as an administrator, you may want to notify your organization’s security team to investigate further. The team can then audit the event, find out what the user did, and in case of a breach, determine the severity and scope of the incident.

### Availability

Availability is the assurance that “information and systems are available for operation and use to meet the entity’s objectives.” Limited availability of even a single component can have numerous effects on your total operations, including:

- Limiting customers’ access to their data
- Reducing the availability of other components
- Reducing trust in your services

The problem may be as simple as a network connection failure, or as critical as a component failure, but without a way of monitoring availability, your team may spend hours diagnosing the cause of the problem.

Monitoring for availability is straightforward with logs. Nearly all systems, devices, and applications generate log data, and a lack of log data is a fairly reliable indicator of a communication or operational problem. [Absence alerts](https://mezmo.com/blog/mezmo-absence-alerting/) are a useful method of monitoring availability, since they will raise a notification when log volume drops below a certain level over a period of time. Using logs to monitor availability won’t just alert you to a problem, but it will also give you the means to troubleshoot and identify the cause of the problem.

### Processing Integrity

Processing integrity ensures that systems “perform their intended functions in an unimpaired manner, free from error, delay, omission, and unauthorized or inadvertent manipulation.” If a system fails to process data correctly, or if it does so slowly, it can rapidly erode customer trust in your service.

The challenge to monitoring processor integrity is knowing when an error occurs. If you tried to monitor the timing and accuracy of every single processing activity in your system, your logs would quickly grow unwieldy. Instead, you might consider logging processing activities for key systems, especially systems containing or operating on sensitive customer data.

In addition, you can use trace logs to monitor the flow of data throughout the application and ensure each step is working as intended. In our blog post on [Challenges Logging Services Applications](/docs/filters)(https://www.mezmo.com/blog/challenges-with-logging-serverless-applications)&cma; we showed how logging contextual data makes it easy to index logs by request or other custom fields. You can then use the [Mezmo web app](https://app.Mezmo.com/) to quickly filter on these fields in order to audit a specific request without having to comb through your other logs.

### Confidentiality and Privacy

Confidentiality and privacy are two different criteria with a similar focus: protecting sensitive information from unauthorized disclosure. The main difference is that “privacy applies only to personal information, whereas confidentiality applies to various types of sensitive information.” The privacy criteria also sets the requirements for collecting, using, retaining, disclosing, and disposing of data, similar to how [the GDPR](https://www.mezmo.com/gdpr) sets restrictions on the use of personal data belonging to EU citizens.

Privacy is one of the most important categories to monitor since it involves a number of scenarios regarding the use of customer data. For example, criteria 2 (choice and consent) requires you to communicate the choices that your data subjects have over the use of their personal information. If a data subject grants or revokes their consent, logging this action creates a historical record in case of a dispute or any uncertainty in how a subject’s data should be handled. The importance of monitoring these types of activities is also outlined in criteria 8 (monitoring and enforcement).

Logging events affecting user data is not only a good practice, but it can also help protect you in case of a dispute.

### Other Considerations

There are several additional points to keep in mind when logging for SOC 2 compliance.

Depending on how long your audit period is, you may need to retain logs for six months or longer. Mezmo offers 30 days of retention, but you can use the [archive feature](/docs/archiving) to export logs to a cloud storage service indefinitely. Although archives can’t be searched in the Mezmo web app, you can use [one of many tools](https://www.mezmo.com/blog/how-to-search-through-mezmo-archives) to parse and search them outside of Mezmo.

In addition, we recommend using views to control and filter your log stream. Auditing an entire infrastructure is no small task, and SOC 2 specifies many different categories of events to analyze. [Using views effectively](https://www.mezmo.com/blog/guide-mezmo-views) will help simplify and streamline the log analysis process, both for your organization and for auditors.

## How Mezmo Supports SOC 2 Compliance

Whether you’re following all five criteria categories or just the common criteria, logging should be a key part of your SOC 2 compliance strategy. Mezmo provides a comprehensive platform for collecting, monitoring, and analyzing logs across your entire infrastructure. We became [SOC 2 compliant](https://www.mezmo.com/compliance) back in 2017, and we want to make sure that our platform can help you reach your SOC 2 compliance targets.

If you have any questions, including questions about Mezmo’s SOC 2 compliance, please feel free to [contact us](https://www.mezmo.com/contact).





