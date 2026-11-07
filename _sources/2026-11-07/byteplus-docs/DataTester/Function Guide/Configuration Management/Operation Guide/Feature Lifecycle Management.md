---
title: "Feature Lifecycle Management"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Feature-Lifecycle-Management"
---

<span id="一、功能简介"></span>
# Introduction to functions

With more and more function iteration/experimentation, the resulting redundant code is also gradually increasing, such as AB test, FeatureFlag use leads to more and more if... else... nested structure in the code, which will introduce technical debt, resulting in: high code maintenance costs & reduced compilation efficiency, APP package size is getting larger and larger, and the cost of newcomers to get started is higher. So hopefully FeatureFlag can help clean up this redundant code.

Therefore, FeatureFlag provides lifecycle management capabilities to help users understand the usage of configuration parameters and assist users in determining whether the code corresponding to the Feature can be cleaned up. Mainly through the key operation Timeline to provide configuration parameters throughout the life cycle changes (including AB, release, rollback, etc.).

<span id="二、如何使用"></span>
# How to use


* Operation entry: Lifecycle Management tab below the Feature details page


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa44902bd2fd4ba1aeeee5f4149d07c3~tplv-goo7wpa0wc-image.image) </span>


* Key Operation Timeline:

   * Show a timeline of key changes to this configuration

      * Operation Items: Items include \- create, edit, publish, open AB test, rollback

      * Operating time: accurate to the minute

      * operator

* Last change time.
