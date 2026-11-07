---
title: "Manage PTR records"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/manage_ptr_records"
---

This document describes how to manage PTR records. For more information about PTR records, see [PTR Record](https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-supported-dns-record-types#ptr-record).

<span id="4nwMlXTr"></span>
## Configure a PTR record

PTR records are a paid feature. You must [purchase a PTR record](https://docs.byteplus.com/en/docs/byteplus-dns-suite/purchase_a_ptr_record) before you can use it.

If you have already purchased PTR records but skipped the configuration step during the purchase process, follow the steps below to configure them:


1. Open the [PTR record](https://console.byteplus.com/dns-suite/dns/publiczone/ptr) page in the BytePlus DNS console.

2. Locate the PTR record you want to configure and click **Configure** in the **Actions** column.

3. On the **Configure** page, configure the following parameters.



|**Parameter** |**Description** |
|---|---|
|**Public IP** |The BypePlus public IPv4 address associated with the PTR record. If your BytePlus account does not have a public IP, you need to [apply for a public IP](https://console.byteplus.com/ecs/region:ecs+ap-southeast-1/eips).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can only configure PTR records for BypePlus public IP addresses.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Each public IP address can be associated with only one PTR record.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Only IPv4 PTR records are supported. IPv6 PTR records are not currently supported.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Make sure that the public IP address remains active. If the public IP address expires or is unsubscribed, the associated PTR record becomes invalid and its status changes to <strong>Abnormal</strong>.</div><br> |
|**Domain Name** |The domain name returned by the PTR record. You can specify any primary or subdomain, such as `example.com` or `abc.example.com`. |
|**TTL** |The amount of time that Local DNS servers cache the PTR record. A smaller TTL value ensures that changes to the PTR record take effect more quickly. |
|**Remark** |The remark or description for the PTR record, with a maximum length of 200 characters. |
|**Project** |The name of the project to which the PTR record belongs, defaulting to **default**. Select a project from the dropdown list, which displays all projects for which your root account or IAM user has management permissions. To create a new project, click **Edit**.<br><br>For more information about using projects to manage BytePlus DNS resources, see [Resource Project](https://docs.byteplus.com/en/docs/resourcemanagement/Resource_Project). |
|**Tags** |Key\-value pairs to help organize and manage your PTR records. Click **Add tag** to add a tag. Enter the tag key and tag value, such as`example-key` and `example-value`, into the respective input boxes. Both tag keys and values support UTF\-8 characters.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can add up to 50 tags per record.</div><br><br><br>For more information about using tags to manage BytePlus DNS resources, see [Resource Tag](https://docs.byteplus.com/en/docs/resourcemanagement/Resource_Tag). |



4. After completing the configuration, click **OK**.


After purchasing and configuring a PTR record in the console, BytePlus is required to coordinate with the upstream authority, CNNIC (China Internet Network Information Center), to complete the final configuration and delegation. This process typically takes 1 to 3 business days to take effect. During this period, the PTR record status will be displayed as **Creating**. Once the record is successfully delegated and active, the status changes to **Active**.

<span id="7ReL2181"></span>
## Update a PTR record

Follow the steps below to update an already configured PTR record:


1. Open the [PTR record](https://console.byteplus.com/dns-suite/dns/publiczone/ptr) page in the BytePlus DNS console.

2. Locate the PTR record you want to update and click **Edit** in the **Actions** column.

3. On the **Edit** page, update the record settings and click **OK**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you update the public IP address or domain name of the PTR record, BytePlus must resubmit the configuration to CNNIC to apply the update. This may take 1 to 3 business days to take effect. During this period, the record status appears as <strong>Creating</strong>, and changes to <strong>Active</strong> after the update is applied.   </div>
   

&nbsp;

<span id="SmgockVc"></span>
## Disable a PTR record

If you need to stop DNS resolution for a PTR record, you can disable the record.

Follow these steps to disable a PTR record:


1. Open the [PTR record](https://console.byteplus.com/dns-suite/dns/publiczone/ptr) page in the BytePlus DNS console.

2. Locate the PTR record you want to disable and click **Disable** in the **Actions** column.

3. Click **Confirm** in the pop\-up dialog box.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After a PTR record is disabled, reverse DNS queries for the associated public IP address may succeed for some users and fail for others. This occurs because Local DNS servers have different cache expiration times.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the cached record has not expired, the user may still receive the cached record value.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the cache has expired, the user will not be able to retrieve the record value.   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The same behavior applies when re\-enabling a previously disabled PTR record.   </div>
   

&nbsp;

<span id="9AspPrVl"></span>
## Enable a PTR record

Follow the steps below to renew a PTR record:


1. Open the [PTR record](https://console.byteplus.com/dns-suite/dns/publiczone/ptr) page in the BytePlus DNS console.

2. Locate the PTR record that you want to enablea and click Enable in the **Actions** column.

3. Click **Confirm** in the pop\-up dialog box.


<span id="LEZGOgED"></span>
## Renew a PTR record

Follow the steps below to renew a PTR record:


1. Open the [PTR record](https://console.byteplus.com/dns-suite/dns/publiczone/ptr) page in the BytePlus DNS console.

2. Locate the PTR record that you want to renew and click **Renew** in the **Actions** column.

3. After confirming the renewal details, click **Next step**, select payment method, and then click **To pay** to complete the payment.


<span id="UR4dIKc4"></span>
## Verify whether a PTR record is active

You can use the `dig` command to verify if a PTR record has taken effect. For example, the following command queries the PTR record corresponding to `1.1.1.1`:

```Bash
dig -x 1.1.1.1
```


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_76dd44fd370991b3f688b632d204e3f7.png) </span>

In this example, the **ANSWER SECTION** returns the corresponding PTR record value: `one.one.one.one.`.

```Plain Text
;; ANSWER SECTION:
1.1.1.1.in-addr.arpa.        300        IN        PTR        one.one.one.one.
```
