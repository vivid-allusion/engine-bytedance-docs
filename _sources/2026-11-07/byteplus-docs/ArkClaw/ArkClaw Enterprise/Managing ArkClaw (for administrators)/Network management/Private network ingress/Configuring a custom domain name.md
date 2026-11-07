---
title: "Configuring a custom domain name"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Configuring-a-custom-domain-name"
---

Administrators can configure a custom domain name for easy recognition and memorization by employees.​ After a custom domain name is configured, employees can access Claw through the private network entry using this domain name.​

<div data-tips="true" data-tips-type="default">Note</div>


<div data-tips="true" data-tips-type="default">Private Network Ingress is currently in the invite\-only beta stage. To request a trial, contact your account manager.</div>


<span id="QQec432K"></span>
### Before you begin


* Ensure no active connections are using the domain to be modified. If any exist, disconnect them first. For procedure, see [Rejecting a connection](https://docs.byteplus.com/en/docs/ArkClaw/Accepting-or-rejecting-a-connection).

* To use a custom domain name, prepare an SSL certificate in advance. You can purchase one from BytePlus (automatically hosted in the Certificate Center after purchase) or upload an existing third\-party CA certificate to BytePlus Certificate Center. For more information, see [What is SSL Certificate](https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-what-is-byteplus-certificate-center).


<span id="Ydql1k3v"></span>
### Procedure


1. Log in to the[ ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. In the "Space Ingress" tab, click the edit icon next to "Access domain".

4. Select "Custom domain"​ as the domain type, enter the custom domain name, and select an SSL certificate from the dropdown list.​

5. Click "OK" to complete the action.
