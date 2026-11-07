---
title: "Reduce the DNS Query Frequency From an ECS Instance"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/AYq9fP"
---

This document describes how to reduce the DNS query frequency from a single ECS instance.

BytePlus PrivateZone limits the frequency of DNS queries from the same ECS instance. If a DNS query frequency from an ECS instance exceeds 5000 queries per second, BytePlus PrivateZone will rate limit the DNS queries for that ECS instance. After rate limiting, the availability of private domain name resolution cannot be guaranteed. See [Editions](https://docs.byteplus.com/docs/byteplus-dns-suite/0K0WyX).

To reduce the DNS query frequency from a single ECS instance, you can either increase the number of ECS instances or cache the DNS records within the ECS instance. For example, you can cache DNS records in the ECS instance via the nscd service.

<span id="7d109e11"></span>
## Increase the number of ECS instances

You can increase the number of ECS instances to distribute the DNS query requests across other ECS instances, thereby reducing the DNS query frequency for a single ECS instance.

<span id="e9636ab9"></span>
## Cache DNS records with nscd service

You can reduce the frequency of DNS requests by using the nscd (Name Service Cache Daemon) service in your ECS instance to cache DNS records. See the [Ubuntu Manuals](https://manpages.ubuntu.com/manpages/trusty/en/man8/nscd.8.html) for more information on nscd.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After using the nscd service, if the DNS records change, the new DNS records will take effect only after the ECS instance cache expires.</div>


<span id="ce29c13e"></span>
### Install nscd

Refer to the official documentation of the specific Linux distribution used by the ECS instance for instructions on how to install nscd.

For example, on Ubuntu, you can install nscd by running the following command:

```Shell
sudo apt install nscd
```


<span id="enable-nscd"></span>
### Enable nscd

For Ubuntu, you can enable nscd immediately by running the following command:

```Shell
sudo systemctl start nscd
```


You can enable nscd to start automatically at boot by running the following command:

```Shell
sudo systemctl enable nscd
```


<span id="configure-nscd"></span>
### Configure nscd

For Ubuntu, the nscd configuration file is located in the `/etc/nscd.conf` directory. You can edit the nscd.conf file using a text editor. See the Ubuntu Manuals for information on how to configure this file.

```Shell
sudo vim /etc/nscd.conf
```


<span id="verify-whether-nscd-is-working"></span>
### Verify whether nscd is working

For Ubuntu, you can verify the nscd service status by running the following command:

```Shell
sudo systemctl status nscd
```


You can view the cache statistics of nscd by running the following command:

```Shell
nscd --statistics
```
