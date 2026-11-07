---
title: "Error Code Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Error-code-overview"
---

When you encounter an error using TOS, TOS returns information such as Code, RequestId, HostId, Message, and EC code to help you quickly identify and resolve the error.

<span id="657b491a"></span>
## Error Response Example

```JSON
HTTP/1.1 400 Bad Request
server: TosServer
Date: Fri, 30 Jul 2021 13:55:03 GMT
x-tos-request-id: 580c15f00eca4e70d84e3c4e036d0b64-ac12****
x-tos-id-2: 580c15f00eca4e70d84e3c4e036d0b64-ac12****
x-tos-ec: 0014-00000034
Content-Type: application/json
Content-Length: Content-Length

{
    "Error": {
        "Code": "InvalidArgument",
        "RequestId": "580c15f00eca4e70d84e3c4e036d0b64-ac12****",
        "HostId": "kElQBDtQvIsxwFYgDlZVQQszhbHt****",
        "Message": "multi destination is not support",
        "EC": "0014-00000034"
    }
}
```


Description:


|response |Description |
|---|---|
|Code |Returned error code. For more information, see [Response Codes](https://docs.byteplus.com/docs/6349/74874). |
|RequestId |Request ID, which you can use to troubleshoot the corresponding issue. |
|HostId |Host address used during the request. |
|Message |Error detailed description. |
|EC |Finer\-grained error codes provided by TOS. Each error corresponds to a unique EC code. Compared to Code and Message, the EC code is more detailed and offers a more precise problem description, helping you quickly locate issues and find solutions.<br><br>If a request fails, the EC code will be returned in both the response header (x\-tos\-ec) and the response body. You can use the EC code to independently diagnose the error cause and solution. For detailed steps, see [Using EC codes for self-diagnosis](https://docs.byteplus.com/docs/tos/Use-ec-code-for-self-troubleshooting). |
