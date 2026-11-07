---
title: "Server Side Filtering Parameters"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Server-Side-Filtering-Parameters"
---

The target audience of the server side experiment cannot use the public properties, user groups, and custom properties of the client. The server side parameters need to be registered in "Audience Management \- Server Side Request Parameters" to support use.

<span id="5abee5b9"></span>
# Server side request parameter list

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99055842e19144a698dc6347f20b73e1~tplv-goo7wpa0wc-image.image) </span>


* **Search:**  You can enter "name, description, creator" to search.

* **Register new filter parameters:**  Click "+ Filter Parameters" and fill in the complete information on the Create Parameters page to create parameters.

* **Operation:**  Support copy, delete, operation history, add value collection and other operations.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Clicking "Delete" will disable the parameter first. All server side experiments and server side features will not be able to use this parameter as a directional filter, and the relevant filter conditions for experiments and features that have used this parameter will be invalid. Please delete with caution.   </div>
   

<span id="7bac1c1d"></span>
# Register server side request parameters

Click on the list page "+ Filter Parameters", which will pop up as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36eb735e3a184eb1839806a14cf1897e~tplv-goo7wpa0wc-image.image) </span>


* **Parameter name:**  must not have the same name as other server side request parameters.

* **Parameter Key:**  You need to ensure that the code\-level variable name (ie Key) between different server\-level request parameters is unique.

* **Parameter types:**  support String, Int, Version, Boolean, Float.

* **Person in charge:**  The default creator.

* **Call source:**  Default server side.


<span id="8177624b"></span>
# Using server side request parameters

**1. SDK offloading usage example**

Refer to the server side SDK integration related documentation: [Server Side SDK Overall Description](https://docs.byteplus.com/docs/DataTester/Server-Side-SDK-Overall-Description).

**2. Create server side experiments/Features**

When creating server side experiments/features, you can use the registered server side request parameters as the target audience.


* The target audience of "server side experiment" is as follows:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/efb140c90c9e4b0bba343de77f925d27~tplv-goo7wpa0wc-image.image) </span>


* "Server side Features" custom audience rules, as shown below:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/17992c6b7df546b2bdd5d7374e065b23~tplv-goo7wpa0wc-image.image) </span>
