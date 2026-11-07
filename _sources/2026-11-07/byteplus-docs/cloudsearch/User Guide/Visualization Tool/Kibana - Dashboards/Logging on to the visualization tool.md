---
title: "Logging on to the visualization tool"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/logging-tool"
---

The visualization tool page allows you to perform data query and data visualization operations. This topic describes how to log on to a visualization tool.

<span id="860da38e"></span>
## Before you begin


* Enable public network access to the visualization tool. This is required if you want to access the visualization tool by using a public endpoint. For more information, refer to [Enabling public network access to the visualization tool](https://docs.byteplus.com/en/docs/cloudsearch/enabling-public-access-tool).

* Internal access is enabled for the visualization tool by default. You do not need to manually enable it.


<span id="3cbdb7b4"></span>
## Accessing the visualization tool by using the public endpoint


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the Region of the target instance.

3. Go to the logon page of the visualization tool using one of the following methods:

   * On the **Instances** page, find the instance and click **Kibana** or **Dashboards** in the **Actions** column.

   1. In **Instance management \>**  **Visulization configuration**, click the public network access address.

4. On the logon page, type your username and password to log on to the visualization tool.

   The username is admin, and the password is the one you set when creating the instance. If you forgot your password, go to the **Basic information** page and reset the password.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/826ab6d2df5f4888a0e6b5a2db4f04e0~tplv-goo7wpa0wc-image.image) </span>


<span id="49da088d"></span>
## Accessing the visualization tool by using the private endpoint

If you want to access the visualization tool using the private endpoint, you must configure the security group to allow traffic through the port specified in the endpoint. By default, port 5601 is specified in the private endpoint of the visualization tool.


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. On the **Instances** page, click the name of the target instance.

3. In **Instance management \>**  **Visulization configuration**, click the private network access address.

4. On the logon page, type your username and password to log on to the visualization tool.

   The username is admin, and the password is the one you set when creating the instance. If you forgot your password, go to the **Basic information** page and reset the password.
