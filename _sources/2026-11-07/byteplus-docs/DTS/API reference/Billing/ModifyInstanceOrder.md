---
title: "ModifyInstanceOrder"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/ModifyInstanceOrder"
---

Call the ModifyInstanceOrder interface to modify the billing configuration of the task.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|TaskId |String |Yes |9863318d02ed4a6f88f14c03a2\*\*\*\*\* |Task ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/DTS/describetransmissiontasks">DescribeTransmissionTasks</a> API to query the task ID.</div><br> |
|OneStep |Boolean |Yes |true |When performing billing conversion, this indicates whether to immediately create and pay for the order after creating the configuration form. The possible values ​​are as follows:<br><br><br>* `Yes`: Create the order and pay immediately after creating the configuration order.<br><br>* `No`: Do not create the order and the modify configuration fails after creating the configuration order.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When calling the <code>ModifyInstanceOrder</code> interface to modify the task's billing configuration, this parameter must be set to <code>true</code>.</div><br> |
|ConvertPostPaidToPrePaid |Object of [ConvertPostPaidToPrePaidReq](https://docs.byteplus.com/en/docs/57/82669#convertpostpaidtoprepaidreq) |No |```json```<br>```{```<br>```   "Times": 3,```<br>```   "AutoRenew": true```<br>```}```<br> |Subscription configuration.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when invoking the ModifyInstanceOrder interface to convert from pay\-as\-you\-go to subscription.</div><br> |
|ModifyInstanceSpec |Object of [ModifyInstanceSpecReq](https://docs.byteplus.com/en/docs/57/82669#modifyinstancespecreq) |No |```json```<br>```{```<br>```   "TrafficSpec": "Compact"```<br>```}```<br> |Task link specifications.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when calling the ModifyInstanceOrder interface to convert the link specifications of synchronization or subscription tasks.</div><br> |


<span id="convertpostpaidtoprepaidreq"></span>
### ConvertPostPaidToPrePaidReq


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Times |Integer |Yes |3 |Subscription purchase time supports values of `1`, `2`, `3`, `4`, `5`, `6`, `7`, `8`, `9`, `12`, `24`, and `36` months. |
|AutoRenew |Boolean |No |true |Whether to enable automatic renewal after the subscription expires. The values are as follows:<br><br><br>* `true`: Indicates automatic renewal.<br><br>* `false`: Indicates no automatic renewal. Default value. |


<span id="modifyinstancespecreq"></span>
### ModifyInstanceSpecReq


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|TrafficSpec |String |No |Compact |Task link specifications. Supports `Compact` and `Standard` values, default is `Compact`. For details about link specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/DTS/product_specifications). |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|OrderIDList |Array of String |Order710938814817460\*\*\*\* |The order ID. |
|PreOrderIDList |Array of String |BO723708552606635\*\*\*\* |When the `OneStep` parameter is set to `false`, the returned configuration order ID indicates that it is impossible to proceed to the next step of creating an order, meaning that modifying the task billing configuration failed. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=ModifyInstanceOrder&Version=2022-10-01 HTTP/1.1
Content-Type: application/json
Host: dts.cn-beijing.byteplusapi.com.cn
X-Date: 20221001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20221001/cn-beijing/dts/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TaskId": "9863318d02ed4a6f88f14c03a2*****",
    "ConvertPostPaidToPrePaid": {
        "Times": 3,
        "AutoRenew": true
    },
    "ModifyInstanceSpec": {
        "TrafficSpec": "Compact"
    },
    "OneStep": true
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "Action": "ModifyInstanceOrder",
        "Region": "cn-beijing",
        "Service": "dts",
        "Version": "2022-10-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "OrderIDList": [
            "Order710938814817460****"
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For more details, see [Error code](https://docs.byteplus.com/en/docs/DTS/error_codes).
