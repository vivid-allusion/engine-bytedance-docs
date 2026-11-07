---
title: "Managing protected websites"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/docs-managing-websites"
---

The website settings page supports viewing all website information added to the WAF instance, such as domain name, source server IP, status, and protection policies enabled or disabled. You can also go to the configuration page of protection policies for each website by clicking on the websites list, or remove the website from the WAF instance.

<span id="0de45e1c"></span>
## Prerequisite

Your websites have been added to the WAF instance.

<span id="a5841343"></span>
## Viewing websites details


1. Log in to the [BytePlus Web Application Firewall Console](https://console.byteplus.com/waf).

2. In the left\-side navigation pane, click **Website settings**.

3. View website information.

   
   |**Parameter** |**Description** |
   |---|---|
   |Website |The domain name of the protected website. Click on the domain name to view the basic information or copy the domain name. |
   |Access type |The way the website is added to the WAF instance. For now, it is **Cloud product**. |
   |Product type |The type of product that website belongs to. For now, it is **CDN**. Before adding to WAF, you should make sure the domain names of the desired websites have been added to CDN. |
   |Status |The protection status of the website.<br><br><br>* Normal: The website is under protection.<br><br>* Abnormal: The website is not under protection. There may be 2 reasons for the malfunction.<br><br>   * The domain name is deleted on CDN. You should add the domain name on CDN again if needed.<br><br>   * Traffic cannot be forwarded from CDN to WAF. Click **Retry** to re\-synchronize the configuration. |
   |Protection policy |Display the enabling status of each protection policy.<br><br><br>* Green: The protection policy is enabled.<br><br>* Gray: The protection policy is disabled.<br><br><br>Click on the protection policy name to enter the configuration page. |
   |Recent attacks |Attack detection on the website in the past 3 days.<br><br><br>* No attack detected.<br><br>* Attacks detected. Click to view attack logs. |
   |Operation |* Protection settings: Click to configure the protection policy page of the website.<br><br>* Delete: Delete the website from the WAF instance. |
   


<span id="d99986e9"></span>
## Editing protection policies


1. Log in to the [BytePlus Web Application Firewall Console](https://console.byteplus.com/waf).

2. In the left\-side navigation pane, click **Website settings**.

3. Go to the configuration page of protection policies.

   * Click the specific policy in the **Protection policy** column.

   * Click **Protection settings** in the **Operation** column.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a1b8f12cc7ca4df6ad9a66cbe8018d28~tplv-goo7wpa0wc-image.image) </span>

4. Configure the desired policies for the website.


<span id="d74345e1"></span>
## Removing the website

The protection policies will be disabled and deleted when the website is removed from the WAF instance.


1. Log in to the [BytePlus Web Application Firewall Console](https://console.byteplus.com/waf).

2. In the left\-side navigation pane, click **Website settings**.

3. Click **Delete** in the **Operation** column.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83df04db0e2c473a8d4ba795e4777561~tplv-goo7wpa0wc-image.image) </span>

4. Click **Delete**.
