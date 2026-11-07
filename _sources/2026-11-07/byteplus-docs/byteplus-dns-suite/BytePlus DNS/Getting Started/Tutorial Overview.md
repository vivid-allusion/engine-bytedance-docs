---
title: "Tutorial Overview"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-tutorial-introduction"
---

This tutorial demonstrates how to use BytePlus DNS to implement the following application scenarios:


* Route user requests accessing your domain to a website server.

* Set up email addresses using your domain.

* Route user requests accessing your domain to a CDN acceleration service.


<span id="prerequisites"></span>
## Prerequisites


* You have [registered a BytePlus account](https://console.byteplus.com/).

* You have registered a domain name with a domain registrar, such as GoDaddy.


<span id="activate-byteplus-dns-and-create-your-domain-in-byteplus-dns"></span>
## Activate BytePlus DNS and create your domain in BytePlus DNS

Follow these steps to activate BytePlus DNS and create your domain in BytePlus DNS.


1. [Activate BytePlus DNS](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-activate-byteplus-dns).

2. [Add your domain](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-adding_a_domain).

3. [Configure DNS Servers for Your Domain](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-adding-dns-servers-to-your-domain-s-registrar).


<span id="implement-application-scenarios"></span>
## Implement application scenarios

After activating BytePlus DNS Suite and creating your domain, you can implement any of the following scenarios.

<span id="route-user-requests-accessing-your-domain-to-your-website-server"></span>
### Route user requests accessing your domain to your website server

You have created a website. The website server has the following IP addresses on the internet:


* IPv4 address: `11.22.33.44`

* IPv6 address: `1dc9:cd46:f3f5:29f6:e700:2780:e6ad:1dfa`


Since IP addresses are difficult to remember, you want to assign an easy\-to\-remember domain name to your website, such as `example.com`. You also want users to be able to access your website server through the domain name.

Traffic accessing this domain can be routed to both the IPv4 and IPv6 addresses of the website server.

Follow these steps to add DNS records and verify if the DNS resolution is active:


1. [Create an A record and an AAAA record](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-adding-dns-records-to-your-domain).

2. [Verify whether the DNS records are active](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-validating-your-dns-records).


<span id="set-up-email-addresses"></span>
### Set up an email address using your domain

You are using an email service provider's service and want to set up email addresses using your domain `example.com`, such as `mail1@example.com`. To verify your domain ownership, the email service provider will require you to add a TXT record for `example.com`. Additionally, to associate your domain with the email server, the email service provider will require you to add an MX record for `example.com`.

This document assumes that the email service provider requires you to add the following DNS records:


|Host Record |Record Type |Record Value |Priority |TTL |Description |
|---|---|---|---|---|---|
|@ |TXT |`verification-code-site-App_abcde_1234` |Not required |10 minutes |Verify your domain ownership. |
|@ |TXT |`v=spf1 a mx ~all` |Not required |10 minutes |SPF record, used for anti\-spam. |
|@ |MX |`mx1.mail.com` |1 |10 minutes |Associate `example.com` with the email server with domain name `mx1.mail.cn`. The priority of this email server is 1. |
|@ |MX |`mx2.mail.com` |2 |10 minutes |Associate `example.com` with the email server with domain name `mx2.mail.cn`. The priority of this email server is 2. |
|@ |MX |`mx3.mail.com` |3 |10 minutes |Associate `example.com` with the email server with domain name `mx3.mail.cn`. The priority of this email server is 3. |


Follow these steps to add DNS records and verify if the DNS resolution is effective:


1. [Create TXT records and MX records](https://docs.byteplus.com/docs/byteplus-dns-suite/ipvFf6).

2. [Verify whether the DNS records are active](https://docs.byteplus.com/docs/byteplus-dns-suite/duY-0a).


<span id="route-user-requests-accessing-your-domain-to-cdn"></span>
### Route user requests accessing your domain to CDN

Your website needs to use a CDN provider's service. To use the CDN acceleration service, you need to add a CNAME record to map your website domain to the CDN's acceleration domain. This allows user traffic accessing your website to be forwarded to CDN cache nodes.

In BytePlus DNS, CNAME records cannot coexist with DNS records other than NS and MX types. If you have already added DNS records for `example.com` that cannot coexist with CNAME records, you need to use a different subdomain in the CNAME record, such as `www.example.com`. This tutorial assumes that the CNAME provided by the CDN provider is `example.com.byteplusgslb.com`.

Follow these steps to create DNS records and verify whether the DNS resolution is active:


1. [Create a CNAME record](https://docs.byteplus.com/docs/byteplus-dns-suite/9h8CZf)

2. [Verify whether the DNS records are active](https://docs.byteplus.com/docs/byteplus-dns-suite/V3qfZ8).
