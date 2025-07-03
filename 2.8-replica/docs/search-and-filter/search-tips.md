---
type: page
title: Search Tips
listed: true
slug: search-tips
description: 
index_title: Search Tips
hidden: 
keywords: 
tags: 
---


Searches that return no results are usually caused by searches that are too vague.

For example, searching for `the` or another common word would result in an excessive number of results, and not all of them will be displayed. For this reason, Mezmo doesn’t support single-character searches.

To avoid this problem, try using the exact match operator such as equal (`:==`) instead of the prefix match operator (`:`). You should also search on a specific field, instead of the entire log. Lastly, if you know exactly how your search term appears in your logs, you can enable case sensitivity by using the `:===` operator.

### [Unexpected Results](https://docs.mezmo.com/docs/search-and-filter#unexpected-results)

Mezmo searches visible fields as well as internal fields, such as metadata and the raw log message. Your query can match on these "invisible" fields, resulting in the log appearing in the results.

You can override this by specifying the field to search. For example, if your logs contain a `level` field and you want to find error-level logs, enter `level:error` as your query instead of just `error`.

### [Search Query Warnings](https://docs.mezmo.com/docs/search-and-filter#search-query-warnings)

The warning `Unsupported visualizations query: symbols` is displayed whenever any symbols are used in a query, for example, `/` , `+`, etc. There is no issue with your query and search results. The warning shows up to let you know that the query was performed without the symbols to populate the Graphs or Timeline Graphs.

To search for symbols in they must be wrapped in quotes.

### [Camel Cased Words And Case Sensitivity](https://docs.mezmo.com/docs/search-and-filter#camel-cased-words-and-case-sensitivity)

When logs lines are stored and indexed, compound words with internal capitalization like `SyntaxError` get split up into separate words, `Syntax` and `Error`. This means that performing a search (defaults to case insensitive) for `syntaxerror` may not return lines containing that term because it was not stored that way. You will need to query for 'SyntaxError' to match the original form in this case.

### [Search Feedback](https://docs.mezmo.com/docs/search-and-filter#search-feedback)

When searching, the Mezmo app will provide feedback if a search is correct.

**Field Search Correct Syntax**

The search will highlight a yellow color.

{% image url="https://uploads.developerhub.io/prod/2KW7/u9ww8ox83fy9tivekhk1hqzktxhh0ziza71glx9ln0m52h69h8i29ij3ivgla3sx.png" caption="Correct field searches are highlighted yellow" mode="responsive" height="128" width="1740" %}
{% /image %}

**Field Search Incorrect Syntax**

The search will have a red underline and offer tips by clicking on the red triangle.

{% image url="https://uploads.developerhub.io/prod/2KW7/nmppoqv8m641z9bbh37fwof15dfilccpijd5qh94x00wn8vk0zjjwnbqdfphzucx.png" caption="Incorrect field searches have a red underline and red warning triangle" mode="responsive" height="406" width="1968" %}
{% /image %}

**Simple Search Feedback**

Simple text searches do not show if a search is correct or not.