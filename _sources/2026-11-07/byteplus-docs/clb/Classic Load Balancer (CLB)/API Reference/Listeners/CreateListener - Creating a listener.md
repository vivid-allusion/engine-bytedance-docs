---
title: "CreateListener - Creating a listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/CreateListener"
---

Call the CreateListener API to add a listener to the specified Classic Load Balancer (CLB) instance.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* When creating a UDP listener, the listening port is not already being listened to by another UDP listener.

* When creating a TCP/HTTP/HTTPS listener, the listening port is not being listened to by another TCP/HTTP/HTTPS listener.

* The CLB instance has bandwidth that is not exclusively occupied. If not, adjust the bandwidth exclusively occupied by existing listeners or upgrade the specifications of the CLB instance.

* Layer\-4 listeners (TCP and UDP protocols) support forwarding requests to backend servers with IPv4 or IPv6 addresses.

* Layer\-7 listeners (HTTP and HTTPS protocols) only support forwarding requests to IPv4 backend servers.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateListener&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|i1JZK7">必选</span> `Example: CreateListener`

Action to execute. Set the value to **CreateListener**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|F1g3yr">必选</span> `Example: 2020-04-01`

Current API version is **2020\-04\-01**.



**LoadBalancerId ** <span data-label="purple">String </span><span data-api-tag="require|HscRJw">必选</span> `Example: clb-bp1o94dp5i6ea****`

CLB instance ID.

You can call the [DescribeLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancers) API to query the CLB instance ID.



**ListenerName ** <span data-label="purple">String </span>`optional` `Example: mylistener`

Listener name.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, periods (.), underscores (_), and hyphens (\-).

* Length limit: 1 to 128 characters.

* If left blank, the listener name defaults to "protocol\-port".



**Description ** <span data-label="purple">String </span>`optional` `Example: This is a listener.`

Description of the listener.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

* Length limit: 0 to 255 characters.

* If left blank, it defaults to an empty string.



**Protocol ** <span data-label="purple">String </span><span data-api-tag="require|gGFpZJ">必选</span> `Example: TCP`

Listener protocol. Valid values:


* TCP

* UDP

* HTTP

* HTTPS



**Port ** <span data-label="purple">Integer </span><span data-api-tag="require|yjEKKW">必选</span> `Example: 80`

The port used by the listener to receive requests. Value range: 0\-65535.

When the parameter `Protocol` is "TCP" or "UDP", passing 0 is supported, indicating that full port listening is enabled.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Full port listening for layer 4 listeners is in the invite\-only Beta stage and temporarily only supports accounts that have completed enterprise certification to apply for trial. If you need a trial, contact your account manager.</div>




**StartPort ** <span data-label="purple">Integer </span>`optional` `Example: 80`

Start port for full port listening. Value range: 1\-65535.

When the parameter `Port` is "0", this parameter must be passed.



**EndPort ** <span data-label="purple">Integer </span>`optional` `Example: 100`

The end port for full port listening, with a value range of 1 to 65535.

When the parameter `Port` is "0", this parameter must be passed, and its value should be greater than `StartPort`.



**Scheduler ** <span data-label="purple">String </span>`optional` `Example: wrr`

Scheduling algorithm used by the listener. Valid values:


* wrr (default): Weighted Round Robin. Backend servers with higher weights are polled more frequently (with higher probability).

* wlc: Weighted Least Connection. This method maintains minimum connections and assigns a weight to each server based on its processing capacities of the server. Servers with higher weights receive a proportionally larger share of incoming requests.

* sh: Source IP Hash. Consistent Hashing Based on Source IP Address, requests from the same source IP address are dispatched to the same backend server.



**Cps ** <span data-label="purple">Integer </span>`optional` `Example: -1`

The upper limit of the number of new connections per second.


* \-1 (default value): No limit, meaning the maximum number of new connections of the CLB instance.

* Value range: 1 to the maximum number of new connections of the CLB instance.

   For CLB instance types, see [Product specifications](https://docs.byteplus.com/en/docs/clb/Product-Overview-02).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is currently in the invite\-only Beta stage. For a trial, contact your account manager.</div>




**MaxConnections ** <span data-label="purple">Integer </span>`optional` `Example: -1`

The upper limit of the maximum number of max connections.


* \-1 (default): No limit, which is the maximum number of max connections of the CLB instance.

* Value range: 1 to the maximum number of max connections of the CLB instance. For CLB instance types, see [Product specifications](https://docs.byteplus.com/en/docs/clb/Product-Overview-02).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is currently in the invite\-only Beta stage. For a trial, contact your account manager.</div>




**Bandwidth ** <span data-label="purple">Integer </span>`optional` `Example: 10`

The bandwidth cap of the listener, meaning this listener exclusively occupies the bandwidth of the CLB instance, in Mbps.


* \-1 (default value): This listener does not exclusively occupy the CLB bandwidth; it shares the non\-exclusively occupied bandwidth of the CLB instance with other listeners.

* Value range: 1 to the non\-exclusively occupied bandwidth of the CLB instance. For the CLB instance specification bandwidth, see [Product specifications](https://docs.byteplus.com/en/docs/clb/Product-Overview-02).



**ServerGroupId ** <span data-label="purple">String </span><span data-api-tag="require|pRufS2">必选</span> `Example: rsp-bp1o94dp5i6ea****`

ID of the backend server group associated with the listener.

You can call the [DescribeServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeServerGroups) API to query the backend server group ID.



**CertificateSource ** <span data-label="purple">String </span>`optional` `Example: clb`

Certificate source.


* clb (default): Certificate uploaded via CLB

* cert_center: Certificate uploaded via Certificate Center.



**CertificateId ** <span data-label="purple">String </span>`optional` `Example: cert-bp1o94dp5i6ea****`

ID of the certificate uploaded to CLB.

You can call the [DescribeCertificates](https://docs.byteplus.com/en/docs/clb/DescribeCertificates) API to query the certificate ID.



**CertCenterCertificateId ** <span data-label="purple">String </span>`optional` `Example: cert-bp1o94dp5i6eb****`

Certificate ID uploaded via the Certificate Center.

You can call the [DescribeCertificates](https://docs.byteplus.com/en/docs/clb/DescribeCertificates) API to query the certificate ID.



**CAEnabled ** <span data-label="purple">String </span>`optional` `Example: off`

Whether to enable mutual authentication.


* on: Enable.

* off (default): Do not enable.



**CACertificateId ** <span data-label="purple">String </span>`optional` `Example: pca_leaf_M6gaihuZRcO****`

The ID of the CA certificate for mutual authentication.



**HealthCheck.Enabled ** <span data-label="purple">String </span>`optional` `Example: on`

Whether the listener has health check enabled.


* on (default): Enable.

* off: Disable.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only when the value of this parameter is on are the parameters under <code>HealthCheck.****</code> valid.</div>




**HealthCheck.Interval ** <span data-label="purple">Integer </span>`optional` `Example: 2`

The interval for performing health checks. Value range: 1 to 300. Default value: 2. Unit: seconds.



**HealthCheck.Timeout ** <span data-label="purple">Integer </span>`optional` `Example: 2`

The response timeout for health checks. If the backend server does not respond correctly within the specified time, it is considered exception.

Value range: 1 to 60. Default: 2. Unit: seconds.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The response timeout must be less than or equal to the check interval.</div>




**HealthCheck.HealthyThreshold ** <span data-label="purple">Integer </span>`optional` `Example: 3`

The healthy threshold for health checks. If a backend server consecutively passes health checks for the specified number of times, it will be deemed normal.

Value range: 2 to 10, default: 3, unit: times.



**HealthCheck.UnhealthyThreshold** <span data-label="purple">Integer</span> `optional` `Example: 3`

The unhealthy threshold for health checks. If a backend server consecutively fails health checks for the specified number of times, it will be deemed exception.

Value range: 2 to 10, default: 3, unit: times.



**HealthCheck.UdpRequest** <span data-label="purple">String</span> `optional` `Example: Request123`

Request string for health checks.


* Only letters and numbers are allowed, with a maximum length of 64 characters.

* This parameter takes effect when the parameter `Protocol` is set to UDP and the parameter `HealthCheck.Enabled` is set to on.

* The values of the parameters `HealthCheck.UdpRequest` and `HealthCheck.UdpExpect` must either both be empty or both be non\-empty.



**HealthCheck.UdpExpect ** <span data-label="purple">String </span>`optional` `Example: Expect123`

Expected response string for health checks.


* Only letters and numbers are allowed, with a maximum length of 64 characters.

* This parameter takes effect when the parameter `Protocol` is set to UDP and the parameter `HealthCheck.Enabled` is set to on.

* The values of the parameters `HealthCheck.UdpRequest` and `HealthCheck.UdpExpect` must either both be empty or both be non\-empty.



**HealthCheck.Method ** <span data-label="purple">String </span>`optional` `Example: HEAD`

Health check method of listeners.

This parameter is valid only when `Protocol` is set to HTTP or HTTPS and `HealthCheck.Enabled` is set to on. Valid values:


* GET (default): The server must support the GET method.

* HEAD: The server returns only the HEAD header information, which reduces backend overhead but requires the server to support the HEAD method.



**HealthCheck.Domain ** <span data-label="purple">String </span>`optional` `Example: www.test.com`

The domain name for health checks must be configured as the actual externally accessible address of the backend server.


* This parameter is valid only when `Protocol` is set to HTTP or HTTPS and `HealthCheck.Enabled` is set to on.

* Must contain at least one dot (.) and cannot start or end with a dot (.).

* A single string consists of letters, numbers, hyphens (\-), and periods (.). Hyphens (\-) cannot appear at the beginning or end of the string.

* Length limit: 1 to 128 characters.

* When this parameter is not passed or no value is passed, it defaults to empty, indicating that the CLB uses the private IP addresses of each backend server for health checks.



**HealthCheck.URI ** <span data-label="purple">String </span>`optional` `Example: /test`

The path for health checks must be configured as the actual externally accessible address of the backend server.


* This parameter is valid only when `Protocol` is set to HTTP or HTTPS and `HealthCheck.Enabled` is set to on.

* Must start with a slash character (/).

* Only contains letters, numbers, hyphens (\-), underscores (_), slashes (/), periods (.), percent signs (%), question marks (?), #, &, and equals signs (=).

* Length limit: 1 to 128 characters.

* If this parameter is omitted or left unset, the default value is /.



**HealthCheck.HttpCode ** <span data-label="purple">String </span>`optional` `Example: http_2xx,http_3xx`

The HTTP status code indicates a successful health check.

This parameter is valid only when `Protocol` is set to HTTP or HTTPS and `HealthCheck.Enabled` is set to on. Valid values:


* http_2xx (default)

* http_3xx

* http_4xx

* http_5xx


Separate multiple status codes with half\-width commas (,).



**HealthCheck.Port ** <span data-label="purple">String </span>`optional` `Example: 80`

The health check port ranges from 1 to 65535.



**EstablishedTimeout ** <span data-label="purple">Integer </span>`optional` `Example: 800`

The connection timeout period of the listener.

This parameter is valid only when the parameter `Protocol` is set to TCP or UDP. Valid values:


* TCP protocol: 10\-900 seconds. Default: 900 seconds.

* UDP protocol: 1\-300 seconds. Default: 90 seconds.



**ClientHeaderTimeout ** <span data-label="purple">Integer </span>`optional` `Example: 60`

The timeout for reading the client_header_timeout. The client initiates a request to CLB. If the client does not transmit the entire header within the timeout period, CLB will return a 408 error code to the client, indicating a request timeout.


* Value range: 30\-120 seconds. Default: 60 seconds.

* This parameter is valid only when `Protocol` is set to HTTP or HTTPS.



**ClientBodyTimeout ** <span data-label="purple">Integer </span>`optional` `Example: 60`

The timeout for reading the client_body_timeout. The client initiates a request to CLB. If the client does not send any request body within the timeout period, CLB will return a 408 error code to the client, indicating a request timeout.


* This timeout applies only between two consecutive reads, not to the entire request transmission.

* Value range: 30\-120 seconds. Default: 60 seconds.

* This parameter is valid only when the `Protocol` parameter is set to HTTP or HTTPS.



**KeepaliveTimeout** <span data-label="purple">Integer</span> `optional` `Example: 60`

Keepalive timeout between the client and the CLB. If there is no access request within the timeout period, CLB will interrupt the current connection and re\-establish a new connection when the next request arrives.


* Value range: 0\-900 seconds. Default: 75 seconds.

* 0 indicates that keepalive is disabled.

* This parameter is valid only when `Protocol` is set to HTTP or HTTPS.



**ProxyConnectTimeout** <span data-label="purple">Integer</span> `optional` `Example: 60`

The connection establishment timeout between the CLB and a backend server. If the connection between CLB and the backend server is not established within the timeout period, the connection establishment is terminated.


* It is recommended to be greater than the health check timeout.

* Value range: 4\-120 seconds. Default: 4 seconds.

* This parameter is valid only when `Protocol` is set to HTTP or HTTPS.



**ProxySendTimeout ** <span data-label="purple">Integer </span>`optional` `Example: 60`

The timeout period for the CLB to transmit a request to a backend server. CLB initiates a request to the backend server. If the backend server does not receive any content within the timeout period, it will close this connection.


* This timeout is set only between two consecutive writes, not for the entire request transmission process.

* Value range: 30\-3600 seconds. Default: 60 seconds.

* This parameter is valid only when `Protocol` is set to HTTP or HTTPS.



**ProxyReadTimeout ** <span data-label="purple">Integer </span>`optional` `Example: 60`

The timeout for reading a response from the backend server. CLB initiates a request to the backend server. If the backend server that receives the request does not respond within the timeout period, this connection will be closed.


* This timeout applies only between two consecutive reads, not to the entire response transmission.

* Value range: 30\-3600 seconds. Default: 60 seconds.

* This parameter is valid only when `Protocol` is set to HTTP or HTTPS.



**SendTimeout ** <span data-label="purple">Integer </span>`optional` `Example: 60`

The timeout period for the CLB to send a response to the client. CLB sends a response to the client. If the client does not receive any content within the timeout period, the connection will be closed.


* This timeout applies only between two consecutive writes, not to the entire response transmission.

* Value range: 1–3600 seconds. Default: 60 seconds.

* This parameter is valid only when `Protocol` is set to HTTP or HTTPS.



**SecurityPolicyId ** <span data-label="purple">String </span>`optional` `Example: default_policy`

TLS security policy for HTTPS listeners.


* This parameter is valid only when the `Protocol` is set to HTTPS. Valid values:

* default_policy (default): Supports SSL v3, TLS v1.0, TLS v1.1, TLS v1.2.

* tls_cipher_policy_1_0: Supports TLS v1.0, TLS v1.1, and TLS v1.2.

* tls_cipher_policy_1_1: Supports TLS v1.1 and TLS v1.2.

* tls_cipher_policy_1_2: Supports TLS v1.2.

* tls_cipher_policy_1_2_strict: Supports TLS v1.2.

* tls_cipher_policy_1_3: Supports TLS v1.3.

* tls_cipher_policy_1_2_strict_with_1_3: Supports TLS v1.2 and TLS v1.3.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For details on the cipher suites supported by the above TLS security policies, see <a href="https://docs.byteplus.com/en/docs/clb/Creating-an-HTTPS-listener">Creating an HTTPS listener</a>.</div>


* <div data-tips="true" data-tips-type="tip">If not specified, the default configuration takes effect according to: <code>ECDH+AESGCM:DH+AESGCM:ECDH+AES256:DH+AES256:ECDH+AES128:DH+AES:ECDH+3DES:DH+3DES:RSA+AESGCM:RSA+AES:RSA+3DES:!aNULL:!MD5</code>.</div>


* <div data-tips="true" data-tips-type="tip">Security policies tls_cipher_policy_1_3 and tls_cipher_policy_1_2_strict_with_1_3 are in an invite\-only Beta stage. For trial requests, contact your account manager.</div>




**AclStatus ** <span data-label="purple">String </span>`optional` `Example: off`

Enable access control. Valid values:


* on: Enable.

* off (default): Do not enable.



**AclType ** <span data-label="purple">String </span>`optional` `Example: black`

Access control method. Valid values:


* white: Allowlist. When the listener listens to the traffic of the CLB, the CLB only forwards requests from IP addresses that are in the ACL associated with its allowlist.

* black (default): Denylist. When the listener listens to the traffic of the CLB, the CLB refuses to forward requests from IP addresses that are in the ACL associated with its allowlist.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the parameter <code>AclStatus</code> is set to <strong>on</strong>, <code>AclType</code> and <code>AclIds.N</code> are required.</div>




**AclIds.N ** <span data-label="purple">String </span>`optional` `Example: cl-3cj44nv0jhhxc6c6rrtet****`

The ID of the ACL bound to the listener.

You can call the [DescribeAcls](https://docs.byteplus.com/en/docs/clb/DescribeAcls) API to get the Access Control List (ACL) ID.


* Parameter \- N: Indicates the serial number of the ACL, with a maximum of 5.

* Separate multiple access control list IDs with ampersands ( & ).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the parameter <code>AclStatus</code> is set to <strong>on</strong>, <code>AclType</code> and <code>AclIds.N</code> are required.</div>




**ProxyProtocolType ** <span data-label="purple">String </span>`optional` `Example: off`

Enable the Proxy Protocol.

This parameter is valid only when the parameter `Protocol` is set to TCP or UDP. Valid values:


* off (default): Disable.

* standard: Enable.



**PersistenceType ** <span data-label="purple">String </span>`optional` `Example: off`

Session persistence type. Valid values:


* off (default): Session persistence is disabled.

* source_ip: Source IP address, valid only when parameter `Protocol` is TCP or UDP.

* insert: Implant cookies. This value is valid only when the parameter `Protocol` is HTTP or HTTPS and `Scheduler` is wrr.

* server: Rewrite cookie. This value is valid only when the parameter `Protocol` is HTTP or HTTPS and `Scheduler` is wrr.



**PersistenceTimeout ** <span data-label="purple">Integer </span>`optional` `Example: 10`

Session persistence timeout. Unit: seconds. The default value is 1000 seconds. The value range varies depending on the value of the parameter `PersistenceType`.


* When `PersistenceType` is set to source_ip, the value range is 1\-3600.

* When `PersistenceType` is set to insert, the value range is 1\-86400.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid when <code>PersistenceType</code> is set to source_ip or insert.</div>




**Cookie ** <span data-label="purple">String </span>`optional` `Example: cookie123`

The cookie name for session persistence configured on the backend server.


* This parameter is required and valid only when the parameter `PersistenceType` is set to server.

* Can only contain letters, numbers, underscores (_), and hyphens (\-).

* Length: 1 to 200 characters.



**Http2Enabled ** <span data-label="purple">String </span>`optional` `Example: off`

Listener enables frontend HTTP 2.0 protocol.

This parameter is valid only when the Protocol is set to HTTPS. Values:


* on: Enable.

* off (default): Do not enable.



**ConnectionDrainEnabled ** <span data-label="purple">String </span>`optional` `Example: on`

Listener enables Connection Drain feature.

This parameter is valid only when the parameter `Protocol` is set to TCP or UDP. Valid values:


* on: Enable.

* off (default): Do not enable.



**ConnectionDrainTimeout ** <span data-label="purple">Integer </span>`optional` `Example: 2`

Connection draining timeout period. Value range: 0 to 900 seconds.


* When the parameter `ConnectionDrainEnabled` is set to on, this parameter is required.

* When the parameter `ConnectionDrainEnabled` is set to off, this parameter is required.



**Enabled ** <span data-label="purple">String </span>`optional` `Example: on`

Enable the listener. Valid values:


* on (default): Enable.

* off: Disable.



**Tags.N.Key ** <span data-label="purple">String </span>`optional` `Example: key1`

The tag key of the custom tag.


* N represents the serial number of a tag key. Valid range: 1 to 20.

* Separate multiple tag keys with ampersands (&).

* It cannot start with `volc:` or `sys:` in any case form.

* It can be 1 to 128 characters in length. It may contain characters in different languages, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* If a tag key contains leading or trailing spaces, the system will automatically delete them.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Duplicate tag keys are not allowed for the same resource.</div>




**Tags.N.Value** <span data-label="purple">String</span> `optional` `Example: value1`

The tag value of the custom tag.


* N represents the serial number of the tag value. Valid range: 1–20.

* Separate multiple tag values with ampersands (&).

* The value can be 0 to 256 characters in length. If left blank, the parameter defaults to an empty value.

* The following characters are allowed: characters from all languages, numbers, spaces ( ), underscores (_), periods (.), colons (:), forward slashes (/), equal signs (=), plus signs (+), hyphens (\-), and the at symbol (@).

* Case\-sensitive.

* If a tag value starts or ends with a space, the system will automatically delete them.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To provide this parameter, provide <code>Tags.N.Key</code> first.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



**ListenerId ** <span data-label="purple">String </span>`Example: lsn-2fek3rgsxhrsw5oxruwec****`

Listener ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=CreateListener&Version=2020-04-01&LoadBalancerId=clb-bp1o94dp5i6ea****&Protocol=TCP&Port=80&ServerGroupId=rsp-bp1o94dp5i6ea****
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateListener",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "ListenerId": "lsn-2fek3rgsxhrsw5oxruwec****",
        "RequestId": "20210811152539010225146063030****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |EnhancedSchedulerEnable.UnSupport |The specified Listener not support EnhancedSchedulerEnable. |The specified listener does not support MLB listener. |
|400 |InvalidAclStatus.Malformed |The specified AclStatus is malformed. |The specified AclStatus parameter format is invalid. |
|400 |InvalidAclType.Malformed |The specified AclType is malformed. |The specified AclType parameter format is invalid. |
|400 |InvalidBandwidth.Malformed |The specified Bandwidth is malformed. |The format of specified Bandwidth is invalid. |
|400 |InvalidCACertificate.UnSupportAction |The specified CACertificate does not support this action, due to the content of the ca certificate is illegal. |The specified CA certificate is invalid and does not support the current action. |
|400 |InvalidCAEnabled.CACertificateIdMismatch |The specified CAEnabled not match with CACertificateId. |The specified HTTPS mutual authentication switch status does not match the CA certificate ID. |
|400 |InvalidCAEnabled.Malformed |The specified CAEnabled is malformed. |The specified CAEnabled parameter format is invalid. |
|400 |InvalidCAEnabled.ProtocolMismatch |The specified CAEnabled not match with Protocol. |The specified HTTPS mutual authentication switch does not match the listener protocol type. |
|400 |InvalidCertificate.UnSupportAction |The specified Certificate does not support this action, due to the content of the certificate is illegal. |The specified certificate is invalid and does not support the current action. |
|400 |InvalidCertificateLength.Malformed |The specified CertificateLength is malformed. |The specified CertificateLength parameter format is invalid. |
|400 |InvalidCertificateSource.CertCenterCertificateIdMismatch |The specified CertificateSource not match with CertCenterCertificateId. |The specified CertificateSource does not match CertCenterCertificateId. |
|400 |InvalidCertificateSource.CertificateIdMismatch |The specified CertificateSource not match with CertificateId. |The specified CertificateSource does not match CertificateId. |
|400 |InvalidCertificateSource.Malformed |The specified CertificateSource is malformed. |The format of the specified CertificateSource is invalid. |
|400 |InvalidClientBodyTimeout.Malformed |The specified ClientBodyTimeout is malformed. |The specified ClientBodyTimeout parameter format is invalid. |
|400 |InvalidClientBodyTimeout.ProtocolMismatch |The specified ClientBodyTimeout not match with Protocol. |The specified client request body timeout does not match the listener protocol type. |
|400 |InvalidClientHeaderTimeout.Malformed |The specified ClientHeaderTimeout is malformed. |The specified ClientHeaderTimeout parameter format is invalid. |
|400 |InvalidClientHeaderTimeout.ProtocolMismatch |The specified ClientHeaderTimeout not match with Protocol. |The specified client request header timeout does not match the listener protocol type. |
|400 |InvalidConnectionDrainEnabled.Malformed |The specified ConnectionDrainEnabled is malformed. |The specified ConnectionDrainEnabled parameter format is invalid. |
|400 |InvalidConnectionDrainTimeout.Malformed |The specified ConnectionDrainTimeout is malformed. |The specified ConnectionDrainTimeout parameter format is invalid. |
|400 |InvalidCookie.Malformed |The specified Cookie is malformed. |The specified Cookie parameter format is invalid. |
|400 |InvalidCps.Malformed |The specified Cps is malformed. |The specified Cps parameter format is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The specified Description parameter format is invalid. |
|400 |InvalidEnabled.Malformed |The specified Enabled is malformed. |The specified Enabled parameter format is invalid. |
|400 |InvalidEndPort.Malformed |The specified EndPort is malformed. |The specified EndPort parameter format is invalid. |
|400 |InvalidEnhancedSchedulerEnable.Malformed |The specified EnhancedSchedulerEnable is malformed. |The specified EnhancedSchedulerEnable parameter format is invalid. |
|400 |InvalidEstablishedTimeout.Malformed |The specified EstablishedTimeout is malformed. |The specified EstablishedTimeout parameter format is invalid. |
|400 |InvalidHealthCheck.Domain.Malformed |The specified HealthCheck.Domain is malformed. |The specified HealthCheck.Domain parameter format is invalid. |
|400 |InvalidHealthCheck.Enabled.Malformed |The specified HealthCheck.Enabled is malformed. |The specified HealthCheck.Enabled parameter format is invalid. |
|400 |InvalidHealthCheck.HealthyThreshold.Malformed |The specified HealthCheck.HealthyThreshold is malformed. |The specified HealthCheck.HealthyThreshold parameter format is invalid. |
|400 |InvalidHealthCheck.HttpCode.Malformed |The specified HealthCheck.HttpCode is malformed. |The specified HealthCheck.HttpCode parameter format is invalid. |
|400 |InvalidHealthCheck.Interval.Malformed |The specified HealthCheck.Interval is malformed. |The specified HealthCheck.Interval parameter format is invalid. |
|400 |InvalidHealthCheck.Method.Malformed |The specified HealthCheck.Method is malformed. |The specified HealthCheck.Method parameter format is invalid. |
|400 |InvalidHealthCheck.Port.Malformed |The specified HealthCheck.Port is malformed. |The specified HealthCheck.Port parameter format is invalid. |
|400 |InvalidHealthCheck.Timeout.Malformed |The specified HealthCheck.Timeout is malformed. |The specified HealthCheck.Timeout parameter format is invalid. |
|400 |InvalidHealthCheck.URI.Malformed |The specified HealthCheck.URI is malformed. |The specified HealthCheck.URI parameter format is invalid. |
|400 |InvalidHealthCheck.UdpExpect.Malformed |The specified HealthCheck.UdpExpect is malformed. |The specified HealthCheck.UdpExpect parameter format is invalid. |
|400 |InvalidHealthCheck.UdpRequest.Malformed |The specified HealthCheck.UdpRequest is malformed. |The specified HealthCheck.UdpRequest parameter format is invalid. |
|400 |InvalidHealthCheck.UnhealthyThreshold.Malformed |The specified HealthCheck.UnhealthyThreshold is malformed. |The specified HealthCheck.UnhealthyThreshold parameter format is invalid. |
|400 |InvalidHttp2Enabled.Malformed |The specified Http2Enabled is malformed. |The specified Http2Enabled parameter format is invalid. |
|400 |InvalidHttp2Enabled.ProtocolMismatch |The specified Http2Enabled not match with Protocol. |The specified HTTP2.0 switch does not match the listener protocol type. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidKeepaliveTimeout.Malformed |The specified KeepaliveTimeout is malformed. |The specified KeepaliveTimeout parameter format is invalid. |
|400 |InvalidKeepaliveTimeout.ProtocolMismatch |The specified KeepaliveTimeout not match with Protocol. |The specified client connection idle timeout does not match the listener protocol type. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified CLB's state is incompatible with this request. |
|400 |InvalidLoadBalancer.UnSupportAction |The specified LoadBalancer does not support this action. |The specified CLB does not support this action. |
|400 |InvalidLoadBalancerOrAcl.UnSupportAction |The specified LoadBalancer or Acl status does not support this action. |The specified CLB or ACL is in a state that does not support the current action. |
|400 |InvalidLoadType.Malformed |The specified LoadType is malformed. |The specified LoadType parameter format is invalid. |
|400 |InvalidMaxConnections.Malformed |The specified MaxConnections is malformed. |The specified MaxConnections parameter format is invalid. |
|400 |InvalidName.Malformed |The specified Name is malformed. |The specified Name format is invalid. |
|400 |InvalidParameter.ProtocolConflictsToaType |The specified Protocol and ToaType conflict. |The specified Protocol and ToaType parameters conflict. |
|400 |InvalidPersistenceTimeout.Malformed |The specified PersistenceTimeout is malformed. |The specified PersistenceTimeout parameter format is invalid. |
|400 |InvalidPersistenceType.EnhancedSchedulerMismatch |The specified PersistenceType and EnhancedSchedulerEnable are not matched. |The specified session persistence type does not match the MLB listener switch. |
|400 |InvalidPersistenceType.Malformed |The specified PersistenceType is malformed. |The specified PersistenceType parameter format is invalid. |
|400 |InvalidPersistenceType.ProtocolMismatch |The specified PersistenceType and Protocol are not matched. |The specified session persistence type does not match the protocol. |
|400 |InvalidPersistenceType.SchedulerMismatch |The specified PersistenceType and Scheduler are not matched. |The specified session persistence type does not match the scheduling algorithm. |
|400 |InvalidPort.Malformed |The specified Port is malformed. |The format of the specified Port is invalid. |
|400 |InvalidPort.NotAllowed |The specified Port is not allowed. |The specified listener port is not within the allowed usage range of the instance. |
|400 |InvalidPrivateKey.Malformed |The specified PrivateKey is malformed. |The specified PrivateKey parameter format is invalid. |
|400 |InvalidProject.Malformed |The specified Project is malformed. |The specified Project parameter format is invalid. |
|400 |InvalidProtocol.Malformed |The specified Protocol is malformed. |The specified Protocol parameter format is invalid. |
|400 |InvalidProtocol.ServerGroupIpVersionMismatch |The specified Protocol and ServerGroup IpVersion are not matched. |The specified protocol does not match the server group IP version. |
|400 |InvalidProxyConnectTimeout.Malformed |The specified ProxyConnectTimeout is malformed. |The specified ProxyConnectTimeout parameter format is invalid. |
|400 |InvalidProxyConnectTimeout.ProtocolMismatch |The specified ProxyConnectTimeout not match with Protocol. |The specified backend connection establishment timeout does not match the listener protocol type. |
|400 |InvalidProxyProtocolType.Malformed |The specified ProxyProtocolType is malformed. |The specified ProxyProtocolType parameter format is invalid. |
|400 |InvalidProxyReadTimeout.Malformed |The specified ProxyReadTimeout is malformed. |The specified ProxyReadTimeout parameter format is invalid. |
|400 |InvalidProxyReadTimeout.ProtocolMismatch |The specified ProxyReadTimeout not match with Protocol. |The specified backend response timeout does not match the listener protocol type. |
|400 |InvalidProxySendTimeout.Malformed |The specified ProxySendTimeout is malformed. |The specified ProxySendTimeout parameter format is invalid. |
|400 |InvalidProxySendTimeout.ProtocolMismatch |The specified ProxySendTimeout not match with Protocol. |The specified backend forwarding request timeout does not match the listener protocol type. |
|400 |InvalidPublicKey.Malformed |The specified PublicKey is malformed. |The specified PublicKey format is invalid. |
|400 |InvalidPublicKey.PrivateKeyMisMatch |The PublicKey and PrivateKey are not matched. |The specified public key does not match the private key. |
|400 |InvalidQuotaCode.Malformed |The specified QuotaCode is malformed. |The specified QuotaCode parameter format is invalid. |
|400 |InvalidResponseCheckEnabled.Malformed |The specified ResponseCheckEnabled is malformed. |The specified ResponseCheckEnabled parameter format is invalid. |
|400 |InvalidResponseCheckEnabled.ProtocolMismatch |The specified ResponseCheckEnabled not match with Protocol. |The specified response detection switch does not match the listener protocol type. |
|400 |InvalidScheduler.Malformed |The specified Scheduler is malformed. |The specified Scheduler parameter format is invalid. |
|400 |InvalidSecurityPolicyId.Malformed |The specified SecurityPolicyId is malformed. |The format of the specified SecurityPolicyId parameter is invalid. |
|400 |InvalidSecurityPolicyId.ProtocolMismatch |The specified SecurityPolicyId not match with Protocol. |The specified security policy ID does not match the listener protocol type. |
|400 |InvalidSendTimeout.Malformed |The specified SendTimeout is malformed. |The specified SendTimeout parameter format is invalid. |
|400 |InvalidSendTimeout.ProtocolMismatch |The specified SendTimeout not match with Protocol. |The specified client forwarding response timeout does not match the listener protocol type. |
|400 |InvalidServerGroup.ListenerMismatch |The specified ServerGroup.AnyPortEnabled and Listener.Port are not matched. |The specified AnyPortEnabled attribute of the backend server group does not match the Port setting of the listener. |
|400 |InvalidServerGroup.LoadBalancerMismatch |The specified ServerGroup and LoadBalancer are not matched. |The specified backend server group does not match CLB. |
|400 |InvalidSite.NotSupportBidirectionalAuthentication |The specified site does not support https bidirectional authentication. |The specified account environment does not have the HTTPS mutual authentication feature enabled. |
|400 |InvalidStartOrEndPort.Malformed |The specified StartOrEndPort is malformed. |The format of the specified StartOrEndPort is invalid. |
|400 |InvalidStartPort.Malformed |The specified StartPort is malformed. |The specified StartPort parameter format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey parameter format is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |InvalidToaType.Malformed |The specified ToaType is malformed. |The specified ToaType parameter format is invalid. |
|400 |LimitExceeded.AclNumbers |You've reached the limit on the number of ACL that you can associate. |The maximum number of associated ACLs has been reached. |
|400 |LimitExceeded.ServiceManagedTag |You've reached the limit on the number of service managed tags that you can create. |You have reached the limit for the number of managed resource tag key\-value pairs that can be created in a single request. |
|400 |LimitExceeded.TagOperation |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum number of tag entries that can be operated on in a single request. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'Protocol'. |This request is missing a required parameter. ensure your API request includes all required parameters, such as Protocol. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'Port'. |This request is missing a required parameter. ensure the request includes all required parameters, such as Port. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ConnectionDrainTimeout'. |This request is missing a required parameter. ensure the request includes all required parameters, such as ConnectionDrainTimeout. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'HealthCheck.Port'. |This request is missing a required parameter. ensure your API request includes all required parameters, such as HealthCheck.Port. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ServerGroupId'. |This request is missing a required parameter. ensure the request includes all required parameters, such as ServerGroupId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'Scheduler'. |This request is missing a required parameter. ensure the request includes all required parameters, such as Scheduler. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'AclIds'. |This request is missing a required parameter. ensure the request includes all required parameters, such as AclIds. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'LoadBalancerId'. |This request is missing a required parameter. ensure the request includes all required parameters, such as LoadBalancerId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'CertificateId'. |This request is missing a required parameter. ensure the request includes all required parameters, such as CertificateId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'LoadType'. |This request is missing a required parameter. ensure the request includes all required parameters, such as LoadType. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'CertCenterCertificateId'. |This request is missing a required parameter. ensure the request includes all required parameters, such as CertCenterCertificateId. |
|400 |OperationFailed.QueryCertificateService |The request for the specified resource operation failed due to an abnormal access issue with the certificate center service. |The action request on the specified resource failed due to an access exception with the Certificate Center service. |
|400 |OperationFailed.QueryPcaService |The request for the specified resource operation failed due to an abnormal access issue with the pca service. |The action request on the specified resource failed due to an access exception with the Certificate Center PCA service. |
|400 |QuotaExceed.ListenerNumberEachAcl |You've reached the limit on the number of listeners that you can associate. |The quota limit for the number of listeners that can be associated with an ACL has been reached. |
|400 |QuotaExceed.PortRangeListenerNumberEachInstance |You've reached the limit on the number of portRange listeners that you can create. |The quota limit for the number of full\-port listeners that can be created for a single instance has been reached. |
|400 |UnsupportedOperation.AccountArrears |The request on the specified instance is denied due to the account in arrears status. |The request on the specified instance is denied because the account is in arrears. |
|403 |Forbidden |You are not authorized to perform operations on the system tag. |No permission to tag the specified resource with a system tag. |
|403 |Forbidden |You are not authorized to perform operations on the specified service; for example, the 'ToaType'. |No permission to operate on the specified service, such as ToaType. |
|403 |Forbidden |You are not authorized to perform operations on the specified service; for example, the 'ResponseCheckEnabled'. |No permission to operate on the specified service, such as ResponseCheckEnabled. |
|403 |Forbidden |You are not authorized to perform operations on the specified service; for example, the 'Bandwidth'. |No permission to operate on the specified service, such as Bandwidth. |
|403 |Forbidden |You are not authorized to perform operations on the service managed tag. |No permission to tag the specified resource with managed tags. |
|403 |Forbidden |You are not authorized to perform operations on the specified service; for example, the 'Cps'. |No permission to operate the specified service, such as Cps. |
|403 |Forbidden |You are not authorized to perform operations on the certificate of certificate center. |You are not authorized to operate on the specified certificate from the certificate center. |
|403 |Forbidden |You are not authorized to perform operations on the specified service; for example, the 'MaxConnections'. |No permission to operate on the specified service, such as MaxConnections. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |No permission to perform actions on the specified service. |
|403 |InvalidResourceType.ServcieManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidAcl.NotFound |The specified ACL does not exist. |The specified ACL does not exist. |
|404 |InvalidCACertificate.NotFound |The specified CACertificate does not exist. |The specified CA certificate does not exist. |
|404 |InvalidCertificate.NotFound |The specified Certificate does not exist. |The specified certificate does not exist. |
|404 |InvalidExclusiveCluster.NotFound |The specified ExclusiveCluster does not exist. |The specified Exclusive Cluster does not exist. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified CLB does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup does not exist. |The specified server group does not exist. |
|409 |InvalidAclId.Conflict |The specified AclId already exists. |The specified ACL already exists. |
|409 |InvalidPort.Conflict |The specified Port already exists. |The specified port already exists. |
|412 |InvalidExclusiveCluster.Expired |The specified ExclusiveCluster has expired. |The specified Exclusive Cluster has expired. |
|412 |InvalidExclusiveCluster.UnPurchased |The specified ExclusiveCluster is not purchased. |The specified Exclusive Cluster is not purchased. |
|412 |InvalidLoadBalancer.Expired |The specified LoadBalancer has expired. |The specified CLB has expired. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
