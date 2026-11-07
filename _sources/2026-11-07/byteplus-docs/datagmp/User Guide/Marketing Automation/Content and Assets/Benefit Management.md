---
title: "Benefit Management"
product: "Byteplus GMP"
product_code: "datagmp"
source: "https://docs.byteplus.com/en/docs/datagmp/Benefits_Management"
---

<span id="22b203b4"></span>
### **1. Product Overview**

Enterprises can guide users to their online/offline platforms through benefits, achieving operational goals such as acquiring new users, conversion, and extending the customer lifecycle.

<span id="3927a7a8"></span>
### **2. Usage Restrictions**


| **[ 📢 Prerequisites for using this feature ]**  ||
|---|---|
|**Purchasing Benefit Management Module** |The client needs to purchase the "Benefit Management" product module |
|**Enable GMP permissions** |The administrator enables permissions, permission path: Content and Assets\-Benefit Management |


<span id="391d6c3c"></span>
### **3. Function Description**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/039614281cef477fad937a69e192f087~tplv-goo7wpa0wc-image.image" width="439px" /></div>


**3.1 Benefit Import**

Benefit import offers two methods: "Manual Upload" and "Manual Import + Interface Delivery."

 **(1) Import Through Interface**

By configuring the interface connection information, the system integrates with the client\-side third\-party benefit system. Upon next accessing the Benefit Management page, it automatically pulls and displays the interface benefit content. The specific interface configuration access method can be discussed with the Volcano Project Manager or Customer Success Manager.

 **(2) Import by manual upload**

In addition to interface import, you can also upload manually. Template import: Supports creating benefits manually and uploading benefit content via an Excel template.


* Benefit Name: Supports custom benefit naming.

* Benefit ID: The system generates a default ID, and supports custom modifications.

* Benefit Type: Supports the following three types

   * Redemption Code: Benefit contents include specific codes, which need to be uploaded.

   * Physical: Benefit contents consist of physical items, which require quantity to be specified.

   * Points: Benefit contents consist of virtual points, which require quantity to be specified.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/165e87d050084bbb92c5c0963b02cc30~tplv-goo7wpa0wc-image.image" width="439px" /></div>


**3.2 Benefit Distribution**

Supports inserting benefits in webhooks, SMS, and Magic Cube landing pages.

Navigate to the SMS channel configuration page and click "Insert Benefit".

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef217636bbbf4cbc8a0f130666ac2862~tplv-goo7wpa0wc-image.image" width="439px" /></div>


Select the benefit to be inserted in the benefit popup.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7025812f27314b73aeeb3107ae76359d~tplv-goo7wpa0wc-image.image" width="439px" /></div>


After selection, the benefit name will be displayed, and the insertion is completed upon approval.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7360ec552b04a2f93cc4861c8acca36~tplv-goo7wpa0wc-image.image" width="439px" /></div>


**3.3. Benefit Distribution Details**

Supports viewing the details of the benefits distributed on the page, click "View Details" in the benefit action column.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a86e2b5046f742548c90b03c0a92ede2~tplv-goo7wpa0wc-image.image" width="439px" /></div>


Supports viewing detailed list of distributed benefits, including Benefit Type, distribution quantity, distribution channels, and distributor information.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0374218b916840eeadd7f4ab6aa4b985~tplv-goo7wpa0wc-image.image" width="439px" /></div>


Supports downloading and exporting the details of benefits distribution through API.
