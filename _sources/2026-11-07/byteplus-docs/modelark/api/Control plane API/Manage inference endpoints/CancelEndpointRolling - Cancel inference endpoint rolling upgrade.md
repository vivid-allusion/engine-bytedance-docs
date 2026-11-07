---
title: "CancelEndpointRolling - Cancel inference endpoint rolling upgrade"
product: "ModelArk"
product_code: "modelark"
source: "https://docs.byteplus.com/en/docs/modelark/cancel-endpoint-rolling-api"
---

`POST https://ark.ap-southeast-1.byteplusapi.com/?Action=CancelEndpointRolling&Version=2024-01-01`

Cancels the specified in\-progress rolling update task. The endpoint retains the model versions corresponding to the current canary traffic split.

## Authentication

This API supports the following authentication method(s). For details, see [Base URL and authentication](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/base-url-and-authentication).

* Access Key authentication. Go to the [Access Key management](https://console.byteplus.com/iam/keymanage) page. Obtain an Access Key. This API supports only Access Key authentication.

---

## Request parameters

### Body parameters

**Id** `string` `Required`  |  Rolling update task ID

ID of the rolling update task to cancel

**Message** `string`  |  Cancellation reason

Reason for canceling the task

## Response parameters

**Id** `string`  |  Rolling update task ID

ID of the canceled rolling update task
