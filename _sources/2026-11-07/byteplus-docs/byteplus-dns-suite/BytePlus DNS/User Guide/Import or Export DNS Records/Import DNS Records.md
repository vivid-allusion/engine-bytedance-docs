---
title: "Import DNS Records"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-import-dns-records"
---

This document describes how to import DNS records to BytePlus DNS.

<span id="steps"></span>
## Steps

First, you get a DNS record file. Then, you import the DNS record file to BytePlus DNS.

<span id="step-1-get-a-dns-record-file"></span>
### Step 1: Get a DNS record file

You can create a DNS record file per the general template or export a DNS record file from BytePlus DNS or other DNS service providers.

<span id="create-a-dns-record-file-per-the-general-template"></span>
#### Create a DNS record file per the general template

You can create an .xlsx file, an .xls file, or a .zone file per the general template.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The .zone file uses the standard BIND format to describe the DNS records. You can refer to <a href="https://datatracker.ietf.org/doc/html/rfc1034">RFC 1034</a> and <a href="https://datatracker.ietf.org/doc/html/rfc1035">RFC 1035</a> for more information.</div>


<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c8a410bfb444a3d805fb0efdd750abc~tplv-goo7wpa0wc-image.image" name="template.xlsx">template.xlsx</Attachment>


&nbsp;

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bacd9bef58e544129634a2da51002f93~tplv-goo7wpa0wc-image.image" name="template.xls">template.xls</Attachment>


&nbsp;

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a70aca072d149238b176ec094d33abc~tplv-goo7wpa0wc-image.image" name="template.zone">template.zone</Attachment>


<span id="export-a-dns-records-file-from-dns-providers"></span>
#### Export a DNS records file from DNS providers

Alternatively, you can directly import a DNS record file exported from BytePlus DNS or third\-party DNS providers. BytePlus DNS allows you to import DNS record files exported from the following third\-party DNS providers:


* Alibaba Cloud DNS

* Tencent Cloud DNSPod

* Huawei Cloud DNS

* AWS Route53

* CloudFlare DNS

* Akamai Edge DNS


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Each file you upload must not exceed 2 MB in size. Each file can contain a maximum of 1000 DNS records. If your file contains more than 1000 DNS records, only the first 1000 records will be imported.</div>


<span id="dec5ade1"></span>
### Step 2: Import DNS records


1. Open the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns).

2. Go to the **Domain management** page. Click on your domain in the **Domain** column.

3. On the **Record management** tab, click **Import records**.

4. On the **Import records** page, select an import mode in **Import mode**. You can choose from the following modes:

   * **Incremental import**: The existing DNS records under the current domain remain unchanged. The console will add the DNS records from the uploaded file.

   * **Full import**: The console will delete all existing DNS records under the current domain. Then, the console will add the DNS records from the uploaded file.

   <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="1">danger   </div>
   

   <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">If you need to perform a full import, we recommend that you export the current DNS records of the domain as a backup in advance. This will prevent any impact on your online business.   </div>
   

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_65c9174fcfd02203b8a0e3cc33d12b3b.jpeg) </span>


5. On the **Import records** page, select a template in **Template**. You can choose from the following templates:

   * **General template**: Allows you to upload the following types of files:

      * .xls, .xlsx, or .zone files created based on the general template. See [General template description](https://docs.byteplus.com/en/docs/36/8480#general-template-description).

      * .xls, .xlsx, or .zone files exported from BytePlus DNS.

   * **AWS Route53**: Allows you to upload .zone files exported from AWS Route53. AWS Route53 itself currently does not support exporting .zone files. You can use the [third-party open-source tool cli53](https://github.com/barnybug/cli53) to export .zone files from AWS Route53.

   * **CloudFlare DNS**: The Zone file exported from CloudFlare DNS is in .txt format. You must change the file extension to .zone to upload it to BytePlus DNS. See [CloudFlare Official Documentation](https://developers.cloudflare.com/dns/manage-dns-records/how-to/import-and-export/).

   * **Akamai Edge DNS**: Allows you to upload .zone files exported from Akamai Edge DNS. See [Akamai Official Documentation](https://techdocs.akamai.com/edge-dns/docs/welcome-edge-dns).

   * **Alibaba Cloud DNS**: Allows you to upload .xls, .xlsx, or .zone files exported from Alibaba Cloud DNS. See [Alibaba Cloud Official Documentation](https://www.alibabacloud.com/help/en/dns/import-dns-records).

   * **Tencent Cloud DNSPod**: Allows you to upload .xls, .xlsx, or .zone files exported from Tencent Cloud DNSPod. See [Tencent Cloud Official Documentation](https://docs.dnspod.com/dns/dns-record-file-format-description/).

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">It is recommended to convert the .xls file exported from Tencent Cloud DNSPod to .xlsx format before uploading. Otherwise, the DNS record import may fail.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">BytePlus DNS imports weights in .xls and .xlsx files. If the weight exceeds the limitation of the current edition of the domain, the import operation fails. Also, BytePlus DNS ignores comments in .zone files exported from Tencent Cloud DNSPod.      </div>
      

   * **Huawei Cloud DNS**: Allows you to upload .xls, .xlsx, or .zone files exported from Huawei Cloud DNS. See [Huawei Cloud Official Documentation](https://support.huaweicloud.com/intl/en-us/usermanual-dns/dns_usermanual_0024.html).

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">BytePlus DNS will import weights in .xls and .xlsx files exported from Huawei Cloud DNS. If the weight exceeds the limitation of the current edition of the domain, the import operation fails.      </div>
      

6. Click the file upload area to upload the file.

7. After the file is successfully uploaded, click **Start import**. Once the import is complete, the console will display the import result. If some of your DNS records fail to import, you can refer to the **Failed reason** and check the [FAQs](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-frequently-asked-questions) for solutions.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_6592d0dda65adf91b7eeee5a2357af80.jpeg) </span>

&nbsp;

<span id="general-template-description"></span>
## General template description

<span id="xls-xlsx-file"></span>
### .xls/.xlsx file

The content of the .xls/.xlsx file needs to follow the following template:


|**Domain Name** |**Domain Prefix** |**Record Type** |**Line** |**TTL** |**Record Value** |**Enable** |
|---|---|---|---|---|---|---|
|www.example.com |www |A |default |600 |1.1.1.1 |True |
|@.example.com |@ |A |default |600 |1.1.1.1 |False |


<span id="a0243ba0"></span>
### .zone file

The content of the `.zone` file needs to follow the following template:

```Plain
www.example.com.    600           IN    A        1.1.1.1 
@.example.com.      600           IN    A        1.1.1.1
```


Where:


* The first column is the FQDN, which is a combination of the domain prefix and the second\-level domain.

* The second column is the TTL.

* The value in the third column must be `IN`. You can also omit this column in the `.zone` file.

* The fourth column is the record type.

* The fifth column is the record value.


<span id="f9eaaf7e"></span>
### Field comparison

Compared to the `.xls/.xlsx` file, the `.zone` file does not include the following fields:


* **Line**: After importing the `.zone` file, the console will automatically set the **Line** of the relevant DNS records to `default`.

* **Domain Prefix**: After importing the `.zone` file, the console will automatically fill in the domain prefix from the complete domain name into the relevant DNS records.

* **Enable**: After importing the `.zone` file, the console will automatically set the **Enable** of the relevant DNS records to True.


<span id="d430160e"></span>
### Field reference


* **Domain Name**: You can set it to the following values:

   * The FQDN of the DNS record, which is a combination of the domain prefix and the second\-level domain. For example, `www.example.com`.

   * The second\-level domain of the DNS record. For example, `example.com`.

* **Domain Prefix**: The domain name prefix. See [Create DNS Records](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-creating-updating-or-deleting-dns-records).

* **Record Type**: See [Supported DNS Record Types](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-supported-dns-record-types).

* **Line**: The region and ISP corresponding to the DNS record. If you want the DNS record to correspond to all regions and ISPs, you can set the **Line** to **default**. By setting the line, you can configure [DNS-based routing](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-intelligent-dns-based-routing) for the domain. The supported values for this field can be found in the **Line Code** field of [Supported Lines](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-supported-lines). You can find the corresponding line code based on the **Line Name** field.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You can only use line codes, such as <code>os_euro_es</code>, as the value of <strong>Line</strong>. Line names are not supported. For example:   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The DNS record <code>www.example.com www A Europe_Spain 600 1.1.1.1 True</code> will return an error "Line is invalid".   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The DNS record <code>www.example.com www A os_euro_es 600 1.1.1.1 True</code> has a line that complies with the rules.   </div>
   

* **TTL**: The expiration time of the DNS record. See [Create DNS Records](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-creating-updating-or-deleting-dns-records).

* **Record Value**: See [Supported DNS Record Types](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-supported-dns-record-types).

* **Enabled**: Whether to enable the DNS record.

   * True: Enable the DNS record.

   * False: Disable the DNS record.
