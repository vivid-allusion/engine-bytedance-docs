---
title: "Mutual authentication"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Mutual-authentication"
---

ALB supports HTTPS mutual authentication. If you use the HTTPS mutual authentication feature, in addition to binding a server certificate to the listener, you also need to bind a CA certificate to the listener. This CA certificate is used to verify whether the certificate provided by the client is trustworthy.

## Background

In the HTTPS one\-way authentication scenario, only the client verifies whether the server is trustworthy. In this scenario, you only need to configure the server certificate for the listener. The listener proves its identity to the client using its own server certificate.

In scenarios with high business security requirements, such as finance, you can enable the HTTPS mutual authentication feature for the listener. After enabling this feature, both the client and the server need to verify each other's identities. In this scenario, you not only need to configure a server certificate for the listener but also a CA certificate. The listener uses its own server certificate to prove its identity to the client and uses the CA certificate to verify the client's identity.

## Prerequisites

* You have created a listener. For detailed steps, see [Creating a HTTPS listener](https://docs.byteplus.com/docs/clb/ALB-Creating-an-HTTPS-listener), [Creating a HTTP/2 listener](https://docs.byteplus.com/docs/clb/Creating-an-HTTP_2listener), or [Creating a QUIC listener](https://docs.byteplus.com/docs/clb/Creating-a-QUIC-listener).

* You have prepared a CA certificate. You can use a CA certificate issued  from a third\-party certificate platform. If you use a CA certificate from a third\-party certificate platform, you need to first upload this CA certificate to ALB or the Certificate Center.

## Procedures

1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. On the **Instance** page, find the ALB instance to configure and click **Listener** in the **Actions** column.

3. On the **Listener information** tab, click the name of the listener to be associated with the certificate.

4. On the **Listener details** tab, click **Edit** icon next to **Mutual authentication**.

5. In the **Edit Mutual Authentication** dialog box, configure the following settings:

   * **Status**: Turn on the **Status** switch to enable mutual authentication.

   * **Certificate source**: Select the certificate source. You can choose to **Use an existing certificate on the ALB**.

   * **CA certificate**: Select a CA certificate from the dropdown list.

6. After configuration is complete, click **Save**.
