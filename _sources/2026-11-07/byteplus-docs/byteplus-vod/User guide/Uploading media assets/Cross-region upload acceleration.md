---
title: "Cross-region upload acceleration"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-cross-region-upload-acceleration"
---

Cross\-region uploads to a VOD space in Asia Pacific (Johor) can be affected by network conditions between the upload client and the destination region. To improve upload stability and performance, you can use BytePlus IntelliEdge Global Accelerator (IGA) with the upload acceleration settings in BytePlus VOD.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Availability</div>


<div data-tips="true" data-tips-type="tip">Cross\-region upload acceleration is available only for VOD spaces in Asia Pacific (Johor).</div>


<span id="prerequisites"></span>
## Prerequisites

Before you begin, make sure that:


* You have created a VOD space in Asia Pacific (Johor).

* You have a custom domain that you can configure with a CNAME record.

* Your BytePlus account can access [BytePlus IntelliEdge Global Accelerator](https://docs.byteplus.com/en/docs/iga/what_is_intelligedge_global_accelerator_en-us).


<span id="pricing"></span>
## Pricing

IGA charges apply. Acceleration is billed based on data transfer and requests. For details, see [IGA pricing overview](https://docs.byteplus.com/en/docs/iga/billing_overview_en-us).

<span id="procedure"></span>
## Procedure

<span id="step-1-obtain-the-vod-storage-endpoints"></span>
### Step 1: Obtain the VOD storage endpoints


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and select a VOD space in Asia Pacific (Johor).

2. On the left navigation bar, click **System settings** \> **Upload and storage**.

3. Under **Upload acceleration settings**, click **Modify** and enable acceleration.

4. Copy the primary and backup **Storage Endpoint** domain names. Configure both endpoints in IGA so that IGA can use the alternate VOD origin if one endpoint is unavailable.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260811040006-517490256600.png) </span>

<span id="step-2-configure-byteplus-intelliedge-global-accelerator"></span>
### Step 2: Configure BytePlus IntelliEdge Global Accelerator

<span id="add-an-acceleration-domain"></span>
#### Add an acceleration domain


1. Sign in to the [IntelliEdge Global Accelerator console](https://console.byteplus.com/iga).

2. On the **Instances** tab, click **Add domain**.

   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260811045723-413546476325.png) </span>

3. Select the **Uploads** scenario. IGA recommends upload\-specific acceleration settings for this scenario. For details, see [Uploads](https://docs.byteplus.com/en/docs/iga/uploads_en-us).

4. Configure the domain as follows. For descriptions of all fields, see [Configure a domain](https://docs.byteplus.com/en/docs/iga/configure_a_domain_en-us).

   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260811064104-1171190706426.png) </span>

   
   |Field |Configuration |
   |---|---|
   |Access region |Select an access region based on the geographic distribution of your upload clients: **Chinese Mainland**, **Outside Chinese Mainland**, or **Global**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">By default, <strong>Chinese Mainland</strong> is not available for selection. To accelerate access from Chinese Mainland, you must first complete real\-name registration for your BytePlus account. For more information, see <a href="https://docs.byteplus.com/en/docs/Account/real-name-verification?redirect=1">Real name verification</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If your access region is <strong>Chinese Mainland</strong> or <strong>Global</strong>, you must complete an ICP filing for your domain.</div><br> |
   |Domain |Enter your custom domain. When adding a root domain or one of its subdomains for the first time, complete [domain ownership verification](https://docs.byteplus.com/en/docs/iga/verifying_domain_ownership_en-us). |
   |Origin mode |Select **Single origin**. |
   |Origin protocol |Select **HTTPS**. |
   |Origin address |* Set **Origin type** to **Custom domain**.<br><br>* Enter the **Storage Endpoint** you obtained in Step 1 as the **Origin address**.<br><br>* Set **Port** to `443`. |
   

5. Click **Next**.

6. Enable **HTTPS service** and select or import the SSL certificate for your custom domain. For details, see [Enable HTTPS service](https://docs.byteplus.com/en/docs/iga/enable_https_service_en-us).

   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260811064517-1173974718937.png) </span>

7. Click **Submit**.


<span id="configure-cname-resolution"></span>
#### Configure CNAME resolution


1. Copy the CNAME name assigned to your acceleration domain.

   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260811065111-1248935021814.png) </span>

2. At your DNS provider, add a CNAME record for your custom domain. Set the record value to the CNAME name assigned by IGA.

3. Wait for the DNS record to take effect. In the IGA console, click **Verify CNAME resolution**.

4. After the CNAME becomes active, click **Complete configuration**. For details, see [Configure CNAME resolution](https://docs.byteplus.com/en/docs/iga/configure_cname_resolution_en-us).


<span id="configure-origin-requests"></span>
#### Configure origin requests


1. On the **Instances** tab, click the acceleration domain, click **Manage**.

2. Click **Origin requests**, and then click **Edit**.

3. Enable **Origin HOST**, and then set it to the **Storage Endpoint** you obtained in Step 1. For details, see [Configure Origin HOST](https://docs.byteplus.com/en/docs/iga/configure_origin_host_en-us).

4. Set **Origin response timeout** to at least `600` seconds. IGA supports values from `1` to `900` seconds. For details, see [Configure origin response timeout](https://docs.byteplus.com/en/docs/iga/configure_origin_response_timeout_en-us).

5. Click **Submit**.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260811071715-970027862507.png) </span>

<span id="step-3-enable-upload-acceleration-in-byteplus-vod"></span>
### Step 3: Enable upload acceleration in BytePlus VOD


1. Return to **Upload and storage** \> **Upload acceleration settings** in the BytePlus VOD console.

2. Enter the CNAME\-configured custom domain in **IGA custom domain**.

3. Select the default domain returned by the VOD upload service. This is a **space\-level** default setting.

   * **VOD upload domain**: Prioritizes the VOD upload domain. This is the default option.

   * **IGA custom domain**: Returns the IGA custom domain as the primary upload domain and the VOD upload domain as the backup domain.

4. Click **Confirm** to save the configuration. The change takes effect within several minutes.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260811074533-1012159934217.jpg) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Validate the configuration before production use</div>


<div data-tips="true" data-tips-type="warning">An invalid or unreachable IGA custom domain can cause uploads to fail. Test the configuration in a test space before applying it to a production space.</div>


<span id="override-the-domain-for-an-individual-upload"></span>
## Override the domain for an individual upload

When calling [ApplyUploadInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-applyuploadinfo), use the optional `UploadHostPrefer` parameter to override the space\-level default for an individual upload:


* Set the parameter to `dcdn` to prioritize the configured IGA custom domain.

* Set the parameter to `vod` to prioritize the VOD upload domain.

* Omit the parameter to use the space\-level default.


If upload acceleration is not configured for the space, `UploadHostPrefer` does not take effect.

The `UploadHosts` response field contains the upload domains in priority order. Your upload client should try the next domain in the list if the current domain is unavailable.
