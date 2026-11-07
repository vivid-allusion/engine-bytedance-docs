---
title: "ModifyListenerAttributes - Modifying the listener attributes"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ModifyListenerAttributes"
---

Call the ModifyListenerAttributes API to modify the specified listener.

## Instructions

When calling this API, if an optional parameter is not configured, its existing configuration remains unchanged.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyListenerAttributes&serviceCode=clb&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: ModifyListenerAttributes`

Action to execute. Set the value to **ModifyListenerAttributes**.

**Version ** String必选 `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.

**ListenerId ** String必选 `Example: lsn-2fek3rgsxhrsw5oxruwec****`

Listener ID.

You can call the [DescribeListeners](https://docs.byteplus.com/en/docs/clb/DescribeListeners) API to query the listener ID.

**ListenerName ** String`optional` `Example: mylistener`

Listener name.

* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters in length.

**Description ** String`optional` `Example: This is a listener.`

Description of the listener.

* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas ( ， ), and full\-width periods ( 。 ).

* The length limit is 0 to 255 characters.

**Scheduler ** String`optional` `Example: wrr`

Scheduling algorithm used by the listener. Valid values:

* wrr (default): Weighted Round Robin. A load balancing algorithm where backend servers with higher weights values receive more frequent polling attempts (higher probability).

* wlc (Weighted Least Connection): This method maintains minimum connections and assigns a weight to each server based on its processing capacities of the server. Servers with higher weights receive a proportionally larger share of incoming requests.

* sh (Source address hashing): A consistency hash based on the Source IP address, allowing the same source to be scheduled to the same backend server.

**Cps ** Integer`optional` `Example: -1`

The upper limit of the number of new connections per second.

* \-1: No limit, meaning the maximum number of new connections of the CLB instance.

* Value range: 1 to the maximum number of new connections of the CLB instance.

   For CLB instance types, see [Product specifications](https://docs.byteplus.com/en/docs/clb/Product-Overview-02).

> **tip**

> This feature is in the beta stage. If you need a trial, please contact your account manager.

**MaxConnections ** Integer`optional` `Example: -1`

The upper limit of the maximum number of concurrent connections.

* \-1: No limit, which is the maximum number of concurrent connections of the CLB instance.

* Value range: 1 to the maximum number of concurrent connections of the CLB instance. For CLB instance types, see [Product specifications](https://docs.byteplus.com/en/docs/clb/Product-Overview-02).

> **tip**

> This feature is in the beta stage. If you need a trial, please contact your account manager.

**Bandwidth ** Integer`optional` `Example: 10`

The peak bandwidth of the listener. Unit: Mbps.

* Setting to \-1 means that the listener does not specify a rate limit. In this case, the bandwidth peak of the listener defaults to the remaining bandwidth of the CLB instance specification.

* The maximum bandwidth peak of the listener cannot exceed the specification bandwidth of the CLB instance it belongs to. For the specification bandwidth of the CLB instance, see [Product specifications](https://docs.byteplus.com/en/docs/clb/Product-Overview-02).

**ServerGroupId ** String`optional` `Example: rsp-bp1o94dp5i6ea****`

ID of the backend service group associated with the listener.

* For HTTP/HTTPS listeners, this parameter represents the ID of the associated default backend server group.

   You can call the [DescribeServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeServerGroups) API to query the backend server group ID.

* After August 30, 2021, the default backend server group feature was introduced for layer\-7 listeners. When editing an existing layer\-7 listener, this parameter is required; otherwise, other attributes of the listener cannot be modified.

**CertificateSource ** String`optional` `Example: clb`

Certificate source.

* clb: CLB certificate management module.

* cert_center: Certificate Center.

**CertCenterCertificateId ** String`optional` `Example: cert-bp1o94dp5i6eb****`

Certificate ID from the Certificate Center.

**CertificateId ** String`optional` `Example: cert-bp1o94dp5i6ea****`

The certificate ID from the CLB Certificate Management module.

You can call the [DescribeCertificates](https://docs.byteplus.com/en/docs/clb/DescribeCertificates) API to query the certificate ID.

**CAEnabled ** String`optional` `Example: off`

Whether to enable mutual authentication.

* on: Enable.

* off: Disable.

**CACertificateId ** String`optional` `Example: pca_leaf_M6gaihuZRcO****`

The ID of the CA certificate for mutual authentication.

You can call the [ListLeafInstances](https://docs.byteplus.com/en/docs/6638/195535) API to query the certificate ID.

**HealthCheck.Enabled ** String`optional` `Example: on`

Whether the health check feature is enabled for the listener.

* on: Enable.

* off: Disable.

> **tip**

> Only when the value of this parameter is **on** are the parameters under HealthCheck.\*\*\*\* valid.

**HealthCheck.Timeout ** Integer`optional` `Example: 2`

The response timeout for health checks. If the backend server does not respond correctly within the specified time, it is considered "abnormal".

Value range: 1 to 60. Default value: 2. Unit: seconds.

> **tip**

> The response timeout must be less than or equal to the check interval.

**HealthCheck.HealthyThreshold ** Integer`optional` `Example: 3`

The healthy threshold for health checks. If a backend server consecutively passes health checks for the specified number of times, it will be deemed normal.

Value range: 2 to 10, default: 3, unit: times.

**HealthCheck.UnhealthyThreshold ** Integer`optional` `Example: 3`

The unhealthy threshold for health checks. If a backend server consecutively fails health checks for the specified number of times, it will be deemed abnormal.

Value range: 2 to 10, default: 3, unit: times.

**HealthCheck.UdpRequest ** String`optional` `Example: Request123`

The request string for health checks.

Only letters and numbers are allowed, with a maximum length of 64 characters.

> **tip**

* > This parameter takes effect when the parameter `Protocol` is set to UDP and the parameter `HealthCheck.Enabled` is set to on.

* > The values of the parameters `HealthCheck.UdpRequest` and `HealthCheck.UdpExpect` must either both be empty or both be non\-empty.

**HealthCheck.UdpExpect ** String`optional` `Example: Expect123`

Expected response string for health checks.

Only letters and numbers are allowed, with a maximum length of 64 characters.

> **tip**

* > This parameter takes effect when the parameter `Protocol` is set to UDP and the parameter `HealthCheck.Enabled` is set to on.

* > The values of the parameters `HealthCheck.UdpRequest` and `HealthCheck.UdpExpect` must either both be empty or both be non\-empty.

**HealthCheck.Interval ** Integer`optional` `Example: 2`

The interval for performing health checks. Value range: 1 to 300. Default value: 2. Unit: seconds.

**HealthCheck.Method ** String`optional` `Example: HEAD`

Health check method of listeners. Valid values:

* GET (default): The server must support the GET method.

* HEAD: The server returns only the HEAD header information, which reduces backend overhead but requires the server to support the HEAD method.

> **tip**

> This parameter takes effect when the `Protocol` is set to HTTP or HTTPS, and `HealthCheck.Enabled` is set to on.

**HealthCheck.Domain ** String`optional` `Example: www.test.com`

The domain name for health checks must be configured as the actual externally accessible address of the backend server.

* Must contain at least one dot (.) and cannot start or end with a dot (.).

* A single string consists of letters, numbers, hyphens (\-), and periods (.). Hyphens (\-) cannot appear at the beginning or end of the string.

* Length limit is 1 to 128 characters.

* When this parameter is not passed or no value is passed, it defaults to empty, indicating that the CLB uses the private IP addresses of each backend server for health checks.

> **tip**

> This parameter takes effect when the `Protocol` is set to HTTP or HTTPS, and `HealthCheck.Enabled` is set to on.

**HealthCheck.URI ** String`optional` `Example: /test`

The path for health checks must be configured as the actual externally accessible address of the backend server.

This parameter takes effect only when `Protocol` is set to HTTP or HTTPS, and `HealthCheck.Enabled` is set to on.

* Must start with a slash character (/).

* Only contains letters, numbers, hyphens (\-), underscores (_), slashes (/), periods (.), percent signs (%), question marks (?), #, &, and equals signs (=).

* Length limit is 1 to 128 characters.

* If this parameter is omitted or left unset, the default value is /.

**HealthCheck.HttpCode ** String`optional` `Example: "http_2xx,http_3xx"`

The HTTP status code indicates a successful health check.

This parameter takes effect only when `Protocol` is set to HTTP or HTTPS, and `HealthCheck.Enabled` is set to on. Valid values:

* http_2xx (default)

* http_3xx

* http_4xx

* http_5xx

Separate multiple status codes with half\-width commas (,).

**HealthCheck.Port ** String`optional` `Example: 80`

The backend server port for health checks, in the range 1\-65535.

**EstablishedTimeout ** Integer`optional` `Example: 800`

The connection timeout period of the listener.

This parameter is valid only when `Protocol` is set to TCP or UDP. Valid values:

* TCP protocol: 10\-900 seconds.

* UDP protocol: 1\-300 seconds.

**ClientHeaderTimeout ** Integer`optional` `Example: 60`

The timeout for reading the client_header_timeout. The client initiates a request to CLB. If the client does not transmit the entire header within the timeout period, CLB will return a 408 error code to the client, indicating a request timeout.

* Value range: 30\-120 seconds.

* This parameter is valid only when the `Protocol` is set to HTTP or HTTPS.

**ClientBodyTimeout ** Integer`optional` `Example: 60`

The timeout for reading the client_body_timeout. The client initiates a request to CLB. If the client does not send any request body within the timeout period, CLB will return a 408 error code to the client, indicating a request timeout.

* This timeout applies only between two consecutive read operations, not to the entire request transmission.

* Value range: 30\-120 seconds.

* This parameter is valid only when the `Protocol` is set to HTTP or HTTPS.

**KeepaliveTimeout ** Integer`optional` `Example: 60`

Keepalive timeout between the client and the CLB. If there is no access request within the timeout period, CLB will interrupt the current connection and re\-establish a new connection when the next request arrives.

* Value range: 0 to 900 seconds.

* 0 indicates that keepalive is disabled.

* This parameter is valid only when the `Protocol` is set to HTTP or HTTPS.

**ProxyConnectTimeout ** Integer`optional` `Example: 60`

The connection establishment timeout between the CLB and a backend server. If the connection between CLB and the backend server is not established within the timeout period, the connection establishment operation is terminated.

* It is recommended to be greater than the health check timeout.

* Value range: 4 to 120 seconds.

* This parameter is valid only when the `Protocol` is set to HTTP or HTTPS.

**ProxySendTimeout ** Integer`optional` `Example: 60`

The timeout period for the CLB to transmit a request to a backend server. CLB initiates a request to the backend server. If the backend server does not receive any content within the timeout period, it will close this connection.

* This timeout is set only between two consecutive write operations, not for the entire request transmission process.

* Value range: 30\-3600 seconds.

* This parameter is valid only when the `Protocol` is set to HTTP or HTTPS.

**ProxyReadTimeout ** Integer`optional` `Example: 60`

The timeout for reading a response from the backend server. CLB initiates a request to the backend server. If the backend server that receives the request does not respond within the timeout period, this connection will be closed.

* This timeout applies only between two consecutive read operations, not to the entire response transmission.

* Value range: 30\-3600 seconds.

* This parameter is valid only when the `Protocol` is set to HTTP or HTTPS.

**SendTimeout ** Integer`optional` `Example: 60`

The timeout period for the CLB to send a response to the client. CLB sends a response to the client. If the client does not receive any content within the timeout period, the connection will be closed.

* This timeout applies only between two consecutive write operations, not to the entire response transmission.

* Value range: 1\-3600 seconds.

* This parameter is valid only when the `Protocol` is set to HTTP or HTTPS.

**SecurityPolicyId ** String`optional` `Example: default_policy`

The TLS security policy of the listener.

This parameter is valid only when `Protocol` is set to HTTPS. Valid values:

* default_policy: Supports SSL v3, TLS v1.0, TLS v1.1, TLS v1.2.

* tls_cipher_policy_1_0: Supports TLS v1.0, TLS v1.1, and TLS v1.2.

* tls_cipher_policy_1_1: Supports TLS v1.1 and TLS v1.2.

* tls_cipher_policy_1_2: Supports TLS v1.2.

* tls_cipher_policy_1_2_strict: Supports TLS v1.2.

* For details on the cipher suites supported by the above TLS security policies except default_policy, see [Creating an HTTPS protocol listener](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTPS-listener).

* When default_policy is passed, the configuration takes effect according to: `ECDH+AESGCM:DH+AESGCM:ECDH+AES256:DH+AES256:ECDH+AES128:DH+AES:ECDH+3DES:DH+3DES:RSA+AESGCM:RSA+AES:RSA+3DES:!aNULL:!MD5`.

**AclStatus ** String`optional` `Example: off`

Enable access control. Valid values:

* on: Enable.

* off: Disable.

Configuring this parameter will clear the already configured values in the `AclType` and `AclIds` parameters.

> **tip**

> When the `AclStatus` parameter is set to **on**, `AclType` and `AclIds.N` are required.

**AclType** String `optional` `Example: black`

Method of access control. Valid values:

* white: Allowlist. When the listener listens to the traffic of the CLB, the CLB only forwards requests from IP addresses that are in the ACL associated with its allowlist.

* black: Denylist. When the listener listens to the traffic of the CLB, the CLB refuses to forward requests from IP addresses that are in the ACL associated with its denylist.

> **tip**

> When the `AclStatus` parameter is set to **on**, `AclType` and `AclIds.N` are required.

**AclIds.N ** String`optional` `Example: acl-3cj44nv0jhhxc6c6rrtet****`

The ID of the ACL bound to the listener.

You can call the [DescribeAcls](https://docs.byteplus.com/en/docs/clb/DescribeAcls) API to query the ACL ID.

* Parameter \- N: Indicates the serial number of ACL, with a value range of 1 to 5.

* Separate multiple access control list IDs with ampersands ( & ).

> **tip**

> When the `AclStatus` parameter is set to **on**, `AclType` and `AclIds.N` are required.

**ProxyProtocolType ** String`optional` `Example: off`

Enable the Proxy\-Protocol.

This parameter is valid only when `Protocol` is set to TCP or UDP. Valid values:

* off: Disable.

* standard: Enable.

**PersistenceType ** String`optional` `Example: off`

Session persistence type. Valid values:

* off: Session persistence disabled.

* source_ip: Indicates the source IP address; only effective for TCP/UDP protocols.

* insert: Indicates implant cookies; only effective for HTTP/HTTPS protocols and when `Scheduler` is "wrr".

* server: Indicates rewrite cookies; only effective for HTTP/HTTPS protocols and when `Scheduler` is "wrr".

**PersistenceTimeout ** Integer`optional` `Example: 10`

Session persistence timeout. The unit is seconds, and the value range varies depending on the `PersistenceType` parameter.

* When `PersistenceType` is set to source_ip, the value range is 1\-3600.

* When `PersistenceType` is set to insert, the value range is 1\-86400.

> **tip**

> This parameter takes effect when `PersistenceType` is set to source_ip or insert.

**Cookie ** String`optional` `Example: cookie123`

The cookie name for session persistence configured on the backend server.

* Can only contain letters, numbers, underscores (_), and hyphens (\-).

* Length: 1 to 200 characters.

> **tip**

> When `PersistenceType` is set to server, this parameter is required; when `PersistenceType` is set to other values, this parameter does not take effect.

**Http2Enabled ** String`optional` `Example: off`

Listener enables frontend HTTP 2.0 protocol.

This parameter is valid only when `Protocol` is set to HTTPS. Values:

* on: Enable.

* off: Disable.

**ConnectionDrainEnabled** String `optional` `Example: on`

Listener enables Connection Drain feature.

This parameter is valid only when `Protocol` is set to TCP or UDP. Values:

* on: Enable. Please continue to configure the timeout `ConnectionDrainTimeout`.

* off: Disable.

**ConnectionDrainTimeout ** Integer`optional` `Example: 2`

Connection draining timeout period.

* This parameter is valid only when `ConnectionDrainEnabled` is set to on.

* Value range: 0 to 900 seconds.

**Enabled ** String`optional` `Example: off`

Enable the listener. Valid values:

* on: Enable.

* off: Disable.

## Response parameters

**RequestId ** String`Example: 20210811152539010225146063030****`

Request ID.

## Request examples

```json
GET /?Action=ModifyListenerAttributes&Version=2020-04-01&ListenerId=lsn-2fek3rgsxhrsw5oxruwec****
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyListenerAttributes",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210811152539010225146063030****"
    }
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |EnhancedSchedulerEnable.UnSupport |The specified Listener not support EnhancedSchedulerEnable. |The specified listener does not support MLB listener. |
|400 |InvalidAclStatus.Malformed |The specified AclStatus is malformed. |The specified AclStatus parameter format is invalid. |
|400 |InvalidAclType.Malformed |The specified AclType is malformed. |The specified AclType parameter format is invalid. |
|400 |InvalidBandwidth.Malformed |The specified Bandwidth is malformed. |The format specified for Bandwidth is invalid. |
|400 |InvalidCACertificate.UnSupportAction |The specified CACertificate does not support this action, due to the content of the ca certificate is illegal. |The specified CA certificate is malformed and does not support the current operation. |
|400 |InvalidCAEnabled.CACertificateIdMismatch |The specified CAEnabled not match with CACertificateId. |The specified HTTPS mutual authentication switch status does not match the CA certificate ID. |
|400 |InvalidCAEnabled.Malformed |The specified CAEnabled is malformed. |The specified CAEnabled parameter format is invalid. |
|400 |InvalidCAEnabled.ProtocolMismatch |The specified CAEnabled not match with Protocol. |The specified HTTPS mutual authentication switch does not match the listener protocol type. |
|400 |InvalidCertificate.UnSupportAction |The specified Certificate does not support this action, due to the content of the certificate is illegal. |The specified certificate is malformed and does not support the current operation. |
|400 |InvalidCertificateLength.Malformed |The specified CertificateLength is malformed. |The specified CertificateLength format is invalid. |
|400 |InvalidCertificateSource.CertCenterCertificateIdMismatch |The specified CertificateSource not match with CertCenterCertificateId. |The specified CertificateSource does not match CertCenterCertificateId. |
|400 |InvalidCertificateSource.CertificateIdMismatch |The specified CertificateSource not match with CertificateId. |The specified CertificateSource does not match the CertificateId. |
|400 |InvalidCertificateSource.Malformed |The specified CertificateSource is malformed. |The format of the specified CertificateSource is invalid. |
|400 |InvalidClientBodyTimeout.Malformed |The specified ClientBodyTimeout is malformed. |The specified ClientBodyTimeout parameter format is invalid. |
|400 |InvalidClientBodyTimeout.ProtocolMismatch |The specified ClientBodyTimeout not match with Protocol. |The specified client request body timeout does not match the listener protocol type. |
|400 |InvalidClientHeaderTimeout.Malformed |The specified ClientHeaderTimeout is malformed. |The specified ClientHeaderTimeout parameter format is invalid. |
|400 |InvalidClientHeaderTimeout.ProtocolMismatch |The specified ClientHeaderTimeout not match with Protocol. |The specified client request header timeout does not match the listener protocol type. |
|400 |InvalidConnectionDrainEnabled.Malformed |The specified ConnectionDrainEnabled is malformed. |The specified ConnectionDrainEnabled parameter format is invalid. |
|400 |InvalidConnectionDrainTimeout.Malformed |The specified ConnectionDrainTimeout is malformed. |The specified ConnectionDrainTimeout parameter format is invalid. |
|400 |InvalidCookie.Malformed |The specified Cookie is malformed. |The specified Cookie parameter format is invalid. |
|400 |InvalidCps.Malformed |The specified Cps is malformed. |The specified Cps parameter format is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format specified for Description is invalid. |
|400 |InvalidEnabled.Malformed |The specified Enabled is malformed. |The specified Enabled format is invalid. |
|400 |InvalidEstablishedTimeout.Malformed |The specified EstablishedTimeout is malformed. |The specified EstablishedTimeout format is invalid. |
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
|400 |InvalidKeepaliveTimeout.Malformed |The specified KeepaliveTimeout is malformed. |The specified KeepaliveTimeout parameter format is invalid. |
|400 |InvalidKeepaliveTimeout.ProtocolMismatch |The specified KeepaliveTimeout not match with Protocol. |The specified client connection idle timeout does not match the listener protocol type. |
|400 |InvalidListener.UnSupportAction |The specified Listener does not support this action. |The specified listener does not support the current operation. |
|400 |InvalidListenerServerGroup.UnSupportAction |The specified Listener does not support this action. |The specified listener is not bound to a default backend server group, so the current operation is not supported. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified load balancer cannot respond to this request due to its status. |
|400 |InvalidLoadBalancer.UnSupportAction |The specified LoadBalancer does not support this action. |The specified CLB does not support this action. |
|400 |InvalidLoadBalancerOrAcl.UnSupportAction |The specified LoadBalancer or Acl status does not support this action. |The specified CLB is in a state that does not support the current operation. |
|400 |InvalidLoadType.Malformed |The specified LoadType is malformed. |The specified LoadType parameter format is invalid. |
|400 |InvalidMaxConnections.Malformed |The specified MaxConnections is malformed. |The specified MaxConnections format is invalid. |
|400 |InvalidName.Malformed |The specified Name is malformed. |The format specified for Name is invalid. |
|400 |InvalidPersistenceTimeout.Malformed |The specified PersistenceTimeout is malformed. |The specified PersistenceTimeout parameter format is invalid. |
|400 |InvalidPersistenceType.Malformed |The specified PersistenceType is malformed. |The specified PersistenceType parameter format is invalid. |
|400 |InvalidPersistenceType.ProtocolMismatch |The specified PersistenceType and Protocol are not matched. |The specified session persistence type does not match the protocol. |
|400 |InvalidPersistenceType.SchedulerMismatch |The specified PersistenceType and Scheduler are not matched. |The specified session persistence type does not match the scheduling algorithm. |
|400 |InvalidPrivateKey.Malformed |The specified PrivateKey is malformed. |The specified PrivateKey format is invalid. |
|400 |InvalidProtocol.Malformed |The specified Protocol is malformed. |The specified Protocol format is invalid. |
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
|400 |InvalidServerGroup.ListenerMismatch |The specified ServerGroup.AnyPortEnabled and Listener.Port are not matched. |The specified AnyPortEnabled type of the backend server group does not match the Port attributes of the listener. |
|400 |InvalidServerGroup.LoadBalancerMismatch |The specified ServerGroup and LoadBalancer are not matched. |The specified backend server group does not match CLB. |
|400 |InvalidSite.NotSupportBidirectionalAuthentication |The specified site does not support https bidirectional authentication. |The specified account environment does not have the HTTPS mutual authentication feature enabled. |
|400 |InvalidToaType.Malformed |The specified ToaType is malformed. |The specified ToaType parameter format is invalid. |
|400 |InvalidWafProtectionEnabled.Malformed |The specified WafProtectionEnabled is malformed. |The specified WafProtectionEnabled parameter format is invalid. |
|400 |LimitExceeded.AclNumbers |You've reached the limit on the number of ACL that you can associate. |The upper limit on the number of ACLs that can be associated has been reached. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ConnectionDrainTimeout'. |This request is missing a required parameter. Please ensure your request includes all required parameters, such as ConnectionDrainTimeout. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'CertCenterCertificateId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as CertCenterCertificateId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ListenerId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as ListenerId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'CertificateId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as CertificateId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'AclIds'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as AclIds. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'LoadType'. |This request does not contain required parameters. Please ensure the request includes all required parameters, such as LoadType. |
|400 |OperationFailed.QueryCertificateService |The request for the specified resource operation failed due to an abnormal access issue with the certificate center service. |The operation request on the specified resource failed due to an access exception with the Certificate Center service. |
|400 |OperationFailed.QueryPcaService |The request for the specified resource operation failed due to an abnormal access issue with the pca service. |The operation request on the specified resource failed due to an access exception with the Certificate Center PCA service. |
|400 |QuotaExceed.ListenerNumberEachAcl |You've reached the limit on the number of listeners that you can associate. |The quota limit for the number of listeners that can be associated with an ACL has been reached. |
|400 |UnsupportedOperation.AccountArrears |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|400 |WafProtectionEnabled.UnSupport |The specified Listener not support WafProtectionEnabled. |The specified listener does not support WAF inspection. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |Forbidden |You are not authorized to perform operations on the specified service; for example, the 'MaxConnections'. |No permission to operate on the specified service, such as MaxConnections. |
|403 |Forbidden |You are not authorized to perform operations on the certificate of certificate center. |You are not authorized to operate on the specified certificate from the certificate center. |
|403 |Forbidden |You are not authorized to perform operations on the specified service; for example, the 'Bandwidth'. |No permission to operate on the specified service, such as Bandwidth. |
|403 |Forbidden |You are not authorized to perform operations on the specified service; for example, the 'ToaType'. |No permission to operate on the specified service, such as ToaType. |
|403 |Forbidden |You are not authorized to perform operations on the specified service; for example, the 'Cps'. |No permission to operate on the specified service, such as Cps. |
|403 |Forbidden |You are not authorized to perform operations on the specified service; for example, the 'ResponseCheckEnabled'. |No permission to operate on the specified service, such as ResponseCheckEnabled. |
|403 |InvalidResourceType.ServcieManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidAcl.NotFound |The specified ACL does not exist. |The specified ACL does not exist. |
|404 |InvalidCACertificate.NotFound |The specified CACertificate does not exist. |The specified CA certificate does not exist. |
|404 |InvalidCertificate.NotFound |The specified Certificate does not exist. |The specified certificate does not exist. |
|404 |InvalidExclusiveCluster.NotFound |The specified ExclusiveCluster does not exist. |The specified Exclusive Cluster does not exist. |
|404 |InvalidListener.NotFound |The specified Listener does not exist. |The specified listener does not exist. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified load balancer does not exist. |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup does not exist. |The specified server group does not exist. |
|409 |InvalidAclId.Conflict |The specified AclId already exists. |The specified ACL already exists. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|412 |InvalidExclusiveCluster.Expired |The specified ExclusiveCluster has expired. |The specified Exclusive Cluster has expired. |
|412 |InvalidExclusiveCluster.UnPurchased |The specified ExclusiveCluster is not purchased. |The specified Exclusive Cluster is not purchased. |
|412 |InvalidLoadBalancer.Expired |The specified LoadBalancer has expired. |The specified CLB has expired. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
