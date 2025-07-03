---
type: page
title: Webhook Alert Integration
listed: true
slug: webhook-alert-integration
description: 
index_title: Webhook Alert Integration
hidden: 
keywords: 
tags: 
---


The Webhook Alert integration enables customers to easily integrate Mezmo alerts with third-party services.

You can configure the webhook's method, headers, and body. Using an extensive set of tokens, you can customize exactly what content you want to extract from your logs and then include it in your third-party service’s notifications.

For example, if you want to automatically trigger the creation of an Issue in your Jira ticketing system, and include specific information in the Description field, you can do so via webhooks. Read further to see detailed information about webhooks, based on this example of creating a Jira ticket.

## Create an Alert Using the Webhook Integration

As an example throughout this document, we’ll configure our webhook alert to create a new issue in Jira after seeing more than 10 matches for a line with a specific error within 30 seconds.

The first step is to [attach an alert to an existing view](https://docs.mezmo.com/docs/views#attaching-an-alert) that is based on a query for the specific error for which you want to create a Jira ticket. (Alternatively, if you predict that you will want to use webhook integrations for multiple views, you can [create a preset alert](https://docs.mezmo.com/docs/alerts#configure-a-preset-alert-template).

In the image below, we attach an alert to a View named “Errors.”

{% image url="https://uploads.developerhub.io/prod/2KW7/7h7c15qb6ruhq01a15iteqr6c92ha4pfl1gvd07r2zsvjey0roq0i35nw2yzg1sm.png" mode="responsive" height="544" width="666" %}
{% /image %}

On the Alert modal, click the Webhook option.

{% image url="https://uploads.developerhub.io/prod/2KW7/7h7c15qb6ruhq01a15iteqr6c92ha4pfl1gvd07r2zsvjey0roq0i35nw2yzg1sm.png" mode="responsive" height="544" width="666" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/2KW7/8yqglngwu8zkii2xgryngbg7bfj5tdi6b63qaa9dbi5nni9ovdbm62cymk6nwekf.png" mode="responsive" height="1430" width="1634" %}
{% /image %}

## Defining the Alert

First, specify the basic settings for the alert. You can configure the number of matching log lines, the period to observe, and the timing of when the alert is sent. Optionally, you can [create a custom schedule for the alert](https://docs.mezmo.com/docs/custom-schedule-for-alerts).

{% image url="https://uploads.developerhub.io/prod/2KW7/7h7c15qb6ruhq01a15iteqr6c92ha4pfl1gvd07r2zsvjey0roq0i35nw2yzg1sm.png" mode="responsive" height="544" width="666" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/2KW7/8yqglngwu8zkii2xgryngbg7bfj5tdi6b63qaa9dbi5nni9ovdbm62cymk6nwekf.png" mode="responsive" height="1430" width="1634" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/2KW7/y1n86lq6scxfk4u3fu0dn994s5rpwti0acko7pbuy8sxn0jrq4icbwth5kix9mls.jpg" mode="responsive" height="1664" width="754" %}
{% /image %}

## Configuring Your Custom Webhook Integration

In the lower area of the Alert modal, define the specifics of your webhook integration, including the method, the URL for the third-party service, headers for authorization, and finally the body. We will build out the body using our tokens, which enable us to define exactly what log content we want to be written to the Jira ticket.

### Method & URL

First, customize the webhook by selecting the HTTP method and adding the webhook URL. In our example, we select the POST HTTP method and add our webhook URL, https://&lt;YOUR ACCOUNT HERE&gt;.atlassian.net/rest/api/2/issue/. The exact URL and HTTP method will depend on the app for which you add the webhook.

### Headers

Next, set up the headers for the authentication method. The headers depend on the app you are triggering with the webhook.

For our example with Jira, we use [API token authentication](https://confluence.atlassian.com/cloud/api-tokens-938839638.html), which requires us to add an Authorization header with the API token from Atlassian in it.

### Body

By default, the webhook body is pre-populated with alert information. Customize the body to conform to the third-party service’s API; in this case, we customize the webhook body using one or more tokens and structure the body according to the [Jira REST API](https://developer.atlassian.com/server/jira/platform/jira-rest-api-examples/) for creating issues.

So, first we configure the body to create a new issue with the view name in the Summary field of the Issue, and more alert information in the issue description field. We can validate the body to make sure it has valid JSON using the **Validate JSON** button right below the body editor. This validation catches errors and typos without actually executing the webhook.

{% image url="https://uploads.developerhub.io/prod/2KW7/7h7c15qb6ruhq01a15iteqr6c92ha4pfl1gvd07r2zsvjey0roq0i35nw2yzg1sm.png" mode="responsive" height="544" width="666" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/2KW7/8yqglngwu8zkii2xgryngbg7bfj5tdi6b63qaa9dbi5nni9ovdbm62cymk6nwekf.png" mode="responsive" height="1430" width="1634" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/2KW7/y1n86lq6scxfk4u3fu0dn994s5rpwti0acko7pbuy8sxn0jrq4icbwth5kix9mls.jpg" mode="responsive" height="1664" width="754" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/2KW7/74gy4tn5ssi96km9447iju3wm52p2n92wux269vql7pim0jjit58abj58oml1d35.png" mode="responsive" height="400" width="512" %}
{% /image %}

### Body Tokens

The following tokens allow you to further customize the webhook body with specific information about the view or the matched lines that triggered the alert.

- {{ name }} View name
- {{ matches }} Number of matched lines
- {{ lines }} Raw output of matched lines
- {{ level }} Severity level (info, warn, error, etc) in the first line of the log
- {{ url }} The full URL of the View, with first matched line (presence alert only)
- {{ query }} The query of the View to which this alert is attached
- {{ app }} Single application included in the first line of the log
- {{ host }} Single host included in the first line of the log
- {{ tag }} Single tag included in the first line of the log
- {{ line }} The exact text of the first line of the log
- {{ line_objects }} Array of matched line objects
- {{ first_line_object }} First matched line object (the entire line)

{% callout type="info" title="Notes:" %}
- When using the `line_objects` and `first_line_object` tokens, they must be used in isolation because they will insert an array or object into the webhook body, e.g., "lineObjectsArray": "{{ line_objects }}" will turn into lineObjectsArray: [{ ... }].
- Access array indexes and object properties using bracket or dot notation. For example you can use “{{ line_objects[0] }}” or “{{ first_line_object._line }}”.
- Be aware that using some of the tokens, such as the `line_objects`, might result in a large number of returned log lines.
{% /callout %}

### Testing

Test the webhook with the Test link at the top of the pane. The Test link will trigger the webhook with test data. You can also use the Test link to try out what the alert would look like in a real example by filling in the Webhook JSON template. We use it in our example to attempt to create the issue in our Jira project.
After the test runs, we can check that the issue has been appropriately created in our Jira project:

{% image url="https://uploads.developerhub.io/prod/2KW7/7h7c15qb6ruhq01a15iteqr6c92ha4pfl1gvd07r2zsvjey0roq0i35nw2yzg1sm.png" mode="responsive" height="544" width="666" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/2KW7/8yqglngwu8zkii2xgryngbg7bfj5tdi6b63qaa9dbi5nni9ovdbm62cymk6nwekf.png" mode="responsive" height="1430" width="1634" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/2KW7/y1n86lq6scxfk4u3fu0dn994s5rpwti0acko7pbuy8sxn0jrq4icbwth5kix9mls.jpg" mode="responsive" height="1664" width="754" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/2KW7/74gy4tn5ssi96km9447iju3wm52p2n92wux269vql7pim0jjit58abj58oml1d35.png" mode="responsive" height="400" width="512" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/2KW7/rs63kvo4b9kdn78n5yt570h51e22j8qf4sf26wybd1sxd3fuwvjb5vwho2066ray.png" mode="responsive" height="486" width="1318" %}
{% /image %}

## Further Examples

### Microsoft Teams

This webhook will send a message to your [Microsoft Team chat](https://docs.microsoft.com/en-us/microsoftteams/platform/webhooks-and-connectors/how-to/add-incoming-webhook).  Note that you should add the following header to the alert: `Content-Type: application/json`.

{% code %}
{% tab language="json" %}
{
"name": "Mezmo Alarm Topic",
"sentFrom": "{{ name }}",
"summary": "{{ matches }} line(s) matched in {{ name }}. Security level: {{ level }}",
"text": "[Goto]({{ url }}) Mezmo Alert on {{ name }} with {{ matches }} line(s) matched for query {{ query }}\n\nFirst matched log\nApp: {{ appp }}\nHost: {{ host }}\nLevel: {{ level }}\nTag: {{ tag }}\nLine: {{ line }}\n\nLines\n{{ lines }}"
}
{% /tab %}
{% /code %}

### Google Chat

This webhook will send a message to a given [Google Chat Space](https://developers.google.com/chat/how-tos/webhooks).  Note you that you need to add the following header to the alert's webhook: `Content-Type: application/json; charset=UTF-8`.

{% code %}
{% tab language="json" %}
{
"cards": [
{
"header": {
"title": "Mezmo Alert: {{ name }}",
"subtitle": "{{ matches }} matches for {{ query }}"
},
"sections": [
{
"widgets": [
{
"textParagraph":{
"text": "&lt;a href=\"{{ url }}\"&gt;Goto&lt;/a&gt; Mezmo Alert on &lt;b&gt;{{ name }}&lt;/b&gt; with &lt;i&gt;{{ matches }}&lt;/i&gt; line(s) matched for query &lt;b&gt;{{ query }}&lt;/b&gt;\n\n&lt;b&gt;First matched log&lt;/b&gt;\nApp: &lt;b&gt;{{ app }}&lt;/b&gt;\nHost: &lt;b&gt;{{ host }}&lt;/b&gt;\nLevel: &lt;b&gt;{{ level }}&lt;/b&gt;\nTag: &lt;b&gt;{{ tag }}&lt;/b&gt;\nLine: &lt;b&gt;{{ line }}&lt;/b&gt;"
}
}
]
}
]
}
]
}
{% /tab %}
{% /code %}

Which will look like

{% image url="https://uploads.developerhub.io/prod/2KW7/7h7c15qb6ruhq01a15iteqr6c92ha4pfl1gvd07r2zsvjey0roq0i35nw2yzg1sm.png" mode="responsive" height="544" width="666" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/2KW7/8yqglngwu8zkii2xgryngbg7bfj5tdi6b63qaa9dbi5nni9ovdbm62cymk6nwekf.png" mode="responsive" height="1430" width="1634" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/2KW7/y1n86lq6scxfk4u3fu0dn994s5rpwti0acko7pbuy8sxn0jrq4icbwth5kix9mls.jpg" mode="responsive" height="1664" width="754" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/2KW7/74gy4tn5ssi96km9447iju3wm52p2n92wux269vql7pim0jjit58abj58oml1d35.png" mode="responsive" height="400" width="512" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/2KW7/rs63kvo4b9kdn78n5yt570h51e22j8qf4sf26wybd1sxd3fuwvjb5vwho2066ray.png" mode="responsive" height="486" width="1318" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/2KW7/2uvzhz77mypvvk4ln57r7ycm0auqyl54tho11tl249guu2d9ybinyu490lilrsd3.png" mode="responsive" height="572" width="618" %}
{% /image %}