---
title: "Updating HTTPS certificates for LoadBalancer services"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Updating_HTTPS_certificates_for_LoadBalancer_services"
---

When configuring an HTTPS listener for a LoadBalancer service, you can update the listener's certificate via annotation or the certificate center. This topic introduces how to update certificate configurations for HTTPS listeners upon expiration or rotation.

<span id="PC9im04g"></span>
## Background

In VKE, you can annotate a LoadBalancer\-type service to create and manage an HTTPS listener automatically for the instance. The HTTPS listener binds a certificate for server authentication and data encryption, ensuring secure HTTPS connections for client access. For details, see the following documentation:


* [Configuring CLB LoadBalancer Services by using annotations](https://docs.byteplus.com/en/docs/vke/Configuring-a-LoadBalancer-Service-using-annotations)

* [Configuring an NLB Service using annotations](https://docs.byteplus.com/en/docs/vke/Configuring_an_NLB_Service_using_annotations)


HTTPS certificates typically have a fixed validity period. After expiration, if the listener still uses the old certificate, clients may see expiration warnings, security alerts, or connection failures. Thus, before expiration, you need to apply, upload, or prepare a new certificate and update the listener's HTTPS certificate promptly.

The update method depends on the source of the certificate. The following table provides details.


|Configuration method |Certificate source |Certificate update method |
|---|---|---|
|Specify the certificate ID using an annotation |CLB certificate |Manual update. |
||Certificates from Certificate Center |* Manual update.<br><br>* Batch update and deployment are allowed when working with Certificate Center. |


<span id="oW8LpOBt"></span>
## Manual certificate update

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For manual updates, do not replace the certificate directly in the LoadBalancer console's listener page. When the rules change on VKE, the listener will be reconciled to the old certificate, potentially causing service disruptions.</div>


<span id="VG3kOg5p"></span>
### Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. On the Cluster page, click the name of the target cluster to go to the cluster management page.

3. In the left navigation pane, select **Services and Ingresses \> Service**, select the target service, and click **Edit Yaml** in the **Actions** column on the right.

4. In the annotation section of the YAML content, replace the old certificate ID with the new one.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_67cee5767652301aace6a60dee6b7a8b.png) </span>

5. Click **Confirm**.


<span id="s6M77fZy"></span>
### Validate results

After the update succeeds, you can log in to the CLB console to verify the listener's bound certificate. This topic uses CLB LoadBalancer as an example.


1. After configuration, click the service name, go to the **Event** tab, and check the reconciliation success events.

2. Log in to the [LoadBalancer console ](https://console.byteplus.com/clb), check the certificate details of the listener, and confirm the replacement of the certificate ID.


&nbsp;

<span id="jl18lcH8"></span>
## Update certificates via Certificate Center

<span id="qjrp6kZt"></span>
### Usage limits


* Only resources using certificates from Certificate Center support batch update and deployment.

* The account used to update certificates in Certificate Center must have write permissions on VKE cluster resources. For example, in this topic, write permission for service resources is required.


<span id="GrdmYMJM"></span>
### Procedure

We recommend managing certificates via Certificate Center. This section focuses on using the **Deploy** feature in the Center for batch updates.


1. Log in to the [Certificate Center console](https://console.byteplus.com/certificate-center).

2. Purchase or upload a new SSL certificate. For details, see [Creating SSL certificate order](https://docs.byteplus.com/en/docs/6638/118034) and [Uploading SSL certificate](https://docs.byteplus.com/en/docs/6638/118039).

3. In the left navigation pane, select **SSL Certificate** \> **Certificates**.

4. In the certificate list, select the new certificate and click **Deploy** in the **Actions** column to go to the deployment page.

5. In **Deploy to**, select **VKE**, then select the region and resources in **Resource list** and add them to the **Pending deployment list** on the right.

6. Click **Deploy**, confirm the deployment, and the certificate deployment will begin.


<span id="OYIcJtup"></span>
### Validate results

After the update succeeds, you can log in to the CLB console to verify the listener's bound certificate. This topic uses CLB LoadBalancer as an example.


1. Upon completion, the system will show **Succeeded** in the **Deployment status**.

2. Log in to the [CLB console](https://console.byteplus.com/clb), check the listener's certificate details, and confirm the replacement of the certificate ID.
