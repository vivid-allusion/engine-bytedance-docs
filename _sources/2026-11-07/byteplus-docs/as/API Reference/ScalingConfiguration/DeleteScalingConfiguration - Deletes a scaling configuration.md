---
title: "DeleteScalingConfiguration - Deletes a scaling configuration"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/DeleteScalingConfiguration"
---

Delete a scaling configuration. A scaling configuration that is associated with a scaling group cannot be deleted. To delete such a configuration, first associate another scaling configuration with the scaling group.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteScalingConfiguration&groupName=%E4%BC%B8%E7%BC%A9%E9%85%8D%E7%BD%AE&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|uFc25I">必选</span> `Sample value: DeleteScalingConfiguration`

The operation that you want to perform. Valid value: DeleteScalingConfiguration.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|IDtgaY">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**ScalingConfigurationId ** <span data-label="purple">string </span><span data-api-tag="require|9IzI3Y">必选</span> `Sample value: scc-ybmt16auaugh9zfy****`

The scaling configuration ID. You can call [DescribeScalingConfigurations](https://docs.byteplus.com/en/docs/as/DescribeScalingConfigurations) to query the scaling configuration ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ScalingConfigurationId ** <span data-label="purple">string </span>`Sample value: scc-ybmt16auaugh9zfy****`

The scaling configuration ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DeleteScalingConfiguration&ScalingConfigurationId=scc-ybmt16auaugh9zfy****&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T095313Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20240507175321157204123004DC3A7E",
    "Version": "2020-01-01",
    "Service": "auto_scaling",
    "Region": "cn-beijing"
  },
  "Result": {
    "ScalingConfigurationId": "scc-ybmt16auaugh9zfy****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/as/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.ScalingConfigurationId |The required parameter ScalingConfigurationId is not supplied. |The scaling configuration ID cannot be empty. |
|400 |InvalidScalingConfiguration.InUse |The specified ScalingConfiguration [%s] is in use. |The specified scaling configuration is in use. |
|404 |InvalidScalingConfiguration.NotFound |The specified ScalingConfiguration [%s] does not exist. |The specified scaling configuration does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
