---
title: "Adding/Deleting an additional certificate"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Adding_or_deleting_an_additional_certificate"
---

In addition to being associated with one default certificate, an HTTPS listener for CLB can also have multiple additional certificates added to it to meet the security requirements of different scenarios.

> **tip**

> The additional certificates feature of CLB is in Beta stage. If you need a trial, please contact your account manager.

## Add extended certificate

### **Action notes**

* A single HTTPS listener supports a maximum of 20 additional certificates. If the default quota is insufficient, you can go to the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=CLB) to apply for an increase.

   > **tip**

   > Multiple domain names (which must be within the authentication scope supported by the certificate) can be associated with the same additional certificate; however, each domain name counts towards the quota for additional certificates.

* When adding an additional certificate, you need to enter a domain name to associate it with the certificate. The certificate is used only when the listener has a forwarding rule configured for this domain name (supporting wildcard domains).

* The certificate matching rules are as follows:

   1. Requests are matched against forwarding rules first, and the certificate associated with the domain name bound to the corresponding forwarding rule is used.

   2. If no domain name match is found, the default certificate is used.

### Procedures

1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click the target CLB instance name.

4. On the **Listener** tab, click  **···\> Edit additional certificate**.

5. Click **Add additional certificate**.

6. Enter the domain name and select the server certificate.

7. Click **Save** to complete the action.

## Delete additional certificate

1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click the target CLB instance name.

4. On the **Listener** tab, click  **···\> Edit additional certificate**.

5. Click **Delete** next to the target certificate.

6. Click **Delete** to complete the action.
