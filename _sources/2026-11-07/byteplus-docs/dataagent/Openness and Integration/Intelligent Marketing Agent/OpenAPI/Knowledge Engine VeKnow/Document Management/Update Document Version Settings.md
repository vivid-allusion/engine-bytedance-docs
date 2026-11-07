---
title: "Update Document Version Settings"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/update-document-version-settings"
---

Call this interface to update the version writing policy and version number rules uniformly; the rule change will recalculate the historical display version number.

# Interface description

* Interface name: update_version_settings_document_version_settings_put

* Interface address:/document/version/settings

* Request method: PUT

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|doc_id |Number |Yes |Document ID |
|version_policy |String |No |Version write policy, new version by default<br><br><br>* ADD_VERSION<br><br>* OVERWRITE_VERSION |
|version_rule_type |String |No |Version rules<br><br><br>* CUSTOM<br><br>* DAY<br><br>* WEEK<br><br>* MONTH<br><br>* QUARTER<br><br>* YEAR |
|version_rule_config |Object |No |Version number rule configuration; support prefix and timezone, default V and Asia/Shanghai |

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
