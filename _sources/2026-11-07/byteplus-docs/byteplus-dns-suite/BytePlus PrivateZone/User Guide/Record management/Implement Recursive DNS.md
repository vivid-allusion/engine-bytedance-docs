---
title: "Implement Recursive DNS"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/uperuL"
---

This document describes how to enable recursive DNS for a domain name in BytePlus PrivateZone.

If you have created a root domain in BytePlus PrivateZone, and the subdomains of the domain need to be mapped to resources within a VPC and resources on the internet respectively, you can enable the recursive DNS feature for this root domain.

<span id="what-is-recursive-dns"></span>
## What is recursive DNS?

In recursive DNS, BytePlus PrivateZone sends recursive queries to a recursive DNS server on the internet. The recursive DNS server then return DNS response obtained from an authoritative DNS server on the internet.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_193646d60826873bbb4dd5f241eb71c9.jpeg) </span>

<span id="how-does-byteplus-privatezone-match-a-dns-query-to-recursive-dns"></span>
## How does BytePlus PrivateZone match a DNS query to recursive DNS

When BytePlus PrivateZone receives a DNS query, it matches in the following order:


1. Domain names you have created in BytePlus PrivateZone

2. Rules of the type **Forward DNS queries to an external DNS server**

3. Recursive DNS


If both domain names and rules of the type **Forward DNS queries to an external DNS server** fail to match, BytePlus PrivateZone will match the DNS query to recursive DNS in the following cases:


* The domain name in the DNS query is a subdomain of a root domain you created in BytePlus PrivateZone, and recursive DNS is enabled for the root domain

* The domain name in the DNS query is not created in BytePlus PrivateZone


<span id="how-does-byteplus-privatezone-perform-recursive-dns"></span>
## How does BytePlus PrivateZone perform recursive DNS

After matching to recursive DNS, BytePlus PrivateZone will respond to the DNS query by getting a DNS response a Local DNS server on the internet.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If a DNS query is sent to the internet, DNS latency will increase, and DNS changes will take effect more slowly. Therefore, we recommend that you map DNS records to IP addresses within the VPC if possible.</div>


<span id="operation-scenarios"></span>
## Example scenario

Suppose you have associated the domain name `example.com` with a VPC. Resources within the VPC need to access the specified subdomain `api.example.com`. This subdomain points to the internet IP address of the API server. In this scenario, you can enable the recursive DNS feature for the domain name `example.com`.

After the recursive DNS feature is enabled, when resources within the VPC access `api.example.com`, BytePlus PrivateZone will query through the public recursive DNS server on the internet and return the DNS response result. The DNS response is the DNS record returned by the public recursive DNS server.

The subdomain `ecs.example.com` is in the DNS record of the domain name. When resources within the VPC send a DNS query for the subdomain `ecs.example.com`, BytePlus PrivateZone will return the record value `10.0.1.128`.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4135444c447af97744cc81edbd5e5294.jpeg) </span>

<span id="steps"></span>
## Steps

<span id="step-1-create-a-domain"></span>
### Step 1: Create a domain

Create the domain `example.com`. You need to enable recursive DNS when creating the domain. Refer to [Create a Domain](https://docs.byteplus.com/docs/byteplus-dns-suite/PU6MMV) to learn how to create a domain.

<span id="step-2-create-a-dns-record"></span>
### Step 2: Create a DNS Record

Create a DNS record for the domain `example.com`:


* **Domain**: Set the domain prefix to `ecs`. Thus, the domain name will be `ecs.example.com`.

* **Record type**: Set this parameter to **A**.

* **Record value**: Set this parameter to the private IP address of the ECS, which is `10.0.1.128`.


Refer to [Create DNS Records](https://docs.byteplus.com/docs/byteplus-dns-suite/tmjP7G) to learn how to create a DNS record.

<span id="step-3-verify-recursive-dns"></span>
### Step 3: Verify recursive DNS


1. Remotely connect to the ECS instance in the VPC associated with the domain. Use the nslookup command to verify if recursive DNS is effective for `api.example.com`. If the DNS response is an internet IP address, it indicates that recursive DNS is effective.

   ```shell
   $ nslookup api.example.com
      
   Server:         100.96.0.2
   Address:        100.96.0.2#53
      
   Non-authoritative answer:
   Name:   api.example.com
   Address: xx.xxx.xxx.xx
   ```
   


Refer to [Update Domain Configuration](https://docs.byteplus.com/docs/byteplus-dns-suite/9iX1X2) to learn how to disable recursive DNS.


2. In the ECS instance, use the nslookup command to verify if `api.example.com` can still be resolved successfully. If the DNS response is NXDOMAIN, it indicates that recursive DNS has been disabled.

   ```shell
   $ nslookup api.example.com
      
   Server:         100.96.0.2
   Address:        100.96.0.2#53
         
   ** server can't find api.example.com: NXDOMAIN
   ```
