---
title: "Query logs via phrase query (Index edition)"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Phrase_search_Index_edition"
---

This topic describes the basic features, syntax, usage limitations, and examples of phrase query (index edition).

<span id="e17c8355"></span>
## Query types

TLS supports non\-phrase query, phrase query, and phrase query (index edition). Among them, phrase query is used to precisely match specified phrases. Phrase query (index edition) returns exact results and outperforms regular phrase query in performance. The details are as follows:


|Query types |Keyword query (non\-phrase query) |Phrase query |Phrase query (index edition) |
|---|---|---|---|
|Description |Keyword matching is performed using delimiter, which means the phrase is split into individual keywords based on the index delimiter for querying. |Use the `#"specified phrase"` format to precisely match logs containing the specified phrase. For information about restrictions and principles, see [Query logs via phrase query](https://docs.byteplus.com/docs/tls/Phrase-search-2). |Use the `"specified phrase"` format to precisely match logs containing the specified phrase.<br><br><br>* Wildcard usage is not supported.<br><br>* To query **historical data** before enabling phrase query (index edition), you need **rebuild the index** to take effect. See [Rebuild index](https://docs.byteplus.com/docs/tls/Rebuild-indexes-2) for details. |
|Example |* Enable full\-text index<br><br>* Index separator contains a space<br><br>* Query statement `"connection after"` |* Enable full\-text index<br><br>* Index separator contains a space<br><br>* Query statement `#"connection after"` |* Enable full\-text index<br><br>* Index separator contains a space<br><br>* Enable phrase query (index edition)<br><br>* Query statement`"connection after"` |
|Result |Query logs that contain both the keywords `connection`, `after` and `connection after`. |Only query logs that contain the complete phrase `connection after`. |Only query logs that contain the complete phrase `connection after`. |


<span id="80accf51"></span>
## **Basic syntax**

In TLS, when using double quotes (`" "`), there are distinctions depending on whether the phrase query (index edition) feature is enabled:


* Enabled: The string inside the double quotes is not split and is treated as a complete phrase for phrase query.

* Disenabled:

   * Strings inside double quotes are split by preset delimiters, and the resulting keywords are linked with an AND relationship. For details, see [Query syntax](https://docs.byteplus.com/docs/tls/Log-query-syntax-2).

   * When using `#""`, the string inside double quotes is identified as a complete phrase and will be queried as a phrase without splitting.


For example, when the separator is a space, the syntax is explained as follows:


|Query methods |Full\-text query |Key\-value query |
|---|---|---|
|Syntax for keyword query (not phrase query) |`"abc def"` is equivalent to `abc AND def`. |`key: 'abc def'` is equivalent to `key: abc AND key: def`. |
|Phrase query syntax |`#"abc def"` |`key:#"abc def"` |
|Phrase query (index edition) syntax |`"abc def"` |`key:"abc def"` |


<span id="d8d23093"></span>
## Basic principles

After enabling phrase query (index edition), TLS will record the locations of the term split in the original log when building the inverted index, and construct a sparse index for these locations to accelerate location scanning.

During queries, the inverted index and location index are combined to determine whether the query phrase meets the phrase condition. Query results meeting phrase conditions are quickly returned based on the index information scan.

<span id="db6c1d42"></span>
## Billing notes

Phrase query (index edition) is currently in invite\-only testing and is free of charge. We will release billing notes in the upcoming announcements.

<span id="bf4fdb02"></span>
## **Query example**

For logs with full\-text index enabled and a delimiter that includes spaces, consider the query for logs containing `connection after` as an example.


|Query statement examples |Results when phrase query enhancement is **disabled** |Results when phrase query enhancement is **enabled** |
|---|---|---|
|`connection after` |Match logs containing the following keywords (keyword match):<br><br><br>* Both `connection` and `after` are present<br><br>* Only `connection after` is present<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c72e0d6e48c42c7a69d1961f0279994~tplv-goo7wpa0wc-image.image) </span><br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Enabling the enhanced phrase query feature does not affect the query results for this statement.</div><br> ||
|`#"connection after"` |Match logs that contain only the keyword `connection after` (phrase query \- standard version).<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/75626a739b914b0eaf15bef1714ddc04~tplv-goo7wpa0wc-image.image) </span> ||
|`"connection after"` |Match logs containing the following keywords (keyword match):<br><br><br>* Both `connection` and `after` are present<br><br>* Only `connection after` is present<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4455694468084d8ca64e0bbebcf08c79~tplv-goo7wpa0wc-image.image) </span> |Match logs containing only the keyword `connection after` (phrase query \- index edition).<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f82f72d5e4d54f67abd4a75d4c3f84ae~tplv-goo7wpa0wc-image.image) </span> |


Query result analysis:


* A: Matches logs containing both keywords `connection` and `after`, or matches data containing only `connection after`.

* B: Matches data that contains only the keyword `connection after`.



|Query statements |Results when phrase query enhancement is **disabled** |Results when phrase query enhancement is **enabled** |
|---|---|---|
|`connection after` |A |A |
|`#"connection after"` |B |B |
|`"connection after"` |A |B |
