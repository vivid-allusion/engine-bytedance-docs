---
title: "How to query for phrases accurately?"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/How-to-query-for-phrases-accurately"
---

During the log query process, when you need to match phrases accurately, you can use phrase query or LIKE syntax.

<span id="ed138528"></span>
## Background information

Torch Log Service(TLS) uses word segmentation when querying data, and the results of the exact query are not completely accurate. For example, when executing the `successful request` statement, TLS will query according to the `successful and request` statement, and the logs containing `successful` and `request` will be matched, rather than only those that exactly match the phrase `successful request`. If you need to match the exact phrase `successful request`, you can use a phrase query or LIKE syntax.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/979cb885085a475595e5262a94386277~tplv-goo7wpa0wc-image.image) </span>

<span id="132e9262"></span>
## Search example


<Tabs>
<Tab zoneid="jmEjqP1M74" title="Phrase query">
<TabTitle>Phrase query</TabTitle>

The target phrase can be accurately matched through phrase query.

Example: Query the logs that contain the phrase `successful request`.

```SQL
#"successful request"
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/943bab0bb12542d492d56cde969c8a16~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="WxzCw32htl" title="Based on SQL LIKE syntax">
<TabTitle>Based on SQL LIKE syntax</TabTitle>

The SQL LIKE syntax is used to specify query conditions in the WHERE clause, enabling precise querying of logs. In LIKE syntax, the percent sign (%) represents matching any number of characters, including 0; the underscore (_) represents matching a single character.

Example: To query logs where the value of the `tag` field contains`successful requests`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When using LIKE syntax, the target field (such as <code>tag</code>) must have key\-value index enabled and statistics enabled. For more information, please refer to <a href="https://docs.byteplus.com/docs/tls/getting_started_configure_indexes#e3e54d2b">Configure key\-value indexes</a>.</div>


```SQL
* | SELECT * WHERE tag LIKE '%successful request%'
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb7a05f518b740d6b8b09285ce9cdba8~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>
