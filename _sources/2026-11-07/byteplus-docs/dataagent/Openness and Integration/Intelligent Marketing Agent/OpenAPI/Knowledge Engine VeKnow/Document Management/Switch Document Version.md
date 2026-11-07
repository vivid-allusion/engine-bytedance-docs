---
title: "Switch Document Version"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/switch-document-version"
---

Call this interface to switch the effective version in real time, and disable the old version after switching.

# Interface description

* Interface name: switch_document_version_document_version_switch_post

* Interface address:/document/version/switch

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|doc_id |Number |Yes |Document ID |
|id |Number |Yes |Target version record ID, get version list items.id |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Boolean |No |data |
