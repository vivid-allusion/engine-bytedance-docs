---
title: "Regular expression matching examples"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Regular_expression_matching_examples"
---

Some features of CR (for example, registry replication rules, tag retention rules, and more) support matching the namespace, repository name, or image tag using regular expressions. This article provides commonly used regular expression examples for your reference.


|Matching method |Matching target |Regular expression |<div style="text-align: center"><br>Matching target name</div><br> |||||
|---|---|---|---|---|---|---|---|
||||<div style="text-align: center"><br>v1</div><br> |<div style="text-align: center"><br>version\-1</div><br> |<div style="text-align: center"><br>test\-1</div><br> |<div style="text-align: center"><br>v2</div><br> |<div style="text-align: center"><br>v3</div><br> |
|Exact match |Only match the` v1 `tag. |v1 |<div style="text-align: center"><br>√</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |
|Prefix matching |Match all tags starting with `v`. |^v.\*$ |<div style="text-align: center"><br>√</div><br> |<div style="text-align: center"><br>√</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>√</div><br> |<div style="text-align: center"><br>√</div><br> |
|Multi\-prefix match |Match all tags starting with `v` or `t`. |^(v\|t).\*$ |<div style="text-align: center"><br>√</div><br> |<div style="text-align: center"><br>√</div><br> |<div style="text-align: center"><br>√</div><br> |<div style="text-align: center"><br>√</div><br> |<div style="text-align: center"><br>√</div><br> |
|Suffix match |Match all tags ending with `-1`. |^.\*\-1$ |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>√</div><br> |<div style="text-align: center"><br>√</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |
|Multi\-suffix match |Match all tags ending with `1 `or `2`. |^.\*(1\|2)$ |<div style="text-align: center"><br>√</div><br> |<div style="text-align: center"><br>√</div><br> |<div style="text-align: center"><br>√</div><br> |<div style="text-align: center"><br>√</div><br> |<div style="text-align: center"><br>\-</div><br> |
|Tag match |Match tags starting with `v` and ending with Arabic numerals. |^v([0\-9.]+)$ |<div style="text-align: center"><br>√</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>√</div><br> |<div style="text-align: center"><br>√</div><br> |


&nbsp;
