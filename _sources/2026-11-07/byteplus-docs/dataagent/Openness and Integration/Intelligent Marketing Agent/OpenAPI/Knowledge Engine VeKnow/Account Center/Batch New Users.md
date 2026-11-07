---
title: "Batch New Users"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/batch-new-users"
---

Call this interface to create new user accounts in batches, and support email, mobile phone number, status and custom attributes.

# Interface description

* Interface name: portal_batch_create_users

* Interface address:/minibase/portal/openapi/v1/users

* Request method: POST

# **Request parameters**

The request body data type is Array < Object \>, which supports batch creation of user request items.

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|account |String |Yes |account number |
|username |String |Yes |name |
|password |String |Yes |password |
|email |String |No |email |
|mobile_number |String |No |Mobile phone number |
|status |Number |No |Status: 1 enabled, 0 disabled |
|custom_property |Object |No |User\-defined properties, support String type or Array < String \> type |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |No |business status code |
|message |String |No |business message |
|data |Array |No |Create a list of successful users, see the **data** table below |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|id |Number |No |user ID |
|last_login |String |No |Last login time |
|is_superuser |Boolean |No |Is it a super administrator? |
|status |Number |No |state |
|account |String |No |account number |
|username |String |No |name |
|email |String |No |email |
|mobile_number |String |No |Mobile phone number |
|avatar_url |String |No |avatar address |
|current_org_id |Number |No |Current organization ID |
|created_at |String |No |creation time |
|updated_at |String |No |update time |
|custom_property |Object |No |user\-defined properties |
