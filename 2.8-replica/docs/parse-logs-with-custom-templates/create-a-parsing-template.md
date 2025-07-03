---
type: page
title: Create a Parsing Template
listed: true
slug: create-a-parsing-template
description: 
index_title: Create a Parsing Template
hidden: 
keywords: 
tags: 
---


{% callout type="info" title="Permission Level" %}
Must be an [admin or owner](https://docs.mezmo.com/docs/role-based-access-control) to use this feature.
{% /callout %}

You'll learn how to parse ingested log lines. This will cover the parsing screen, the parsing mini map, and using some of the parsing functions available. You can parse all four values or parse one and move onto Validate Templates.

You'll use the following log lines throughout and you'll parse:

- `ip_address: 111.00.11.10`
- `timestamp: 14/Nov/2018:10:35:00 +0000`
- `response: 200`
- `upstream_length_time: 49/0.008`

{% code %}
{% tab language="bash" %}
111.00.11.10 - [111.00.111.10] - - [14/Nov/2018:10:35:00 +0000] "GET /logdna_test/v1/health
HTTP/1.1" 200 44 "-" "Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Trident/5.0; AppInsights)"
586 0.004 [logdna_test-service-80] 111.00.11.10:80 49 0.008 200 230abc56545logdna1238e
{% /tab %}
{% /code %}

## Parse a String

You are going to parse `111.00.11.10` from the log line.

1. Go to [Parsing Templates](https://app.mezmo.com/manage/custom-parsing/templates) and click **Create a Template**.
2. In Choose a Log Line, select **Add my own log line**. You'll be using the log line from the introduction.
3. Click **Build a Parsing Template**. You will see the line you entered as a Reference Line.
4. First, you are going to break the text down into smaller parts to so you can use the part you want. In Choose an Extractor, select **Extract Value By Delimiter**.
5. Enter a space and then a dash.
6. Now you should see `111.00.11.10` and `*[111.00.111.10]` as part of the lines parsed.
7. Select `111.00.11.10` and choose the operator,**Capture in Field.** Give a label `ip_address`.
8. The result is shown at the bottom of the parsing page.

{% image url="https://uploads.developerhub.io/prod/2KW7/bmfkew43n85qtihpi9yml50ibp9qmfj19zwn5h5c1dhc02v0824ta604gjisl0pk.png" caption="Results of parsing the string 111.00.11.10 as the IP Address" mode="300" height="1456" width="1408" %}
{% /image %}

## Parse a Timestamp

You'll parse `14/Nov/2018:10:35:00 +0000` from the log line.

1. Select the circle with the plus sign to create a **Sibling Operator.** When you create a sibling operator, the mini map updates to show the relationship between operators and the template screen updates to have a new Choose an Operator. Learn more in [auto$](/docs/edit-parsing-operations-with-the-mini-map).
2. Check the longer output that includes the timestamp.
3. Choose an operator &gt; **Extract by Delimiter.**
4. Enter a space into the delimiter.
5. Notice the output has split everything by space, including part of timestamp. To fix the timestamp, you need to preserve some of the spaces.
6. Click **Preserve delimiters between.**
7. Start use a left square bracket `[` and end use a right square bracket, `]` .
8. Click **Preserve delimiters between** again**.** Use double quotes `"` for both start and end. You'll notice that the timestamp is now cleaned up, along with some of other output.
9. Now we need to remove the brackets from the timestamp, so it's easier to run diagnosis against. Select the timestamp. `[14/Nov/2018:10:35:00 +0000]` , choose operator, T**rim Value**.
10. Trim Value is 0 based counting. Start, enter `1` , for end enter  `-1`.
11. Your output should be the timestamp.
12. Choose operator &gt; **Capture in Field** and label it `timestamp` .
13. So far, you've captured two fields from the log line.

{% image url="https://uploads.developerhub.io/prod/2KW7/fj0o853ql3kunb7nmsosmvosweqrrw2a4gtvgdcdnxl8i7luz5tfnu4v2dnqe1am.png" caption="Results of parsing the timestamp" mode="300" height="3081" width="1394" %}
{% /image %}

## Parse a Number

You are going to parse `200` from the log line.

1. Using the mini map, select Trim Value. Trim Value is orange, you can also hover over the icons in the mini map. Using the mini map lets you jump between parsed areas. By starting from Trim Value, you can start from a place where the 200 is already separated from the other values, making it easier to use.
2. Click **Add a Sibling Operator**.
3. Select 200.
4. Choose an operator &gt; **Convert to Number.**
5. Choose an operator &gt; **Capture in Field**. Field name is `response.`

{% image url="https://uploads.developerhub.io/prod/2KW7/6l3zqc7w0hjmhz1ido6fbiv3bg7fwvlrpfko2jd3q42w1j9cubv9lxn29jbc3goj.png" caption="Results of parsing the 200 response" mode="300" height="3068" width="1422" %}
{% /image %}

## Concatenate Log Lines

You are going to parse `49` and `0.008` from the log line.

1. Create a sibling operator to either Trim Value or Convert to Number in the mini map.
2. Select `49` and `0.08` from the output.
3. Choose an operator &gt; **Concatenate Values by Delimiter**.
4. Enter a forward slash `\` as the value.
5. Choose an operator &gt; **Capture in Field**.
6. The field name is `upstream_length_time.`

{% image url="https://uploads.developerhub.io/prod/2KW7/az1xeaxsxqdqbw57w8gapn08kk9qcuiqekof0wy4ekyrg9j4kuzkqf4khfvhj724.png" caption="Results of concatenating 49 and 0.008" mode="300" height="1410" width="1416" %}
{% /image %}

## Validate Template

Before you can make a template active, you must check that the log lines you want are working.

1. Add a log line to test against in **Add a Line**. You can use the example line. When testing you want to be sure to test multiple lines by adding lines.
2. You can also test by adding a query to `Apply this parsing template to sample lines matching this query:`. This step is required and is the scope of the parsing template.
3. Mark the log lines as valid or invalid.
    1. If a line is marked as invalid you'll be taken back to the Parsing Template step.

4. Activate changes to apply your changes.

{% callout type="info" title="Active Parsing Templates" %}
Active parsing templates are only applied to the lines that come in after the template has been enabled. All log lines that were ingested prior to the template becoming active are not parsed by the parsing template.
{% /callout %}

## Results

The log lines the template applies to will show in the Log Viewer.

{% image url="https://uploads.developerhub.io/prod/2KW7/3goy2g40133nqghnvjufeylw910ee0jk2x6uq4a8ic4zfozakjm69nyh105vhyiu.png" mode="responsive" height="651" width="2618" %}
{% /image %}