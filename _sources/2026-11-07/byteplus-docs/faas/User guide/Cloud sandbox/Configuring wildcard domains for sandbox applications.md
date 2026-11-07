---
title: "Configuring wildcard domains for sandbox applications"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Configuring_wildcard_domains_for_sandbox_applications"
---

In the sandbox environment, a service contains multiple sandboxes and shares a public access address. By using a wildcard domain, each sandbox can be assigned a unique subdomain to implement independent access. This topic describes how to configure wildcard domains for sandbox applications.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">[<a href="https://docs.byteplus.com/en/docs/faas/How_do_I_apply_for_beta_features">Beta · Apply for trial</a>] This feature is in beta. To use this feature, apply for a trial.</div>


<span id="D0vem14o"></span>
## Background information

A wildcard domain is a domain name format that uses a wildcard character (usually \*) to match all subdomains of a domain. For example, \*.example.com is a wildchard domain. Its core advantage lies in the ability to automatically generate an unlimited number of unique subdomains without the need for manual resolution of each subdomain, thereby enabling convenient assignment to different services or instances.

<span id="PDS7dCtE"></span>
## Prerequisites


* A sandbox application has been created. For details, see [Sandbox applications](https://docs.byteplus.com/en/docs/faas/Sandbox_applications).


<span id="WipY57we"></span>
## Procedure

<span id="fMvd1oBO"></span>
### Step 1: Create a gateway instance


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. Create an API Gateway instance. For details, see [Creating instances](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

3. Create a service on the gateway. For details, see [Creating services](https://docs.byteplus.com/en/docs/apig/Creating_a_service).

4. Bind a domain name to the service. For details, see [Binding custom domain names](https://docs.byteplus.com/en/docs/apig/Adding_domain_name).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For example, <code>*.example.com</code> is a wildcard domain of <code>example.com</code>.   </div>
   

<span id="GhsI6iJh"></span>
### Step 2: Add a DNS record

Log in to the [DNS console](https://console.byteplus.com/dns-suite/dns), add a DNS record for the domain. For details, see [Adding CNAME records](https://docs.byteplus.com/en/docs/byteplus-dns-suite/9h8CZf).

<span id="0M8G09qW"></span>
### Step 3: Verify the gateway service

[Submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001543) to verify the gateway service. After service verification is successful, the gateway service is created.

<span id="VnMdfFof"></span>
### Step 4: Configure a wildcard for the sandbox application


1. Go to the target sandbox application.

   1. Log in to the [Function Service Console](https://console.byteplus.com/vefaas).

   2. In the left navigation bar, click **Cloud sandbox**\>**Sandbox applications.** 

   3. In the top navigation bar, select the project and region of the sandbox application.

   4. Click the name of the target sandbox application.

2. On the **Basic information** tab, go to the Gateway routing configuration section and click **Add** to add a gateway route configuration. Select **Wildcard domain** for **Domain type**. For other parameters, see [Sandbox applications](https://docs.byteplus.com/en/docs/faas/Sandbox_applications)

3. Click **Confirm**.
