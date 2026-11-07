---
title: "AttachSecurityGroupToVpcEndpoint - Attaching a security group to endpoints"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/AttachSecurityGroupToVpcEndpoint"
---

Call the AttachSecurityGroupToVpcEndpoint API to attach a security group to an endpoint. For operation instructions and precautions, see [Changing the associated security group](https://docs.byteplus.com/en/docs/privatelink/Managing-associated-security-groups).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AttachSecurityGroupToVpcEndpoint&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|jqWJwl">必选</span> `Example: AttachSecurityGroupToVpcEndpoint`

Action to execute. Set the value to **AttachSecurityGroupToVpcEndpoint**.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|wdf_hu">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**EndpointId ** <span data-label="purple"> String  </span><span data-api-tag="require|x1tCHY">必选</span> `Example: ep-273yuq6q7bgn47fap8squ****`

The ID of the endpoint.

You can call the [DescribeVpcEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpoints) API to obtain the ID of the endpoint.



**SecurityGroupId ** <span data-label="purple"> String  </span><span data-api-tag="require|omDlPq">必选</span> `Example: sg-bp67acfmxazb4p****`

Security group ID.

You can call the [DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups) API to get the security group ID.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple"> String  </span>`optional` `Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=AttachSecurityGroupToVpcEndpoint&Version=2020-04-01&EndpointId=ep-273yuq6q7bgn47fap8squ****&SecurityGroupId=sg-bp67acfmxazb4p**** HTTP/1.1
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****",
        "Action": "AttachSecurityGroupToVpcEndpoint",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Explain** |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'XXX'. |This request does not contain required parameters. Ensure that your request includes all required parameters, such as XXX.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Here, XXX represents the name of the missing parameter.</div><br> |
|400 |InvalidSecurityGroup.Conflict |The specified security group is duplicated. |The specified security groups are duplicated. |
|400 |InvalidEndpoint.InvalidStatus |The specified endpoint is not in the correct status for the request. |The specified endpoint is in a status that cannot respond to this request. |
|400 |UnsupportedOperation.AccountArrears |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|400 |SecurityGroupExist |The specified security group already exists. |The specified security group already exists. |
|400 |QuotaExceeded.SecurityGroup |The number of security groups bound to the ENI exceeded quota. |The current network interface has reached the maximum number of security groups that can be created. |
|400 |InvalidSecurityGroup.VpcMismatch |The specified security group and elastic network interface are not in the same VPC. |The specified security group and the Elastic Network Interface (ENI) are not in the same VPC. |
|400 |InvalidAccount.SecurityGroupMisMatch |The specified account and security group don't match. |The specified account and security group do not match. |
|400 |InvalidServiceManaged.Conflict |The specified endpoint is not service\-managed. |The specified endpoint is not a managed endpoint. |
|400 |InvalidEndpoint.ServiceDeleted |The specified endpoint's service has been deleted for the request. |The specified endpoint's associated endpoint service has been deleted, and the request cannot be processed. |
|403 |Forbidden.ServiceManagedEndpoint |You are not authorized to perform operations on the service managed endpoint. |You do not have permission to perform operations on the service\-managed endpoint. |
|404 |SecurityGroup.NotFound |The specified security group does not exist. |The specified security group does not exist. |
|404 |InvalidEndpoint.NotFound |The specified endpoint does not exist. |The specified endpoint does not exist. |
|404 |InvalidEndpointService.NotFound |The specified EndpointService does not exist. |The specified endpoint service does not exist. |
|409 |InvalidSecurityGroupId.Conflict |The specified security group is duplicated with another security group associated with the same elastic network interface. |The specified security group is already associated with this network interface and cannot be bound again. |
