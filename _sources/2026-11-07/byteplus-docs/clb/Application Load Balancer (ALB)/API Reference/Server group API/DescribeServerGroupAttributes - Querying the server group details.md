---
title: "DescribeServerGroupAttributes - Querying the server group details"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-DescribeServerGroupAttributes"
---

Call the DescribeServerGroupAttributes API to query the detailed information of the server group.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Submit up to 200 API requests per second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeServerGroupAttributes&groupName=%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%BB%84&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|x1RI3m">必选</span> `Example: DescribeServerGroupAttributes`

Action to execute. Set the value to DescribeServerGroupAttributes.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|6g2QDB">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**ServerGroupId ** <span data-label="purple">string </span><span data-api-tag="require|hrWKYs">必选</span> `Example: rsp-bp1o94dp5i6ea****`

Backend server group ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 20210811152539010225146063030****`

Request ID.



**ServerGroupId ** <span data-label="purple">string </span>`Example: rsp-bp1o94dp5i6ea****`

ID of the backend server group.



**ServerGroupName ** <span data-label="purple">string </span>`Example: default_servergroup`

Name of the backend server group.



**ServerGroupType ** <span data-label="purple">string </span>`Example: instance`

Type of the backend server group.


* instance: Server type. This type of server group supports adding ECS and ENI instances as backend servers.

* ip: IP type. This type of server group supports adding IP addresses as backend servers.



**Description ** <span data-label="purple">string </span>`Example: This is the default servergroup`

Description of the backend server group.



**Status ** <span data-label="purple">string </span>`Example: Active`

Server group status.


* Creating

* Active: Running.

* Configuring: Pending configuration.

* Deleting



**VpcId ** <span data-label="purple">string </span>`Example: vpc-3th8z3ajkd4bwbhc****`

ID of the VPC to which the backend server group belongs.



**Scheduler ** <span data-label="purple">string </span>`Example: wrr`

Scheduling algorithm.


* wrr: Weighted Round Robin.

* wlc: Weighted Least Connection.

* sh: Source Address Hash.



**HealthCheck ** <span data-label="purple">object </span>`Example: --`

Health check configuration information of the server group.


**Enabled ** <span data-label="purple">string </span>`Example: on`

Whether the listener has health check enabled.


* on: Enable.

* off: Disable.



**Interval ** <span data-label="purple">integer </span>`Example: 2`

The time interval for performing health checks. Unit: seconds. Range: 1\-60s. Default: 2.



**Timeout ** <span data-label="purple">integer </span>`Example: 2`

The response timeout of the health check.


* This indicates that if the backend server does not respond correctly within the specified time, the health check will be marked as exception.

* Unit: seconds. Range: 1\-60. Default: 2.



**HealthyThreshold ** <span data-label="purple">integer </span>`Example: 3`

The health threshold for health check.


* It means a backend server that continuously runs the specified number of health checks and returns all results as normal will be marked as normal.

* Unit: time(s). Range: 2\-10. Default: 3.



**UnhealthyThreshold ** <span data-label="purple">integer </span>`Example: 3`

The unhealthy threshold for health check.


* Indicates a backend server that continuously runs the specified number of health checks and returns all results as exception will be marked as exception.

* Unit: time(s). Range: 2\-10. Default: 3.



**Method ** <span data-label="purple">string </span>`Example: HEAD`

Health check method. This parameter exists only when the Protocol is HTTP.


* GET: The server must support the GET method.

* HEAD: The server returns only the HEAD header information, which can reduce backend performance consumption, but the server must support the HEAD method.



**Domain ** <span data-label="purple">string </span>`Example: www.test.com`

The domain name for health checks must be configured as the actual externally accessible address of the backend server. This parameter exists only when the Protocol is HTTP.



**URI ** <span data-label="purple">string </span>`Example: health`

Health check path. It must be configured as the actual path provided on the backend server. This parameter exists only when the Protocol is HTTP.



**HttpCode ** <span data-label="purple">string </span>`Example: "http_2xx,http_3xx"`

The HTTP status codes considered healthy for health checks, with multiple status codes separated by commas (","). This parameter exists only when the Protocol is HTTP.


* http_2xx (default).

* http_3xx (default).

* http_4xx.

* http_5xx.



**Protocol ** <span data-label="purple">string </span>`Example: HTTP`

Health check protocol. Currently supports HTTP and TCP.



**Port ** <span data-label="purple">integer </span>`Example: 80`

Health check port. When the parameter value is 0, it indicates that the backend server port is used for health checks.



**HttpVersion ** <span data-label="purple">string </span>`Example: HTTP1.0`

The HTTP protocol version for health checks. This parameter exists only when the Protocol is HTTP.


* HTTP1.0 (default HTTP protocol version when using the API).

* HTTP1.1.




**Listeners ** <span data-label="purple">string[] </span>`Example: [lsn-2fek3rgsxhrsw5oxruwec****,lsn-3fek4rgsxhrsw5oxruwec****]`

Listener associated with the backend server group.



**Servers ** <span data-label="purple">object[] </span>`Example: --`

Information about servers in the backend server group.


**ServerId ** <span data-label="purple">string </span>`Example: rs-3cig8e5o0kxs06c6rrsqn****`

Backend server ID.



**InstanceId ** <span data-label="purple">string </span>`Example: i-3tkuehz8oa3vj0wz****`

ID of the ECS instance or network interface.



**Type ** <span data-label="purple">string </span>`Example: ecs`

Backend server instance type.


* ecs: Elastic Compute Service instance.

* eni: Secondary network interface.

* ip: IP address (valid only for IP type server groups).



**RemoteEnabled ** <span data-label="purple">string </span>`Example: on`

Enable the remote IP feature. When the backend server instance type is IP address (i.e., Type takes the value ip), this field is valid.


* on: Enable.

* off: Disable.



**Weight ** <span data-label="purple">integer </span>`Example: 100`

Weight of the backend server.



**Ip ** <span data-label="purple">string </span>`Example: 192.XX.XX.2`

Private IP address of the backend server.



**Port** <span data-label="purple">integer</span> `Example: 88`

Port number on which the backend server receives requests.



**Description ** <span data-label="purple">string </span>`Example: This is a backend server`

Description of the backend server.




**StickySessionConfig ** <span data-label="purple">object </span>`Example: --`

Parameter information for the session persistence feature.


**Cookie ** <span data-label="purple">string </span>`Example: MY_COOKIE`

The session persistence cookie name configured for the service.



**CookieTimeout ** <span data-label="purple">integer </span>`Example: 1000`

Session persistence cookie timeout period. Timeout value range: 1\-86400. Unit: seconds.



**StickySessionType ** <span data-label="purple">string </span>`Example: insert`

Cookie handling method. Valid values:


* insert: Cookie placement. The ALB records the backend server to which the client's first request is forwarded. The ALB inserts a cookie into the response. When subsequent client requests carry this cookie, the ALB forwards the requests to the previously recorded backend server.

* server: Rewrite cookie. After session persistence with cookie rewrite is enabled, when the client's first request is forwarded to the backend server, the ALB, upon finding your custom cookie in the response, rewrites the original cookie. Subsequent client requests carrying the rewritten cookie will cause the ALB to forward the requests to the previously recorded backend server.



**StickySessionEnabled ** <span data-label="purple">string </span>`Example: off`

Enable session persistence Valid values:


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


* on: Enable.

* off: Disable.



**SlowStartDuration** <span data-label="purple">integer</span> `Example: 30`

Slow start duration. Unit: seconds.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DescribeServerGroupAttributes&ServerGroupId=rsp-bp1o94dp5i6ea****&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20260331155608038225060003DE8808",
    "Action": "DescribeServerGroupAttributes",
    "Version": "2020-04-01",
    "Service": "alb",
    "Region": "cn-beijing"
  },
  "Result": {
    "RequestId": "20210811152539010225146063030****",
    "ServerGroupId": "rsp-bp1o94dp5i6ea****",
    "ServerGroupName": "default_servergroup",
    "ServerGroupType": "instance",
    "Description": "This is the default servergroup",
    "Status": "Active",
    "VpcId": "vpc-3th8z3ajkd4bwbhc****",
    "Scheduler": "wrr",
    "HealthCheck": {
      "Enabled": "on",
      "Interval": 2,
      "Timeout": 2,
      "HealthyThreshold": 3,
      "UnhealthyThreshold": 3,
      "Method": "HEAD",
      "Domain": "www.test.com",
      "URI": "health",
      "HttpCode": "http_2xx,http_3xx",
      "Protocol": "HTTP",
      "Port": 80,
      "HttpVersion": "HTTP1.0"
    },
    "Listeners": [
      "[lsn-2fek3rgsxhrsw5oxruwec****,lsn-3fek4rgsxhrsw5oxruwec****]"
    ],
    "Servers": [
      {
        "ServerId": "rs-3cig8e5o0kxs06c6rrsqn****",
        "InstanceId": "i-3tkuehz8oa3vj0wz****",
        "Type": "ecs",
        "RemoteEnabled": "on",
        "Weight": 100,
        "Ip": "192.XX.XX.2",
        "Port": 88,
        "Description": "This is a backend server"
      }
    ],
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
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request is missing a required parameter. Ensure that your request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup does not exist. |The specified server group does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
