---
title: "Create an GTM Instance"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/k_FIn3"
---

This document describes how to create a GTM instance in BytePlus GTM.

<span id="steps"></span>
## Steps

Complete the following steps to create an GTM instance.


1. Open the BytePlus GTM [Instance management page](https://console.byteplus.com/dns-suite/gtm/instances).

2. On the **Instance management** page, click **Create instance**.

3. On the **Create instance** page, set the following parameters:



|Parameter |Description |
|---|---|
|Connection method |The way your domain connects to BytePlus GTM. Supports **CNAME** and **Domain** connection methods. If the **Connection method** is **CNAME**, you need to set the **Routing domain**; if the **Connection method** is **Domain from BytePlus DNS**, you need to set the **Domain name**.<br><br><br>* **CNAME**: BytePlus GTM automatically generates a routing domain based on the domain prefix you enter and the routing domain suffix you choose. BytePlus GTM resolves this routing domain to the target addresses you add in the GTM instance. You also need to create a CNAME record with your DNS service provider and point your domain to this routing domain. See [Connect Your Domain to BytePlus GTM](https://docs.byteplus.com/docs/byteplus-dns-suite/pHJ6zL). You can use this connection method if your domain's DNS service provider is not BytePlus DNS.<br><br>* **Domain name**: BytePlus GTM resolves your domain to the target addresses you add in the GTM instance. You can only use this connection method if your domain's DNS service provider is BytePlus DNS. |
|Routing domain |The routing domain required for **CNAME** connection method. This parameter only appears when **Connection method** is **CNAME**.<br><br><br>1. **Set routing domain suffix**: Select a domain suffix from the dropdown menu.<br><br>2. **Set routing domain prefix**: Enter a domain prefix. It's recommended to enter your domain as the prefix for the routing domain. For example, if your domain is `www.example.com`, you can enter `www.example.com`.<br><br><br>If you set the routing domain prefix to `www.example.com` and choose `byteplus.com` as the routing domain suffix, your routing domain will be `www.example.com.byteplus.com`. |
|Domain name |The domain required for **Domain from BytePlus DNS** connection method. This parameter only appears when **Connection method** is **Domain from BytePlus DNS**. Follow these steps to set up your domain:<br><br><br>1. **Set domain suffix**: Select from the dropdown menu a domain you created in BytePlus DNS. For example, if you created the domain `example.com` in BytePlus DNS, you can select `example.com` from the dropdown. You need to ensure that the domain's **Status** in BytePlus DNS is **Active**.<br><br>2. **Set domain prefix**. For example, if you set the domain prefix to `test`, your domain will be `test.example.com`. GTM does not limit the number of levels in the domain prefix. |
|Edition |You can set this to either standard edition or ultimate edition. See [Editions](https://docs.byteplus.com/docs/byteplus-dns-suite/8cqTK1). |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The domain name must comply with the following rules:</div>



* <div data-tips="true" data-tips-type="tip">Supports English letters (a\-z, A\-Z), numbers (0\-9), hyphens (\-), underscores (_), periods (.), wildcards (\*), and Chinese characters.</div>


* <div data-tips="true" data-tips-type="tip">Hyphens cannot be used at the beginning or end of each label, and periods should not appear consecutively.</div>


* <div data-tips="true" data-tips-type="tip">Wildcards can only be used at the beginning of each label to denote wildcard domains.</div>


* <div data-tips="true" data-tips-type="tip">The length of each label should not exceed 63 characters.</div>



<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After you successfully create a GTM instance, you cannot modify the domain name of the GTM instance. If you need to use a new domain name, you must create a new GTM instance.</div>


After setting the parameters, check the agreement and click **Confirm order**.

You can see the GTM instance you created on the **Instance management** page.

<span id="follow-up-steps"></span>
## Follow\-up steps

After creating the GTM instance, you can configure the GTM instance.
