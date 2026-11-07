---
title: "Configuring a custom enterprise domain (old version)"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/configuring-a-custom-enterprise-domain-old-version"
---

This topic describes how to configure a custom enterprise domain for the ArkClaw public network ingress, enabling access to the ArkClaw service using your own enterprise domain.

<span id="oZr9rqoE"></span>
## Before you begin


* Domain preparation: Have a registered, available public domain. This domain must have completed Internet Content Provider (ICP) filing or access filing.

* Certificate preparation: Custom domains only support HTTPS access and must be bound to a valid SSL certificate. Prepare a compliant certificate in advance (PEM format, containing both the certificate and private key files).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Currently, SM2 certificates are not supported. Please use RSA/ECC certificates.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">ArkClaw Enterprise is integrated with <a href="https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-what-is-byteplus-certificate-center">BytePlus Certificate Center</a>. Please purchase, upload, or manage your certificates in the certificate center. For related actions, see <a href="https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-manageing-ssl-certificates">Certificate management</a>.   </div>
   


<span id="vVkn1oIm"></span>
## Use limits


* Only administrators of the enterprise space can configure this feature.

* An enterprise space supports binding only 1 custom domain, and that domain can only be bound to 1 login entry.


<span id="gVKnXRtS"></span>
## Procedures

<span id="9Kuk6zH4"></span>
### Configure in the ArkClaw Enterprise console


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise?_vtm_=a78999.b69280.0_0.0_0.0.49_7646310380663539205) with an administrator account.

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. On the "Network Configuration" page, locate the "Public network ingress" section and click "Edit".

4. On the "Custom domain for public network ingress" page, locate the "Method 1: Custom enterprise domain" section, then configure the following settings.

   
   |Configuration item |Description |
   |---|---|
   |Configure custom domain name |Click the "Configure custom domain name" toggle to set it to "Enabled". |
   |Custom domain name |Input your registered, ICP\-filed domain in the "Custom domain name" input field.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Wildcard domains (e.g., <code>*.example.com</code>) are currently not supported. Please bind a specific subdomain or the root domain.</div><br> |
   |Certificate configuration |<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When configuring a certificate for the first time, you must complete cross\-service authorization. After authorization, ArkClaw can read your certificate information from the Certificate Center and provide it for selection. If authorization is not completed, the certificate list cannot be fetched.</div><br><br><br><br>1. Select project: Choose the project containing the certificate from the left dropdown. The system defaults to the "default" project.<br><br>2. Select certificate: After switching projects, select the SSL certificate that matches your custom domain from the right dropdown.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If no certificates are available in the current project, click "+ Upload certificate​" at the bottom of the dropdown. The system will guide you to <a href="https://console.byteplus.com/certificate-center/ssl/certificate?showUploadCertDrawer=true">BytePlus Certificate Center</a> for upload. For details, see <a href="https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-uploading-an-ssl-certificate">Uploading an SSL certificate</a>. After uploading, return to this page, refresh the certificate list, and you can select the newly uploaded certificate.   </div><br>   <br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning"><strong>Monitor certificate validity</strong>: Keep close track of your certificate's validity. Once a certificate expires, the custom domain will become inaccessible via HTTPS, impacting your service.</div><br><br><br>   <div data-tips="true" data-tips-type="warning">BytePlus Certificate Center sends alert notifications via SMS, email, and internal messages before certificates expire. Please <a href="https://docs.byteplus.com/en/docs/byteplus-certificate-center/certificate-messages">ensure the contact information (phone, email, etc.) associated with your account is accurate and valid</a>, and pay attention to these reminders to renew or replace certificates in advance.   </div><br>   <br><br>* <div data-tips="true" data-tips-type="warning"><strong>Manual replacement</strong>: ArkClaw does not​ provide automatic certificate renewal or replacement. To avoid service interruption, you must proactively update and rebind the certificate in the ArkClaw console before it expires.</div><br> |
   

5. After configuration, click "OK" in the bottom\-right corner.

   After a successful addition, you can view the full "Login link," configuration status, and associated "Certificate name" in the "Custom enterprise domain"​ field.


&nbsp;

<span id="lU5U9zRp"></span>
### Configure a CNAME record

After configuring a custom enterprise domain for the ArkClaw public network ingress, you must go to the DNS provider for your domain and add a CNAME record to point the custom domain to the ArkClaw service's default domain. Without this record, requests sent via the custom domain cannot be resolved to the ArkClaw service.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After adding the CNAME record, please wait for the configuration to take effect. The CNAME propagation time depends on the TTL value you set (typically ranging from 10 minutes to 24 hours).</div>


<span id="wDyN88co"></span>
#### Get the ArkClaw default domain

In the "Public network ingress"​ section of the "Network Configuration​" page, locate the "Employee login link". Copy the complete default domain, which will be used as the record value​ for the CNAME record.

<span id="USnnhOh5"></span>
#### Configuration procedures

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This topic uses BytePlus DNS as an example to demonstrate the CNAME record configuration procedure. For detailed steps, see <a href="https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-creating-updating-or-deleting-dns-records">Add DNS records</a>. If you use a different DNS provider, follow the general steps below and consult its official documentation.</div>



1. Log in to the [BytePlus DNS Suite](https://console.byteplus.com/dns-suite/dns/publiczone/zones) console.

2. On the Domain management page, locate the domain you bound to ArkClaw, and click the domain name to enter the DNS records page.

3. On the "Record management" tab, click "Create record set".

4. In the "Create record set" pane, configure the following information as required. Leave other parameters as default.

   
   |**Configuration item** |**Description** |
   |---|---|
   |Record type |Select "CNAME" to point your domain to another domain. |
   |Domain name |Input the host record (domain prefix). Complete the subdomain to be resolved.<br><br><br>* To resolve `www.example.com`, set the host record to `www`.<br><br>* To resolve `example.com`, set the host record to `@`. |
   |Record value |Input the default domain obtained from the ArkClaw service. |
   

5. Click "Submit" to complete the configuration.


<span id="6dXt9Oub"></span>
## Manage a custom enterprise domain

<span id="PCQl8rBy"></span>
### Update a custom enterprise domain

If you have already configured a custom enterprise domain, you can modify the existing configuration by following the steps below.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise?_vtm_=a78999.b69280.0_0.0_0.0.49_7646310380663539205) with an administrator account.

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. On the "Network Configuration" page, locate the "Public network ingress" section and click "Edit".

4. On the "Custom domain for public network ingress" page, locate the "Method 1: Custom enterprise domain" section, then configure the following settings.

   
   |Configuration item |Description |
   |---|---|
   |Configure custom domain name |Enable this toggle. |
   |Custom domain name |Input your registered, ICP\-filed domain in the "Custom domain name" input field. |
   |Certificate configuration |1. Select project: Choose the project containing the certificate from the left dropdown. The system defaults to the "default" project.<br><br>2. Select certificate: After switching projects, select the SSL certificate that matches your custom domain from the right dropdown.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If no certificates are available in the current project, click "+ Upload certificate​" at the bottom of the dropdown. The system will guide you to <a href="https://console.byteplus.com/certificate-center/ssl/certificate?showUploadCertDrawer=true">BytePlus Certificate Center</a> for upload. For details, see <a href="https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-uploading-an-ssl-certificate">Uploading an SSL certificate</a>. After uploading, return to this page, refresh the certificate list, and you can select the newly uploaded certificate.   </div><br>   <br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning"><strong>Monitor certificate validity</strong>: Keep close track of your certificate's validity. Once a certificate expires, the custom domain will become inaccessible via HTTPS, impacting your service.</div><br><br><br>* <div data-tips="true" data-tips-type="warning"><strong>Manual replacement</strong>: ArkClaw does not​ provide automatic certificate renewal or replacement. To avoid service interruption, you must proactively update and rebind the certificate in the ArkClaw console before it expires.</div><br> |
   

5. After configuration, click "OK" in the bottom\-right corner.

   After a successful action, you can view the updated full login address in the "Custom enterprise domain"​ field.

6. After modifying the custom domain, remember to update the CNAME record with your DNS provider to point the new domain to the ArkClaw default login link. For specific steps, see [Configure a CNAME record](https://docs.byteplus.com/en/docs/ArkClaw/configuring-a-custom-enterprise-domain-old-version?lang=en#lU5U9zRp).


<span id="RHbrRS6q"></span>
### Delete a custom enterprise domain

If you have already configured a custom enterprise domain, you can delete the existing configuration by following the steps below.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise?_vtm_=a78999.b69280.0_0.0_0.0.49_7646310380663539205) with an administrator account.

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. On the "Network Configuration" page, locate the "Public network ingress" section and click "Edit".

4. On the "Custom domain for public network ingress" page, locate the "Method 1: Custom enterprise domain" section.

5. Click the "Configure custom domain name" toggle to set it to "Disabled", then click "OK".

   After a successful action, the configured custom enterprise domain is deleted.


&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;
