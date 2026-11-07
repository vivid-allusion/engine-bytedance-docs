---
title: "Transfer DNS Service to BytePlus DNS"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-transferring-dns-service-to-byteplus-dns"
---

This document introduces how to transfer your DNS service to BytePlus DNS.

<span id="business-scenario"></span>
## Business scenario

Your domain name is hosted by a registrar, such as Godaddy. At the same time, your domain name is using the DNS service of another DNS provider, such as AWS Route 53.

Now, you need to transfer your DNS service to BytePlus DNS. You can follow the steps below:


1. Transfer DNS records.

2. Change DNS servers.

3. Validate whether the DNS result is from BytePlus DNS.


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">If your domain has DNSSEC enabled, you need to delete the domain's DS record at your domain registrar to disable DNSSEC before transferring the DNS service. Otherwise, after you change the DNS server to BytePlus DNS, your domain may not be resolved correctly.</div>


<span id="step-1-transfer-dns-records"></span>
## Step 1: Transfer DNS records

You need to transfer the DNS records from your DNS provider to BytePlus DNS.

<span id="if-you-have-already-created-dns-records-with-your-dns-provider"></span>
### If you have already created DNS records with your DNS provider

If your DNS provider supports exporting DNS records, you can export the DNS records from your DNS provider and then import them into BytePlus DNS.


1. Export the DNS records of your domain name from your DNS provider. It is recommended to export the DNS records as `.xlsx`, `.xls`, or `.zone` files.

2. [Create your domain name in BytePlus DNS](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-creating-a-domain-na).

3. In BytePlus DNS, [import the exported DNS records to your created domain name](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-import-dns-records).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You need to confirm whether the format of the exported DNS record file complies with the <a href="https://docs.byteplus.com/docs/byteplus-dns-suite/docs-import-dns-records">template</a>. If not, you need to modify the exported DNS record file before importing it into BytePlus DNS.</div>


If your DNS provider does not support exporting DNS records, you need to manually create DNS records in BytePlus DNS.


1. [Create your domain name in BytePlus DNS](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-creating-a-domain-na).

2. [Create DNS records for the domain name](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-creating-updating-or-deleting-dns-records).

3. Check if all the DNS records of your DNS provider are exactly the same as the DNS records in BytePlus DNS.


<span id="if-you-haven-t-created-dns-records-with-the-dns-provider"></span>
### If you haven't created DNS records with the DNS provider

You can directly create DNS records in BytePlus DNS.


1. [Create your domain name in BytePlus DNS](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-creating-a-domain-na).

2. [Create DNS records for the domain name](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-creating-updating-or-deleting-dns-records).


<span id="step-2-change-the-authoritative-dns-servers-used-by-the-domain-name"></span>
## Step 2: Change the authoritative DNS servers used by the domain name

At your domain name registrar, remove the authoritative DNS servers provided by the previous DNS provider. At the same time, you need to add the authoritative DNS servers of BytePlus DNS.

During the DNS resolution process, the top\-level domain DNS server returns the IP address of the corresponding authoritative DNS server to the local DNS server in the form of NS records. The local DNS server caches this NS record. After you change the authoritative DNS servers at the domain name registrar, the top\-level domain DNS server will return the authoritative DNS servers of BytePlus DNS for the domain name. However, the local DNS server still caches the authoritative DNS servers provided by the previous DNS provider.

The expiration time of NS records is generally 48 hours. After you switch the authoritative DNS servers at the domain name registrar, it takes at least 48 hours for most local DNS servers to cache the new NS records.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Different ISPs have different cache durations for local DNS servers. Most ISPs have a relatively long cache time. Therefore, it takes a long time for local DNS servers of ISPs to update the cached NS records. Before updating the cached NS records, local DNS servers of ISPs will request DNS resolution results from the DNS servers of the previous DNS provider. Therefore, if you transfer all the DNS records to BytePlus DNS, we recommend that you keep the DNS records at the previous DNS provider for at least 2 weeks.</div>


<span id="get-byteplus-authoritative-dns-servers"></span>
### Get BytePlus authoritative DNS servers


1. Open the [BytePlus DNS Suite console](https://console.byteplus.com/dns-suite/dns).

2. Go to the **Domain management** page. Click your domain in the **Domain** column.

3. Select the **Instance information** tab. You can see BytePlus DNS servers in the **DNS information** section. You must add all the listed DNS servers to the authoritative DNS server list (or name server list) of your domain name at your domain name registrar.


<span id="update-your-domain-s-authoritative-dns-servers"></span>
### Update your domain's authoritative DNS servers

Refer to the documentation of domain name registrars to learn how to use BytePlus authoritative DNS servers (name servers) for your domain. Some of the documentation links are listed below:


* [Godaddy](https://ca.godaddy.com/help/edit-my-domain-nameservers-664)

* [IONOS](https://www.ionos.com/help/domains/using-your-own-name-servers/using-your-own-name-servers-for-a-domain/)

* [Namecheap](https://www.namecheap.com/support/knowledgebase/article.aspx/767/10/how-to-change-dns-for-a-domain/)


<span id="step-3-test-whether-the-dns-result-is-from-byteplus-dns"></span>
## Step 3: Test whether the DNS result is from BytePlus DNS

You can test whether the DNS result is from BytePlus DNS using the following methods.


* Get authoritative DNS servers from the top\-level domain DNS server.

* Get authoritative DNS servers from the local DNS server.


<span id="get-authoritative-dns-servers-from-the-top-level-domain-dns-server"></span>
### Get authoritative DNS servers from the top\-level domain DNS server

The authoritative DNS servers configured for your domain name are registered in the top\-level domain DNS server. Therefore, obtaining the authoritative DNS servers for your domain name directly from the top\-level domain DNS server is accurate and not affected by other factors. You can use the trace function of the dig command to query the top\-level domain DNS server.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The dig command is natively supported on macOS and Linux platforms. For Windows platforms, you can download the <a href="https://www.isc.org/download/#BIND">Windows version of the BIND tool</a> for testing. The BIND tool includes the dig command. BIND versions 9.16.27 and earlier support Windows.</div>


Run the following command in the command line:

```Shell
dig <domain> +trace
```


> Note: `<domain>` represents your domain name.


If the authoritative DNS servers are successfully updated at your domain's registrar, the result contains BytePlus authoritative DNS servers.

<span id="get-authoritative-dns-servers-from-the-local-dns-server"></span>
### Get authoritative DNS servers from the local DNS server

The expiration time of NS records is generally 48 hours. After you switch the authoritative DNS servers at the domain name registrar, it takes at least 48 hours for most local DNS servers to cache the new NS records. Before updating the cached NS records, local DNS servers still use the authoritative DNS servers provided by the previous DNS provider for domain name resolution.

Run the following command in the command line:

```Shell
nslookup -type=ns <domain>
```


> Note: `<domain>` represents your domain name.


If the local DNS server caches the updated NS record, the result contains BytePlus authoritative DNS servers.
