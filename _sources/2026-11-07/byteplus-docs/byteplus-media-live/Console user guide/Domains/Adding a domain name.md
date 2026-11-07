---
title: "Adding a domain name"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-domain"
---

This page details the basic operations you can perform with a domain name, including adding, disabling, enabling and deleting a domain name.

<span id="bb9e1337"></span>
## Adding domain names

To use BytePlus MediaLive, you need to add at least two domain names, one for stream pushing, and the other for stream pulling.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each domain name is associated with a unique BytePlus account ID. Users can re\-add a domain name if they have previously deleted it themselves. However, it is not possible to add a domain name that has already been added by another user.</div>


<span id="0020f4f0"></span>
### Context

MediaLive uses a domain name space to associate domain names for stream pushing and pulling. Domain names for stream pushing and pulling that serve the same line of business need to be in the same domain name space. Refer to [Domain name space](https://docs.byteplus.com/docs/byteplus-media-live/docs-glossary#Vhost) for more details.

<span id="dfaf1970"></span>
### Prerequisite


* If you want to include the Chinese mainland in your acceleration region, you must get an Internet Content Provider (ICP) license for the domain names. You can complete the verification process on the [ICP/IP Address/Domain Name Information Filing Management System](https://beian.miit.gov.cn/#/Integrated/index).

* If you want to use the [Real Time Media (RTM)](https://docs.byteplus.com/en/byteplus-media-live/docs/introduction) protocol, you must configure an SSL certificate for your domain names.


<span id="ede4d646"></span>
### Procedure


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, click **Domains**.

3. Click **Add domain name** on the **Domains** page that appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9a352edba664b328bc21c588bc8a64a~tplv-goo7wpa0wc-image.image) </span>

   The parameters needed to be filled in are described in the table below:

   
   |**Parameters** |**Description** |
   |---|---|
   |**Add domain name** |1. Select **Push** or **Pull** as the domain name type. You cannot change the domain name type after the domain name is added.<br><br>2. Enter a domain name for stream pushing or pulling. You cannot add a wildcard domain name. We recommend that you use a second\-level domain name, such as `example.live.com`. You can add a maximum of 10 domain names under each account.<br><br>3. Select the region where you want to accelerate content delivery. The live\-streaming service fees vary depending on the acceleration region. Refer to [Live-streaming service fees](https://docs.byteplus.com/docs/byteplus-media-live/docs-live-streaming-service-fees) for detailed pricing information.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you select <strong>Global acceleration</strong> or <strong>The Chinese mainland</strong>, you must get an Internet Content Provider (ICP) license for the domain name.   </div><br>   <br><br>4. If you want to use the [Real Time Media (RTM)](https://docs.byteplus.com/en/byteplus-media-live/docs/introduction) protocol, you must configure an SSL certificate for your domain names. |
   |**Associate with domain name space** |The domain name space must be lowercase and should be a second\-level domain or higher. We recommend that you use the first domain name added as the name of the domain name space.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can add a maximum of 10 domain name spaces under each account. If you need more domain name spaces, please contact <a href="https://www.byteplus.com/en/support">BytePlus technical support</a>.</div><br> |
   |**Project** |For a new domain name space, you must select a project. After the domain name space is associated with a project, you can manage resources used by different businesses or projects in groups to achieve project\-based bill viewing, sub\-account authorization, and other functions. |
   

4. Click **Next** to save the settings.

5. Configure a CNAME record for your domain name by following the steps in [Adding a CNAME record](https://docs.byteplus.com/docs/byteplus-media-live/docs-adding-a-cname-record).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After you configure the CNAME record for your domain name, please allow approximately 15 minutes for the change to take effect. You can refresh the console page to verify if the CNAME record has been resolved.   </div>
   

<span id="f03302e5"></span>
## Managing domain names

After adding a domain name, you can disable or enable a domain name or remove it from the console.

<span id="11a495d4"></span>
### Procedure


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, click **Domains**.

3. On the **Domains** page that appears, find the domain name that you are about to configure, click **Disable** or **Enable** in the **Actions** column to disable or enable a domain name, or click **Delete** in the **Actions** column to remove a domain name.


<span id="f2d5069d"></span>
### Result


* Deleted domain names are dissociated from their domain name space. If you re\-add these domain names, BytePlus MediaLive will re\-associate them with the corresponding domain name spaces.

* After you delete a domain name, BytePlus MediaLive will keep the corresponding domain name space in order to preserve the history data.

* You can query the usage, stream data, and other statistics of a deleted domain name.


The following table lists the differences between disabling and deleting a domain name:


| |**Disabling a domain name** |**Deleting a domain name** |
|---|---|---|
|**CNAME** |The domain name stops pointing to the assigned CNAME address. |The CNAME address is deleted. |
|**Domain name space** |No changes. |The domain name is deleted, but the domain name space remains. |
|**Certificate** |No changes. |The related certificate is dissociated from the domain name. |
|**Domain settings** |No changes. |Related domain settings are deleted. |


Suppose you delete a domain name and then add it to your account again:


|**Action** |**Results** |
|---|---|
|Delete the `pull.a.com` domain name for stream pulling |* The domain name, `pull.a.com`, is deleted from the domain name space, `pull.a.com`.<br><br>* The related certificate is dissociated from the domain name.<br><br>* If this domain name is associated with one for stream pushing, the association is removed.<br><br>* Related configurations are deleted, including URL authentication, referer, and IP blocklist and allowlist. |
|Re\-add the `pull.a.com`domain name for stream pulling |* The domain name, `pull.a.com`, is added to the domain name space, `pull.a.com`.<br><br>* The domain name is not associated with any certificate.<br><br>* The domain name is not associated with any domain name for stream pushing.<br><br>* Related configurations are disabled, including URL authentication, referer, and IP blocklist and allowlist. |
|Delete the `push.a.com` domain name for stream pushing |* The domain name, `push.a.com`, is deleted from the domain name space, `push.a.com`.<br><br>* The related certificate is dissociated from the domain name.<br><br>* If this domain name is associated with one for stream pulling, the association is removed.<br><br>* Related configurations are deleted, including URL authentication and IP blocklist and allowlist. |
|Re\-add the `push.a.com` domain name for stream pushing |* The domain name, `push.a.com`, is added to the domain name space, `push.a.com`.<br><br>* The domain name is not associated with any certificate.<br><br>* If the domain name was associated with a domain name for stream pulling before deletion, association is resumed.<br><br>* URL authentication is enabled by default.<br><br>* IP blocklist and allowlist are disabled. |
