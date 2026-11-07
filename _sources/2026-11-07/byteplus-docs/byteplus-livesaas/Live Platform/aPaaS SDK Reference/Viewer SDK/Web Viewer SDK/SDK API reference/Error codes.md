---
title: "Error codes"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/error-codes"
---

Type: `enum`


|Value |Property |Description |Solution |
|---|---|---|---|
|101 |INIT_FAIL |* Error message: Initialization failed for lack of required parameters.<br><br>* Callback parameter: Initialization configurations. |Make sure values are set for the `activityId`, `token`, `service`, `mode`, and `modules` parameters. |
|102 |TOKEN_FAIL |* Error message: Failed to validate the token.<br><br>* Callback parameter: API error message. |Make sure the value of `token` is valid. |
|103 |DIV_NOT_FOUND |* Error message: Failed to find the corresponding rendered parent node.<br><br>* Callback parameter: ID of the parent node. |Make sure each `id` under `modules` corresponds to one DOM node. |
|104 |RENDER_ERROR |* Error message: Failed to render modules.<br><br>* Callback parameter: Module name, error stack, and error message. |None. |
|105 |COMP_NOT_FOUND |* Error message: Failed to find the corresponding component.<br><br>* Callback parameter: ID of the parent node. |Make sure the value of `modules.mode` parameter is valid. |
|106 |MOBILE_ALL_ERROR |* Error message: `mobile` or `mobile-portrait` modules cannot be used with other modules.<br><br>* Callback parameter: None. |Make sure the `mobile` and `mobile-portrait` modules are not used with other modules. |
|201 |LIVE_INFO_FAILED |* Error message: Failed to get the live room information.<br><br>* Callback parameter: Request data. |None. |
|204 |LIVE_DUPLICATE_LOGIN |* Error message: Duplicate logins to the live room.<br><br>* Callback parameter: None. |None. |
|206 |IP_BANNED |* Error message: The current viewer's IP has been banned.<br><br>* Callback parameter: None. |None. |
|207 |KICK_OUT |* Error message: The current viewer has been kicked out.<br><br>* Callback parameter: None. |None. |
