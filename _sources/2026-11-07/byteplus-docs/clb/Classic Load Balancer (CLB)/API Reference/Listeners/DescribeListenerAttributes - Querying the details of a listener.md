---
title: "DescribeListenerAttributes - Querying the details of a listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeListenerAttributes"
---

Call the DescribeListenerAttributes API to view the detailed information of the specified listener.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeListenerAttributes&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|gvQ2KK">必选</span>`Example: DescribeListenerAttributes`

Action to execute. Set the value to **DescribeListenerAttributes**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|1KaUXL">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**ListenerId ** <span data-label="purple">String </span><span data-api-tag="require|F1jwFm">必选</span> `Example: lsn-2fek3rgsxhrsw5oxruwec****`

Listener ID.

You can call the [DescribeListeners](https://docs.byteplus.com/en/docs/clb/DescribeListeners) API to query the listener ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



**LoadBalancerId ** <span data-label="purple">String </span>`Example: clb-bp1o94dp5i6ea****`

The CLB instance ID to which the listener belongs.



**ListenerId ** <span data-label="purple">String </span>`Example: lsn-2fek3rgsxhrsw5oxruwec****`

Listener ID.



**ListenerName ** <span data-label="purple">String </span>`Example: mylistener`

Listener name.



**Description ** <span data-label="purple">String </span>`Example: test`

Description of the listener.



**Protocol ** <span data-label="purple">String </span>`Example: TCP`

The protocol of the listener.


* TCP

* UDP

* HTTP

* HTTPS



**Port ** <span data-label="purple">Integer </span>`Example: 80`

Listening port.


* 0: Enable full port listening. Full port listening is currently in beta stage. For trial requests, contact your account manager.

* Other ports: Specific listening ports.



**StartPort ** <span data-label="purple">Integer </span>`Example: 80`

Start port for full port listening.

This parameter is returned only when full port listening is enabled.



**End port ** <span data-label="purple">Integer </span>`Example: 100`

End port for full port monitoring.

This parameter is returned only when full port listening is enabled.



**Scheduler** <span data-label="purple">String</span> `Example: wrr`

Scheduling algorithm used by the listener.


* wrr (default): Weighted Round Robin. A load balancing algorithm where backend servers with higher weights values receive more frequent polling attempts (higher probability).

* wlc (Weighted Least Connection): This method maintains minimum connections and assigns a weight to each server based on its processing capacities of the server. Servers with higher weights receive a proportionally larger share of incoming requests.

* sh (Source address hashing): A consistency hash based on the Source IP address, allowing the same source to be scheduled to the same backend server.



**Cps ** <span data-label="purple">Integer </span>`Example: 10`

The maximum number of new connections per second for the listener.



**MaxConnections ** <span data-label="purple">Integer </span>`Example: 10`

The maximum number of max connections for the listener.



**Bandwidth ** <span data-label="purple">Integer </span>`Example: 10`

The peak bandwidth of the listener. Unit: Mbps.

Returns \-1, indicating that the listener does not have a rate limit specified. In this case, the bandwidth peak of the listener defaults to the remaining bandwidth of the CLB instance specification.



**ServerGroupId ** <span data-label="purple">String </span>`Example: rsp-bp1o94dp5i6ea****`

The ID of the backend server group associated with the TCP/UDP listener. The default backend server group ID associated with the HTTP/HTTPS listener.



**CertificateSource ** <span data-label="purple">String </span>`Example: clb`

Certificate source.


* clb: CLB certificate management module.

* cert_center: Certificate Center.



**CertCenterCertificateId ** <span data-label="purple">String </span>`Example: cert-bp1o94dp5i6eb****`

Certificate ID from the Certificate Center.



**CertificateId ** <span data-label="purple">String </span>`Example: cert-bp1o94dp5i6ea****`

The certificate ID from the CLB Certificate Management module.



**CAEnabled ** <span data-label="purple">String </span>`Example: off`

Whether to enable mutual authentication.


* on: Enable.

* off: Disable.



**CACertificateId ** <span data-label="purple">String </span>`Example: pca_leaf_M6gaihuZRcO****`

The CA certificate for mutual authentication.



**HealthCheck ** <span data-label="purple">Object </span>`Example: -`

Health check information.


**Enabled ** <span data-label="purple">String </span>`Example: off`

Whether the health check feature is enabled for the listener.


* on: Enable.

* off: Disable.



**UdpRequest ** <span data-label="purple">String </span>`Example: Request123`

The request string for performing health checks.

This parameter is returned only when a request string is specified for a UDP listener.



**UdpExpect ** <span data-label="purple">String </span>`Example: Expect123`

Expected response string for health checks.

This parameter is returned only when a request string is specified for a UDP listener.



**Interval ** <span data-label="purple">Integer </span>`Example: 2`

The time interval for performing health checks.



**Timeout ** <span data-label="purple">Integer </span>`Example: 2`

The response timeout for health checks. If the backend server does not respond correctly within the specified time, it is considered "abnormal".



**HealthyThreshold ** <span data-label="purple">Integer </span>`Example: 3`

The healthy threshold for health checks. If a backend server consecutively passes health checks for the specified number of times, it will be deemed normal.



**UnHealthyThreshold ** <span data-label="purple">Integer </span>`Example: 3`

The unhealthy threshold for health checks. If a backend server consecutively fails health checks for the specified number of times, it will be deemed abnormal.



**Method ** <span data-label="purple">String </span>`Example: GET`

Health check method of listeners.


* GET: The server must support the GET method.

* HEAD: The server returns only the HEAD header information, which reduces backend overhead but requires the server to support the HEAD method.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is not returned for TCP/UDP listeners.</div>




**Uri ** <span data-label="purple">String </span>`Example: /`

Health check path.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is not returned for TCP/UDP listeners.</div>




**Domain ** <span data-label="purple">String </span>`Example: www.test.com`

Health check domain name.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is not returned for TCP/UDP listeners.</div>




**HttpCode ** <span data-label="purple">String </span>`Example: http_2xx`

The HTTP status code indicates a successful health check.


* http_2xx

* http_3xx

* http_4xx

* http_5xx


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is not returned for TCP/UDP listeners.</div>




**Port ** <span data-label="purple">Integer </span>`Example: 80`

Backend server port of health check.


* When full port listening is enabled, this parameter is returned to indicate the port used for health checks.

* When full port listening is not enabled, this parameter is not returned, and health checks use the service port of the backend server.




**ProxyProtocolType ** <span data-label="purple">String </span>`Example: off`

Enable the Proxy\-Protocol.


* off: Disable.

* standard: Enable.



**PersistenceType ** <span data-label="purple">String </span>`Example: off`

Type of session persistence.


* off: Session persistence disabled.

* source_ip: Source IP address.

* insert: Implant cookies.

* server: Rewrite cookie.



**AclStatus ** <span data-label="purple">String </span>`Example: off`

Enable access control.


* on: Enable.

* off: Disable.



**AclType ** <span data-label="purple">String </span>`Example: black`

Method of access control.


* white: Allowlist. When the listener listens to the traffic of the CLB, the CLB only forwards requests from IP addresses that are in the ACL associated with its allowlist.

* black: Denylist. When the listener listens to the traffic of the CLB, the CLB refuses to forward requests from IP addresses that are in the ACL associated with its allowlist.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This is returned only when the <code>AclStatus</code> parameter is set to <strong>on</strong>.</div>




**AclIds ** <span data-label="purple">String[] </span>`Example: ["acl-2fe5excqgk6ww5oxruvcv****","acl-2febxt4pu0zy85oxruw0t****"]`

The ID of the ACL bound to the listener.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This is returned only when the <code>AclStatus</code> parameter is set to <strong>on</strong>.</div>




**PersistenceTimeout ** <span data-label="purple">Integer </span>`Example: 10`

Session persistence timeout, in seconds.



**Cookie ** <span data-label="purple">String </span>`Example: cookie123`

The cookie name for session persistence configured on the backend server.



**ConnectionDrainEnabled ** <span data-label="purple">String </span>`Example: on`

Listener enables Connection Drain feature.


* on: Enable.

* off: Disable.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the <code>Protocol</code> parameter returns HTTP or HTTPS, this parameter is fixed to return off.</div>




**ConnectionDrainTimeout ** <span data-label="purple">Integer </span>`Example: 2`

Timeout for connection draining, in seconds.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the parameter <code>ConnectionDrainEnabled</code> returns off, this parameter returns 0.</div>




**Http2Enabled ** <span data-label="purple">String </span>`Example: off`

Whether the HTTPS protocol listener enables the frontend HTTP/2.0 protocol.


* on: Enable.

* off: Disable.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is not returned for TCP, UDP, and HTTP protocol listeners.</div>




**EstablishedTimeout ** <span data-label="purple">Integer </span>`Example: 100`

The connection timeout period of the listener.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is returned only for TCP/UDP listeners.</div>




**ClientHeaderTimeout ** <span data-label="purple">Integer </span>`Example: 60`

The timeout for reading the client_header_timeout. The client initiates a request to CLB. If the client does not transmit the entire header within the timeout period, CLB will return a 408 error code to the client, indicating a request timeout.

This parameter is returned only for HTTP/HTTPS listeners.



**ClientBodyTimeout ** <span data-label="purple">Integer </span>`Example: 60`

The timeout for reading the client_body_timeout. The client initiates a request to CLB. If the client does not send any request body within the timeout period, CLB will return a 408 error code to the client, indicating a request timeout.


* This timeout applies only between two consecutive read operations, not to the entire request transmission.

* This parameter is returned only for HTTP/HTTPS listeners.



**KeepaliveTimeout ** <span data-label="purple">Integer </span>`Example: 60`

Keepalive timeout between the client and the CLB. If there is no access request within the timeout period, CLB will interrupt the current connection and re\-establish a new connection when the next request arrives.


* 0 indicates that keepalive is disabled.

* This parameter is returned only for HTTP/HTTPS listeners.



**ProxyConnectTimeout ** <span data-label="purple">Integer </span>`Example: 60`

The connection establishment timeout between the CLB and a backend server. If the connection between CLB and the backend server is not established within the timeout period, the connection establishment operation is terminated.

This parameter is returned only for HTTP/HTTPS listeners.



**ProxySendTimeout ** <span data-label="purple">Integer </span>`Example: 60`

The timeout period for the CLB to transmit a request to a backend server. CLB initiates a request to the backend server. If the backend server does not receive any content within the timeout period, it will close this connection.


* This timeout is set only between two consecutive write operations, not for the entire request transmission process.

* This parameter is returned only for HTTP/HTTPS listeners.



**ProxyReadTimeout ** <span data-label="purple">Integer </span>`Example: 60`

The timeout for reading a response from the backend server. CLB initiates a request to the backend server. If the backend server that receives the request does not respond within the timeout period, this connection will be closed.


* This timeout applies only between two consecutive read operations, not to the entire response transmission.

* This parameter is returned only for HTTP/HTTPS listeners.



**SendTimeout ** <span data-label="purple">Integer </span>`Example: 60`

The timeout period for the CLB to send a response to the client. CLB sends a response to the client. If the client does not receive any content within the timeout period, the connection will be closed.


* This timeout applies only between two consecutive write operations, not to the entire response transmission.

* This parameter is returned only for HTTP/HTTPS listeners.



**SecurityPolicyId ** <span data-label="purple">String </span>`Example: default_policy`

TLS security policy for HTTPS listeners. This parameter is returned only for HTTPS listeners.


* default_policy: Supports SSL v3, TLS v1.0, TLS v1.1, TLS v1.2.

* tls_cipher_policy_1_0: Supports TLS v1.0, TLS v1.1, TLS v1.2.

* tls_cipher_policy_1_1: Supports TLS v1.1, TLS v1.2.

* tls_cipher_policy_1_2: Supports TLS v1.2.

* tls_cipher_policy_1_2_strict: Supports TLS v1.2.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For details on the cipher suites supported by the above TLS security policies except default_policy, see <a href="https://docs.byteplus.com/en/docs/clb/Creating-an-HTTPS-listener">Creating an HTTPS protocol listener</a>.</div>


* <div data-tips="true" data-tips-type="tip">When default_policy is passed, the configuration takes effect according to: <code>ECDH+AESGCM:DH+AESGCM:ECDH+AES256:DH+AES256:ECDH+AES128:DH+AES:ECDH+3DES:DH+3DES:RSA+AESGCM:RSA+AES:RSA+3DES:!aNULL:!MD5</code>.</div>




**Status ** <span data-label="purple">String </span>`Example: Active`

Listener status.


* Creating

* Active: Running.

* Deleting

* Disabled



**Enabled ** <span data-label="purple">String </span>`Example: off`

Enable the listener.


* on: Enable.

* off: Disable.



**WafProtectionEnabled ** <span data-label="purple">String </span>`Example: off`

Whether to send traffic passing through the layer‑7 listener to the Web Application Firewall for inspection and filtering.


* on: Yes.

* off: No.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

Tag information.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




**CreateTime ** <span data-label="purple">String </span>`Example: 2021-08-11T16:37:37Z`

Creation time of listener.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-08-11T16:37:37Z`

Last operation time of the listener.



**DomainExtensions ** <span data-label="purple">Object[] </span>`Example: --`

The list of additional domains associated with the eligible listener.


**Domain ** <span data-label="purple">String </span>`Example: www.test.com`

Domain name.



**CertificateSource ** <span data-label="purple">String </span>`Example: cert_center`

Certificate source.


* cert_center: SSL certificate from the BytePlus Certificate Center.



**DomainExtensionId ** <span data-label="purple">String </span>`Example: de-***`

Additional domain ID.



**CertCenterCertificateId ** <span data-label="purple">String </span>`Example: cert-***`

Certificate ID.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeListenerAttributes&Version=2020-04-01&ListenerId=lsn-2fek3rgsxhrsw5oxruwec****
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeListenerAttributes",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "AclIds": [
            "acl-2fe5excqgk6ww5oxruvcv****",
            "acl-2febxt4pu0zy85oxruw0t****"
        ],
        "AclStatus": "off",
        "AclType": "black",
        "Bandwidth": 10,
        "CACertificateId": "pca_leaf_M6gaihuZRcO****",
        "CAEnabled": "off",
        "CertCenterCertificateId": "cert-bp1o94dp5i6eb****",
        "CertificateId": "cert-bp1o94dp5i6ea****",
        "CertificateSource": "clb",
        "ClientBodyTimeout": 60,
        "ClientHeaderTimeout": 60,
        "ConnectionDrainEnabled": "on",
        "ConnectionDrainTimeout": 2,
        "Cookie": "cookie123",
        "Cps": 10,
        "CreateTime": "2021-08-11T16:37:37Z",
        "Description": "test",
        "DomainExtensions": [
            {
                "Domain": "www.test.com",
                "CertificateSource": "cert_center",
                "DomainExtensionId": "de-***",
                "CertCenterCertificateId": "cert-***"
            }
        ],
        "Enabled": "off",
        "EndPort": 100,
        "EstablishedTimeout": 100,
        "HealthCheck": {
            "Uri": "/",
            "Port": 80,
            "Domain": "www.test.com",
            "Method": "GET",
            "Enabled": "off",
            "Timeout": 2,
            "HttpCode": "http_2xx",
            "Interval": 2,
            "UdpExpect": "Expect123",
            "UdpRequest": "Request123",
            "HealthyThreshold": 3,
            "UnHealthyThreshold": 3
        },
        "Http2Enabled": "off",
        "KeepaliveTimeout": 60,
        "ListenerId": "lsn-2fek3rgsxhrsw5oxruwec****",
        "ListenerName": "mylistener",
        "LoadBalancerId": "clb-bp1o94dp5i6ea****",
        "MaxConnections": 10,
        "PersistenceTimeout": 10,
        "PersistenceType": "off",
        "Port": 80,
        "Protocol": "TCP",
        "ProxyConnectTimeout": 60,
        "ProxyProtocolType": "off",
        "ProxyReadTimeout": 60,
        "ProxySendTimeout": 60,
        "RequestId": "20210811152539010225146063030****",
        "Scheduler": "wrr",
        "SecurityPolicyId": "default_policy",
        "SendTimeout": 60,
        "ServerGroupId": "rsp-bp1o94dp5i6ea****",
        "StartPort": 80,
        "Status": "Active",
        "Tags": [
            {
                "Key": "k1",
                "Value": "v1"
            }
        ],
        "UpdateTime": "2021-08-11T16:37:37Z",
        "WafProtectionEnabled": "off"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ListenerId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as ListenerId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|404 |InvalidListener.NotFound |The specified Listener does not exist. |The specified listener does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
