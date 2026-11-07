---
title: "QR Code Channel (Including QR Code Statistics, QR Code Management)"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/QR_Code_Channel_Including_QR_Code_Statistics_QR_Code_Management"
---

<span id="_1-概念介绍"></span>
# 1. Introduction to the concept

In the QR code channel, you can perform unified analysis and management of Mini Program QR codes for multiple platforms through the Finder.

The current available operations include:


* View the statistical results of all QR codes of the product, and can analyze the statistical results from multiple dimensions;

* View products All QR codes and QR code groups, create new QR codes and QR code groups, manage already created QR codes and QR code groups.


<span id="_2-使用说明"></span>
# 2. Instructions for use

<span id="_2-1-二维码统计"></span>
## 2.1 QR code statistics

<span id="_2-1-1-功能介绍"></span>
### 2.1.1 Function introduction

In the QR code statistics module, you can:


* Filter the QR code scope you want to analyze. Filter dimensions include time, platform, and group to which the QR code belongs.

* View the statistical results and trends of all QR codes, including the number of scan codes, the number of scan codes, the number of new scan codes, the number of QR codes and the number of QR code groups;

* View and download the detailed data of each QR code, including QR code name, page URL, group, number of scans, number of scans, new scan codes and creation time.


<span id="_2-1-2-页面介绍"></span>
### 2.1.2 Page introduction

The "QR code statistics" page is as follows, taking Toutiao channel as an example:


* Filter the time range for statistics, you can choose the hour level or the day level;

* Screening the Mini Program platform for statistics;

* Browse and select the group to which the QR code belongs;

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c453710fcf2f4fe0ac38f2729048b2a6~tplv-goo7wpa0wc-image.image) </span>

* Check the statistical results and changing trends of the filtered QR code;

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9650947843b544faacdfd19d88ac5e77~tplv-goo7wpa0wc-image.image) </span>

* View the detailed name list and corresponding data of the filtered QR code;

* Download filtered QR code details.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6c5cb582dfab4f8092ada729c3660290~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-2-二维码管理"></span>
## 2.2 QR code management

<span id="_2-2-1-功能介绍"></span>
### 2.2.1 Function introduction

In the QR code management module, you can:


* Create QR code and QR code group;

* Filter the platform and view the name, page URL, group, creation time, style, and size of the QR code that has been created in that platform.

* Operate the QR code that has been created, including downloading, modifying or deleting it;

* Filter the platform and view the name, QR code list, and creation time of QR code groups that have been created in that platform.

* Actions on QR code groups that have been created, including modification or deletion.


<span id="_2-2-2-页面介绍"></span>
### 2.2.2 Page introduction

The "QR code management" page is as follows, taking WeChat channel as an example:


* Mini Program platform that can be screened for QR code management;

* Browse and manage QR codes;

* Browse and manage QR code groups;

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ee821aff3e445b28ec9dea65acd4aa9~tplv-goo7wpa0wc-image.image) </span>

* You can enter the QR code name, page URL or QR code group to search for QR code;

* Can create a new QR code;

* You can view the details of the QR code and operate it;

* You can create a QR code group;

* You can view the details of the QR code group and take action.


<span id="_2-2-3-如何创建二维码？"></span>
### How do 2.2.3 create a QR code?

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When creating a QR code in the following ways, no additional processing is performed on the DataFinder side, and the size and style of the generated QR code are controlled by the corresponding creation platform.</div>



* WeChat platform creates QR code, the page is as follows:


Method 1: Generate by Mini Program ID and secret

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2672a0d4b56949d09149bfd8400d40df~tplv-goo7wpa0wc-image.image) </span>

Method 2: Generate through access token

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When using this method, the access token is the certificate for calling the WeChat API, which is time\-sensitive. Generally, the valid period is 2 hours (7200 seconds), and it needs to be re\-acquired after expiration.</div>


* <div data-tips="true" data-tips-type="tip">You need to obtain the access token by yourself on demand to configure on this page. Automatic acquisition and automatic configuration filling are not supported for the time being.</div>



<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4263e552c701422fa844ea823f21a225~tplv-goo7wpa0wc-image.image) </span>


* "Alipay" platform creates a QR code, the page is as follows:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f02f031c9c5c4af7b1736c721c3e34e3~tplv-goo7wpa0wc-image.image) </span>


* Toutiao platform creates QR code, the page is as follows:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e4f90d937e5748c780da4a0fafca45bd~tplv-goo7wpa0wc-image.image) </span>

Note: DataFinder is a former name for BytePlus User Growth.
