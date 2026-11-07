---
title: "Debug network connectivity"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Debug_network_connectivity"
---

For general Flink tasks, accessing upstream data sources (such as Kafka, databases, etc.) is necessary to perform real\-time computation and write to downstream data sinks (such as Kafka, OLAP, etc.).

<span id="c00a16f0"></span>
## Prerequisites


* Testing network connectivity requires creating a resource pool and a Session cluster. Refer to [Create Resource Pool](https://docs.byteplus.com/docs/flink/Create_Resource_Pool) and [Session Cluster](https://docs.byteplus.com/docs/flink/Session_Cluster) to create the related resources in advance.


<span id="2f2825fa"></span>
## Notes


1. The Session cluster serves only as a development and testing environment. If network connectivity tests pass on the Session cluster but production tasks still cannot connect, carefully check to ensure:

   1. The Session cluster and production tasks must belong to the same resource pool; otherwise, the test results are not valid.

   2. The Session cluster and production tasks must have consistent parameter configurations, especially network\-related settings.

2. If using an older version of the Session cluster without the network testing feature, initiating a network test will cause an error. Restarting the Session cluster will restore normal function.


<span id="f04554c6"></span>
## Debugging methods

<span id="cf62206c"></span>
### Function entry


1. **Entry one**: Compute resource \- Resource pools \- Actions \- Network Test


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cbd57a630c2f4150b0d224dabc63ad2e~tplv-goo7wpa0wc-image.image) </span>


2. **Entry two**: Task development \- Tasks \- Select Task \- Network Test


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c0bd6fd69f748198d071949316edbf2~tplv-goo7wpa0wc-image.image) </span>

<span id="bf9ca39e"></span>
### Usage instructions

After entering from the function entry, click Network Test, then select the resource pool and Session cluster in the popup. Also, enter the IP/domain and port to be tested. Click Confirm to start the network test.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06306011142341fd830954b170a72c7c~tplv-goo7wpa0wc-image.image) </span>

If the test fails, check the specific reason for the failure.
