---
title: "Basic Configuration"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Basic_Configuration"
---

This document describes what basic configuration you need to do as an administrator of the group's management/systems when using growth analysis products, and where to find these configuration items.

<span id="_1-saas产品基础配置说明"></span>
# SaaS product basic configuration description

**Operations for group management:** 


1. Part of it is done and managed in the BytePlus console:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d19f4358c8742ad81ad5a96161289c8~tplv-goo7wpa0wc-image.image) </span>

2. After creating a growth analysis project in the console, you may also need to enter the growth analysis product for further configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f8b96b8df5f450eb2c9630ada220017~tplv-goo7wpa0wc-image.image) </span>

   The specific configuration items involved are:

   1. Create and manage applications, see the documentation for details[App List](https://docs.byteplus.com/docs/DataFinder/App_List)

   2. Configure the preset identity of the role in each project (the preset identity determines the operation permissions of the functions in the project), the visibility of the functions, and the permissions of the data.

   3. Create and manage ak/sk.

      The configuration path within the growth analysis is: **Group Settings** in the page prompt box or the **Settings icon** in the upper right corner of the page.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8abd0a8318c74e48a5611f85c79d6abd~tplv-goo7wpa0wc-image.image) </span>

      **Application management**, project **role management** and **application credential** management three functions are described below.

   
   |**Function name** |**Function introduction** |
   |---|---|
   |Application |Apps are data sources within growth analytics projects, and only one app is supported per project. Creating an app is the first step to getting started with growth analysis. After creating the application, you also need to report data to the application according to the guidance. Data from the same user system is recommended to be reported to an application.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6cf960e528d46c3822f753b8284993a~tplv-goo7wpa0wc-image.image) </span> |
   |Role |The roles shown here are a list of roles created in the console that allow access to growth analysis. Identity within the growth analytics product (which determines action permissions within the project), functional visibility, and data permissions cannot be configured in the console. If you need to set these role permissions, you need to create the role in the console, and then enter the corresponding role in the growth analysis to set it again.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d552c3d763ee47eba997bec4cc95ef2f~tplv-goo7wpa0wc-image.image) </span> |
   |Application certificate |Used to create and reset AK/SK, permissions are shared across the group. |
