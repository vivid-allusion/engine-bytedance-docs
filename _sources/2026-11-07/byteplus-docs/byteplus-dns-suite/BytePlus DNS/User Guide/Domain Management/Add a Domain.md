---
title: "Add a Domain"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-creating-a-domain-na"
---

This document describes how to add your domain name in BytePlus DNS.

Before creating DNS records for your domain name, you need to add your domain name in BytePlus DNS.

<span id="steps"></span>
## Steps

Complete the following steps to add a domain.


1. Open the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns).

2. On the **Domain management** page, click **Add domain**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The domain name must meet the following requirements:</div>



* <div data-tips="true" data-tips-type="tip">Supports English letters (a\-z, A\-Z), numbers (0\-9), hyphens (\-), and periods (.).</div>


* <div data-tips="true" data-tips-type="tip">Supports Internationalized Domain Names (IDNs), such as <code>example.中文网</code>, <code>example.닷컴</code>.</div>


* <div data-tips="true" data-tips-type="tip">Hyphens (\-) cannot be used at the beginning or end of a label</div>


* <div data-tips="true" data-tips-type="tip">Multiple periods (.) cannot appear consecutively.</div>


* <div data-tips="true" data-tips-type="tip">The length of a label should not exceed 63 characters. In FQDN format, the total length of the domain name after Punycode encoding should not exceed 254 characters.</div>


3. In the **Add domain** dialog box, enter your domain name and comments. The console will validate the domain name. If the validation passes, click **OK** to add the domain name.


If the validation fails, you can move the mouse over the question mark in front of the error message. A tooltip will automatically appear on the question mark. You can view possible reasons through the tooltip.

The successfully creasted domain name will be displayed in the domain name list. If the DNS resolution for the domain name is normal in BytePlus DNS, the **DNS status** of the domain name will be displayed as **Active**. If there are issues with the DNS resolution of the domain name, the **DNS status** will display the corresponding problem description. You can move the mouse over the problem description to view a tooltip with possible reasons. You can also refer to the [FAQs](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-frequently-asked-questions) for solutions to some common problems.
