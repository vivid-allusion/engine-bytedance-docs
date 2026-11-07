---
title: "DescribeServerGroups - Querying a server group list"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-DescribeServerGroups"
---

Call the DescribeServerGroups API to query the list of server groups.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Submit up to 200 API requests per second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeServerGroups&groupName=%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%BB%84&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|wsf1XF">必选</span> `Example: DescribeServerGroups`

Action to execute. Set the value to DescribeServerGroups.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|vphyE4">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**VpcId ** <span data-label="purple">string </span>`optional` `Example: vpc-3th8z3ajkd4bwbhc****`

ID of the VPC to which the backend server group belongs.



**PageNumber ** <span data-label="purple">integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple">integer </span>`optional` `Example: 10`

Number of rows per page for paginated queries. Valid range: 1 to 100. Default value: 10.



**ServerGroupIds.N ** <span data-label="purple">string[] </span>`optional` `Example: ServerGroupIds.1=rsp-2fel9y8pxr56o5oxruuuu****&ServerGroupIds.2=rsp-1g0ogy36a8t8g8ibuxwy5****`

ID of the backend server group.


* Parameter \- N: Indicates the serial number of the backend server group, ranging from 1 to 20.

* Separate multiple backend server group IDs with ampersands (&).



**ServerGroupNames.N ** <span data-label="purple">string[] </span>`optional` `Example: ServerGroupNames.1=servergroup_1&ServerGroupNames.2=servergroup_2`

Name of the backend server group.


* Parameter \- N: Indicates the serial number of the backend server group, ranging from 1 to 10.

* Separate multiple backend server group IDs with ampersands (&).



**ServerGroupType ** <span data-label="purple">string </span>`optional` `Example: instance`

Type of the backend server group. Valid values:


* instance: Server type. This type of server group supports adding ECS and ENI instances as backend servers.

* ip: IP type. This type of server group supports adding IP addresses as backend servers.



**TagFilters.N.Values.N ** <span data-label="purple">string[] </span>`optional` `Example: TagFilters.1.Value.1=v1&TagFilters.1.Value.2=v2&TagFilters.2.Value.1=v3`

The tag value.


* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns ALB server groups that have any of the specified tag values for that key.

* Separate multiple tag values with an ampersand (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If this parameter is passed in, TagFilters.N.Key must be passed in first.</div>


* <div data-tips="true" data-tips-type="tip">Passing an empty string queries for ALB server groups with an empty tag value.</div>




**TagFilters.N.Key ** <span data-label="purple">string[] </span>`optional` `Example: TagFilters.1.Key=k1&TagFilters.2.Key=k2`

The tag key.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns ALB server groups tagged with all the specified keys.

* Duplicate values are not allowed.



**ProjectName ** <span data-label="purple">string </span>`optional` `Example: default`

The name of the project to which the backend server group belongs.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 20210811152539010225146063030****`

Request ID.



**PageSize ** <span data-label="purple">integer </span>`Example: 20`

The number of rows on the current page.



**PageNumber ** <span data-label="purple">integer </span>`Example: 1`

Current page number.



**TotalCount ** <span data-label="purple">integer </span>`Example: 50`

Total number of backend server groups that meet the conditions.



**ServerGroups ** <span data-label="purple">object[] </span>`Example: --`

List of server groups that meet the conditions.


**ServerGroupId ** <span data-label="purple">string </span>`Example: rsp-2fel9y8pxr56o5oxruuuu****`

ID of the backend server group.



**ServerGroupName ** <span data-label="purple">string </span>`Example: default_servergroup`

Name of the backend server group.



**ServerGroupType ** <span data-label="purple">string </span>`Example: instance`

Type of the backend server group.



**Description ** <span data-label="purple">string </span>`Example: this is the default servergroup`

Description of the backend server group.



**CreateTime ** <span data-label="purple">string </span>`Example: 2021-08-11T16:37:37Z`

Creation time of the backend server group.



**UpdateTime ** <span data-label="purple">string </span>`Example: 2021-08-11T16:37:37Z`

Last operation time of the backend server group.



**VpcId ** <span data-label="purple">string </span>`Example: vpc-3th8z3ajkd4bwbhc****`

ID of the VPC to which the backend server group belongs.



**Status ** <span data-label="purple">string </span>`Example: Active`

Status of the server group.


* Creating

* Active: Running.

* Configuring: Pending configuration.

* Deleting



**Scheduler ** <span data-label="purple">string </span>`Example: wrr`

Scheduling algorithm.


* wrr: Weighted Round Robin.

* wlc: Weighted Least Connection.

* sh: Source Address Hash.



**ServerCount ** <span data-label="purple">integer </span>`Example: 50`

Number of backend servers in the server group.



**Listeners ** <span data-label="purple">string[] </span>`Example: [lsn-2fek3rgsxhrsw5oxruwec****,lsn-3fek4rgsxhrsw5oxruwec****]`

Listener associated with the backend server group.



**HealthCheck ** <span data-label="purple">object </span>`Example: --`

Health check configuration information of the server group.


**Enabled ** <span data-label="purple">string </span>`Example: on`

Whether the listener has health check enabled.


* on: Enable.

* off: Disable.



**Interval ** <span data-label="purple">integer </span>`Example: 2`

The time interval for performing health checks. Unit: second(s).



**Timeout ** <span data-label="purple">integer </span>`Example: 2`

The response timeout of the health check.


* This indicates that if the backend server does not respond correctly within the specified time, the health check will be marked as exception.

* Unit: seconds.



**HealthyThreshold ** <span data-label="purple">integer </span>`Example: 3`

The health threshold for health check.


* It means a backend server that continuously runs the specified number of health checks and returns all results as normal will be marked as normal.

* Unit: time(s).



**UnhealthyThreshold ** <span data-label="purple">integer </span>`Example: 3`

The unhealthy threshold for health check.


* Indicates a backend server that continuously runs the specified number of health checks and returns all results as exception will be marked as exception.

* Unit: time(s).



**Method ** <span data-label="purple">string </span>`Example: HEAD`

Health check method. This parameter exists only when Protocol is HTTP.


* GET: The server must support the GET method.

* HEAD: The server returns only the HEAD header information, which can reduce backend performance consumption, but the server must support the HEAD method.



**Domain ** <span data-label="purple">string </span>`Example: www.test.com`

The domain name for health checks must be configured as the actual externally accessible address of the backend server. This parameter exists only when Protocol is HTTP.



**URI ** <span data-label="purple">string </span>`Example: health`

Health check path. It must be configured as the actual path provided on the backend server. This parameter exists only when Protocol is HTTP.



**HttpCode ** <span data-label="purple">string </span>`Example: "http_2xx,http_3xx"`

The HTTP status codes considered healthy for health checks, with multiple status codes separated by commas (","). This parameter exists only when Protocol is HTTP.


* http_2xx (default).

* http_3xx (default).

* http_4xx.

* http_5xx.



**Protocol ** <span data-label="purple">string </span>`Example: HTTP`

Health check protocol. Currently supports HTTP and TCP. Default: HTTP.



**Port ** <span data-label="purple">integer </span>`Example: 80`

Health check port. When the parameter value is 0, it indicates that the backend server port is used for health checks.



**HttpVersion ** <span data-label="purple">string </span>`Example: HTTP1.0`

The HTTP protocol version for health checks. This parameter exists only when the Protocol is HTTP.


* HTTP1.0 (default HTTP protocol version when using the API).

* HTTP1.1.




**StickySessionConfig ** <span data-label="purple">object </span>`Example: --`

Parameter information for the session persistence feature.


**Cookie ** <span data-label="purple">string </span>`Example: MY_COOKIE`

The session persistence cookie name configured for the service.



**CookieTimeout ** <span data-label="purple">integer </span>`Example: 1000`

Session persistence cookie timeout. Timeout value range: 1\-86400. Unit: seconds.



**StickySessionType ** <span data-label="purple">string </span>`Example: insert`

Cookie handling method.


* insert: Cookie placement. The ALB records the backend server to which the client's first request is forwarded. The ALB inserts a cookie into the response. When subsequent client requests carry this cookie, the ALB forwards the requests to the previously recorded backend server.

* server: Rewrite cookie. After session persistence with cookie rewrite is enabled, when the client's first request is forwarded to the backend server, the ALB, upon finding your custom cookie in the response, rewrites the original cookie. Subsequent client requests carrying the rewritten cookie will cause the ALB to forward the requests to the previously recorded backend server.



**StickySessionEnabled ** <span data-label="purple">string </span>`Example: off`

Enable session persistence


* on: Enable.

* off: Disable.




**Protocol ** <span data-label="purple">string </span>`Example: HTTP`

Backend protocol.


* HTTP

* HTTPS



**CrossZoneEnabled ** <span data-label="purple">string </span>`Example: on`

Cross\-zone load balancing is enabled for the server group.


* on: Enabled.

* off: Disable.



**ProjectName ** <span data-label="purple">string </span>`Example: default`

The name of the project to which the backend server group belongs.



**Tags ** <span data-label="purple">object[] </span>`Example: --`

The tags associated with the server group.


**Key ** <span data-label="purple">string </span>`Example: key`

The tag key of the custom tag.



**Value ** <span data-label="purple">string </span>`Example: value`

The tag value of the custom tag.




**IpAddressType ** <span data-label="purple">string </span>`Example: IPv4`

IP address type of the server group.


* IPv4: IPv4 type.



**SlowStartConfig ** <span data-label="purple">object </span>`Example: --`

Slow start configuration.


**SlowStartEnabled ** <span data-label="purple">string </span>`Example: off`

Enable slow start feature.


* on: Enable

* off: Disable



**SlowStartDuration ** <span data-label="purple">integer </span>`Example: 30`

Slow start duration. Unit: seconds.





&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DescribeServerGroups&ServerGroupIds.1=rsp-1g0lh2f1a****8ibuxx6z7fm8&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "2026033115584005508013913991E43D",
    "Action": "DescribeServerGroups",
    "Version": "2020-04-01",
    "Service": "alb",
    "Region": "cn-beijing"
  },
  "Result": {
    "RequestId": "20210811152539010225146063030****",
    "PageSize": 20,
    "PageNumber": 1,
    "TotalCount": 50,
    "ServerGroups": [
      {
        "ServerGroupId": "rsp-2fel9y8pxr56o5oxruuuu****",
        "ServerGroupName": "default_servergroup",
        "ServerGroupType": "instance",
        "Description": "this is the default servergroup",
        "CreateTime": "2021-08-11T16:37:37Z",
        "UpdateTime": "2021-08-11T16:37:37Z",
        "VpcId": "vpc-3th8z3ajkd4bwbhc****",
        "Status": "Active",
        "Scheduler": "wrr",
        "ServerCount": 50,
        "Listeners": [
          "[lsn-2fek3rgsxhrsw5oxruwec****,lsn-3fek4rgsxhrsw5oxruwec****]"
        ],
        "HealthCheck": {
          "Enabled": "on",
          "Interval": 2,
          "Timeout": 2,
          "HealthyThreshold": 3,
          "UnhealthyThreshold": 3,
          "Method": "HEAD",
          "Domain": "www.test.com",
          "URI": "health",
          "HttpCode": "\"http_2xx,http_3xx\"",
          "Protocol": "HTTP",
          "Port": 80,
          "HttpVersion": "HTTP1.0"
        },
        "StickySessionConfig": {
          "Cookie": "MY_COOKIE",
          "CookieTimeout": 1000,
          "StickySessionType": "insert",
          "StickySessionEnabled": "off"
        },
        "Protocol": "HTTP",
        "CrossZoneEnabled": "on",
        "ProjectName": "default",
        "Tags": [
          {
            "Key": "key",
            "Value": "value"
          }
        ],
        "IpAddressType": "IPv4",
        "SlowStartConfig": {
          "SlowStartEnabled": "off",
          "SlowStartDuration": 30
        }
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request does not contain required parameters. Please ensure the request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |LimitExceed.ServerGroup |You've reached the limit on the number of server groups that you can operate at a time. |The maximum number of server groups that can be operated on at one time has been reached. |
|400 |InvalidServerGroupName.Malformed |The specified ServerGroupName is malformed. |The specified ServerGroupName format is invalid. |
|400 |InvalidServerGroupType.Malformed |The specified ServerGroupType is malformed. |The specified ServerGroupType parameter format is invalid. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
