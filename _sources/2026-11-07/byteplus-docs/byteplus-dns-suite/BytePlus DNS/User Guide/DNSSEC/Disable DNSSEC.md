---
title: "Disable DNSSEC"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/EdDgnp"
---

This document introduces how to disable DNSSEC for your domain in BytePlus DNS.

<span id="steps"></span>
## Steps

Refer to the following steps to disable DNSSEC for your domain.

<span id="step-1-delete-the-ds-record-at-your-domain-registrar"></span>
### Step 1: Delete the DS record at your domain registrar

To avoid DNS resolution unavailability, you need to delete the DS record at your domain registrar before disabling DNSSEC.

<span id="step-2-disable-dnssec-in-byteplus-dns"></span>
### Step 2: Disable DNSSEC in BytePlus DNS

After deleting the DS record, refer to the following steps to disable DNSSEC in BytePlus DNS.


1. Open the [BytePlus DNS Console](https://console.byteplus.com/dns-suite/dns/public-zone).

2. In the **Domain management** page, click your domain name in the **Domain** column.

3. In the **DNS security** tab, click **Disable DNSSEC**.
