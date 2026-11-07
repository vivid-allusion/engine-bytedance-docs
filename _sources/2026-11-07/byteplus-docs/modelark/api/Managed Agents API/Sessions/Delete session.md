---
title: "Delete session"
product: "ModelArk"
product_code: "modelark"
source: "https://docs.byteplus.com/en/docs/modelark/delete-session-api"
---

`DELETE https://ark.ap-southeast.bytepluses.com/api/v3/sessions/{session_id}`

Permanently delete sessions that are no longer needed and free up their active session usage. After the deletion succeeds, the session can no longer be accessed through [Get session details](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/get-session-api) or [List sessions](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/list-sessions-api). Related runtime resources may continue to be reclaimed in the background. You do not need to poll the deletion status.

Before deleting a session, handle it based on the session status:

* **`status`** ** is ** **`idle`** ** or ** **`terminated`**: You can delete it directly.

* **`status`** ** is ** **`running`**: First send `user.interrupt`, wait until `status` returns to `idle`, and then delete it.

* **`status`** ** is any other value**: Wait for the current operation to complete, and then delete it after `status` returns to `idle`.

If you need to interrupt the current task but keep the session, send `user.interrupt` instead of deleting the session.

## Authentication

This API supports the following authentication method(s). For details, see [Base URL and authentication](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/base-url-and-authentication).

* API Key authentication. Go to the [API Key Management](https://ai.byteplus.com/ark/region:ap-southeast-1/apiKey) page. Obtain a long\-lived API key.

---

## Request parameters

### Path parameters

**session_id** `string` `Required`  |  Session ID

The ID of the session to be deleted. It is a string that starts with `sesn-`.

## Response parameters

**id** `string`  |  Session ID

ID of the deleted session.

**type** `string`  |  Object type

Object type. Fixed to `session_deleted`.
