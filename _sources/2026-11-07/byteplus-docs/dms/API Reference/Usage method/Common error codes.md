---
title: "Common error codes"
product: "Data Migration Service"
product_code: "dms"
source: "https://docs.byteplus.com/en/docs/dms/Common_error_codes"
---

This article describes public error codes for DMS API calls. For platform error codes, see [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|**Error Code** |**HTTP status code** |**Error message** |**Description** |
|---|---|---|---|
|InvalidParameter |400 |Invalid Parameter. |Parameter exception. |
|InvalidTaskName |400 |Task name must contain 3\-32 letters, numbers, and dash (\-), and cannot start or end with dash (\-). |Invalid task name. |
|TaskNotFound |404 |TaskNotFound. |The task does not exist. |
|CreateDataMigrateTaskTimeout |408 |Wait creating task timeout. |Task creation timed out. |
|TaskNameExists |409 |Task name already exists, please select another task name. |The task name already exists. Choose another task name. |
|CommonInner |500 |This feature is currently unavailable. |This feature is currently unavailable. |
|InnerDBAccessErr |500 |Access DB failed. |Internal error. |
