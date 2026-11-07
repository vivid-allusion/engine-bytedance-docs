---
title: "Create QUIC listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Creating-a-QUIC-listener"
---

This topic explains how to create a QUIC listener in the ALB console. QUIC listeners are suitable for scenarios requiring secure transmission, low latency, and improved application performance under poor network conditions.

Each ALB instance must have at least one listener to function properly. A listener accepts client requests and distributes them to backend servers based on the forwarding rules and load balancing algorithms you configure. You can create multiple listeners under a single ALB instance and configure them with different listener protocols to handle client requests using different protocols.

## Background

### QUIC protocol

The QUIC protocol integrates features such as multiplexing, congestion control, security encryption, and reliable transmission, enabling low\-latency, efficient, and secure data transfer.

ALB supports gQUIC and iQUIC:

* gQUIC is the QUIC protocol developed by Google. The gQUIC protocol versions supported by ALB include: 39, 43, 44, 46, 47.

* iQUIC is the standardized QUIC protocol defined by IETF. HTTP/3 is an application\-layer protocol built on top of QUIC.

### Certificate

When creating a QUIC listener, you must associate a server certificate with the listener.

#### Certificate source

ALB instances allow you to select certificates from the following sources:

* Certificates from the ALB side

   If you use a certificate from the ALB side, you first need to upload your certificate to the ALB. ALB only allows you to upload certificates in PEM format. Certificates in other formats must be converted to PEM format before they can be uploaded. For related operations, see [Adding a certificate](https://docs.byteplus.com/docs/clb/Adding-and-deleting-a-certificate#.5re75Yqg6K-B5Lmm) and [Converting the certificate format](https://docs.byteplus.com/docs/clb/Converting-certificate-formats).

* Certificate from Certificate Center

   If you use a certificate from the Certificate Center, you first need to either upload your certificate to the Certificate Center or purchase a certificate from the Certificate Center. Afterwards, you can directly select your certificate in the ALB console. For more information, see [ALB using Certificates from the Certificate Center](https://docs.byteplus.com/docs/clb/Using-certificates-from-BytePlus-Certificate-Center).

   We recommend using certificates from the Certificate Center. In the [Certificate Center console](https://console.byteplus.com/certificate-center/ssl/overview), you have a one\-stop shop for purchasing, uploading, and managing certificates.

#### Certificates supported by different ALB instance editions

Basic Edition ALB Instances support: Certificates from the ALB side and certificates from the Certificate Center.

Standard Edition ALB Instances support: Certificates from the Certificate Center.

#### Certificates for QUIC Listeners

Only Standard Edition ALB instances support QUIC listeners. Standard Edition ALB Instances only support Certificates from the Certificate Center. Therefore, when creating a QUIC listener, you can only select certificates from the Certificate Center.

## Limits

* Only Standard Edition ALB instances support the QUIC feature. Currently, to use the QUIC feature, please [submit ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000645) or contact your account manager.

* If you are using a dual\-stack ALB instance, you cannot enable the QUIC feature for its listeners.

## Prerequisites

* You have [created an ALB instance](https://docs.byteplus.com/docs/clb/Creating-an-instance).

* You have [created the required server group](https://docs.byteplus.com/docs/clb/Server-groups-Overview).

* You have [Prepared a server certificate](https://docs.byteplus.com/docs/clb/Using-certificates-from-BytePlus-Certificate-Center).

## Procedures

1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. Click **Listener** to the right of the target ALB instance.

4. On the Listeners tab, click Add listener.

5. configure relevant parameters based on the table below. Then click **Next: default backend server group**.

   |Parameter name |Explanation |Example |
   |---|---|---|
   |Name |Enter the listener name. Naming rules are as follows:<br><br><br>* Can contain English letters, Chinese characters, numbers, half\-width period (.), underscore (_), and hyphen (\-).<br><br>* Must start with an English letter or a Chinese character.<br><br>* Cannot start with http:// or https://.<br><br>* A maximum of 128 characters is allowed.<br><br>* If left blank, it defaults to **Protocol\-port**, such as **HTTPS\-443**. |HTTPS\-443 |
   |Listening protocol |Set the listener protocol to HTTPS.<br><br>HTTPS listeners support the WebSocket Secure (WSS) protocol by default; no additional configuration is required. |HTTPS |
   |Listening port |Set the port for the listener. Valid range: 1\-65535.<br><br>The ports for different listeners under the same ALB instance must be unique. |443 |
   |Access control |Optional. Enable the Access Control feature for the listener to allow or deny requests from specific clients.<br><br>If the access control feature is not enabled, requests from all clients will be allowed. |Check |
   |Control mode |Configure access control mode. After enabling Access Control, you must select access control mode.<br><br><br>* Allowlist: The listener only allows requests originating from IP addresses within the selected policy group(s).<br><br>* Denylist: The listener denies requests originating from IP addresses within the selected policy group(s). |Denylist |
   |Policy group |Select policy group. After enabling Access Control, you must configure a policy group.<br><br>A maximum of 5 policy groups can be selected. Each policy group can contain up to 300 IP address entries. Each IP address entry can be a single IP address or a CIDR block. For more information about policy groups, see [Access Control](https://docs.byteplus.com/docs/clb/Access-control). |acl\-a |
   |Certificate source |Select the source of the server certificate to be associated with the listener.<br><br>Standard Edition ALB Instances only support Certificates from the Certificate Center. |Certificate Center |
   |Server certificate |Select the specific server certificate to be associated with the listener. The server certificate is used to verify the server's identity and establish an encrypted connection. |certificate\-A |
   |HTTP/2 |Retain the default configuration, i.e., do not enable HTTP/2. |Do not enable |
   |QUIC |Enable QUIC. |Check |
   |Tags |A tag consists of a key\-value pair and is used for categorizing and searching resources [Prerequisite](https://docs.byteplus.com/en/docs/clb/Tag-Overview)<br><br>Click the Add icon, input the tag key and tag value, and add a tag for the listener. |* Tag key: alb\-QUIC<br><br>* Tag value: http\-443 |

6. On the **Default Server Group** tab, select the prepared server group from the dropdown menu and click **Next: Confirm configuration**.

7. After confirming the listener’s configuration is correct, click **Save**.

## What to do next

1. [Configure custom configuration](https://docs.byteplus.com/en/docs/clb/Custom-configurations): allows you to customize settings such as long connection retention time, established timeout, client request body maximum size, custom response headers, and custom request headers.

2. [Configure forwarding rule](https://docs.byteplus.com/en/docs/clb/Forwarding-rule-Overview): ALB distributes access traffic according to the forwarding rules you set based on different traffic characteristics.

## Related actions

* You can enable or disable QUIC on the listener details page as needed. After disabling QUIC, your listener will no longer be able to handle QUIC protocol requests from clients.

* You can enable both QUIC and HTTP/2 simultaneously for an HTTPS listener. This allows the listener to handle client requests using either the QUIC or HTTP/2 protocol.
