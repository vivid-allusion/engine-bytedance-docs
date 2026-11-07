---
title: "CDN-Hosted Certificates"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cdn-cert-hosting_en-us"
---

By default, certificates uploaded through BytePlus CDN are stored in the BytePlus Certificate Center. CDN also provides its own certificate hosting capability, but you must [submit a ticket](https://console.byteplus.com/workorder/create) to enable it.

In addition to server certificates, CDN can also host CA certificates. To enable CDN features that depend on a CA certificate (for example, [Mutual TLS](https://docs.byteplus.com/en/docs/byteplus-cdn/mtls_en-us)), upload the corresponding CA certificate to CDN\-hosted storage first.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can host up to 500 certificates in CDN\-hosted storage under your primary account.</div>


Before you enable CDN\-hosted certificates, the **Security Center** menu in the BytePlus CDN console only contains **Certificate Center**. After it is enabled, a separate **CDN\-Hosted Certificates** menu item is added under **Security Center** — that page is the entry point for CDN\-hosted certificate management.

The **CDN\-Hosted Certificates** page provides the following actions at the top:


* **Configure Certificate**: Associate a CDN\-hosted certificate to one or more domain names. For details, see [Configure Certificate](https://docs.byteplus.com/en/docs/18/106489#associate-domains).

* **Upload Certificate**: Upload a certificate to CDN\-hosted storage. For details, see [Upload Certificate](https://docs.byteplus.com/en/docs/18/106489#upload-certificate).


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260604125108-1587189483960.png) </span>

The list below shows all certificates currently hosted in CDN. The fields are described as follows:


|**Field** |**Description** |
|---|---|
|Certificate ID |The ID of the certificate in CDN\-hosted storage. The value starts with `cert_hosting-`. |
|Name |The name of the certificate. |
|Status |The current status of the certificate. Possible values:<br><br><br>* **Active**: The certificate is valid.<br><br>* **Expiring soon**: The certificate expires within one month.<br><br>* **Expired**: The certificate has expired.<br><br><br>You can click the filter icon in the column header to filter by **Active**, **Expiring soon**, or **Expired**. |
|Source |For CDN\-hosted certificates, this field is **CDN\-Hosted**. |
|Type |The certificate type, either **Server Certificate** or **CA Certificate**. |
|Eligible Domains |Domain names in CDN that can be associated with the certificate. |
|Associated Domains |Domain names in CDN that are already associated with the certificate. |
|Issued On |The issuance date of the certificate. |
|Actions |Available actions:<br><br><br>* **Associate Domains**: Associate the certificate to one or more domain names. For details, see [Associate Domains from the Certificate List](https://docs.byteplus.com/en/docs/18/106489#associate-domains-from-the-certificate-list).<br><br>* **Delete**: Delete the CDN\-hosted certificate. |


<span id="upload-certificate"></span>
## Upload Certificate

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Whether you upload a server certificate or a CA certificate, include the full certificate chain in the file.</div>



1. In the left navigation pane of the BytePlus CDN console, choose **Security Center** \> **CDN\-Hosted Certificates**.

2. On the **CDN\-Hosted Certificates** page, click **Upload Certificate**.

3. On the **Upload Certificate** page, configure the fields as described in [Field Reference](https://docs.byteplus.com/en/docs/18/106489#field-reference), and then click **Upload**.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260604125143-1656027129564.png) </span>

<span id="field-reference"></span>
### Field Reference


|**Field** |**Description** |
|---|---|
|Source |Fixed at **CDN\-Hosted**. |
|Type |The type of certificate to upload. Available options:<br><br><br>* **Server Certificate**: Used for HTTPS access to your domain names.<br><br>* **CA Certificate**: Used by CDN features that depend on a CA certificate (for example, [Mutual TLS](https://docs.byteplus.com/en/docs/byteplus-cdn/mtls_en-us)). |
|Upload Method |How the certificate is provided. Available options:<br><br><br>* **Paste Content**: Paste the contents of the certificate and key files.<br><br>* **Upload File**: Upload the certificate and key files directly. |
|Certificate / CA Certificate |The certificate file. The file must contain the full certificate chain, use the `.crt` or `.pem` extension, and start with `-----BEGIN CERTIFICATE-----`.<br><br><br>* When **Type** is **Server Certificate**, this field is labeled **Certificate**.<br><br>* When **Type** is **CA Certificate**, this field is labeled **CA Certificate**. |
|Private Key |The private key file. The file uses the `.key` or `.pem` extension and starts with `-----BEGIN XXX PRIVATE KEY-----`.<br><br>This field is only shown when **Type** is **Server Certificate**. |
|Remark |An optional remark for the certificate. |


<span id="associate-domains"></span>
## Associate Domains

A CDN\-hosted certificate can only be used by your domain names after it is associated with them. The **CDN\-Hosted Certificates** page provides two entry points for this.

<span id="associate-domains-from-configure-certificate"></span>
### Associate Domains from Configure Certificate

Use this entry point to associate the same certificate to multiple domain names in a single flow.

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260604125259-358786596065.png) </span>


1. In the left navigation pane of the BytePlus CDN console, choose **Security Center** \> **CDN\-Hosted Certificates**.

2. On the **CDN\-Hosted Certificates** page, click **Configure Certificate**.

3. In the **Configure Certificate** dialog, complete the following three steps:

   1. **Select Certificate**:

      * **Source**: Fixed at **CDN\-Hosted**.

      * **Type**: Choose **Server Certificate** or **CA Certificate**.

      * **Mode**: Choose **Single Certificate** or **Dual Certificate**.

      * **Select Certificate**: The interaction depends on **Mode**.

         * **Single Certificate**: Pick a single certificate from the list. If the certificate you need is missing, go to [Upload Certificate](https://docs.byteplus.com/en/docs/18/106489#upload-certificate) to upload it first.

         * **Dual Certificate**: In the **Available** list, click **Add** on each target row to move the certificate into the **Selected** list. If the certificate you need is missing, click **Upload Other Certificate** to upload one inline.

         When done, click **Next**.

   2. **Associate Domains**: In the **All** list on the left, select the domain names you want to associate with the certificate. Selected domain names appear in the **Selected** list on the right.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The list only shows domain names eligible for this certificate; offline domain names are not shown.      </div>
      

      When done, click **Next**.

   3. **Pre\-Check**: BytePlus validates the target configuration on each selected domain name. The **Validation Results** table shows the **Status** for each domain name (for example, **No conflicts**).

      To skip a domain name, click **Skip** in its row. When the result looks correct, click **Confirm** to apply.


<span id="associate-domains-from-the-certificate-list"></span>
### Associate Domains from the Certificate List

Use this entry point to quickly associate or adjust domain names for a single certificate.

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260604125429-674452509323.png) </span>


1. In the left navigation pane of the BytePlus CDN console, choose **Security Center** \> **CDN\-Hosted Certificates**.

2. On the **CDN\-Hosted Certificates** page, locate the target certificate in the list and click **Associate Domains** in its **Actions** column.

3. In the **Associate Domains** dialog, complete the following two steps:

   1. **Associate Domains**: In the **All** list on the left, select the domain names you want to associate with the certificate. Selected domain names appear in the **Selected** list on the right.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The list only shows domain names eligible for this certificate; offline domain names are not shown. The current certificate status of each domain name (for example, <strong>Expired</strong>) is also shown to help you filter.      </div>
      

      When done, click **Next**.

   2. **Pre\-Check**: BytePlus validates the target configuration on each selected domain name. The **Validation Results** table shows the **Status** for each domain name. To skip a domain name, click **Skip** in its row. When the result looks correct, click **Confirm** to apply.
