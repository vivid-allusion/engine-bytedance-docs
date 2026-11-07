---
title: "Responses"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Responses"
---

All responses contain the fields : `RequestId`, `Action`, `Version`, `Service`, and `Region`.

<span id="sample-of-a-normal-response"></span>
## Sample of a normal response

If an API call is successful, the API returns the request ID and response parameters. This is considered a normal response. The status code of `HTTP` is `2xx`.

In the following example, when you call the **CreateVpnGateway** action, a normal response is as follows:

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "202004011722300102****", //RequestId is the unique ID of each API request.
        "Action": "CreateVpnGateway",//The requested API action. It is a common request parameter.
        "Version": "2020-04-01",//The version of the request.
        "Service": "vpn",//The requested service.
        "Region": "ap-southeast-1"  //The Region that the request is sent to.
    },
    "Result": {   
        "RequestId":"2022032111142501022524314704AF****", 
        "OrderId":"Order7078570823273845****",  //The response result.
        "VpnGatewayId":"vgw-12bfa2du7fojk17q7y1rk****"
    }  
}
```


If a request is normally processed, the response contains two fields `ResponseMetadata` and `Result`. The following table describes the fields:


|Field |Description |
|---|---|
|RequestId |RequestId is the unique ID of each API request. |
|Action |The requested API action. It is a common request parameter. |
|Version |The version of the request. It is a common request parameter. |
|Service |The requested service. It is a common request parameter. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The value of Result depends on the requested API. Different Result values are returned for different APIs.</div>


<span id="sample-of-an-abnormal-response"></span>
## Sample of an abnormal response

If an error occurs in calling an API, the request ID and an error message are returned. This kind of response is an abnormal response. In an abnormal response, the status code of `HTTP` is `4xx` or `5xx`. You can troubleshoot issues according to `Code` and `Message`. For details, refer to Common error codes and API error codes.

In the following example, when you call the **CreateVpnGateway** action, the abnormal response is as follows:

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "202010201722300102****",
        "Action": "CreateVpnGateway",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "ap-southeast-1",
        "Error": {
            "Code": "InvalidBillingType.Malformed",
            "Message": "The specified billing type is malformed."
        }
    }
}
```


Compared to a normal response, in an abnormal response, the `Result` field is no longer contained, and `ResponseMetadata` contains an additional `Error` field. The following table describes the fields:


|Field |Description |
|---|---|
|Error |Indicates that the request failed. |
|Code |Indicates the specific error code. You can refer to the corresponding API error code document to troubleshoot issues. |
|CodeN |Indicates a numeric ID that is used to identify the error code. You can use the ID to locate the issue conveniently, but CodeN is only provided for some APIs. |
|Message |Describes the specific reason why an error occurs. |
|RequestId |Indicates the unique ID of each API request. If an issue occurs and you fail to solve it, contact us through the ticket system and provide RequestID of your request. We can help you troubleshoot the issue. |
