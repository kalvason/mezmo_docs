---
type: page
title: GDPR Compliance
listed: true
slug: gdpr-compliance
description: 
index_title: GDPR Compliance
hidden: 
keywords: 
tags: 
---




The General Data Protection Regulation (GDPR) is a European Union regulation that grants extensive data privacy protections to EU citizens. It describes the rights of individuals concerning the collection, transmission, and processing of their data. It also describes the obligations of organizations handling this data, including organizations not based in the EU.

Although the GDPR is an EU regulation, the scope and restrictiveness of its laws have made it the de-facto standard under which organizations operate. Organizations that handle EU citizen data without following GDPR can be subject to fines of up to [€20 million or 4% of their annual global turnover](https://www.itgovernance.co.uk/dpa-and-gdpr-penalties), investigations, and even a ban on serving EU citizens in the future.

In this guide, we’ll explain how to remain compliant with the GDPR as a customer of Mezmo. This document does not provide legal advice but is a general-purpose guide to help you identify and understand your potential obligations. Always check with your legal team before making any changes to your operations.



## The Basics of GDPR
The crux of the GDPR is _personal data_, which is defined under Article 4 as “any information relating to an identified or identifiable natural person.” This includes names, addresses, physiological data, and even online identifiers like IP addresses. Anyone who can be identified through this information is considered a _data subject_. Essentially, the GDPR protects data subjects by restricting the use of their personal data.

Some of the rights that the GDPR gives to data subjects include:
*   Requiring consent before their data can be collected, processed, or shared (Article 7)
*   Learning how their personal data is being collected, processed, shared, and safeguarded (Article 15)
*   Recourse in correcting inaccurate data records (Article 16)
*   Requesting permanent deletion of their data, also called the “right to erasure” or the “right to be forgotten” (Article 17)
*   Restricting how their data is processed (Article 18)
*   Requesting electronic copies of their data (Article 20)
*   Objecting to certain types of data processing, including automated processing (Article 21)



### Data Controllers and Data Processors
The GDPR makes a distinction between [data controllers and data processors](https://ec.europa.eu/info/law/law-topic/data-protection/reform/rules-business-and-organisations/obligations/controller-processor/what-data-controller-or-data-processor_en). A _data controller_ determines how and why personal data is collected and processed. A _data processor_ processes personal data on behalf of a data controller. The relationship between a processor and a controller must be outlined in a legal document explaining how the data is to be managed. Note that even though controllers and processors have different obligations under the GDPR, a controller can still be held liable for breaches caused by their processors.

In addition, Section 4 requires controllers and processors to designate a Data Protection Officer (DPO) to oversee the organization’s GDPR compliance.



## What GDPR Means for Logging
Logs contain a wealth of information about application performance, system operations, user activity, and errors. However, this data creates a substantial risk of personal data making its way into logs, whether deliberately or accidentally.

Consider a web server access log. A single entry may contain a user’s IP address, the requested URL, their browser’s user agent, and even their username if they’re logged into your application. If the user causes the application to throw an exception, additional personal data could be logged in a stack trace or variable dump. All of this qualifies as personal data and is enforceable under the GDPR.

Under Article 6, this data can be used lawfully in certain scenarios, including when:
*   The data subject gives their explicit consent
*   It’s necessary to fulfill a contract or agreement with the data subject
*   You are complying with other legal obligations
*   You are protecting the interests of the data subject

The GDPR also grants data collectors some flexibility to use personal data as long as those uses are legitimate, don’t conflict with other obligations, and are transparent to data subjects.



## Best Practices for Becoming Compliant
The following are general recommendations for mitigating your risk under the GDPR. These are only recommendations and don’t constitute legal advice. Always consult with your DPO before making any changes to your logging strategy.



### Shrink and Reduce Your Logs
The easiest way to reduce your risk is to avoid logging personal data in the first place. When reviewing your current logging practices, consider:

1. What personal data is contained within your logs
2. Where your logs are being stored, and for how long

Collecting too much data is a liability, especially if it doesn’t contribute to your operations. Some data—such as session IDs—can be useful for auditing and troubleshooting, but you should be able to justify its inclusion in your logs. Article 6 only protects legitimate uses of personal data, so consider whether the data in your logs is essential to your everyday operations.

If you’re not sure which data is protected, refer to Article 4(1). Examples of personal data can include IP addresses, geolocation data, and user IDs. Keep in mind that some of this data may be exposed through automated memory dumps and stack traces. If this is a risk, consider modifying your logging implementation to remove or pseudonymize this data if possible.



### Pseudonymize User Data
If you need to link a log to a particular data subject, swap out their personal data with pseudonymized data. Pseudonymization is the process of using non-identifying data in place of personal data, while still allowing the non-identifying data to identify an individual.

For example, consider an application that logs each successful login. Normally these logs would contain the name of the user that logged in, but if the logs were ever breached, an attacker could identify all of our active users. Instead, we assign a randomly generated number for each user, store it with the rest of their user data, then log this number in place of the user’s name. This way, we can use the number to find the associated user, but an attacker would only see the random number. This is the key difference from _anonymized_ data, which is impossible to link back to an individual.

Under Article 25, pseudonymization is considered an appropriate measure for safeguarding data without losing the ability to log user activities.



### Log GDPR-Related Activities
Any activities that impact your requirements under the GDPR—including how you can use personal data—should be logged. Certain actions can affect your ability to process data, but it’s your responsibility to show that you have the right to do so.

For example, Article 7 allows you to process personal data if the data subjects gives you their consent. However, you must be able to prove that you received this consent, which means storing a record of this consent. Even when a data subject has granted consent, they can revoke that consent or make requests to have their data amended, deleted, or removed from certain types of processing. Not only do you need to prove that you received these requests, but you also need to prove that you honored them.

The main purpose of logging GDPR-related activities is to create an audit trail. Article 12 gives data subjects the right to take legal action against controllers if a request has gone unanswered for longer than one month. Logging these activities can protect you in case of a dispute.



### Secure Your Logs
Part of protecting personal data means protecting your logs from unauthorized access. Encryption is your first line of defense against a breach by preventing logs from being read by anyone other than its intended recipient. Mezmo uses military-grade encryption to protect your logs both in transit and at rest. Using the [Mezmo agent](/docs/introducing-the-agent), HTTPS endpoint, [syslog with TLS](/docs/rsyslog#tcptls-recommended), or one of our code libraries will automatically encrypt your logs before sending them to Mezmo.

If you have [archiving](/docs/archiving) enabled, make sure the storage device receiving your archives is also encrypted. Some of the [largest data leaks](https://businessinsights.bitdefender.com/worst-amazon-breaches) to date resulted from unsecured and unencrypted cloud storage devices. Refer to your cloud storage provider’s documentation to learn how to secure your cloud storage bucket.

Lastly, only certain members of your organization should have access to logs containing personal data. Mezmo provides role-based access controls (RBAC) that lets you restrict certain members’ access to logs. Members who sign into Mezmo are only shown a subset of logs according to their role, reducing the chance of them accidentally viewing or leaking personal data. We recommend you give each member of your Mezmo organization the fewest privileges necessary to perform their tasks.



### Limit Retention
The GDPR doesn’t specify a minimum or maximum retention period for log data. Article 5(1)(e) says to retain personal data for no longer than necessary to process it, or when archiving under the conditions outlined in Article 89(1). Generally speaking, stick to shorter retention periods unless you’re certain that your logs contain no personal data.

One major exception is audit logging. According to Recital 85, if a breach occurs, you are required to report the breach to a supervisory authority within 72 hours of detecting it, or otherwise prove that no personal data was leaked. Storing a minimum of 72 hours' worth of log data will help you determine the cause and scope of a breach, or prove that there was no unauthorized access to personal data.

Mezmo only retains your logs for the duration specified by your plan, after which they are securely deleted. If you want to retain logs for longer, consider using [Mezmo's archive feature](/docs/archiving).



## How Mezmo Supports GDPR Compliance
Mezmo works diligently to protect your privacy and your customers’ privacy. You can learn more about our compliance practices on our [GDPR compliance page](https://www.mezmo.com/gdpr). And if you’re not sure how logging with Mezmo might impact your obligations under GDPR, [contact us](https://www.mezmo.com/contact) for more information.





