---
title: "Query Document Version Settings"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/query-document-version-settings"
---

Call this interface query version write policy and version number rules.

# Interface description

* Interface name: get_version_settings_document_version_settings_get

* Interface address:/document/version/settings

* Request method: GET

# Request parameters

## Query

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|doc_id |Number |Yes |Document ID |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |Document version settings, see the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|doc_id |Number |Yes |Document ID |
|version_policy |String |Yes |version write policy |
|version_rule_type |String |Yes |Version rules |
|version_rule_config |Object |No |version number rule configuration |
|version_rule_revision |Number |Yes |Version number Rule revision number |
