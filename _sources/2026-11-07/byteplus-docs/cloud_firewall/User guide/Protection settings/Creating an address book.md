---
title: "Creating an address book"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Creating_an_address_book"
---

You can add multiple IP addresses, ports, or domains to an address book for easy one\-click reference when configuring access control policies. This enables you to efficiently manage the network traffic for specific objects. Using an address book eliminates the need to repeat the same configurations for multiple access control policies. Additionally, updates to an address book will be automatically synchronized with relevant access control policies, requiring no manual reconfigurations, which facilitates policy adjustments and management.

<span id="402c968b"></span>
## Introducing address book types

The address book types supported by different product editions or products with different specifications may vary. To find out which types are supported by the product you purchased, refer to its specifications.


* IP address book: Can be used to manage IP addresses centrally. You can associate it with access sources and destinations.

* Port address book: Can be used to manage destination ports centrally. You can associate it with destination ports.

* Domain address book: Can be used to manage domains centrally. You can associate it with destinations in the policies for internet outbound traffic and VPC firewall policies.


<span id="6266dbec"></span>
## Steps


1. Log in to the Cloud Firewall console.

2. On the left side of the page, click **Access control** \> **Address book**.

3. Click **Add address book** and fill in the parameters for the address book.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83f1511e453949e8bbf0cf7814de4da5~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameter** |**Description** |
   |---|---|
   |Address book type |* IP address book: Can be IP addresses or CIDR blocks, such as `192.168.1.1` and `192.168.1.0/24`. Separate addresses with a comma ( , ) or a newline character. A maximum of 20,000 IP addresses and CIDR blocks can be added.<br><br>* Port address book: Can be numbers between 0 and 65535, such as `0/65535`, `22`, and`80/88`. Separate ports with a comma ( , ) or a newline character. A maximum of 20,000 ports can be added.<br><br>* Domain address book: Can be single domains, wildcard domains, and multi\-level domains, such as `example.com`, `*.example.com`, and `*.example.example.com`. Separate domains with a comma ( , ) or a newline character. A maximum of 20,000 domains can be added. |
   |Address book name |Enter the name of the address book. Up to 64 characters. |
   |Address book description |Used to describe the purpose of the address book. |
   

4. Click **Add.** 

   Once the address book is created, you can view, edit, or delete it from the address book list.
