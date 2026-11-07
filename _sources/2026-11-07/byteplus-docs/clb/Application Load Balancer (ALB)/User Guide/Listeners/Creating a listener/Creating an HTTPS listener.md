---
title: "Creating an HTTPS listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-Creating-an-HTTPS-listener"
---

This topic explains how to create an HTTPS listener in the ALB console. HTTPS listeners are suitable for scenarios that require encrypted transmission and have higher requirements for data security and authentication.

Each ALB instance must have at least one listener to function properly. A listener accepts client requests and distributes them to backend servers based on the forwarding rules and load balancing algorithms you configure. You can create multiple listeners under a single ALB instance and configure them with different listener protocols to handle client requests using different protocols.

## Background

### Certificate

When creating an HTTPS listener, you must associate a server certificate with the listener.

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

## Prerequisites

* You have [created an ALB instance](https://docs.byteplus.com/docs/clb/Creating-an-instance).

* You have [created the required server group](https://docs.byteplus.com/docs/clb/Server-groups-Overview).

* You have Prepared a server certificate. For related operations, see [Adding a Certificate](https://docs.byteplus.com/docs/clb/Adding-and-deleting-a-certificate#.5re75Yqg6K-B5Lmm) or [ALB using Certificates from the Certificate Center](https://docs.byteplus.com/docs/clb/Using-certificates-from-BytePlus-Certificate-Center).

## Procedures

1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. Click **Listener** to the right of the target ALB instance.

4. On the Listeners tab, click Add listener.

5. Configure relevant parameters based on the table below. Then click **Next: default backend server group**.

   |Parameter |Explanation |Example |
   |---|---|---|
   |Name |Enter the listener name. Naming rules are as follows:<br><br><br>* Can contain English letters, Chinese characters, numbers, half\-width period (.), underscore (_), and hyphen (\-).<br><br>* Must start with an English letter or a Chinese character.<br><br>* Cannot start with http:// or https://.<br><br>* A maximum of 128 characters is allowed.<br><br>* If left blank, it defaults to **Protocol\-port**, such as **HTTPS\-443**. |HTTPS\-443 |
   |Listening protocol |Set the listener protocol to HTTPS.<br><br>HTTPS listeners support the WebSocket Secure (WSS) protocol by default; no additional configuration is required. |HTTPS |
   |Listening port |Set the port for the listener. Valid range: 1\-65535.<br><br>The ports for different listeners under the same ALB instance must be unique. |443 |
   |Access control |Optional. Enable the Access Control feature for the listener to allow or deny requests from specific clients.<br><br>If the access control feature is not enabled, requests from all clients will be allowed. |Check |
   |Control mode |Configure control mode. This parameter is mandatory only after the Access Control feature is enabled.<br><br><br>* Allowlist: Only IP addresses within the selected policy group will be permitted access to the listener.<br><br>* Denylist: IP addresses within the selected policy group will be denied access to the listener. |Denylist |
   |Policy group |Select policy group. This parameter is mandatory only after the Access Control feature is enabled.<br><br>A maximum of 5 policy groups can be selected. Each policy group can contain up to 300 IP address entries. Each IP address entry can be a single IP address or a CIDR block. For more information about policy groups, see [Access Control](https://docs.byteplus.com/docs/clb/Access-control). |acl\-A |
   |Certificate source |Select the source of the server certificate to be associated with the listener.<br><br>Basic Edition ALB Instances support: Existing Certificates from the ALB side and certificates from the Certificate Center.<br><br>Standard Edition ALB Instances support: Certificates from the Certificate Center. |Certificate Center |
   |Server certificate |Select the specific server certificate to be associated with the listener. The server certificate is used to verify the server's identity and establish an encrypted connection. |certificate\-A |
   |HTTP/2 |Retain the default configuration, i.e., do not enable HTTP/2. |Do not enable |
   |QUIC |Retain the default configuration, i.e., do not enable QUIC. |Do not enable |
   |Tags |A tag consists of a key\-value pair and is used for categorizing and searching resources [Prerequisite](https://docs.byteplus.com/en/docs/clb/Tag-Overview)<br><br>Click the Add icon, input the tag key and tag value, and add a tag for the listener. |* Tag key: alb\-https<br><br>* Tag value: http\-443 |

6. On the **Default server group** tab, select the prepared server group from the dropdown, then click **Next step: confirm the configuration**.

7. After confirming the listener configuration, click **Save**.

## What to do next

1. [Configure personalized settings](https://docs.byteplus.com/en/docs/clb/Custom-configurations): allows you to customize configuration items such as long connection retention time, timeout, maximum client request body size, custom response headers, and custom request headers.

2. [Configure forwarding rules](https://docs.byteplus.com/en/docs/clb/Forwarding-rule-Overview): ALB distributes access traffic based on different characteristics according to the forwarding rules you set.
