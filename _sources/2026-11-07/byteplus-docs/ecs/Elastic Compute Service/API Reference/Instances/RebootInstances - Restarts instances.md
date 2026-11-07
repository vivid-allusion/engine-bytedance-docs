---
title: "RebootInstances - Restarts instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/RebootInstances"
---

Call the RebootInstances operation to restart one or more instances.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

Only ECS instances in the **Running** state can be restarted.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Restarting a bare metal instance using this operation may result in instance data loss. Complete the restart operation in the [ECS console](https://console.byteplus.com/ecs/instance).

* Restarting an instance will interrupt your business for a short period of time. Proceed with caution.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=RebootInstances&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, please refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|lleUSy">必选</span> `Sample value: RebootInstances`

The operation that you want to perform. Valid value: RebootInstances.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|TN6zO3">必选</span> `Sample value: 2020-04-01`

The API version. Valid value: 2020\-04\-01.



**ClientToken ** <span data-label="purple">string </span>`Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**ForceStop ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether to forcibly shut down the instance before restarting the instance. Valid values:


* true: Forcibly shuts down the instance. It is equivalent to a typical power\-off operation, and all cached data that has not been written to the storage device will be lost.

* false (default): Normal shutdown.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the following types of instances, regardless of whether <code>ForceStop</code> is set to <code>true</code> or <code>false</code>, the instances will be forcibly shut down.</div>



* <div data-tips="true" data-tips-type="tip">EBM instances.</div>


* <div data-tips="true" data-tips-type="tip">HPC\-optimized ebmhpcpni2l, ebmhpcpni2, and ebmhpchfpni2 instances.</div>


> <div data-tips="true" data-tips-type="tip" data-wrapper-indent="0">ebmhpcpni2l, ebmhpcpni2, and ebmhpchfpni2 instances are currently in Beta. If you need a trial, please contact your account manager.</div>




**InstanceIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|2V6M5X">必选</span> `Sample value: InstanceIds.1=i-ybo349sxoncm9t******&InstanceIds.2=i-ybo349sxolcm9t******`

The instance ID. A maximum of 100 instance IDs are supported.


* Argument \- N: specifies the serial number of the instance.

* Separate multiple instance IDs with ampersands (&).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following <a href="https://docs.byteplus.com/en/docs/49/12892#.6ZSZ6K-v56CB">error code</a> for the operation is displayed only when an invalid value is specified for a request parameter. If valid values are specified for the request parameters, no error code is displayed, and a status code of 200 is returned. However, this does not mean that the operation on all instances is successful. To view the operation result on a single instance, see the information in the following response parameters.</div>




**OperationDetails ** <span data-label="purple">object[] </span>`Sample value: --`

The operation details.


**Error ** <span data-label="purple">object </span>`Sample value: --`

The error message for the instance being operated on.


**Code ** <span data-label="purple">string </span>`Sample value: InvalidInstance.NotFound`

The error code for the failure of a specific request during batch operations. Value:


* InvalidInstance.NotFound: The specified instance does not exist.

* MissingParameter.InstanceId: The instance ID cannot be empty.

* InvalidInstanceStatus: The current status of the instance does not support this operation.

* OperationDenied.ResourceLocked: The specified operation is rejected because your resource has been locked by another operation.

* OperationDenied.ResourceCreatedByOtherService: The specified operation is rejected because your resource has been created by another service. You can query the corresponding service based on the system tag of the resource.

* OperationDenied.InstanceIsCreatingImage: The specified operation is rejected because the instance is being used to create a custom image.

* FlowLimitExceeded: You have exceeded the rate limit for resource requests.

* InternalError: An internal error occurred. Try again. If multiple attempts fail, submit a ticket.

* Insufficient.Balance: The account balance is insufficient.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each <code>Code</code> corresponds to a <code>Message</code> in sequence.</div>




**Message ** <span data-label="purple">string </span>`Sample value: The specified instance does not exist.`

The error information for the failure of a specific request during batch operations. Value:


* The specified instance does not exist.

* The required parameter InstanceId is not supplied.

* The status of the specified instance does not support this request.

* The specified operation is denied as your resource is locked for another operation.

* The specified operation is denied as your resource is created by other service. You can check system tags to find the service.

* The specified operation is denied as your instance is creating image.

* You've reached the limit on request rate of resources.

* An internal error has occurred.

* The request is denied due to the lack of balance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each <code>Code</code> corresponds to a <code>Message</code> in sequence.</div>





**InstanceId ** <span data-label="purple">string </span>`Sample value: i-ybo349sxoncm9t******`

The ID of the instance on which the operation is performed.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=RebootInstances&Version=2020-04-01&InstanceIds.1=i-ybo349sxoncm9t******&InstanceIds.2=i-ybo349sxolcm9t****** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "RebootInstances",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "OperationDetails": [
            {
                "InstanceId": "i-ybo349sxoncm9t******",
                "Error": {
                    "Code": "InvalidInstanceStatus",
                    "Message": "The status of the specified instance does not support this request."
                }
            },
            {
                "InstanceId": "i-ybo349sxolcm9t******",
                "Error": {
                    "Code": "InvalidInstance.NotFound",
                    "Message": "The specified instance does not exist."
                }
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |The request uses the same client token as a previous, but non\-identical request. Do not reuse a client token with different requests, unless the requests are identical. |The idempotent parameters are inconsistent. |
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|400 |InvalidCount.Malformed |The specified count is malformed. |The specified Count is invalid. |
|400 |InvalidDedicatedHostStatus.Unsupported |The status of the specified dedicated host does not support this request. |The dedicated host in current status does not support this action. |
|403 |InvalidInstance.RequestForbidden |Request is forbidden by the server. |The specified resource can no longer be used because your account has violated relevant rules. To restore service availability, submit a ticket to our service team for assistance. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still in process. Please try again later. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
