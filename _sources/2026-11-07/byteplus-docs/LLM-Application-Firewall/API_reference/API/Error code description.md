---
title: "Error code description"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Error_code_description"
---

You can refer to the following table to learn about the error codes returned when an LLM Application Firewall API call fails.


|HTTP response codes |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter<br><br> |The specified parameter Action is invalid. |Action is invalid. Please check and ensure that Action matches the interface name. |
|400 |InvalidParameter |The specified parameter Version is invalid.<br><br> |Version is invalid. Please check and ensure that Version matches the interface version. |
|400 |InvalidParameter |The specified parameter BodyNoAppID is invalid. |AppID is invalid. Please go to the console to verify the asset's AppID. |
|400 |InvalidParameter |The specified parameter NotMatchAccessmode is invalid.<br><br> |The asset type being accessed is invalid. Please verify that the entered AppID corresponds to an asset configured for SDK access. |
|400 |AuthCheckFailed<br><br> |Auth Check Failed %s. |Authentication failed. Please check whether the AK and SK are correct. Recommended actions:<br><br><br>* Use the sample SDK directly to call the interface.<br><br>* To generate a signature yourself, refer to [API authentication](https://docs.byteplus.com/docs/LLM-Application-Firewall/API_authentication)。 |
|400 |Resource.NotExist<br><br> |The specified resource does not exist. Please check NoFoundApp and try again. |The asset for the specified AppID is not associated with a protection instance. This might be because the asset was deleted or was never added. Please go to the console to confirm the asset's AppID. |
|400 |Resource.NotExist<br><br> |The specified resource does not exist. Please check UserNotFound and try again. |The LLM Application Firewall instance has expired. Please go to the console to confirm the validity period of the instance. |
