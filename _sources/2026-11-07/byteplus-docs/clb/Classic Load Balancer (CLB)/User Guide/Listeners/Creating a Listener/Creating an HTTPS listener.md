---
title: "Creating an HTTPS listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Creating-an-HTTPS-listener"
---

## Instructions

* The listener port to be added cannot be the same as other TCP, HTTP, or HTTPS listener ports under the same Classic Load Balancer (CLB) instance.

* A CLB instance cannot create new listeners when the aggregate bandwidth of its existing listeners equals the instance's maximum bandwidth limit. If you still need to create it, first see [Editing a listener](https://docs.byteplus.com/en/docs/clb/Editing-the-listener) to adjust the bandwidth of existing listeners, or see [Changing the instance specifications](https://docs.byteplus.com/en/docs/clb/CLB-instances-03) to upgrade the CLB instance specification, so that the total bandwidth is less than the bandwidth allowed by the CLB instance specification.

* Through Layer 7 listeners (HTTP and HTTPS protocols), IPv6 access requests are currently only supported when forwarded to IPv4 backend servers.

## Procedure

1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click **Edit listener** on the right side of the target CLB instance.

4. Click **Add listener** and see the table below to complete the basic configuration of the listener.

   |Parameter |Description |Sample |
   |---|---|---|
   |Listener name |Set the name of Listener. If left blank, it defaults to **Protocol\-port**, such as HTTPS\-80. |listener\-1 |
   |CLB protocol |Select the protocol type for CLB instance listener. |HTTPS |
   |Listening port |Refers to the listening port; the listener forwards access requests from this port to the backend server group. |443 |
   |Scheduling algorithm |Specify the rules that the listener follows when forwarding requests.<br><br><br>* Weighted Round Robin (WRR): Higher weights values receive more frequent polling attempts (higher probability).<br><br>* Weighted Least Connections (WLC): First calculate the current connections/weight value of the backend server, then dispatch the request to the backend server with the smallest value.<br><br>* Source IP Hash (SH): A consistency hash based on the Source IP address, allowing the same source to be scheduled to the same backend server. |Weighted Round Robin (WRR) |

5. Configure the timeout period based on the table below.

   |Parameter |Description |Sample |
   |---|---|---|
   |keepalive_timeout |Enter the keepalive timeout between the client and the CLB. If there is no access request within the timeout period, CLB will interrupt the current connection and re\-establish a new connection when the next request arrives.<br><br>Input range: 0–900 seconds; 0 disables keepalive. |75 seconds |
   |client_header_timeout |Enter the timeout for reading client request headers.​ The client initiates a request to CLB. If the client does not transmit the entire header within the timeout period, CLB will return a 408 error code to the client, indicating a request timeout.<br><br>Input range: 30–120 seconds. |60 seconds |
   |client_body_timeout |Enter the timeout for reading the client_body_timeout. The client initiates a request to CLB. If the client does not send any request body within the timeout period, CLB will return a 408 error code to the client, indicating a request timeout.<br><br><br>* This timeout applies only between two consecutive read operations, not to the entire request transmission.<br><br>* Input range: 30–120 seconds. |60 seconds |
   |send_timeout |Enter the timeout period for the CLB to send a response to the client. CLB sends a response to the client. If the client does not receive any content within the timeout period, the connection will be closed.<br><br><br>* This timeout applies only between two consecutive write operations, not to the entire response transmission.<br><br>* Input range: 1 to 3600 seconds. |60 seconds |
   |proxy_read_timeout |Enter the timeout for reading a response from the backend server. CLB initiates a request to the backend server. If the backend server that receives the request does not respond within the timeout period, this connection will be closed.<br><br><br>* This timeout applies only between two consecutive read operations, not to the entire response transmission.<br><br>* Input range: 30–3600 seconds. |60 seconds |
   |proxy_send_timeout |Enter the timeout period for the CLB to transmit a request to a backend server. CLB initiates a request to the backend server. If the backend server does not receive any content within the timeout period, it will close this connection.<br><br><br>* This timeout is set only between two consecutive write operations, not for the entire request transmission process.<br><br>* Input range: 30–3600 seconds. |60 seconds |
   |proxy_connect_timeout |Enter the connection establishment timeout between the CLB and a backend server. If the connection between CLB and the backend server is not established within the timeout period, the connection establishment operation is terminated.<br><br><br>* It is recommended to be greater than the health check timeout.<br><br>* Input range: 4\-120 seconds. |4 seconds |

6. See the table below to configure more advanced features for the listener.

   |Parameter |Description |Sample |
   |---|---|---|
   |Access control |Indicates whether the listener applies denylist/allowlist control to access requests, i.e., allows or denies access from certain IPs. Default is disabled. For details, see [ACL overview](https://docs.byteplus.com/en/docs/clb/Access-control-list-01).<br><br>After enabling access control, select the control method and configure the policy group name.<br><br><br>* **Control method**<br><br>   * Denylist: Denies access to the CLB instance from IPs in the selected policy group. If no IP is added to the selected policy group, all source IPs are allowed to access this listener.<br><br>   * Allowlist: Only allows IPs in the selected policy group to access the CLB instance. If no IP is added to the selected policy group, all source IPs are denied access to this listener. Set this carefully.<br><br>* **Policy group name**<br><br>   Select an access control policy group; the IPs in the policy group will be added to the listener's denylist or allowlist. Up to 5 policy groups can be selected. If no policy group exists yet, click **Create access control policy group** in the dropdown and see [Creating a policy group](https://docs.byteplus.com/en/docs/clb/Managing-access-control-policy-groups). |Enable, denylist, policy01 |
   |Session persistence |When the scheduling algorithm is **Weighted Round Robin (WRR)** , enabling session persistence for the listener is optional.<br><br>After session persistence is enabled, CLB forwards requests from the same client to the same backend server based on cookies. Select the cookie handling method as needed and set the session persistence timeout or cookie name.<br><br>**Cookie handling method**: Supports both Implant Cookie and Rewrite Cookie.<br><br><br>* **Cookie insertion**: The CLB notes the backend server to which the client's request is initially forwarded and injects Cookies (CLBSERVERID and CLBSERVERCORSID) into the response before forwarding it to the client. When the client subsequently initiates access requests carrying this cookie information, the CLB forwards the requests to the corresponding backend server.<br><br>   When selecting this method, you must specify the cookie expiration time, i.e., the **Session persistence timeout**. The session persistence timeout defaults to 1000 seconds, with a range of 1–86400 seconds.<br><br>* **Rewrite Cookie**: You define the name of the backend cookie to be rewritten. When the client's first request is responded to by the backend server and reaches CLB, the CLB locates the specified cookie name in the response and rewrites it before forwarding the response to the client. When the client subsequently initiates access requests carrying the specified cookie information, the CLB forwards the requests to the corresponding backend server.<br><br>   When selecting this method, you must specify the cookie to be injected into the response, namely **Cookie name**.<br><br>   > **tip**<br>   <br><br>   > If the cookie in the backend server's response does not match the cookie name you specified, the CLB will not rewrite the cookie and will forward requests normally according to the scheduling algorithm you set.<br>    |Enable, implant Cookie, 1000 seconds |
   |Enable HTTP 2.0 |Choose whether to enable HTTP 2.0 as the frontend protocol version of the CLB.<br><br>HTTP 2.0 is a secure and efficient next\-generation HTTP transport protocol, backward compatible with HTTP 1.X. If you want HTTPS services to be more secure, you can enable HTTP 2.0 when configuring an HTTPS protocol listener. |Disable |
   |Bandwidth cap |Choose whether to enable bandwidth throttling for the listener.<br><br>After enabling, you must set the bandwidth upper limit for the listener. The maximum value is the remaining unallocated bandwidth of the CLB instance specification to which the listener belongs, in Mbps. |Enable, 100Mbps |
   |New connections cap |Enter the upper limit of new connections as needed.<br><br><br>* Value range: 1 to the maximum of new connections. The default value is CLB's maximum new connections.<br><br>* When new connections captured by the listener exceed the configured threshold, excess connections will be discarded and not forwarded to the backend server.<br><br><br>> **tip**<br><br><br>> This feature is currently in the invite\-only Beta stage. For trial requests, please contact your account manager.<br> |。。30000 |
   |Max connections cap |Type CLB's maximum limit of max connections as needed.<br><br><br>* Value range: 1 to the CLB maximum limit of max connections. Default value: CLB Max Connections.<br><br>* When max connections captured by the listener exceed the configured threshold, excess connections will be discarded and not forwarded to the backend server.<br><br><br>> **tip**<br><br><br>> This feature is currently in the invite\-only Beta stage. For trial requests, please contact your account manager.<br> |300000 |
   |Tag |A tag consists of a key\-value pair and is used for categorizing and searching resources. For more information about tags, see [Tag management](https://docs.byteplus.com/en/docs/clb/Tag-management).<br><br>Click the Add icon, input the tag key and tag value, and add a tag for the listener. |* Tag key: listener\-key<br><br>* Tag value: listener\-test |

7. Click **Next step** to configure the SSL certificate.

   |Parameters |Description |Sample |
   |---|---|---|
   |Certificate source |Select the certificate source; supports BytePlus Certificate Center and the CLB certificate management module.<br><br>> **tip**<br><br><br><br>* > When using a certificate from BytePlus Certificate Center for the first time, complete the cross\-service access authorization as prompted.<br><br><br>* > To facilitate unified certificate management, CLB is already integrated with BytePlus Certificate Center. We recommend uploading certificates via the [Certificate Center console](https://console-stable.volcanicengine.com/certificate-center/ssl/overview?). In the Certificate Center, you can perform certificate purchase, upload, renewal, and deletion in one stop.<br> |BytePlus Certificate Center |
   |Select server certificate |Select a server certificate from the dropdown. |xx\-certificate\-xx |
   |TLS security policy |Select whether to enable the TLS (Transport Layer Security) security policy. |Yes |
   |Select policy |Select a TLS security policy. Supports tls_cipher_policy_1_0, tls_cipher_policy_1_1, tls_cipher_policy_1_2, and tls_cipher_policy_1_2_strict, tls_cipher_policy_1_3, and tls_cipher_policy_1_2_strict_with_1_3. The TLS protocols and cipher suites supported by different TLS security policies are as follows:<br><br><br>* Supported TLS protocol versions:<br><br>   * **tls_cipher_policy_1_0**: Includes TLS v1.0, TLS v1.1, TLS v1.2.<br><br>   * **tls_cipher_policy_1_1**: Includes TLS v1.1, TLS v1.2.<br><br>   * **tls_cipher_policy_1_2**: Includes TLS v1.2.<br><br>   * **tls_cipher_policy_1_2_strict**: Includes TLS v1.2.<br><br>   * **tls_cipher_policy_1_3**: Includes TLS v1.3.<br><br>   * **tls_cipher_policy_1_2_strict_with_1_3**: Includes TLS v1.2 and TLS v1.3.<br><br>* Supported cipher suites:<br><br>   * **tls_cipher_policy_1_0, tls_cipher_policy_1_1, tls_cipher_policy_1_2**: ECDHE\-ECDSA\-AES128\-GCM\-SHA256, ECDHE\-ECDSA\-AES256\-GCM\-SHA384, ECDHE\-ECDSA\-AES128\-SHA256, ECDHE\-ECDSA\-AES256\-SHA384, ECDHE\-RSA\-AES128\-GCM\-SHA256, ECDHE\-RSA\-AES256\-GCM\-SHA384, ECDHE\-RSA\-AES128\-SHA256, ECDHE\-RSA\-AES256\-SHA384, AES128\-GCM\-SHA256, AES256\-GCM\-SHA384, AES128\-SHA256, AES256\-SHA256, ECDHE\-ECDSA\-AES128\-SHA, ECDHE\-ECDSA\-AES256\-SHA, ECDHE\-RSA\-AES128\-SHA, ECDHE\-RSA\-AES256\-SHA, AES128\-SHA, AES256\-SHA, DES\-CBC3\-SHA.<br><br>   * **tls_cipher_policy_1_2_strict**: ECDHE\-ECDSA\-AES128\-SHA, ECDHE\-ECDSA\-AES256\-SHA, ECDHE\-RSA\-AES128\-SHA, ECDHE\-RSA\-AES256\-SHA, ECDHE\-ECDSA\-AES128\-GCM\-SHA256, ECDHE\-ECDSA\-AES256\-GCM\-SHA384, ECDHE\-ECDSA\-AES128\-SHA256, ECDHE\-ECDSA\-AES256\-SHA384, ECDHE\-RSA\-AES128\-GCM\-SHA256, ECDHE\-RSA\-AES256\-GCM\-SHA384, ECDHE\-RSA\-AES128\-SHA256, ECDHE\-RSA\-AES256\-SHA384.<br><br>   * **tls_cipher_policy_1_3: ** TLS_AES_128_GCM_SHA256, TLS_AES_256_GCM_SHA384, TLS_CHACHA20_POLY1305_SHA256<br><br>   * **tls_cipher_policy_1_2_strict_with_1_3: ** ECDHE\-ECDSA\-AES128\-SHA, ECDHE\-ECDSA\-AES256\-SHA, ECDHE\-RSA\-AES128\-SHA, ECDHE\-RSA\-AES256\-SHA, ECDHE\-ECDSA\-AES128\-GCM\-SHA256, ECDHE\-ECDSA\-AES256\-GCM\-SHA384, ECDHE\-ECDSA\-AES128\-SHA256, ECDHE\-ECDSA\-AES256\-SHA384, ECDHE\-RSA\-AES128\-GCM\-SHA256, ECDHE\-RSA\-AES256\-GCM\-SHA384, ECDHE\-RSA\-AES128\-SHA256, ECDHE\-RSA\-AES256\-SHA384, TLS_AES_128_GCM_SHA256, TLS_AES_256_GCM_SHA384, TLS_CHACHA20_POLY1305_SHA256<br><br><br>> **tip**<br><br><br>> Policy tls_cipher_policy_1_3, tls_cipher_policy_1_2_strict_with_1_3 is in an invite\-only Beta stage. For trial requests, please contact your account manager.<br> |tls_cipher_policy_1_2 |

8. Click **Next step** to configure the default backend server group.

   1. Select the addition method and backend server group as needed.

      * If a backend server group that meets your needs already exists, you can select it.

      * If backend servers are unavailable, you can add a new one. For more information, see [Creating a backend server](https://docs.byteplus.com/en/docs/clb/Creating-a-server-group).

   2. Click **Next step** to add backend servers to the backend server group.

      Select the addition method as needed and configure the backend servers.

      * If backend servers are available, you can choose Add now, then add backend servers and configure ports and weights for them. For more information, see [Adding a backend server](https://docs.byteplus.com/en/docs/clb/Adding-a-server).

      * If no backend servers are available, choose to add them after the listener is created.

   > **tip**

   * > After the listener is created, the platform automatically creates a default forwarding rule and associates it with the default backend server group. The default forwarding rule has an empty domain and a URL of `/`, meaning it can forward requests to any domain and URL. When a request cannot match other forwarding rules in the listener, it is forwarded to the default backend server group via the default forwarding rule. For more information on forwarding rules, see [Configuring a forwarding rule](https://docs.byteplus.com/en/docs/clb/Configuring-a-forwarding-rule-01).

   * > When selecting an existing backend server group or adding a backend server to a server group, ensure the security group allows traffic using the same protocol as the listener by seeing [Configuring a backend server security group](https://docs.byteplus.com/en/docs/clb/Configuring-a-server-security-group).

9. Click **Next step** to enter the health check configuration page, as shown below.

   Keep the health check configuration here at the default values. If modification is required, see [Configuring the health check](https://docs.byteplus.com/en/docs/clb/Editing-health-check) for detailed parameter descriptions.

   > **tip**

   > After health check is configured, the CLB instance periodically sends requests to backend servers to test their running status and determine whether they are available. If a backend server is detected to be in poor health, traffic will stop being forwarded to it and will be redirected to other normally functioning backend servers.

10. Click **Next step** to review all listener configurations and complete the listener creation.

   * If the configuration information is incorrect, click the edit icon to return to the corresponding page and change the configuration.

   * After confirming the configuration is correct, click **Add** to complete the listener creation.

## What to do next

* HTTPS listeners enable Gzip data compression by default.

   When a client request carries the `accept-encoding: gzip` header, if the backend server returns a file of a specific type (including text/plain, text/css, text/xml, application/xml, text/javascript, application/x‑javascript, application/json, application/javascript, application/x‑protobuf) to the client, the CLB compresses it before returning it to the client.

* In addition to forwarding traffic to servers in the default backend server group, you can also add forwarding rules to forward traffic to servers in other backend server groups. For specific steps, see [Configuring a forwarding rule](https://docs.byteplus.com/en/docs/clb/Configuring-a-forwarding-rule-01).

## Related documentation

[CreateListener](https://docs.byteplus.com/en/docs/clb/CreateListener)
