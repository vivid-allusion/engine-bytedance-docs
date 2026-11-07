---
title: "DescribeCustomizedCfgs - Querying the custom configuration list"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeCustomizedCfgs"
---

Call the DescribeCustomizedCfgs API to query the list of custom configurations.

## Instructions

Submit up to 40 API requests per second.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeCustomizedCfgs&serviceCode=alb&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: DescribeCustomizedCfgs`

The interface name. The current API name is `DescribeCustomizedCfgs`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. Current API version is `2020-04-01`.

**PageNumber** Integer `optional` `Example: 1`

The page number of the list. Default: 1.

**PageSize ** Integer`optional` `Example: 10`

Number of rows per page for paginated queries. Valid range: 1 to 100. Default value: 10.

**CustomizedCfgName ** String`optional` `Example: myCustomizedCfgName`

The name of the custom configuration to be queried.

**CustomizedCfgIds.N ** String[]`optional` `Example: CustomizedCfgIds.1=ccfg-xxxxx&CustomizedCfgIds.2=ccfg-yyyyy`

The list of custom configuration IDs to query, up to 20 IDs.

**ListenerId ** String`optional` `Example: listenerId=lsn-3tihaugk2y3vj0wt****`

Query the custom configuration associated with the specified listener.

**ProjectName ** String `optional` `Example value: default`

The name of the project to which the custom configuration belongs.

**TagFilters.N.Key ** String[]`optional` `Example: TagFilters.1.Key=k1&TagFilters.2.Key=k2`

The tag key.

* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns custom configurations tagged with all the specified keys.

* Duplicate values are not allowed.

**TagFilters.N.Values.N ** String[]`optional` `Example: TagFilters.1.Values.1=v1&TagFilters.1.Values.2=v2&TagFilters.2.Values.1=v3`

The tag value.

* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns custom configurations that have any of the specified tag values for that key.

* Separate multiple tag values with an ampersand (&).

> **tip**

* > If this parameter is passed in, TagFilters.N.Key must be passed in first.

* > Passing an empty string queries for custom configurations with an empty tag value.

## Response parameters

**RequestId ** String`Example: 20210811152539010225146063030****`

Request ID.

**PageSize ** Integer`Example: 20`

The number of rows on the current page.

**PageNumber** Integer `Example: 1`

Current page number.

**TotalCount ** Integer`Example: 50`

Total number of custom configurations that match the criteria.

**CustomizedCfgs ** Object[]`Example: --`

Information of custom configurations that match the criteria.

**CustomizedCfgId ** String`Example: ccfg-3cj44nv0jhhxc6c6rrtet****`

ID of the custom configuration.

**CustomizedCfgName** String `Example: myCustomizedCfg`

Name of the custom configuration.

**CreateTime ** String`Example: 2021-08-11T16:37:37Z`

Creation time of the custom configuration.

**UpdateTime ** String`Example: 2021-08-11T16:37:37Z`

Last operation time of the custom configuration.

**CustomizedCfgContent ** String`Example: client_max_body_size 60M; keepalive_timeout 75s;`

The content of the custom configuration items to be modified. The specific rules are as follows:

* The length must not exceed 4096 characters, with different configuration items separated by ";".

* Currently supported configuration items include ssl_protocols, ssl_ciphers, client_max_body_size, keepalive_timeout, proxy_request_buffering, proxy_connect_timeout, add_header, client_header_timeout, proxy_read_timeout, proxy_send_timeout, client_body_timeout, send_timeout, and ssl_verify_depth. For details, see **Custom configuration items** at the end.

**Status ** String`Example: Active`

Status of the custom configuration.

* Active

* Configuring

* Creating

* Deleting

**Listeners ** String[]`Example: [ lsn-3tihaugk2y3vj0wt**** , lsn-2fe6fszjgeznk5oxruv0u**** ]`

ID of listeners associated with the custom configuration.

**Description ** String`Example: test`

Description of the custom configuration.

**ProjectName** String `Example: default`

The name of the project to which the custom configuration belongs.

**Tags ** Object[]`Example: --`

The tags associated with the custom configuration.

**Key ** String`Example: key`

The tag key of the custom tag.

**Value ** String`Example: value`

The tag value of the custom tag.

## Request examples

```JSON
GET /?Action=DescribeCustomizedCfgs&ProjectName=default&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "2026061214514121603709220665CC2A",
    "Action": "DescribeCustomizedCfgs",
    "Version": "2020-04-01",
    "Service": "alb",
    "Region": "cn-beijing"
  },
  "Result": {
    "RequestId": "20210811152539010225146063030****",
    "PageSize": 20,
    "PageNumber": 1,
    "TotalCount": 50,
    "CustomizedCfgs": [
      {
        "CustomizedCfgId": "ccfg-3cj44nv0jhhxc6c6rrtet****",
        "CustomizedCfgName": "myCustomizedCfg",
        "CreateTime": "2021-08-11T16:37:37Z",
        "UpdateTime": "2021-08-11T16:37:37Z",
        "CustomizedCfgContent": "client_max_body_size 60M;\nkeepalive_timeout 75s;",
        "Status": "Active",
        "Listeners": [
          "[ lsn-3tihaugk2y3vj0wt**** , lsn-2fe6fszjgeznk5oxruv0u**** ]"
        ],
        "Description": "test",
        "ProjectName": "default",
        "Tags": [
          {
            "Key": "key",
            "Value": "value"
          }
        ]
      }
    ]
  }
}
```

## Error codes

If the response body contains an Error field, it indicates the API request failed. This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Error-codes).

|**Status code** |**Error codes** |**Error message** |**Notes** |
|---|---|---|---|
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |LimitExceed.CustomizedCfg |You've reached the limit on the number of CustomizedCfgs that you can operate at a time. |You have reached the maximum number of custom configurations that can be operated on in a single request. |
|400 |InvalidCustomizedCfgName.Malformed |The specified CustomizedCfgName is malformed. |The specified CustomizedCfgName parameter format is invalid. |
|400 |LimitExceed.TagFilters.Values |You've reached the limit on the number of tag filter values that you can operate at a time. |You have reached the maximum number of tag values that can be operated on in a single request. |
|400 |InvalidTagFilters.Key.Malformed |The specified TagFilters.Key is malformed. |The specified TagFilters.Key parameter format is invalid. |
|400 |InvalidTagFilters.Value.Malformed |The specified TagFilters.Value is malformed. |The specified TagFilters.Value parameter format is invalid. |
|400 |InvalidTagFilters.Key.Duplicated |The specified TagFilters.Key is duplicated. |The specified TagFilters.Key is duplicated. |

**Custom configuration item content**

|**Configuration item** |**Notes** |**Value range** |**Default** |
|---|---|---|---|
|proxy_connect_timeout |Upstream backend connection timeout. |4~120s |4s |
|keepalive_timeout |Client\-server keep\-alive timeout. Set to 0 to disable keep\-alive. |0~900s |75s |
|client_max_body_size |* Maximum value of the client request body.<br><br>* If the value exceeds 256, proxy_request_buffering must be set to off. |1~30720M |60M |
|ssl_protocols |The version of the TLS protocol used. Default selection: TLSv1, TLSv1.1, TLSv1.2. ALB supports enabling TLSv1.3 for allowlisted users. To try it out, please submit a ticket. The specific rules for TLS protocol versions are as follows:<br><br><br>* Supports single or multiple selection. When selecting multiple versions, they must be selected consecutively.<br><br>* Duplicate protocol configurations are not supported. |Multiple selections: TLSv1, TLSv1.1, TLSv1.2, TLSv1.3 (available only to allowlisted users) |TLSv1 TLSv1.1 TLSv1.2 |
|proxy_request_buffering |* on: Indicates caching of the client request body. After the entire request body is received, it is forwarded to the backend server in chunks.<br><br>* off: Indicates no caching of the client request body. After receiving the request, it is immediately forwarded to the backend server. |On or off |on |
|ssl_ciphers |Cipher suite. Separate multiple cipher suites with colons (:). |* TLSv1.0 and TLSv1.1 support:<br><br>   * ECDHE\-ECDSA\-AES128\-SHA<br><br>   * ECDHE\-ECDSA\-AES256\-SHA<br><br>   * ECDHE\-RSA\-AES128\-SHA<br><br>   * ECDHE\-RSA\-AES256\-SHA<br><br>   * AES128\-SHA<br><br>   * AES256\-SHA<br><br>   * DES\-CBC3\-SHA<br><br>* TLSv1.2 supports:<br><br>   * ECDHE\-ECDSA\-AES128\-SHA<br><br>   * ECDHE\-ECDSA\-AES256\-SHA<br><br>   * ECDHE\-RSA\-AES128\-SHA<br><br>   * ECDHE\-RSA\-AES256\-SHA<br><br>   * AES128\-SHA<br><br>   * AES256\-SHA<br><br>   * DES\-CBC3\-SHA<br><br>   * ECDHE\-ECDSA\-AES128\-GCM\-SHA256<br><br>   * ECDHE\-ECDSA\-AES256\-GCM\-SHA384<br><br>   * ECDHE\-ECDSA\-AES128\-SHA256<br><br>   * ECDHE\-ECDSA\-AES256\-SHA384<br><br>   * ECDHE\-RSA\-AES128\-GCM\-SHA256<br><br>   * ECDHE\-RSA\-AES256\-GCM\-SHA384<br><br>   * ECDHE\-RSA\-AES128\-SHA256<br><br>   * ECDHE\-RSA\-AES256\-SHA384<br><br>   * AES128\-GCM\-SHA256<br><br>   * AES256\-GCM\-SHA384<br><br>   * AES128\-SHA256<br><br>   * AES256\-SHA256 |ECDH+AESGCM:DH+AESGCM:ECDH+AES256:DH+AES256:ECDH+AES128:DH+AES:ECDH+3DES:DH+3DES:RSA+AESGCM:RSA+AES:RSA+3DES:!aNULL:!MD5 |
|add_header |Add the specified fields to the response header. The specific rules are as follows:<br><br><br>* header key<br><br>   * Can only contain English letters, numbers, underscores (_), and hyphens (\-).<br><br>   * Length: 1 to 128 characters.<br><br>   * Keys must not be duplicated.<br><br>* value<br><br>   * Can only contain English letters, numbers, spaces, and the following special characters: _ \- \* , / \ : @ = .( ) ;.<br><br>   * If the header value contains special characters other than numbers and letters, enclose the entire value in double ("") or single ('') quotes, such as "POST, OPTIONS".<br><br>   * Length: 1 to 128 characters.<br><br>   * Must not contain "\r" or "\n".<br><br>* always<br><br>   * always is the third parameter of add_header and is optional<br><br>   * With the always parameter: The added custom response header will only be included for response codes 200, 201, 204, 206, 301, 302, 303, 304, 307, 308 (i.e., 2xx and 3xx codes are supported)<br><br>   * Without the always parameter: The added custom response header will be included for all response codes (2xx, 3xx, 4xx, and 5xx are all supported)<br><br>* A maximum of 10 custom response headers can be configured. |Configuration description for typical scenarios:<br><br><br>* Allow cross\-origin requests using different methods<br><br>   * Custom header name: Access\-Control\-Allow\-Methods<br><br>   * Custom header value: "POST, OPTIONS"<br><br>   * To also obtain cross\-origin response headers when the response code is 4xx or 5xx, specify the always parameter.<br><br>* Specifies which domain names are allowed to access the ALB<br><br>   * Custom header name: Access\-Control\-Allow\-Origin<br><br>   * Custom Header Value: A specific domain name. Using "\*" allows requests from any origin to access the ALB.<br><br>   * To also obtain cross\-origin response headers when the response code is 4xx or 5xx, specify the always parameter.<br><br><br>Configuration example:<br><br><br>* add_header Access\-Control\-Allow\-Methods "POST, OPTIONS";\r\n<br><br>* add_header Access\-Control\-Allow\-Methods "POST, OPTIONS" always;\r\n<br><br>* add_header Strict\-Transport\-Security "max\-age=63072000; includeSubdomains; preload";\r\n |\- |
|client_header_timeout |* Defines the timeout for reading the client request header.<br><br>* If the client does not transmit the entire header within this period, an HTTP 408 error (Request Timeout) will be returned to the client. |30\-120s |60s |
|proxy_read_timeout |* Defines the timeout for ALB to read a response from a backend server.<br><br>* This timeout applies only between two consecutive read operations, not to the entire response transmission.<br><br>* If the backend server does not transmit any data within this period, the connection will be closed. |30\-3600s |60s |
|proxy_send_timeout |* Defines the timeout for establishing a connection with a backend server.<br><br>* This timeout applies only between two consecutive write operations, not to the entire request transmission process.<br><br>* If the backend server does not receive any data within this period, the connection will be closed. |30\-3600s |60s |
|client_body_timeout |* Defines the timeout for reading the client request parameters.<br><br>* This timeout applies only to the interval between two consecutive read operations, not to the entire request transmission.<br><br>* If the client sends no data within this period, an HTTP 408 error (Request Timeout) is returned to the client. |30\-120s |60s |
|send_timeout |* Defines the timeout for sending a response to the client.<br><br>* This timeout applies only between two consecutive write operations, not to the entire response transmission process.<br><br>* If the client does not receive any content within this time, the connection will be closed. |1\-3600s |60s |
|ssl_verify_depth |Defines the verification depth for the client certificate chain. |3~10 |3 |
|ssl_session_timeout |* Defines the time for which the client retains the Session Ticket.<br><br>* After expiration, the client will delete the Ticket. |1\-60 minutes |10 minutes |
|proxy_buffer_size |Sets the buffer size for receiving backend responses. |4\-32k |4k |
|large_client_header_buffers |* Set the maximum number and size of buffers used for reading large client request headers.<br><br>* The request line must not exceed the size of one buffer, otherwise a 414 error is returned to the client. A request header field must not exceed the size of one buffer, otherwise a 400 error is returned to the client. |Maximum number input range: 4\-8.<br><br>Size input range: 8k–16 k. |Default value for the maximum quantity input range: 4.<br><br>Default value for the size input range: 8k. |
|more_set_input_headers |Add specified fields to the request header. The specific rules are as follows:<br><br><br>* header key<br><br>   * A string composed of underscores (_), hyphens (\-), letters, and numbers.<br><br>   * Length must not exceed 128 characters.<br><br>   * Cannot start with a hyphen (\-).<br><br>   * Duplicate values are not allowed.<br><br>* value<br><br>   * Must be either a variable or another string.<br><br>   * A string composed of letters, numbers, underscores (_), hyphens (\-), asterisks (\*), commas (,), forward slashes (/), at signs (@), equals signs (=), periods (.), parentheses, spaces, and single quotes. Must not contain semicolons (;).<br><br>   * Quotation marks (") can only appear at the very beginning and very end of the value.<br><br>   * No leading or trailing spaces are allowed.<br><br>   * Length must not exceed 128 characters.<br><br>* A maximum of 10 custom response headers can be configured. |* Header key is case\-insensitive. Not supported: x\-real\-ip, x\-forwarded\-for, x\-forwarded\-proto, x\-alb\-waf\-requestid, x\-alb\-waf\-real\-port, upgrade, connection, x\-vport, x\-vip, x\-clb\-cluster, x\-toutiao\-lb\-ip, x\-vni, content\-length, transfer\-encoding, keep\-alive, host, cookie, authority.<br><br>* When the value is a variable, the following are supported: $remote_addr, $proxy_add_x_forwarded_for, $remote_port, $scheme, $vport, $load_balancer_id |\- |
|proxy_pass_header |Specifies the backend response headers to be forcibly passed through. Such response headers will be forcibly passed through to the client. Even if the ALB has response headers with the same name, the specified headers from the backend server will not be overwritten. |Server |Server |
