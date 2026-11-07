---
title: "Back to example"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Responses"
---

All returned data will carry the fields `RequestId `, `Action `, `Version `, `Service `, `Region `.

<span id=".5q2j5bi46L-U5Zue56S65L6L"></span>
## Normal return example

After the interface call is successful, the request ID and interface return parameters will be returned. We call such a return a normal return. The normal return `HTTP `status code is `2xx `.

Taking the calling **CreateDirectConnectGateway ** as an example, the normal return example is as follows:

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "202111161611080102121461940900****",//RequestId is the unique identifier for each API request.
        "Action": "CreateDirectConnectGateway",//The API name of the request, which is a public parameter of the request.
        "Version": "2020-04-01",//The requested version number.
        "Service": "directconnect",//the requested service.
        "Region": "cn-Beijing"//The requested region.
    },
    "Result": {
        "RequestId": "202111161611080102121461940900****",
        "DirectConnectGatewayId": "dcg-7qthudw0ll6jmc****"//returns the result.
    }
}
```


After the request is processed normally, the return will contain two parts: `ResponseMetadata `and `Result `. The fields are explained as follows:


|field |explain |
|---|---|
|RequestId |RequestId is the unique identifier for each API request. |
|Action |The interface name of the request, which is a public parameter of the request. |
|Version |The version number of the request, which is a public parameter of the request. |
|Service |The requested service is a public parameter of the request. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The result depends on the interface requested, and different interfaces will return different results.</div>


<span id=".5byC5bi46L-U5Zue56S65L6L"></span>
## exception return example

When an interface call fails, the request ID and error message are returned, which is called an exception return. Exception returns an `HTTP `status code of `4xx `or `5xx `. You can troubleshoot errors based on the interface BigInt ( `Code `) and error message ( `Message `), referring to the public error code and interface error code.

Taking the calling **CreateDirectConnectGateway ** as an example, the return example of the exception is as follows:

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "202111161611080102121461940900****",
        "Action": "CreateDirectConnectGateway",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing",
        "Error": {
            "Code": "UnsupportedOperation",
            "Message": "The request on the specified instance is denied due to the account in arrears status. "
        }
    }
}
```


In contrast to the normal return result, the abnormal result will no longer have a `Result `section, and an additional Error field will appear in ResponseMet`Error field will appear in ResponseMetadata `, which is explained as follows:


|field |explain |
|---|---|
|Error |An Error appears indicating that the request failed. |
|Code |Code content is a specific error code. You can query the error code document of the corresponding API to solve the problem by yourself. |
|CodeN |CodeN is a numeric ID that identifies the error code, which is convenient for finding problems. Only some interfaces provide CodeN. |
|Message |The message describes the specific reason why the error occurred. |
|RequestId |RequestId is the unique identifier of each API request. When there is a problem that cannot be solved by yourself, you can contact us through the [ticket system ](https://console.byteplus.com/ticket/createTicketV2/)and provide the RequestID of the request. We will assist in troubleshooting. |
