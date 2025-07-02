---
type: page
title: Custom Parsing & How to Parse Logs
listed: true
slug: custom-parsing
description: 
index_title: Custom Parsing & How to Parse Logs
hidden: 
keywords: 
tags: 
---



Mezmo supports [common log types](/docs/ingestion#supported-types) and parses the lines automatically for you. However, if you have a log format that does not fit one of the supported log types, you can create your own parsing rules within a custom parsing template.

Mezmo takes a more visual approach to defining custom parsing rules. We created a step-by-step wizard that walks you through the process of splitting (or tokenizing) your logs into separate fields and extracting those fields. You have full control over how your logs are tokenized and how each field is formatted, without the frustration of writing regex. In addition, you can see the effect of each operation on your logs in real-time.

## General log parsing template rules

- Your organization's Parsing Templates are managed under the **Manage Parsing** page which can be found under settings.
- There are 3 status types for parsing templates:
- _Active:*_ Valid parsing templates that will be applied against your logs.
- _Inactive:** Valid parsing templates that will *not_ be applied against your logs.
- _Draft:*_ Invalid parsing templates. These are either incomplete, contains errors or have not yet been validated.
- Activated parsing templates are only applied to the lines that come in after the template has been enabled. All log lines that were ingested prior to the template becoming active are not parsed by the parsing template.
- Parsing templates are applied to your logs based on the order of active templates. If you have 2 active parsing templates that are targeting the same log line, then the order of how parsing templates are applied is determined by the order seen in the Manage Parsing page. The template below gets applied after and if they both use the same field name, the template below overrides the one below.

**Here's an example:**
According to this example case, if Template A and Template B is targeting the same log line, Template A gets applied first and then Template B gets applied second to the line. If Template A and Template B contains the same field name, Template B's rule to capture the value for the field overrides the Template A's.

## Steps to create a custom parsing template

1. **Choose Log Line:** To build a template, a sample log line is needed. Either manually enter a sample logline or use a search query to have Mezmo bring up suggestions from your ingested lines.
2. **Parsing Template:** The sample log line is used as a reference and you can build the parsing rules with the parsing operators. A variety of delimiters can be used to split the log into its individual fields. If the log line is a stringified JSON object, that can be used to split the log lines as well.
3. **Test & Verify:** The custom parsing template can be tested with another sample log line either manually entered or through a query. Parsing rule is run through different sample lines and each result requires you to mark it Valid or Invalid. The template can now be Activated.

- Parsing Template has to have a`Query` defined either on stage 1 or stage 3, which targets the log lines that need to be parsed by the parsing template so that Mezmo knows where what group of log lines to apply the parsing to. It is used to filter the log lines. If `Query` field for the parsing template is added during **Choose Log Line** stage, it used as a query for the template. If not, you are asked to provide "Query" on Test & Verify stage.
- If you choose to add sample log line manually on Choose Log Line (Stage 1), you also need to manually add different sample log lines in Test & Verify (Stage 3). At least 1, at most 10 log lines can be added and verified at this stage. This stage ensures that your parsing template can handle different cases and still parses the values for the fields in a way you like.
- In Test & Verify (Stage 3), it's required you to confirm the result of parsed fields of each sample log line, and mark as `Valid` or `Invalid`. Each sample line has to be "Validated" (marked as `Valid`) to consider the parsing template shows key-value pairs as expected. If a sample line is marked as `Invalid` because one or more of the values for the line is not what you expected, you will be sent back to the Parsing Template (Stage 2) where the sample log line (that is marked as invalid) is applied as a reference line to help you identify the template issue.

## Parsing Template Minimap

- Rule path is the branch that contains the chain of operators used to capture the fields for your line.
- In Parsing Template (Stage 2), as you set up rules by connecting the parsing operators, the minimap appears on the right section of the page. Every parsing template contains its own Minimap structure.
- Minimap helps you to navigate through other branches within the parsing template. It is shown on the left-hand side in the Parsing Template (Stage 2). Clicking on the node reveals the rule path that node is connected to.
- In one parsing template, more than one field can be captured. Sibling operators inherit the same outputs from the parent as an input. In the minimap, this action is represented as branching out.
- Removing an operator block also removes all the connected operators below (Removing parent operator, also removes the child operators).
- After using Concatenate Values by Delimiter, Trim Value, Convert to Number, you cannot use Extract Values by Delimiters and Extract Values Between Delimiters operators in the same rule path (rule branch).

## Parsing Operators

### Extract Values by Delimiters

Extracts values between the delimiter, creates token(s) that can be selected and used for the next operator in the rule path (rule branch). 1 token is accepted as an input, 1 or many tokens are returned as an output (One to Many).



{% table %}
| Operator Fields | Description | 
| ---- | ---- | 
| Delimiter | The delimiter that the logline or string should be split on. | 
| Preserve Delimiters Between (Start & End) | Preserve any encountered delimiters between start and end keys.&#124; | 
{% /table %}

### Extract Values Between Delimiters

Extracts values between start and end delimiters, creates token(s) that can be selected and used for the next operator in the rule path (rule branch). 1 token is accepted as an input, 1 or many tokens are returned as an output (One to Many).



{% table %}
| Operator Fields | Description | 
| ---- | ---- | 
| Start Key | The delimiter that the logline or string should be split on. | 
| End Key | String delimiter for the end of an extraction. | 
{% /table %}

### Concatenate Values by Delimiter

Combines all of the selected values into a single token separated by a delimiter.
At least 2 or more tokens are accepted as an input, 1 token returned as an output (Many to One).



{% table %}
| Operator Fields | Description | 
| ---- | ---- | 
| Delimiter | The key to add between each token selected. | 
{% /table %}

### Trim Value

Trims the selected value by specifying start and end indices. Indices are numbered from 0 to n.
0 represents the first character, n represents the last character. 1 token is accepted as an input, 1 token returned as an output (One to One).



{% table %}
| Operator Fields | Description | 
| ---- | ---- | 
| Start | Start index for partial selection. | 
| End | End index for partial selection | 
{% /table %}

### Convert to Number

Converts a string value to a number. 1 token is accepted as an input, 1 token returned as an output (One to One).

### Capture in Field

Captures the value in a field. This operator ends the rule path (rule branch). The field name is required to successfully end the rule path. Field name has to be unique within the parsing template.
1 or more token is accepted as an input, 1 token returned as an output (One to One, or Many to One).
Operator fieldsDescriptionField nameThe field or key that the token(s) should be placed into.
**Example**
dogs_owned: pug and golden retriever



{% image url="https://uploads.developerhub.io/prod/2KW7/ygnke6smowcues0i0euznsuze037b3pvocqtp8p09ekt9kczzmk9osjtzxfbkevj.png" caption="" mode="responsive" height="200" width="598" %}
{% /image %}





