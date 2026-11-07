---
title: "ModifyDBInstanceChargeType"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceChargeType"
---

Call the ModifyDBInstanceChargeType API to modify the instance's billing method.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The instance currently has no **pending** configuration change events. You can search and view them by instance ID in the **Planned event** list. For steps, see [Viewing event list](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_event_list).

* Modifying the storage billing type for a subscription instance is not supported through API calls and can only be done in the console. For specific steps, refer to [Modifying storage billing type](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_storage_billing_type).


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBInstanceChargeType&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-dfaa2zic\*\*\*\* |Instance ID. When batch changing the instance billing method, separate multiple Instance IDs with an English comma (,).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When performing batch changes, you can only select instances that have the same Calculate billing type and Storage billing type. You can select up to 50 instances at a time.</div><br> |
|ChargeType |String |Yes |PrePaid |Calculate billing type. The valid values are:<br><br><br>* `PostPaid` (Pay\-as\-you\-go): Changes a subscription instance to a pay\-as\-you\-go instance.<br><br>* `PrePaid` (Subscription): Changes a pay\-as\-you\-go instance to a subscription instance. |
|StorageChargeType |String |No |PostPaid |Storage billing type. The valid values are:<br><br><br>* `PostPaid`: Pay\-as\-you\-go.<br><br>* `PrePaid`: Yearly or monthly subscription.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When <code>ChargeType</code> is set to <code>PostPaid</code>, this parameter can only be set to <code>PostPaid</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When <code>ChargeType</code> is set to <code>PrePaid</code>, this parameter can be set to <code>PostPaid</code> or <code>PrePaid</code> (default).</div><br> |
|PrePaidStorageGB |Integer |No |100 |Set the size of the storage space. The supported storage space size varies by instance specification. For details, refer to [Product specifications](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Product_specifications).<br><br><br>* If this parameter is not specified, the storage space size defaults to `current used space` + `15 GB`.<br><br>* When customizing the storage space size, it is recommended to choose a size larger than the currently used storage space. If you choose a size smaller than the currently used storage space, the excess usage will be billed on a pay\-as\-you\-go basis. Similarly, when batch\-modifying the instance billing method, it is recommended to select a size larger than the maximum storage space used among all instances. If the size is smaller than the maximum storage space currently used, the excess capacity of some instances will be charged on a pay\-as\-you\-go basis.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when <code>ChargeType</code> is set to <code>PrePaid</code>.</div><br> |
|AutoRenew |Boolean |No |false |Specifies whether to enable Due Automatic renewal for prepaid instances. Value:<br><br><br>* `true`: enables auto\-renewal.<br><br>* `false`: no automatic renewal.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when <code>ChargeType</code> is set to <code>PrePaid</code>.</div><br> |
|PeriodUnit |String |No |Month |The prepaid purchase duration.<br><br><br>* `Month`: Monthly subscription.<br><br>* `Year`: Yearly subscription.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when <code>ChargeType</code> is set to <code>PrePaid</code>.</div><br> |
|Period |Integer |No |1 |The purchase duration for a subscription.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when <code>ChargeType</code> is set to <code>PrePaid</code>.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |vedbm\-dfaa2zic\*\*\*\* |Instance ID. |
|OrderNO |String |Order728156369167322\*\*\*\* |Order ID. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Request example 1

Single instance switch to subscription.

```JSON
POST /?Action=ModifyDBInstanceChargeType&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId":"vedbm-dfaa2zic****",
    "ChargeType":"PrePaid",
    "Period":1,
    "AutoRenew":false,
    "PeriodUnit":"Month"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example 1

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230922162644526CE9EB684703C1F9E4",
        "Action": "ModifyDBInstanceChargeType",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "vedbm-dfaa2zic****",
        "OrderNO": "Order728156369167322****"
    }
}
```


<span id=".6K-35rGC56S65L6LLTI="></span>
### Request example 2

Batch switch to subscription.

```JSON
POST /?Action=ModifyDBInstanceChargeType&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId":"vedbm-pzfq2zif****,vedbm-dfaa2zic****",
    "ChargeType":"PrePaid",
    "Period":1,
    "AutoRenew":false,
    "PeriodUnit":"Month"
}
```


<span id=".6L-U5Zue56S65L6LLTI="></span>
### Response example 2

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230922162644526CE9EB684703C1F9E4",
        "Action": "ModifyDBInstanceChargeType",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "vedbm-dfaa2zic****",
        "OrderNO": "Order728156369167322****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
