---
title: "Workflow status codes"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/workflow-status-codes"
---

This article provides detailed explanations for status codes returned in the

[GetWorkflowExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-getworkflowexecution) interface.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><strong>1XXX</strong>: Non\-retryable status codes.</div>


* <div data-tips="true" data-tips-type="tip"><strong>2XXX</strong>: Retryable status codes.</div>




|**Status code** |**Description** |
|---|---|
|0 |Successfully executed the workflow.<br><br><br>* No exceptions occurred.<br><br>* If any exceptions occurred, they were caught and handled. |
| **[1000,1999]: User error.**  ||
|1001 |Source file corrupted, parsing failed. |
|1002 |Missing audio or video streams. |
|1003 |Source file download failed, possibly due to a URI transcoding error. |
|1004 |Too many transcoding outputs. |
|1005 |Missing subtitle stream. |
|1006 |Workflow parameter error. |
| **[2000,2999]: System error.**  ||
|2000 |Unknown system error. |
|2001 |Source file download failed, possibly due to a vid transcoding error. |
|2002 |Upload error. |
|2003 |Transcoding timeout. |
|2004 |Automatic video publishing failed. |
|2005 |User callback error. |
