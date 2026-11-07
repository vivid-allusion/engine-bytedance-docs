---
title: "Adding a listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Adding-a-listener"
---

## Scenarios

After an NLB instance is created, at least one listener must be configured to forward traffic from the client to the backend server.

## Action notes

* Within the same NLB instance, TLS and TCP listeners cannot share the same port. However, both can coexist on the same port with a UDP listener.

* TCP and TLS listeners must be associated with TCP server groups, while UDP listeners require UDP server groups.

* To associate a TLS listener with a server group, the server group must meet the following requirements:

   * Full port forwarding is not enabled.

   * Backend protocol: TCP.

   * IP version: IPv4.

   ## Procedures

**TCP listener**

1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click **Edit listener** to the right of the target NLB instance.

4. Click **Add listener** and configure the listener as shown in the table below.

   |Parameters |Notes |Example |
   |---|---|---|
   |Listener name |Enter the listener name. If left blank, it defaults to **Protocol\-port**, such as **TCP\-80**. |listener01 |
   |Listener protocol |Select the protocol type for NLB instance listener. This topic uses TCP. [Learn more](https://docs.byteplus.com/en/docs/clb/NLB-Listener-overview#.55uR5ZCs5Y2P6K6u57G75Z6L) |TCP |
   |Listener port |Enter the listening port. The range is 1 to 65535.<br><br><br>* Single port listener: Enter a single port. When the listener receives a TCP request to this port, it replaces the destination IP address and port in the request with the backend server's IP address and port before forwarding to the backend server.<br><br>* Full port listening: Enter a port range. When the listener receives a TCP request on this port, it replaces the destination IP in the request with the backend server's IP address before forwarding to the backend server.<br><br><br>[Learn more](https://docs.byteplus.com/en/docs/clb/NLB-Listener-overview) |80 |
   |Timeout |Set the timeout period. If no data is transferred over the connection within the timeout period, it will be automatically disabled.<br><br>For TCP listeners, the timeout period ranges from 10 to 900 seconds, with a default value of 900 seconds. |900 seconds |
   |New connection rate limit |Whether to enable the new connection rate limiting switch.<br><br>After enabling, enter the rate limit value:<br><br><br>* Value range: 0~1000000. 0 means no rate limit.<br><br>* When new connections captured by the listener exceed the configured threshold, excess connections will be discarded and not forwarded to the backend server.<br><br><br>> **tip**<br><br><br>> This feature is currently in Beta stage. For trial requests, please contact your account manager.<br> |30000 |
   |Max connections |Whether to enable the concurrent connection rate limiting switch.<br><br>After enabling, enter the rate limit value:<br><br><br>* Value range: 0~10000000. 0 means no rate limit.<br><br>* When concurrent connections captured by the listener exceed the configured threshold, excess connections will be discarded and not forwarded to the backend server.<br><br><br>> **tip**<br><br><br>> This feature is currently in Beta stage. For trial requests, please contact your account manager.<br> |300000 |
   |Tag |A tag consists of a key\-value pair and is used for categorizing and searching resources. [Learn more](https://docs.byteplus.com/en/docs/clb/NLB-Tag-Management)<br><br>Click the Add icon, input the Tag key and Tag value, and add a tag for the listener. |* Tag key: listener\-key<br><br>* Tag value: listener\-test |

5. Click **Next** and select a **TCP protocol server group**.

6. Click **Next** to confirm the configuration information.

7. Click **Confirm** to complete the action.

**UDP listener**

1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click **Edit listener** to the right of the target NLB instance.

4. Click **Add listener** and configure the listener as shown in the table below.

   |Parameters |Notes |Example |
   |---|---|---|
   |Listener name |Enter the listener name. If left blank, it defaults to **Protocol\-port**, such as **UDP\-88**. |listener01 |
   |Listener protocol |Select the protocol type for NLB instance listener. This action uses UDP. [Learn more](https://docs.byteplus.com/en/docs/clb/NLB-Listener-overview#.55uR5ZCs5Y2P6K6u57G75Z6L) |UDP |
   |Listener port |Enter the listening port. The range is 1 to 65535.<br><br><br>* Single port listener: Enter a single port. When the listener receives a UDP request to this port, it replaces the destination IP address and port in the request with the backend server's IP address and port before forwarding to the backend server.<br><br>* Full port listening: Enter a port range. When the listener receives a UDP request on this port, it replaces the destination IP in the request with the backend server's IP address before forwarding to the backend server.<br><br><br>[Learn more](https://docs.byteplus.com/en/docs/clb/NLB-Listener-overview) |88 |
   |Timeout |Set the timeout period. If no data is transferred over the connection within the timeout period, it will be automatically disabled.<br><br>The timeout period for the UDP listener ranges from 10 to 120 seconds, with a default value of 20 seconds. |20 seconds |
   |New connection rate limit |Whether to enable the new connection rate limiting switch.<br><br>After enabling, enter the rate limit value:<br><br><br>* Value range: 0~1000000. 0 means no rate limit.<br><br>* When new connections captured by the listener exceed the configured threshold, excess connections will be discarded and not forwarded to the backend server.<br><br><br>> **tip**<br><br><br>> This feature is currently in Beta stage. For trial requests, please contact your account manager.<br> |30000 |
   |Max connections |Whether to enable the concurrent connection rate limiting switch.<br><br>After enabling, enter the rate limit value:<br><br><br>* Value range: 0~10000000. 0 means no rate limit.<br><br>* When concurrent connections captured by the listener exceed the configured threshold, excess connections will be discarded and not forwarded to the backend server.<br><br><br>> **tip**<br><br><br>> This feature is currently in Beta stage. For trial requests, please contact your account manager.<br> |300000 |
   |Tag |A tag consists of a key\-value pair and is used for categorizing and searching resources [Learn more](https://docs.byteplus.com/en/docs/clb/NLB-Tag-Management)<br><br>Click the Add icon, input the tag key and tag value, and add a tag for the listener. |* Tag key: udplistener\-key<br><br>* Tag value: udplistener\-test |

5. Click **Next** and select the **UDP protocol server group**.

6. Click **Next** to confirm the configuration information.

7. Click **Confirm** to complete the action.

**TLS listener**

1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click **Edit listener** to the right of the target NLB instance.

4. Click **Add listener** and configure the parameters based on the table below.

   |Parameters |Notes |Example |
   |---|---|---|
   |Listener name |Enter the listener name. If left blank, it defaults to **Protocol\-port**, such as **TLS\-80**. |listener01 |
   |Listener protocol |Select the protocol type for NLB instance listener. This action uses TLS. [Learn more](https://docs.byteplus.com/en/docs/clb/NLB-Listener-overview#.55uR5ZCs5Y2P6K6u57G75Z6L) |TLS |
   |Listener port |Enter the listening port. The range is 1 to 65535.<br><br><br>* Single port listener: Enter a single port. When the listener receives a TLS request on this port, it replaces the destination IP and port in the request with the backend server's IP address and port, then forwards the request to the backend server.<br><br>* Full port listening: Enter a port range. When the listener receives a TLS request on this port, it replaces the destination IP in the request with the backend server's IP address before forwarding to the backend server.<br><br><br>[Learn more](https://docs.byteplus.com/en/docs/clb/NLB-Listener-overview) |80 |
   |Timeout |Set the timeout period. If no data is transferred over the connection within the timeout period, it will be automatically disabled.<br><br>The timeout period for a TLS listener ranges from 10 to 900 seconds, with a default value of 900 seconds. |900 seconds |
   |New connection rate limit |Whether to enable the new connection rate limiting switch.<br><br>After enabling, enter the rate limit value:<br><br><br>* Value range: 0~1000000. 0 means no rate limit.<br><br>* When new connections captured by the listener exceed the configured threshold, excess connections will be discarded and not forwarded to the backend server.<br><br><br>> **tip**<br><br><br>> This feature is currently in Beta stage. For trial requests, please contact your account manager.<br> |30000 |
   |Max connections |Whether to enable the concurrent connection rate limiting switch.<br><br>After enabling, enter the rate limit value:<br><br><br>* Value range: 0~10000000. 0 means no rate limit.<br><br>* When concurrent connections captured by the listener exceed the configured threshold, excess connections will be discarded and not forwarded to the backend server.<br><br><br>> **tip**<br><br><br>> This feature is currently in Beta stage. For trial requests, please contact your account manager.<br> |300000 |
   |Tag |A tag consists of a key\-value pair and is used for categorizing and searching resources [Learn more](https://docs.byteplus.com/en/docs/clb/NLB-Tag-Management)<br><br>Click the **Add** icon, input the tag key and tag value, and add a tag for the listener. |* Tag key: listener\-key<br><br>* Tag value: listener\-test |

5. Click **Next** to configure the SSL certificate.

   |Parameters |Notes |Example |
   |---|---|---|
   |Certificate source |Select the source of the server certificate.<br><br><br>* BytePlus Certificate Center SSL certificate (**recommended**). <br><br>* BytePlus Certificate Center Private CA. <br><br><br>> **tip**<br><br><br>> The feature supporting CA certificates in server certificates is currently in Beta stage. For trial requests, please contact your account manager.<br> |BytePlus Certificate Center SSL certificate<br><br> |
   |Server certificate |Select a server certificate from the dropdown. You can purchase or upload server certificates in the Certificate Center. The NLB retrieves and uses these certificates from the Certificate Center.<br><br>> **tip**<br><br><br>> Note that the NLB does not perform integrity verification on server certificates—this validation is handled by the Certificate Center.<br><br><br>> Certificates without integrity verification may pose security risks; proceed with caution after thorough evaluation.<br> |xx\-certificate\-xx |
   |Mutual authentication |Select whether to enable mutual authentication. Mutual authentication requires not only the client to verify the server's legitimacy, but also the server to verify the client's legitimacy.  |Don't enable |
   |CA certificate source |Supported certificate sources for CA certificates:<br><br><br>* Private Root CA<br><br>* Private Sub CA |Private Sub CA |
   |CA certificate |Select the CA certificate based on the CA certificate source. |xx\-certificate\-xx |
   |TLS Security Policy |Select policy.<br><br><br>* System default policy: Select the system default policy from dropdown menu.<br><br>* Custom policy: Select the custom policy from dropdown menu.<br><br><br>[Learn more](https://docs.byteplus.com/en/docs/clb/NLB-TLS-Overview) |System policy<br><br>tls_cipher_policy_1_0 |

6. Click **Next** and select a **TCP protocol server group**.

7. Click **Next** to confirm the configuration information.

8. Click **Confirm** to complete the action.

## What to do next

* [Resolve your own domain name to the NLB domain name via CNAME](https://docs.byteplus.com/en/docs/clb/Setting-up-an-IPv4-NLB#YAJjurNK), and access the NLB service through your own domain name.

* For listeners with health check enabled, confirm that their health status is **Normal** on the details page.

   * If the health check status is **Normal**, the NLB configuration is complete. You can obtain the IP address of the NLB instance on the Availability Zone tab of the NLB instance details page to Verify NLB service capabilities.

   * When the health check status is not **Normal**, please see the following for troubleshooting:

      * When the health check status is **No target**, please [Add backend servers](https://docs.byteplus.com/en/docs/clb/NLB-Adding-removing-backend-server) to the server group associated with the listener.

      * When the health check status is **Exception**, please [Troubleshoot the root cause of the abnormalities](https://docs.byteplus.com/en/docs/clb/NLB-Troubleshooting-exceptions-found-in-health-check).

## Related documents

[CreateNLBListener](https://docs.byteplus.com/en/docs/clb/CreateNLBListener)
