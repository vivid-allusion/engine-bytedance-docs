---
title: "Import DNS Records"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/9UKJkK"
---

This document introduces how to create a DNS record file and import the DNS records from the file for a specified domain.

<span id="steps"></span>
## Steps

Complete the following steps to import DNS records.

<span id="step-1-create-a-dns-record-file"></span>
### Step 1: Create a DNS record file

The console only supports uploading `.xlsx` or `.xls` files or `.zone` files. You can refer to the following file templates to create `.xlsx`, `.xls` files or `.zone` files. Additionally, you can directly import [DNS records exported from the console](https://docs.byteplus.com/docs/byteplus-dns-suite/gsFtGn).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The <code>.zone</code> file uses the standard BIND format to describe the DNS records. You can refer to <a href="https://datatracker.ietf.org/doc/html/rfc1034">RFC 1034</a> and <a href="https://datatracker.ietf.org/doc/html/rfc1035">RFC 1035</a> for more information.</div>


<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_3ae5bf087401b9f381031d20f003d506.xls" name="template.xls">template.xls</Attachment>


&nbsp;

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_1c7bd2629e2d169fbfd43659e5070b9b.xlsx" name="template.xlsx">template.xlsx</Attachment>


&nbsp;

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4a9c041a5e4f2e9817575a1106b0216b.zone" name="template.zone">template.zone</Attachment>


<span id="step-2-import-dns-records"></span>
### Step 2: Import DNS records


1. Open the [BytePlus PrivateZone console](https://console.byteplus.com/dns-suite/privatezone).

2. Go to the **Domain management** page. Click on your domain in the **Domain** column.

3. On the **Record management** tab, click **Import records**.

4. On the **Import records** page, select an import mode. You can choose from the following modes:

   * **Incremental import**: The existing DNS records under the current domain remain unchanged. The console will add the DNS records from the uploaded file.

   * **Full import**: The console will delete all existing DNS records under the current domain. Then, the console will add the DNS records from the uploaded file.


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">If you need to perform a full import, we recommend that you export the current DNS records of the domain as a backup in advance. This will prevent any impact on your online business.</div>



5. Click the file upload area to upload the file. You can upload files in the following formats:

   *  **.xlsx**

   *  **.xls**

   *  **.zone**

6. After the file is successfully uploaded, click **Start import**. Once the import is complete, the console will display the import result.


If your DNS records fail to import, you can refer to the **Failed reason** and check the [FAQs](https://docs.byteplus.com/byteplus-dns-suite/docs/frequently-asked-questions) for solutions.

<span id="dceb810c"></span>
## Template description

<span id="0b18600d"></span>
### .xls/.xlsx file

The content of the `.xls/.xlsx` file needs to follow the following template:


|**Domain Name** |**Domain Prefix** |**Record Type** |**Line** |**TTL** |**Record Value** |**Enable** |
|---|---|---|---|---|---|---|
|www.example.com |www |A |default |600 |10.0.0.1 |True |
|@.example.com |@ |A |default |600 |10.0.0.1 |False |


<span id="a0243ba0"></span>
### .zone file

The content of the `.zone` file needs to follow the following template:

```Plain
www.example.com.    600           IN    A        10.0.0.1 
@.example.com.      600           IN    A        10.0.0.1
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

* **Domain prefix**: After importing the `.zone` file, the console will automatically fill in the domain prefix from the complete domain name into the relevant DNS records.

* **Enable**: After importing the `.zone` file, the console will automatically set the **Enable** of the relevant DNS records to True.


<span id="d430160e"></span>
## Field Reference


* **Domain**: You can set it to the following values:

   * The full domain name of the resolution record, which is a combination of the host record and the secondary or multi\-level domain name. For example, `example.internal.com`.

* **Domain prefix**: The prefix of the domain name. Depending on the value of **Domain**, you can set the **Domain prefix** to the following values:

   * **Empty value**: If you set the **Domain** to the full domain name, you can set the **Domain prefix** to an empty value.

   * **Actual domain prefix value**: If you set the **Domain** to the full domain name, secondary domain name, or multi\-level domain name, you can set the **Domain prefix** to the actual domain prefix value.

* **Record type**: The type of the record. For more information on record types, refer to [DNS Record Types](https://docs.byteplus.com/docs/byteplus-dns-suite/prQAdU).

* **Line**: The VPC subnet ID corresponding to the resolution record.

   * If the specified domain name has enabled [Intelligent DNS](https://docs.byteplus.com/docs/byteplus-dns-suite/-Gvd2s), you need to fill in the VPC subnet ID corresponding to the resolution record, such as `subnet-3rfajeb0ufif45zsk2iw82ttd`. You can also fill in `default` to use the IP addresses of all subnets in the VPC.

   * If the specified domain name has disabled [Intelligent DNS](https://docs.byteplus.com/docs/byteplus-dns-suite/-Gvd2s), you need to fill in `default`.

* **TTL**: The expiration time of the resolution record, in seconds. If your resolution record does not change frequently, you can set a longer expiration time. For TTL restrictions, refer to [Editions](https://docs.byteplus.com/docs/byteplus-dns-suite/0K0WyX).

* **Record value**:

   * A: Points the domain name to an IPv4 address. For example, `10.10.10.10`.

   * AAAA: Points the domain name to an IPv6 address. For example, `ff03:0:0:0:0:0:0:c1`.

   * CNAME: Points the domain name to another domain name. For example, `www.example.com`.

   * MX: Points the domain name to the mail server address. The format is `<priority> <domain name>`. For example, `10 www.example.com`. The priority is a number ranging from 1 to 99.

   * TXT: Stores additional text for the domain name, usually used for SPF records and domain ownership verification.

   * PTR: Resolves an IP address to a domain name. For example, `example.internal.com`.

* **Enabled**: Whether to enable the record.

   * True: Enable the record.

   * False: Disable the record.
