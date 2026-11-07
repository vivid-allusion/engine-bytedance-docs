---
title: "IP address allowlist"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/consultation_faq_ip_address_allowlist"
---

Before importing data from Elasticsearch clusters on Alibaba Cloud or Tencent Cloud, you must configure an IP address allowlist on the source node. Doing so allows data import tasks of BytePlus Torch Log Service (TLS) to access the data of the source node. This topic describes the list of IP addresses in each Region.

<span id="配置说明"></span>
## Configuration description

When you import data from Elasticsearch, data streams must flow over the internet. To access data in Elasticsearch clusters, TLS must use the internet. In such scenarios, Elasticsearch clusters on Alibaba Cloud or Tencent Cloud only allow access from the IP addresses in an allowlist. Therefore, before you create an import task, make sure that you have added the public IP addresses in the corresponding Region to the allowlist on the source node.

<span id="ip-地址列表"></span>
## IP address list


|Region |Public IP Addresses |
|---|---|
|China (Beijing) |* 221.194.188.8<br><br>* 221.194.188.9<br><br>* 111.62.119.244<br><br>* 111.62.119.245 |
|China (Shanghai) |* 61.129.54.8<br><br>* 61.129.54.9<br><br>* 180.153.35.8<br><br>* 180.153.35.9 |
|China (Guangzhou) |* 111.45.13.8<br><br>* 111.45.13.9<br><br>* 125.88.248.8<br><br>* 125.88.248.9 |
