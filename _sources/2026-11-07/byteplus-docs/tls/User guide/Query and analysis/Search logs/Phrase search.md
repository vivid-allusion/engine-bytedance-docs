---
title: "Phrase search"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Phrase-search-2"
---

Torch Log Service (TLS) offers the phrase search feature to exactly match a specified phrase. This topic describes the syntax and limits of the phrase search feature, and offers examples on how to use the feature.

<span id="8003376a"></span>
## Query type

TLS supports both phrase search and Non\-phrase search, as detailed in the following table:


|Query type |Description |
|---|---|
|Non\-phrase search |Keyword matching is performed using tokenization, which means that phrases are split into individual keywords based on the index delimiters and then searched.<br><br>For example, if a full\-text index is enabled and the index delimiters contain a space, then when executing the search statement `"error warning"` , TLS will search according to the `error AND warn`statement. Any log that contains both keywords `error`and `warn`, the log will be retrieved. |
|Phrase search |Exact match for logs containing the specified phrase.<br><br>For example, if the full\-text index is enabled and the index delimiters contain a space, then when executing the phrase query statement `#"error warning"`, the log will only be retrieved if the log contains the complete phrase `error warning`. |


<span id="55afd97d"></span>
## **Basic grammar**

Phrase search uses a hash symbol (#) as an identifier. The detailed explanation is shown in the table below:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Here, we use a space as the delimiter.</div>



|Query method |Phrase search grammar |Non\-phrase search grammar |
|---|---|---|
|Key\-Value search |`key:#"abc def"` |`Key: "abc def"`, equivalent to `key: abc AND key: def`. |
|Full\-text search |`#"abc def"` |`"Abc def"`, equivalent to `abc AND def`. |


<span id="51705395"></span>
## Basic principle

The following content describes how the phrase search feature works:


1. When the TLS backend receives a phrase search request, TLS first executes the corresponding non\-phrase search statement to query logs. For example, if the phrase search statement is `#"abc def"`, TLS first executes the `abc AND def` statement to match the keywords.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To avoid data overload, TLS backend allows up to 10,000 logs to be returned in Step 1.   </div>
   

2. TLS backend selects the logs that match the target phrase from the aforementioned search results and returns the final search results.


<span id="b4f4499f"></span>
## Precautions


* The phrase query selects up to 10,000 logs for phrase matching.

* After a phrase search is performed, the log distribution histogram displays the results of the non\-phrase search.

* For phrase search results, only consecutive page navigation forward or backward is supported; random jumping to a specific page is not supported.

* A fuzzy search cannot be used with a phrase search.

* In a phrase search statement, enclose the phrase with double quotation marks ( " " ).

* The NOT operator cannot be used with a phrase search statement. For example, `not #"abc def"` is invalid.

* A SQL statement cannot be used with a phrase search statement. For example, `#"abc def" | select ***` is invalid. Therefore, the quick analysis feature is not supported in phrase searches.


<span id="9c0079b1"></span>
## Page turns

When you perform a page turn operation, TLS performs a phrase search to ensure the continuity of the search results.

Each time a phrase search is performed, up to 10,000 logs are retrieved for phrase matching. It's possible that the number of logs displayed on a page is less than the specified number of logs per page, but you can still navigate to the next page. This indicates that there are more than 10,000 logs that meet the non\-phrase search statement, but of the 10,000 logs in the current phrase query, the number of logs that meet the phrase query condition is less than the number of logs specified to be displayed.

For example, the total number of logs is 40,000, and it is specified to display 100 logs per page. When you perform a phrase search and the current page shows only 40 logs but you can still page back, it means that only 40 of the current 10,000 logs meet the phrase search condition. When you continue to perform a page turn operation, TLS automatically performs a second phrase search on the following 10,000 logs and returns eligible logs.

<span id="f9c89198"></span>
## **Examples**

Assume that you query logs that contain `success Request`. The query results of non\-phrase search and phrase search statements are as follows:


* If you use a non\-phrase search statement `"success Request"`, TLS searches for logs that contain the keywords `success` and `Request`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/251a642351ea4f229f476642eaf0c3ae~tplv-goo7wpa0wc-image.image) </span>

* If you use a phrase search statement `#"success Request"`, TLS searches for logs that contain the complete phrase `success Request`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/03f2dce969fc4604be4dc035edcf3710~tplv-goo7wpa0wc-image.image) </span>
