---
title: "ListMCPServices - Batch queries MCP service details"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/ListMCPServices_-_Batch_queries_MCP_service_details"
---

You can batch query MCP service details using custom filter conditions.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action**<span data-label="purple"> string</span><span data-api-tag="require|JVIgWD">必选</span>  `Sample value: ListMCPServices`

The action that you want to perform. Value: ListMCPServices.



**Version**<span data-label="purple"> string</span><span data-api-tag="require|XzwtEZ">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**Filters.N.Name ** <span data-label="purple">string[] </span>`Optional Sample value: name1`

Field name used for exact filtering.


* Parameter \- N: Indicates the serial number of the filter condition. Value range: 1–10.

* Separate multiple field names with ampersands (&), representing an "Or" relationship.

* Valid values:

   * name: MCP service name.

   * status: MCP service status.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>Filters.N.Name</code> and <code>Filters.N.NameContains</code> are both passed in, only <code>Filters.N.Name</code> takes effect.</div>




**Filters.N.NameContains ** <span data-label="purple">string[] </span>`Optional Sample value: name1`

Field name used for fuzzy filtering.


* Parameter \- N: Indicates the serial number of the filter condition. Value range: 1–10.

* Separate multiple field names with ampersands (&), representing an "Or" relationship.

* Valid values:

   * name: MCP service name.

   * status: MCP service status.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>Filters.N.Name</code> and <code>Filters.N.NameContains</code> are both passed in, only <code>Filters.N.Name</code> takes effect.</div>




**Filters.N.Values.N ** <span data-label="purple">string[] </span>`Optional Sample value: mcp-****`

Value of the filter field.


* Parameter \- N: Indicates the serial number of the filter condition. Value range: 1–10.

* Separate multiple field names with ampersands (&).


When the filter field is Status, the values are:


* Ready: Running.

* Creating: Being created.

* Updating: Being updated.

* Deleting: Being deleted.

* Error: Unavailable.



**MaxResults**<span data-label="purple"> integer</span>` Optional Sample value: 100`

The number of entries returned on each page in a pagination query.


* Minimum value: 1.

* Maximum value: 100. 

* Default value: 10



**NextToken ** <span data-label="purple">string </span>`Optional Sample value: bS15ZTcwMjZiaWY0cTdvaTVjc3****==`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the `NextToken` parameter to the value returned by the previous API call.



**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: default`

The name of the associated project.



**TagFilters.N.Key ** <span data-label="purple">string[] </span>`Optional` `Sample value: TagFilters.1.Key=k1`

Tag key specified when querying resources by tag. Each tag key must be unique.


* Parameter \- N: specifies the serial number of the tag key. Value range: 1–10.

* Separate multiple tag keys with ampersands (&).



**TagFilters.N.Values.N ** <span data-label="purple">string[]</span>` Optional Sample value: TagFilters.1.Values.1=v1`

The tag value specified when resources are queried based on tags.


* The first N: specifies the serial number of the tag key. Valid range: 1–10.

* The second N: specifies the serial number of the tag value. Valid range: 1\-3. That is, you can query up to three tag values of the same tag key.

* Separate multiple tag values with &.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in TagFilters.N.Key first.</div>


* <div data-tips="true" data-tips-type="tip">If you do not pass in this parameter, all tag values under the same tag key are queried.</div>


* <div data-tips="true" data-tips-type="tip">If you specify an empty string, you query tags with an empty tag value.</div>




**GatewayInstanceId ** <span data-label="purple">string </span>`Optional` `Sample value: gw-********`

The ID of the dedicated gateway instance associated with the MCP service. You can obtain the dedicated gateway instance ID in the AgentKit console under "Gateway \> Gateway instance \> Dedicated gateway".


* If this parameter is specified, only the MCP services under the dedicated gateway are returned.

* If this parameter is not specified, all MCP services that meet the query conditions are returned.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**MCPServices ** <span data-label="purple">object[] </span>`Sample value: --`

MCP service details.


**IsAllTools ** <span data-label="purple">boolean </span>`Sample value: true`

Whether all tools have been added.



**CreatedAt ** <span data-label="purple">string </span>`Sample value: 2006-01-02T15:04:05Z07:00`

Creation time of the MCP service.



**MCPServiceId ** <span data-label="purple">string </span>`Sample value: m-ye7f6gd7nktv3gi6c***`

MCP service ID.



**Name ** <span data-label="purple">string </span>`Sample value: mcp-name-***`

The name of the MCP service.



**NetworkConfigurations ** <span data-label="purple">object[] </span>`Sample value: --`

Network configuration details of the MCP service.


**Endpoint ** <span data-label="purple">string </span>`Sample value: ***.apigateway-ap-southeast-1.volceapi.com`

Endpoint for accessing the MCP service.



**NetworkType ** <span data-label="purple">string </span>`Sample value: Public`

Access type enabled for the MCP service. Value:


* Public: Public network access.

* Private: Access using private network



**VpcConfiguration ** <span data-label="purple">object </span>`Sample value: --`

VPC configuration information.


**SecurityGroupIds ** <span data-label="purple">string[] </span>`Sample value: ["sg-w08tvkc3e****"]`

List of security group IDs.



**SubnetIds ** <span data-label="purple">string[] </span>`Sample value: ["subnet-ye7s6jatq8rxg218****"]`

List of subnet IDs.



**VpcId ** <span data-label="purple">string </span>`Sample value: vpc-ye7s6jatq8rxg218****`

VPC ID.




**EnableSharedInternetAccess ** <span data-label="purple">boolean </span>`Sample value: false`

Specifies whether to enable shared public network access.


* false: Not enabled.

* true: Enabled.




**Path ** <span data-label="purple">string </span>`Sample value: /mcp`

Access path of the MCP service.



**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

Name of the project with which the MCP service is associated.



**ProtocolConfiguration ** <span data-label="purple">object </span>`Sample value: --`

Protocol configuration details of the MCP service.


**ProtocolConvertConfiguration ** <span data-label="purple">string </span>`Sample value: --`

When the MCP service backend is of the HTTP type, parse the result based on the API information.




**ProtocolType ** <span data-label="purple">string </span>`Sample value: MCP`

The access method for the MCP service. Valid values:


* HTTP: HTTP to MCP.

* MCP: Direct access to MCP.



**Status ** <span data-label="purple">string </span>`Sample value: Ready`

MCP service status. Value:


* Ready: Running.

* Creating: Being created.

* Updating: Being updated.

* Deleting: Being deleted.

* Error: Unavailable.



**Tags ** <span data-label="purple">object[] </span>`Sample value: --`

MCP service tags.


**Type ** <span data-label="purple">string </span>`Sample value: system`

Tag type.


* system: system tag

* custom: user tag



**Key ** <span data-label="purple">string </span>`Sample value: k1`

The tag key.



**Value ** <span data-label="purple">string </span>`Sample value: v1`

The tag value.




**UpdatedAt ** <span data-label="purple">string </span>`Sample value: 2006-01-02T15:04:05Z07:00`

Update time of the MCP service.



**CanDelete ** <span data-label="purple">boolean </span>`Sample value: true`

Whether the MCP service can be deleted.


* true: Deletion is allowed.

* false: Deletion is not allowed. The MCP service cannot be deleted when it is referenced by an MCP toolset.



**GatewayMode ** <span data-label="purple">string </span>`Sample value: Shared`

The gateway mode of the MCP service.


* Shared: Shared gateway.

* Exclusive: Dedicated gateway.



**InboundAuthorizerConfiguration ** <span data-label="purple">object </span>`Sample value: --`

Inbound authentication configuration of the MCP service.


**AuthorizerType ** <span data-label="purple">string </span>`Sample value: ApiKey`

The type of outbound identity authentication security for the MCP service.


* ApiKey: API Key\-based authentication.

* Identity: Identity\-and\-permissions\-based authentication.



**Authorizer ** <span data-label="purple">object </span>`Sample value: --`

Authentication configuration details.


**KeyAuth ** <span data-label="purple">object </span>`Sample value: --`

The API Key configuration, used when the backend service uses an API Key as the outbound credential.


**ApiKeys ** <span data-label="purple">object[] </span>`Sample value: 8b02f2e2-ae83-11f0-b6e5-******&In`

API Key information.


**Key ** <span data-label="purple">string </span>`Sample value: 65a075a2-aeff-11f0-****-00163e72f914`

The value of the API Key.



**Name ** <span data-label="purple">string </span>`Sample value: key-ye7f6gd7nktv3gi6c***`

API Key name.




**ApiKeyLocation ** <span data-label="purple">string </span>`Sample value: HEADER`

The location where the API Key is passed.



**Parameter ** <span data-label="purple">string </span>`Sample value: Authorization`

The parameter name corresponding to the API Key carried in the request headers.




**CustomJwtAuthorizer ** <span data-label="purple">object </span>`Sample value: --`

The authentication configuration of OAuth JWT, used when the backend service uses OAuth JWT as the outbound credential.


**DiscoveryUrl ** <span data-label="purple">string </span>`Sample value: https://example.com/.well-known/openid-configuration`

Authentication service address.



**AllowedClients ** <span data-label="purple">string[] </span>`Sample value: ["client1","client2"]`

List of allowed clients.




**IdentityAuthorizer ** <span data-label="purple">object </span>`Sample value: --`

The configuration of credential management when the backend service uses identity and permissions as outbound credentials.


**ProviderType ** <span data-label="purple">string </span>`Sample value: Oauth2M2m`

The type of credential management. Valid values:


* ApiKey: Use API Key credentials.

* Oauth2M2m: Use OAuth Client.



**CredentialProviderName ** <span data-label="purple">string </span>`Sample value: Oauth2M2m01`

The name of credential management.







**NextToken ** <span data-label="purple">string </span>`Sample value: bS15ZTcwMjZiaWY0cTdvaTVjc***w==`

The pagination token returned by this call. If this value is empty, the current page is the last page.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=ListMCPServices&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "MaxResults": 100,
    "NextToken": ""
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "ListMCPServices",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "ListMCPServicesResNextToken": {
      "MCPServices": [
        {
          "MCPServiceId": " mcp-xxx",
          "Name": " mcp-service-x",
          "Path": " /mcp",
          "Status": " Ready",
          "NetworkConfigurations": [
            {
              "NetworkType": " Public",
              "Endpoint": " ",
            }
          ],
          "ProtocolType": " HTTP",
          "ProtocolConfiguration": {
            "ProtocolConvertConfiguration": " "
          },
          "CreatedAt": " 2006-01-02T15:04:05Z07:00",
          "UpdatedAt": " 2006-01-02T15:04:05Z07:00"
        }
      ],
      "NextToken": " eyJwYWdlIjoyLCJ****"
    }
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |LimitExceeded.MaximumMaxResults |The number of specified MaxResults exceeds the maximum limit. |The value specified for MaxResults exceeds the upper limit. |
