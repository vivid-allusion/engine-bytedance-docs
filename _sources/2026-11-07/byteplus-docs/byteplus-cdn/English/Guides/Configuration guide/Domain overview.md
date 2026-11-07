---
title: "Domain overview"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-add-domain-name_1"
---

To accelerate content delivery for your website, you need to add your domain name to the BytePlus CDN. This guide provides step\-by\-step instructions on how to add a domain, configure its settings, and perform other essential management operations such as enabling, disabling, deleting, and viewing its history. It also details the various checks the CDN performs when you add a domain to ensure a smooth setup process.

<span id="overview"></span>
## Overview

To direct requests for your domain name to the CDN, you must first add your domain name to the CDN. After adding your domain name, the CDN will assign a CNAME to it. You only need to create a CNAME record with your domain name's DNS provider. In this record, point your domain name to this CNAME. Afterward, all requests to your domain name will be directed to the CDN.

When adding your domain name to the CDN, you need to perform some general configurations for your domain name and bind it to a delivery policy. The delivery policy is the configuration of CDN functionalities, such as the origin server configuration that defines how the CDN accesses your origin server.

<span id="add-domain-names"></span>
## Add Domain Names

<span id="prerequisites"></span>
### Prerequisites

There must be a published delivery policy in the CDN.

To create and publish a delivery policy, refer to [Policy Overview](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-policy).

<span id="steps"></span>
### Steps


1. Log in to the [BytePlus CDN Management Console](https://console.byteplus.com/cdn).

2. In the left navigation bar, click **Domain Names**.

3. On the **Domain Names** page, click **Add Domain Names**.

4. On the **Add Domain Names** page, configure according to the configuration instructions below.

5. After completing the configuration, click **OK**.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260804135931-11713815884.png) </span>

<span id="configuration-instructions"></span>
#### Configuration Instructions


|**Configuration** |**Description** |
|---|---|
|Service Region |Specifies the service region. The cache nodes within this region are responsible for responding to user requests. The service region provided by CDN is **Outside Chinese Mainland**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you need to specify a service region that includes Chinese Mainland, please <a href="https://console.byteplus.com/workorder/create">submit a ticket</a>. Before adding a domain name with a service region that includes Chinese Mainland in CDN, your BytePlus account must complete <a href="https://console.byteplus.com/user/authentication/">real\-name authentication</a>.</div><br><br><br>If a request comes from a country or region not within your specified service region, the CDN will still use nodes within the specified service region to respond to the request. In this case, the data transfer speed will be slower. |
|Chinese Mainland Optimization |Improves performance for users in the Chinese Mainland when they access CDN domains whose service region is set to **Outside the Chinese Mainland**. You cannot enable this setting while adding a domain. After the domain is created, you can enable it on the domain details page. Before you enable it, authorize BytePlus CDN to use BytePlus Global Accelerator and make sure an available accelerator is ready. For more information, see [Manage Chinese Mainland Optimization Accelerators](https://docs.byteplus.com/en/docs/byteplus-cdn/cross-mlc-border-acceleration_en-us). |
|Domain Name |Indicates the domain name you want to add. If you want to add multiple domain names, click **Add Domain Names**. You can add 50 domain names at a time.<br><br>&nbsp;<br><br>The domain names you add must meet the following conditions:<br><br><br>* The domain name must not be longer than 100 characters.<br><br>* The domain name cannot contain uppercase letters or Chinese characters.<br><br>* The domain name must not be the same as an existing domain name under the primary account.<br><br>* The domain name does not contain these suffixes: zjgslb.com, yangyi19.com, volcgslb.com, veew\-alb\-cn1.com, bplgslb.com, bplslb.com, ttgslb.com.<br><br><br>**About Domain Check**<br><br>When you add a domain in CDN, CDN performs a series of checks on the domain. If the domain fails any check, you will receive a corresponding error message. See [Domain Check](https://docs.byteplus.com/en/docs/18/6593#domain-check).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the service region is <strong>Global</strong> or <strong>Chinese Mainland</strong>, your domain name must have an ICP registration in China, and your BytePlus account must complete <a href="https://console.byteplus.com/user/authentication/">Real\-name Authentication</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you want to add a wildcard domain, please <a href="https://console.byteplus.com/workorder/create">submit a ticket</a>.</div><br> |
|Project |Indicates the project to which the domain name belongs. In the CDN, each domain name must belong to a project. The default project is `default`. |
|Delivery Policy |Indicates the delivery policy to be bound to the domain name. |
|Encryption |Indicates whether to enable HTTPS access for your domain name. This configuration is disabled by default. If you enable this configuration, users will be able to access your domain name using the HTTPS protocol.<br><br>&nbsp;<br><br>After enabling this configuration, you need to specify a certificate. This certificate must be uploaded to the certificate center.<br><br>&nbsp;<br><br>If you also need to enable HTTPS\-based security features, you need to bind the domain name to an existing encryption policy. This encryption policy includes the configuration of these security features.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This configuration is disabled (grayed out) when you add multiple domain names at once. In this case, after adding the domain names, you can associate the added domain names with the corresponding certificates on the <strong>Certificate Center</strong> page.</div><br> |


<span id="other-domain-name-operations"></span>
### Other Domain Name Operations

In the **Actions** column of the domain list, you can perform the following operations on a domain name:


|**Action** |**Description** |
|---|---|
|Manage |View or modify general configurations of the domain. You can modify the project that the domain belongs to, domain tags, policies bound to the domain, and certificates associated with the domain.<br><br>&nbsp;<br><br>Additionally, you can enable Edge Functions for the domain name. In Edge Functions, you can create functions to handle user requests. Refer to [Edge Functions](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-overview-of-edge-function). |
|Enable |Enable a domain name that is in the **Disabled** status. After enabling a domain name, its status will be **Enabled**. |
|Disable |Disable a domain name that is in the **Enabled** status. After disabling a domain name, its status will be **Disabled**.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After a domain name is disabled, the CDN will not delete the domain name's configuration, but the CNAME assigned to the domain name by the CDN will be resolved to 127.0.0.1. When accessing the domain name, users will receive a 403 status code. Before disabling a domain name, please resolve the domain name to a valid address with your domain name's DNS provider.</div><br><br><br><div data-tips="true" data-tips-type="warning"></div><br><br><br><div data-tips="true" data-tips-type="warning">If a domain name is still resolved to your domain name's CNAME after being disabled, the CDN's 403 response to user requests will generate a small amount of traffic, and this traffic will be billed.</div><br> |
|Delete |Delete a domain name that is in the **Disabled** status.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After a domain name is deleted, the CDN will permanently delete the domain name's configuration and access logs. When accessing the domain name, users will receive a 404 status code. If you no longer need a domain name, it is recommended to disable the domain name instead of deleting it.</div><br><br><br><div data-tips="true" data-tips-type="warning"></div><br><br><br><div data-tips="true" data-tips-type="warning">Before deleting a domain name, please ensure that the domain name has been resolved to a valid address.</div><br> |
|History |View the operation history of a domain name. The list shows up to the 10 most recent operations for the domain name.<br><br>The operation history records the following types of operations:<br><br><br>* Add domain name<br><br>* Change configurations<br><br><br>For **Change configurations**, you can view the differences before and after the changes. |


<span id="export-domain-name-configurations"></span>
### Export Domain Name Configurations

Click the export button at the top right of the domain list to export all its contents. The name of the export file is `ByteplusCDN\<AccountID\>_\<ExportTime\>.csv`.

<span id="more-information"></span>
## More Information

<span id="domain-check"></span>
### Domain Check

When you add a domain in CDN, CDN performs the following checks on the domain to be added.

<span id="domain-specification-check"></span>
#### Domain Specification Check

If the domain to be added does not comply with the domain specifications described in the **Domain Name** configuration instructions, you will receive a corresponding error message.

<span id="domain-quota-check"></span>
#### Domain Quota Check

If the number of domains under your primary account has reached the limit, you cannot add more domains. To add more domains, please [submit a ticket](https://console.byteplus.com/workorder/create).

<span id="wildcard-domain-check"></span>
#### Wildcard Domain Check

By default, you cannot add wildcard domains in CDN. To add wildcard domains, please [submit a ticket](https://console.byteplus.com/workorder/create).

<span id="conflict-domain-check"></span>
#### Conflict Domain Check

In CDN, if the domain to be added meets any of the following conditions, you cannot add the domain. Such a domain is called a "conflict domain."


* The domain to be added already exists under your primary account.

* The domain to be added already exists under another BytePlus primary account.

* There is a wildcard domain under another BytePlus primary account that includes the domain you want to add. For example, a wildcard domain `*.example.com` already exists under another BytePlus primary account. The domain you are trying to add is `my.example.com`.

* You are trying to add a wildcard domain, but there is already a subdomain included in that wildcard domain under another BytePlus primary account. For example, `my.example.com` exists under another BytePlus primary account. The domain you are trying to add is `*.example.com`.


<span id="icp-filing-check"></span>
#### ICP Filing Check

According to the regulations of the People's Republic of China, domains used in mainland China must have an ICP filing.

<span id="reserved-domain-detection"></span>
#### Reserved Domain Detection

In CDN, you cannot add domains reserved by BytePlus. The **Domain Name** configuration instructions in this document list some of BytePlus's reserved domains.
