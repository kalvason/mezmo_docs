---
type: page
title: Power User Guide to Mezmo Search
listed: true
slug: experts-guide-to-mezmo-search
description: 
index_title: Power User Guide to Mezmo Search
hidden: 
keywords: 
tags: 
---




Searching in Mezmo is designed to be as easy and straightforward as possible. Just type in your search terms, and Mezmo will return your results almost instantaneously. For cases where you need to perform a more advanced search, or where you need greater control over your search results, Mezmo provides a number of features that can help you find exactly what you’re looking for.

In this article, we’ll walk through some of the expert-level features of Mezmo’s search engine and how you can use them to perform in-depth searches. We’ll start by explaining the basics of how Mezmo interprets searches, then we’ll present frequently asked questions about how searching works.



## Search Query Syntax

When you enter a query into the search input box, Mezmo parses it into a series of terms and operators.

A term is a string consisting of a single word, or a phrase surrounded by quotes. Mezmo scans each log to see if it contains your term(s), and if so, displays the log. Terms are searched against the entire log, but can be searched on a particular field if one is specified. By default, terms are also case insensitive and treated as prefixes. For example, search `lin` will return logs containing `lin`, `line`, and `Linux`.

Operators change how Mezmo interprets one or more search terms. Using operators gives you greater control over the search process in order to provide more relevant results. You can find a full list of operators with examples in the [Mezmo search documentation page](/docs/search#quick-reference-of-field-search-operators).

Mezmo also supports the boolean operators `AND`, `OR`, and `NOT`. Any whitespace between search terms is automatically interpreted as `AND`. For example, searching `warning error` returns logs containing both `warning` and `error`. The only exception is when using lists, which treat whitespace as a part of the search term. For example, searching `message:[file, exists]` will only search for instances of `exists` that are preceded by a space.

Lastly, you can use parentheses to group operations that should be evaluated first. For example, the query `source:node1 AND (file:/var/log/syslog OR ERROR)` searches first for logs scanned from `/var/log/syslog` or that contain the word `ERROR`, then limits the results to `node1`. You can also use parentheses to group operations on a single field. For example, the query `status:(>100 AND <= 503)` returns logs where the value stored in the `status` field is greater than 100 and less than 503.



## Common Pitfalls and How to Overcome Them

You may find that one of your queries doesn’t return the results you expected, or displays a warning or error message. Here are some common pitfalls you may run into, and how to resolve them.



### No Search Results Found, or Limited Results Returned

The most common problem with developing queries is not getting the results you expect. This is commonly due to search queries that are too vague, or queries that return a significant number of matches. Mezmo searches work best when they are specific. For example, searching for `the` or another common word would result in an excessive number of results, and not all of them will be displayed. For this reason, Mezmo doesn’t support single-character searches.

To avoid this problem, try using the exact match operator (`:==`) instead of the prefix match operator (`:`). You should also search on a specific field, instead of the entire log. Lastly, if you know exactly how your search term appears in your logs, enable case sensitivity by using the `:===` operator.



### Unexpected Results

After running a search, you may see results that don’t appear to match your query. Mezmo doesn’t just search visible fields, but also internal fields. These fields aren’t visible in the Mezmo web UI, but contain additional information such as metadata and the raw log message. Your query could match on these “invisible” fields, resulting in the log appearing in the results.

You can override this by specifying the field to search. For example, if your logs contain a `level` field and you want to find error-level logs, enter `level:error` as your query instead of just `error`.



### Spaces Affect Results

If your query contains whitespace and doesn’t contain quotes, Mezmo treats the whitespace as an `AND` operator. For example, the query `file does not exist` will return any log containing all four words, regardless of their order. It could match `file "myfile.txt" does not exist`, but it could also match `Could not open file: does it exist?` To search for the exact phrase, surround it in double quotes.

The only exception is when searching in lists. With lists, whitespace is treated as part of the list item that it’s next to. For example, `message:[file, exists]` searches for logs where `exists` is preceded by a space. To avoid this, remove any whitespace between list items.



### UI Feedback, Errors, and Warnings

Mezmo provides visual feedback based on whether your query is properly formatted. A properly formatted field search will appear highlighted, as shown in this screenshot:




{% image url="https://uploads.developerhub.io/prod/2KW7/tqvii02mcg5bgf4y66ckyu72kronebm82uxzdmto6erred9sebr1efc4tjit7zeb.png" caption="" mode="responsive" height="48" width="613" %}
{% /image %}




Well-formatted non-field searches won’t appear highlighted, but will still run without problems. However, if your query is improperly formatted or contains errors, the help icon on the right-hand side of the search box will turn into an alert explaining the problem in detail. In this screenshot, we’re trying to use a comparison operator on a string field, which is invalid:




{% image url="https://uploads.developerhub.io/prod/2KW7/tqvii02mcg5bgf4y66ckyu72kronebm82uxzdmto6erred9sebr1efc4tjit7zeb.png" caption="" mode="responsive" height="48" width="613" %}
{% /image %}







{% image url="https://uploads.developerhub.io/prod/2KW7/prlfvpz3jlgw60c307dnqbpbj5revio290b959p4oaor5utachwhpc9exmvza32z.png" caption="" mode="responsive" height="195" width="809" %}
{% /image %}




A common issue is using symbols in your query, such as inequality signs. This displays the warning “Unsupported visualization query: symbols.” This warning is only relevant when using graphs or the timeline feature, but it doesn’t affect normal queries. The following example will still return results containing `<hello`:





{% image url="https://uploads.developerhub.io/prod/2KW7/tqvii02mcg5bgf4y66ckyu72kronebm82uxzdmto6erred9sebr1efc4tjit7zeb.png" caption="" mode="responsive" height="48" width="613" %}
{% /image %}







{% image url="https://uploads.developerhub.io/prod/2KW7/prlfvpz3jlgw60c307dnqbpbj5revio290b959p4oaor5utachwhpc9exmvza32z.png" caption="" mode="responsive" height="195" width="809" %}
{% /image %}







{% image url="https://uploads.developerhub.io/prod/2KW7/i9e61dwhk3qtl2jm4pmt71d9hi0qiqh0syvmbqixpm5g4i50r2as0g8tfui4s4jw.png" caption="" mode="responsive" height="173" width="814" %}
{% /image %}




If the warning persists, or if you’re not getting the expected results, you can escape the problematic characters by adding a backslash “\” before them. For example, the following query searches for a specific phrase containing quotes:






{% code %}
{% tab language="none" %}
message:"Host "logdna-host" not found"
{% /tab %}
{% /code %}







This search is valid, but won’t return the expected results. Instead, you would use:






{% code %}
{% tab language="none" %}
message:"Host \"logdna-host\" not found"
{% /tab %}
{% /code %}







You can learn more in the [Mezmo search documentation](/docs/search#special-characters).


## Conclusion

Mezmo’s search engine allows for a great deal of flexibility and control. It’s important to be aware of how Mezmo interprets each part of your query, especially for complex searches. Fortunately Mezmo offers some of the fastest search results in the industry, so if at first you don’t succeed, you can try again right away!

For a more in-depth look at searches, check out the [Mezmo documentation page on searching](/docs/search). And if you still need help crafting the perfect query, [contact us](https://mezmo.com/contact-us/).





