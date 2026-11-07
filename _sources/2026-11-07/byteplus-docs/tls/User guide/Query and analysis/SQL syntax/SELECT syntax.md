---
title: "SELECT syntax"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/SELECT-syntax-2"
---

The SELECT syntax selects one or more columns specified by the Key parameter from a table. By default, the statement returns data that meets the query condition from the current topic.

<span id="99203ddc"></span>
## Syntax format

The SELECT syntax format is as follows:

```SQL
* | SELECT [Key]
```



|Parameter |Description |
|---|---|
|Key |The Key parameter specifies the log fields, expressions, SQL functions, asterisks ( *) and so on. When set to an asterisk (* ), such as `*\| SELECT *`, it indicates that all fields of the log will be returned. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The SELECT analysis statement does not require a <code>FROM</code> clause. By default, log data in the specified topic is analyzed.</div>


<span id="7ecf1b93"></span>
## Examples


|Sample SQL statement |Description |
|---|---|
|<PreCode lang="SQL" text={`* \| SELECT status, request_method`}\> |Selects the values of the status and request_method columns in all log data. |
|<PreCode lang="SQL" text={`* \| SELECT *`}\> |Selects all columns in all log data. |
|<PreCode lang="SQL" text={`* \| SELECT bytes_sent / request_time AS rate`}\> |Queries the outbound traffic per second in all log data. |
