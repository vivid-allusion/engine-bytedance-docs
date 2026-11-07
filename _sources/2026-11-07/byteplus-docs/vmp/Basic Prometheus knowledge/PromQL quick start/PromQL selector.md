---
title: "PromQL selector"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/PromQL-selectors"
---

You can filter data by label in PromQL. This topic describes how to use labels.

<span id=".5qCH562-6YCJ5oup5Zmo"></span>
## Label selector

The raw data in Prometheus contains multiple labels. In most cases, you only need to view the content of specified labels. In this case, you need to use a label selector. A label selector is placed in  **{}** . The following sample code shows how to query the number of requests with an HTTP status code 400.

```Plain Text
http_requests_total{code="400"}
```
In the label selector, you can use label matching operators to select labels, including


* `=`: matches the string.

* `!=`: does not match the string.

* `=~`: regex\-matches the string.

* `!~`:  does not regex\-match the string.


<span id=".6IyD5Zu06YCJ5oup5Zmo"></span>
## Range selector

The range selector is often used to specify a period of time. The following sample code shows how to query sampling records with an HTTP status code 400 in the last 5 minutes.

```Plain Text
http_requests_total{code="400"}[5m]
```
In the range selector, you can specify different periods of time.


|**Time Unit** |**Descriptions** |
|---|---|
|s |Second |
|m |Minute |
|h |Hour |
|d |Day |
|w |Week |
|y |Year |
