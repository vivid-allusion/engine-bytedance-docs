---
title: "Server Side Access Instructions"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Server_Side_Access_Instructions"
---

**In order to achieve more complete data access and reduce the complexity of data access, BytePlus Growth Analysis supports server level access of data.** 

**Before you choose server level data access, please read the following instructions carefully:** 


1. Before referring to a document, please be sure to check whether the document corresponds according to the product version you are using (SaaS/SaaS cloud native/privatized), so as to avoid data access problems due to wrong documents viewed.

2. The data access function of some servers is available in the paid official version. If you use the SaaS Tinder limited free version, you may not be able to access. You need to contact the work order or contact BytePlus by phone to inquire about the use;

3. The data access function of some servers is not enabled by default. You need to contact the customer success manager to activate it.


<span id="服务端数据接入"></span>
# **Server side data access**


* `HTTP API`: Provide event tracking data reporting of HTTP interface externally to meet the scenario of your own event tracking report, you can view [HTTP API](https://docs.byteplus.com/docs/DataFinder/HTTP_API)[5. Report user properties](https://docs.byteplus.com/docs/DataFinder/HTTP_API#_5-%E4%B8%8A%E6%8A%A5%E7%94%A8%E6%88%B7%E5%B1%9E%E6%80%A7)[6. Report business object properties](https://docs.byteplus.com/docs/DataFinder/HTTP_API#_6-%E4%B8%8A%E6%8A%A5%E4%B8%9A%E5%8A%A1%E5%AF%B9%E8%B1%A1%E5%B1%9E%E6%80%A7) using HTTP API. Direct integration of system recommendations based on Java language development [Java SDK Integration](https://docs.byteplus.com/docs/DataFinder/Java_SDK_Integration);

* `Server level SDK`: easy to report events, user attributes, business objects, can be viewed [Java SDK Integration](https://docs.byteplus.com/docs/DataFinder/Java_SDK_Integration);

   And [PHP SDK](https://docs.byteplus.com/docs/DataFinder/PHP_SDK).

* When reporting server level data, please note that the reported uuid cannot be NULL, or set uuid = "+ device_id to report, otherwise the reported data will be abnormal.


<span id="eba07aa9"></span>
# Differences in reporting user attributes in different ways

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/572c6a1be0b142b8be0508ffcd72d31f~tplv-goo7wpa0wc-image.image) </span>

<span id="7958d592"></span>
# Video explanation and demo

The following provides you with an introduction video to the process of server level data access. You can open the corresponding video, download the demo sample file, and then learn the operation of server level data access in combination with the detailed documentation.


|**Example demo** |**Explanation video** |
|---|---|
|<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a5dd245e7fa423790af6d912a1a0076~tplv-goo7wpa0wc-image.image" name="ServerIntegrateDemo.zip">ServerIntegrateDemo.zip</Attachment><br><br><br>&nbsp;<br><br>The basic integration code has been made for you in the sample demo, and you can learn and rewrite it according to the documents and videos after downloading. |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a121f258000c45f2a7cee5d6eb8f9465~tplv-goo7wpa0wc-image.image" controls></video><br> |
