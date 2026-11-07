---
title: "Enable Version Management"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/enable-version-management"
---

Call this interface to create a version group for the specified document and enable version management.

# Interface description

* Interface name: create_version_group_sophon_version_group_create_post

* Interface address:/sophon/version_group/create

* Request method: POST

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|docId |Number |No |Document ID |
|versionType |String |Yes |version type |
|knowledgeVersionTime |Number |No |Initial document versiontimestamp, milliseconds |
|knowledgeVersion |String |No |Version number, automatically generated if not filled in |

# **Response parameters**

Response Result Object Type
