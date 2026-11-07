---
title: "AS syntax"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/AS-syntax-2"
---

The AS syntax specifies an alias for a field.

<span id="a3a20d83"></span>
## Syntax format

The AS syntax format is as follows:

```SQL
* | SELECT Key AS  Alias
```


Key specifies the name of a log field, and Alias specifies the alias for the field.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the column alias specified by the AS syntax contains special characters (such as spaces, hyphens, etc.), you need to enclose it in double quotes (""). For example: <code>"r-w"</code>.</div>


<span id="5eb2701c"></span>
## Examples


|Sample SQL statement |Description |
|---|---|
|<PreCode lang="SQL" text={`* \| SELECT COUNT(*) AS PV`}\> |Count the page views of a website. |
|<PreCode lang="SQL" text={`* \| SELECT bytes_sent / request_time AS rate`}\> |Query the outbound traffic per second in all log data. It is calculated by dividing bytes_sent by request_time and expressed as a rate. |
