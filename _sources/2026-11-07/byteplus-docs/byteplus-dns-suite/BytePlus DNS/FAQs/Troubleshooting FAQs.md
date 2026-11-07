---
title: "Troubleshooting FAQs"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-frequently-asked-questions"
---

This document lists common issues when using BytePlus DNS.

<span id="683cc9c2"></span>
## The DNS status of the domain is "**Not using BytePlus DNS** **servers"** 

After adding a domain in BytePlus DNS, the **DNS status** of the domain is shown as **Not using BytePlus DNS servers**.

<span id="84a45dee"></span>
### Cause

The current DNS service for the domain is not provided by BytePlus DNS, so BytePlus DNS cannot resolve the domain.

<span id="ed2e34ad"></span>
### Solution

Make sure your domain uses BytePlus authoritative DNS servers at your domain's registrar.


1. Open the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns).

2. Go to the **Domain management** page. Click your domain in the **Domain** column.

3. Select the **Instance information** tab. You can see BytePlus DNS servers in the **DNS information** section.

4. Add all the listed DNS servers to the authoritative DNS server list (or name server list) of your domain name at your domain name registrar.


<span id="16450ea9"></span>
## The DNS status of the domain is "DNS is managed by another account"

After adding a domain in BytePlus DNS, the **DNS status** of the domain is shown as **DNS is managed by another account**.

<span id="21891184"></span>
### Cause

The domain has been added to BytePlus DNS by another BytePlus account, and the DNS of the domain is active. Therefore, the ownership of the domain in BytePlus DNS belongs to another BytePlus account.

<span id="c26b9c43"></span>
### Solution

In the following cases, you can verify the ownership of the domain for your BytePlus account. After successful verification, you can manage the DNS of the domain in your account:


* The other BytePlus account also belongs to you.

* The other BytePlus account does not belong to you, but it has delegated the DNS service to a third\-party DNS provider through NS records. You have added your domain to the account of that third\-party DNS provider, and the DNS of the domain is active.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After the ownership of the domain for your BytePlus account is verified, if the other BytePlus account also belongs to you, BytePlus DNS will clear the DNS records of your domain in the other BytePlus account. At this point, the DNS resolution of your domain will stop. If you want to transfer the DNS resolution to your BytePlus account without stopping the DNS resolution, you can <a href="https://www.byteplus.com/en/support">submit a support request</a> to contact technical support.</div>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You can only verify domain ownership through the following steps if the edition of the domain in another BytePlus account is <strong>free</strong>. If the edition of the domain is not <strong>free</strong>, you need to <a href="https://www.byteplus.com/en/support">submit a support request</a> to contact technical support.</div>


<span id="step-1-export-dns-records"></span>
#### Step 1: Export DNS records

Before verifying the ownership of the domain, you need to export your DNS records from the other BytePlus account or the third\-party DNS provider. If you export the DNS records from the other BytePlus account, refer to [Export DNS records](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-export-dns-records).

<span id="step-2-verify-domain-ownership"></span>
#### Step 2: Verify domain ownership

You can verify the ownership of the domain through the console or OpenAPI.

**Method 1: Verify domain ownership through the console**

Follow the steps below to verify the ownership of the domain through the console:


1. Open the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns/publiczone).

2. On the **Domain management** page, find your domain and click **DNS is managed by another account**. In the pop\-up window, click **View details**.

3. In the **DNS is managed by another account** dialog box, copy and save the following information:

   * **Domain prefix**

   * **Record type**

   * **Record value**

4. Based on the information saved in the previous step, create a TXT record in the other BytePlus account or the account of the third\-party DNS provider.

5. In your current BytePlus account, open the **DNS is managed by another account** dialog box. Click **Verify**.


If the verification is successful, you can manage the DNS of the domain in your current BytePlus account. If the other BytePlus account also belongs to you, BytePlus DNS will clear the DNS records of your domain in the other BytePlus account.

**Method 2: Verify Domain Ownership through OpenAPI**

Follow the steps below to verify the ownership of the domain through OpenAPI:


1. In your current BytePlus account, call the [RetrieveZone API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-retrievezone) to generate domain verification information.

2. Based on the information saved in the previous step, create a TXT record in the other BytePlus account or the account of the third\-party DNS provider.

3. In your current BytePlus account, call the [CheckRetrieveZone API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-checkretrievezone) to verify the existence of the TXT record.


If the verification is successful, you can manage the DNS of the domain in your current BytePlus account. If the other BytePlus account also belongs to you, BytePlus DNS will clear the DNS records of your domain in the other BytePlus account.

<span id="step-3-import-dns-records"></span>
#### Step 3: Import DNS Records

After verifying the ownership of the domain, you can import the DNS records to the domain. Refer to [Import DNS records](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-import-dns-records).

<span id="failed-to-import-dns-records-to-byteplus-dns"></span>
## Failed to import DNS records to BytePlus DNS

For each failed DNS record import, the console will display the reason for the failure. You can refer to the following troubleshooting steps based on the failure reason.

<span id="failed-reason-domain-name-is-invalid"></span>
### Failed reason: Domain name is invalid

You need to check whether the domain name meets the following rules:


* Only English letters (a\-z, A\-Z), numbers (0\-9), hyphens (\-), underscores (_), periods (.), asterisks (\*), @, and simplified Chinese characters are supported.

* Hyphens cannot be used at the beginning or end of a label, and periods cannot be used consecutively.

* @ can only be used alone to represent an empty value.

* Asterisks (\*) can only be used at the beginning of a label for wildcard resolution.

* The length of a label should not exceed 63 characters.

* The total length of the domain name should not exceed 255 characters.


Also, make sure that the subdomain in the DNS record matches the target domain for the record import. For example, if the target domain for the record import is example.com, and you have the following record in your file:

```Plain
test.sample.com        www        A        default        600        1.1.1.1        Yes
```


The console will return a "Domain name is invalid" error.

<span id="failed-reason-line-is-invalid"></span>
### Failed reason: Line is invalid

You need to check if the following issues exist:


* The **Line** field in the DNS record uses line codes supported by BytePlus DNS. You can refer to [Import DNS records](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-import-dns-records) for a list of supported line codes.


<span id="failed-reason-the-record-duplicates-an-existing-record"></span>
### Failed reason: The record duplicates an existing record

You need to check if the following issues exist:


* The DNS records in the file are duplicates of the records in the console.

* There are duplicate DNS records in the file.


<span id="failed-reason-the-domain-name-does-not-match-the-domain-prefix"></span>
### Failed reason: The domain name does not match the domain prefix

A DNS record contains both a domain name and a domain prefix. If the domain prefix is different from the domain name, a conflict occurs.

For example, if you have the following record in your file:

```Plain
test.example.com        www        A        default        600        1.1.1.1        Yes
```


There will be a conflict between the domain name and the domain prefix.

<span id="failed-reason-line-exceeds-the-limits-of-your-edition"></span>
### Failed reason: Line exceeds the limits of your edition

You need to check if the lines used in the **Line** field of the DNS record complies with your edition. Refer to [Editions](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-editions).

<span id="failed-reason-the-number-of-weighted-records-in-a-line-exceeds-the-limit-of-your-edition"></span>
### Failed reason: The number of weighted records in a line exceeds the limit of your edition

You need to check if the DNS records corresponding to a single line (including default) exceed the limit. Refer to [Editions](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-editions).

<span id="failed-reason-ttl-exceeds-the-limits-of-your-edition"></span>
### Failed reason: TTL exceeds the limits of your edition

You need to check if the value of the TTL field exceeds the limit. Refer to [Editions](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-editions).

<span id="failed-reason-the-record-conflicts-with-an-existing-record"></span>
### Failed reason: The record conflicts with an existing record

You need to check if there are conflicts between the DNS records. Refer to [Avoid Conflicts in DNS Records](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-avoiding-conflicts-in-dns-records).

<span id="failed-reason-record-type-is-invalid"></span>
### Failed reason: Record type is invalid.

You need to check if the record type is supported by BytePlus DNS. Refer to [Supported DNS Record Types](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-supported-dns-record-types).

<span id="why-hasn-t-the-dns-resolution-taken-effect-after-transferring"></span>
## Why hasn't the DNS resolution taken effect after transferring?

The expiration time for NS records is generally 48 hours. After switching the authoritative DNS servers at your domain registrar, it takes at least 48 hours for the new NS records to be cached by most local DNS servers.

The caching time varies among different local DNS servers. Most local DNS servers have relatively long caching times. Therefore, it takes longer for local DNS servers to update their cached NS records. Before updating the cached NS records, local DNS servers will request DNS records from the DNS servers of the original DNS provider.
