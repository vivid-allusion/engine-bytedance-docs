---
title: "Updating HTTPS certificates for CLB Ingress"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Updating_HTTPS_certificates_for_CLB_Ingress"
---

When an HTTPS certificate for a cluster is about to expire, update it promptly to ensure uninterrupted HTTPS access. After expiration, clients will see certificate invalidity warnings, which may cause service unavailability in severe cases. This topic describes how to update HTTPS certificates for CLB Ingress in VKE.

<span id="HRfd3Td8"></span>
## Certificate update methods

The update method depends on the source of the certificate. As shown in the table below.


|Configuration method |Certificate source |Certificate update method |
|---|---|---|
|Use the Secret that contains the certificate ID |CLB certificate |Manual update. |
||Certificates from Certificate Center |* Manual update.<br><br>* Batch update and deployment are allowed when working with Certificate Center. |


<span id="Zbje4JOK"></span>
## Manual update of certificates

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When CLB Ingress uses HTTPS, do not replace the certificate manually in the CLB console's listener page. When the Ingress rules change on VKE, the listener will be reconciled to the old certificate, potentially causing service disruptions.</div>


<span id="6B3ulX6Z"></span>
### Procedure


1. Log in to the [LoadBalancer console ](https://console.byteplus.com/clb)or [Certificate Center console](https://console.byteplus.com/certificate-center) to purchase or upload a new certificate. For details, see [Certificate management](https://docs.byteplus.com/en/docs/clb/Adding-and-deleting-a-certificate), [Creating SSL certificate](https://docs.byteplus.com/en/docs/6638/118034), and [Uploading SSL certificate](https://docs.byteplus.com/en/docs/6638/118039).

2. Log in to the [VKE console](https://console.byteplus.com/vke).

3. On the Cluster page, click the name of the target cluster to go to the cluster management page.

4. In the left navigation bar, click **Services and Ingresses \> Ingress**. In the Ingress list, find the Ingress for which you need to update the HTTPS certificate and click **Update** in the **Actions** column.

5. In **Listener configuration**, select the certificate source and click **Create Secret**.

6. Configure the Secret based on the selected certificate source.

   
   <Tabs>
   <Tab zoneid="7wZYBW47" title="CLB certificate">
   <TabTitle>CLB certificate</TabTitle>
   
   When using a CLB certificate, select **CLB** as the certificate source, and choose the new certificate in the **Server Certificate** drop\-down menu.
   
   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d2dcfc0bde010b1b1c805c903b505006.png) </span>
   
   
   </Tab>
   <Tab zoneid="Tjzq2JjX" title="Certificates from Certificate Center">
   <TabTitle>Certificates from Certificate Center</TabTitle>
   
   When using a certificate from Certificate Center, select **Certificate Center** as the source, and choose the new certificate in the **Server Certificate** drop\-down menu.
   
   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260810062027-1471831302653.png) </span>
   
   
   </Tab>
   </Tabs>
   

7. Select the newly created Secret.

8. Click **Confirm** to complete the Ingress update.


<span id="Uy8o98dZ"></span>
### Validate results


1. After configuration, click the Ingress name, go to the **Event** tab, and check the reconciliation success event.

2. Log in to the [LoadBalancer console](https://console.byteplus.com/clb), check the certificate details of the listener, and confirm the replacement of the certificate ID.


<span id="Sna5c80u"></span>
## Update certificates via Certificate Center

<span id="7WkRSbnH"></span>
### Usage limits


* Only resources using certificates from Certificate Center support batch update and deployment.

* The account used to update certificates in Certificate Center must have write permissions on VKE cluster resources. For example, in this topic, write permission for CLB Ingress is required.


<span id="bIHkbr7k"></span>
### Procedure

We recommend managing certificates via Certificate Center. This section focuses on using the **Deploy** feature in the Center for batch updates.


1. Log in to the [Certificate Center console](https://console.byteplus.com/certificate-center).

2. Purchase or upload a new SSL certificate. For details, see [Creating SSL certificate order](https://docs.byteplus.com/en/docs/6638/118034) and [Uploading SSL certificate](https://docs.byteplus.com/en/docs/6638/118039).

3. In the left navigation pane, select **SSL Certificate** \> **Certificates**.

4. In the certificate list, select the new certificate and click **Deploy** in the **Actions** column to go to the deployment page.

5. In **Deploy to**, select **VKE**, then select the region and resources in **Resource list** and add them to the **Pending deployment list** on the right.

6. Click **Deploy**, confirm the deployment, and the certificate deployment will begin.


<span id="JlgsufDW"></span>
### Validate results


1. Upon completion, the system will show **Succeeded** in the **Deployment status**.

2. Log in to the [CLB console](https://console.byteplus.com/clb), check the listener's certificate details, and confirm the replacement of the certificate ID.
