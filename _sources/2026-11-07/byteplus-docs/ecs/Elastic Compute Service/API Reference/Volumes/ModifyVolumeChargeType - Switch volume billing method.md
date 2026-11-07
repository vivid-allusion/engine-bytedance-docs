---
title: "ModifyVolumeChargeType - Switch volume billing method"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ModifyVolumeChargeType"
---

Call the ModifyVolumeChargeType API to change the volume billing method.

<span id=".5rOo5oSP5LqL6aG5"></span>
## precautions


* Switch from pay\-as\-you\-go to annual or monthly subscription

   * Only pay\-as\-you\-go data volumes mounted on annual or monthly ECS instances can be converted individually to annual or monthly subscription data volumes, and the expiration of the data volume will match the ECS instance.

   * If a pay\-as\-you\-go system volume needs to be converted to annual or monthly subscription, it must be switched together with the attached ECS instance. For details, see [Switch from pay-as-you-go to annual or monthly subscription](https://docs.byteplus.com/en/docs/ecs/Converting-from-pay-as-you-go-to-subscription).

* Switch from annual or monthly subscription to pay\-as\-you\-go

   * If an annual or monthly system volume needs to be converted to pay\-as\-you\-go, it must be switched together with the attached ECS instance. For details, see [Switch from annual or monthly subscription to pay-as-you-go](https://docs.byteplus.com/en/docs/ecs/Converting-from-subscription-to-pay-as-you-go). Annual or monthly data volumes can be converted individually to pay\-as\-you\-go, or together with the instance.

   * When a yearly or monthly volume is converted to pay\-as\-you\-go, the platform will deduct the used amount and refund the remaining amount paid (in cash, excluding coupon deductions) to your BytePlus account balance. Used coupons are non\-refundable. For detailed rules on refund calculation, see [cancellation instructions](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management).


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyVolumeChargeType&groupName=%E4%BA%91%E7%9B%98&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Only the unique request parameters and some common parameters for this interface are listed below. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|ynqpvq">必选</span> `Example value: ModifyVolumeChargeType`

Operation to perform, value: ModifyVolumeChargeType.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|7WiXvb">必选</span> `Example: 2020-04-01`

The version of the API is: 2020\-04\-01.



**InstanceId ** <span data-label="purple">string </span><span data-api-tag="require|S7GyGd">必选</span> `Example: i-bp1i778bq705cvx1****`

Mounted volume instance ID.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only pay\-as\-you\-go data disks attached to subscription instances can be converted to subscription.</div>




**DiskChargeType ** <span data-label="purple">string </span><span data-api-tag="require|pjp4s8">必选</span> `Example: PrePaid`

Volume billing method. Value descriptions are as follows:


* PrePaid: Convert pay\-as\-you\-go data disks to subscription data disks.

* PostPaid: Convert subscription data disks to pay\-as\-you\-go data disks.



**AutoPay ** <span data-label="purple">boolean </span>`Optional` `Example: true`

Enable automatic payment. Value descriptions are as follows:


* true (default): Automatic payment. Ensure your account balance is sufficient, as insufficient funds will result in abnormal orders that can only be voided.

* false: Only generates an order without charging the account. If your account balance is insufficient, a normal unpaid order will be generated. You can log in to the ECS console to pay for this order.



**VolumeIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|LSkZdn">必选</span> `Example: VolumeIds.1=vol-3tiz8tg97u3vj0x0**** VolumeIds.2=vol-3tj20xxpd63vj0wy****`

List of volume IDs to be converted for billing method.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Supports batch conversion. Only data volumes mounted on the same subscription instance can be converted in bulk.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the unique response parameters for this interface are listed below. For more details, refer to [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Number ** <span data-label="purple">string </span>`Example value: Order708151602546642****`

The returned order number.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
GET /?Action=ModifyVolumeChargeType&DiskChargeType=PrePaid&VolumeIds.1=vol-3tiz8tg97u3vj0x0****&VolumeIds.2=vol-3tj20xxpd63vj0wy****&InstanceId=i-l2soxrgan390t1dk**** HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
X-TT-Logid:  202106232008120102251331430A0D7B20
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```json
{
    "ResponseMetadata": {
        "RequestId": "2022040115591901022524315306A6****",
        "Action": "ModifyVolumeChargeType",
        "Version": "2020-04-01",
        "Service": "storage_ebs",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Number": "Order708151602546642****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The following table lists error codes related to this interface and business logic. For public error codes, refer to the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |InvalidInstanceType.ValueUnauthorized |The specified InstanceType is not Supported. |You do not have permission to operate this instance type. |
|400 |Account.Arrearage |Your account has been in arrears. |Insufficient account balance. Please top up your account before proceeding. |
|400 |InvalidInstance.UnPaidOrder |The specified Instance has unpaid order. |The specified instance has unpaid orders. Complete the payment first before proceeding. |
|400 |InvalidInstanceId.Released |The specified Instance is not exist. |The specified instance does not exist. Check whether the instance ID is correct. |
|400 |MissingParameter.InstanceIdNotSupported |InstanceId should not be null. |The InstanceId parameter cannot be empty. |
|400 |OrderCreationFailed |Create Order failed, please check your parameters and try it later. |Failed to create order. Check your parameters and try again. |
