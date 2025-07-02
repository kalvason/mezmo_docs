---
type: page
title: HIPAA Compliance
listed: true
slug: hipaa-compliance
description: 
index_title: HIPAA Compliance
hidden: 
keywords: 
tags: 
---

The Health Insurance Portability and Accountability Act (HIPAA) was created to improve the way organizations handle healthcare data. Not only does it aim to improve the portability of health information, but also requires organizations to protect and secure it. Any entities handling healthcare data are required to comply with HIPAA, even those handling data on behalf of another entity.

If you are a healthcare provider, or an entity providing services to healthcare organizations, you may have compliance obligations under HIPAA. We created this guide to help you understand your potential obligations under HIPAA, and how they may affect your logging strategy.

Note that this is not a legal document, but a guide to help you understand your potential obligations. Always check with your legal team before making any changes to your logging procedures or infrastructure.

## An Overview of HIPAA and HITECH

Title II of HIPAA, known as the Administrative Simplification provisions, sets standards for protecting and securing private health records (known as protected health information, or PHI). This includes patient records, medical records, and even insurance and billing records. Under HIPAA, any entities that handle this kind of data can be held legally accountable if the data is leaked, stolen, or misused.

The Health Information Technology for Economic and Clinical Health Act (HITECH) expands on HIPAA by promoting the use of technology in managing PHI. It offered financial incentives to healthcare providers for adopting electronic health records, while adding tougher penalties for non-compliance. After HITECH was enacted in 2009, the use of electronic records in healthcare organizations jumped from [3.2% in 2008 to 14.2% in 2015](https://www.hipaajournal.com/what-is-the-hitech-act/).

### How Logs Fit Into HIPAA

Monitoring and observability play a significant role in HIPAA compliance. Organizations must be capable of:

- Auditing employee access to ePHI
- Monitoring changes to systems storing ePHI
- Identifying and investigating potential security breaches

Logs play a vital role in this process as they contain information about application and system operations, user activities, and security incidents. They provide specific and vital details about events including the exact time that it occurred, the application that generated the event, and the users or systems that were involved. Using a log management solution like Mezmo allows you to aggregate logs from all of your systems in a secure central location, as well as providing tools to search, analyze, visualize, and archive your logs to ensure compliance.

## Requirements for Logging

The following HIPAA sections outline your requirements for logging. In the following section, we’ll explain how to satisfy these requirements using Mezmo.

Before continuing, we need to explain some of the terms used in HIPAA. A [covered entity](https://www.hhs.gov/hipaa/for-professionals/faq/190/who-must-comply-with-hipaa-privacy-standards/index.html) is generally any healthcare provider, health plan, or healthcare clearinghouse that transmits PHI. A [business associate](https://www.hhs.gov/hipaa/for-professionals/privacy/guidance/business-associates/index.html) is any individual, organization, or entity that processes PHI on behalf of a covered entity. If you are a covered entity sending your logs to Mezmo, then we are considered a business associate and have specific obligations for protecting your data. These obligations are described in a Business Associate Agreement (BAA), which must be signed by both the covered entity and business associate before the business associate can provide service.

### Section 164.312: Technical Safeguards

This section outlines policies and procedures for protecting and monitoring access to systems containing ePHI. § 164.312(b) specifically addresses auditing, requiring “mechanisms that record and examine activity in information systems that contain or use electronic protected health information.”

While this doesn’t specify which activities to log, consider the events that would be important to an audit. Authentication logs, software and hardware modification logs, process logs, and even network logs are all important for monitoring and auditing secured systems.

### Section 164.308: Administrative Safeguards

Covered entities are required to “implement policies and procedures to prevent, detect, contain, and correct security violations.” More specifically, § 164.308(a)(1)(ii)(D) requires regular reviews of information system activity “such as audit logs, access reports, and security incident tracking reports.” This section also includes specific monitoring procedures, including:

- Malicious software activity (§ 164.308(a)(5)(ii)(B))
- Log-in attempts and discrepancies (§ 164.308(a)(5)(ii)(C))
- Suspected or known security incidents (§ 164.308(a)(6)(ii))

### Section 164.316: Policies and Procedures and Documentation Requirements

§ 164.316(b)(2)(1) requires covered entities to retain documentation records for at least six years. However, there’s uncertainty as to whether [audit logs are included in this requirement](https://www.schellman.com/blog/hipaa-audit-log-retention-requirements-do-i-really-need-to-retain-all-my-audit-logs-for-6-years). § 164.316(b)(1)(ii) states that any action, activity, or assessment required to be documented must be recorded, and audit logs technically document activities performed by systems and users.

## Recommendations for HIPAA-Compliant Logging

Given these requirements, these are our recommendations for how you can structure your logging strategy to be HIPAA-compliant. Remember that these are recommendations and not legal advice. Always consult with your legal team before changing your logging strategy.

### Avoid Logging PHI

Audit logs should rarely if ever contain PHI. Storing PHI in logs increases the risk of a violation, especially if those logs are exported, copied, shared, or archived to a third-party service.

If you do need to reference PHI in logs, avoid logging the PHI directly but instead log an abstract identifier that refers back to the PHI. For example, consider an audit log that records access to patient records. Instead of logging protected data such as the patient’s name or Social Security number, log the record number as it appears in the database. This ensures that a patient can’t be identified by logs alone, and can only be identified by accessing both the logs and the patient records. This process is known as de-identification (or pseudonymization) and is a standard under [§ 164.154(a)](https://www.hhs.gov/hipaa/for-professionals/privacy/special-topics/de-identification/index.html).

### Log all Operational and Security Events

HIPAA requires strict oversight over systems containing PHI, as described in §§ 164.308(a) and 164.312(b). While there isn’t an exact definition of the types of activities you’re required to log under HIPAA, consider logging important system and security events such as:

- Access to protected information and applications
- Logins, logouts, and failed attempts
- Password changes
- Changes to security systems (e.g. firewalls, antivirus software)
- Antivirus or antimalware events
- Network changes (e.g. new devices connecting to a secure network)
- Software installations, uninstallations, and updates
- Processes starting and stopping

We recommend retaining audit logs for at least six years. Most Mezmo plans retain 30 days of searchable (i.e. “hot”) log data. For longer retention, Mezmo provides an [archiving service](https://docs.mezmo.com/docs/archiving) that automatically exports older logs to a cloud storage service. Remember to request a BAA from your cloud storage provider and secure your storage bucket before enabling archives.

### Secure Your Logging Infrastructure

Logs may not contain PHI, but they do contain sensitive information about HIPAA-regulated systems and applications. Restricting access to your logs and logging infrastructure is an important step in preventing an attacker from finding vulnerabilities in your infrastructure.

#### Use Encryption

When sending logs to Mezmo’s cloud ingestion servers, use HTTPS or syslog with TLS to encrypt your logs in transit. Otherwise your logs will be sent in plain text, making them trivial to intercept by a malicious third party.

Encryption is enabled by default in the Mezmo agent and in our official code libraries. Mezmo also encrypts your logs when storing them, and only allows access to the web application over secure HTTPS. If you are [archiving your logs](https://docs.mezmo.com/docs/archiving), be sure to encrypt your storage bucket before enabling the archiving process.

#### Apply the Principle of Least Privilege

The principle of least privilege is a general-purpose principle where users are given the fewest permissions necessary to perform a task. For example, if an engineer needs to access logs from a specific system, that engineer should be given read-only access to only that system’s logs. This is referred to as “access control” under § 164.312(a)(1), which requires protected systems to “allow access to only those persons or software programs that have been granted access rights as specified in § 164.308(a)(4).”

Mezmo lets you set granular permissions using [role based access control (RBAC)](https://docs.mezmo.com/docs/rbac). You can restrict each user’s ability to view, create, or modify Mezmo resources, as well as restrict their access to logs based on source or content.

#### Lock Down Your Logging Infrastructure

Sending logs to Mezmo requires you to expose certain ports (e.g. 6514 for Syslog with TLS and 443 for HTTPS). When configuring your firewall, you should only allow outbound traffic from these ports to avoid exposing your systems to unnecessary risk. When using Mezmo on-premise, isolate your logging infrastructure from the public Internet as much as possible to avoid placing your logs in unnecessary risk. In addition, strictly limit system-level access to these systems to specific engineers or members of your operations team.

### Regularly Review Your Logs

Under HIPAA, it’s not enough to simply send your logs to Mezmo and store them in an archive for six years. These logs must be constantly monitored and analyzed for signs of any unusual activities, changes in system and application behavior, or potential security incidents.

Section 164.308(a)(1)(ii)(D) requires regular reviews of “information system activity, such as audit logs, access reports, and security incident tracking reports.” We recommend designating an employee to check logs on a daily basis, as well as using automated analysis tools such as [views and alerts](/docs/add-alerts-to-views). For example, you can use Mezmo to automatically notify your security team if it detects too many failed logins over a short period of time.

#### Auditing Your Logging Systems

Regularly reviewing your logs plays another important role by ensuring the logs themselves remain compliant. As with any information system, logs have a risk of becoming lost or corrupt. Remaining compliant means taking measures to protect against this risk and quickly identify it when it happens.

For example, imagine one of your systems fails to send its logs to Mezmo. Without adequate monitoring, you may not find out about this until you go to search on the system’s logs. To avoid this scenario, create an [absence alert](https://mezmo.com/blog/mezmo-absence-alerting/) that monitors for any sudden, sharp drops in log volume. An absence alert will immediately notify you of a decrease in log volume, letting you troubleshoot the problem faster.

This also applies to archives, as storing archives on a third-party system introduces additional risks of data corruption or loss. This risk is smaller with major providers such as Amazon and Google, but being proactive is much safer than being non-compliant. We recommend periodically checking your archives against the logs stored in your Mezmo account, and if you notice any discrepancies in log volume, [contact us](https://www.mezmo.com/contact-us) to regenerate the archive. As long as the issue is identified within your retention period, we can regenerate the archive with no loss in log volume.

## How Mezmo Supports HIPAA Compliance

Mezmo is ready to help you meet your HIPAA compliance requirements. Our systems are audited annually for HIPAA and HITECH compliance by a third-party qualified security assessor. We are committed to protecting your data and will happily sign a Business Associate Agreement (BAA). You can learn more about our commitment to compliance on our [compliance page](https://mezmo.com/compliance/). If you have any questions about Mezmo or about HIPAA compliance with Mezmo, please [contact us](https://mezmo.com/contact-us/).