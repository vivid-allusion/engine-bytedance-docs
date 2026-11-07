---
title: "Applying for Thrift2 connection address"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Applying_for_Thrift2_connection_address"
---

Table Storage for HBase provides a ZK connection address by default and supports multi\-language access through Thrift. Thrift is a service component in standard HBase instances, built on Apache Thrift, a communication framework for multiple languages. This article describes how to apply for a Thrift2 connection address through the console.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Thrift2 multilingual access is provided by the allowlist feature. If you need to use it, [submit a ticket](https://console.byteplus.com/workorder/create/) and contact technical support to apply for usage.

* The protocol version of the Thrift address provided byTable Storage for HBase is Thrift2, and the Thrift client version must be v0.13.0.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click **Connectivity**.

5. In the **Private network access** area, click **Apply** next to the **Thrift2 connection address**.

6. In the dialog box that appears, click **OK**.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations


* [Access an HBase instance from a Java program using a Thrift2 address](https://docs.byteplus.com/en/docs/HBase/Access_an_HBase_instance_from_a_Java_program_using_a_Thrift2_address)

* [Access an HBase instance from a Python program using a Thrift2 address](https://docs.byteplus.com/en/docs/HBase/Access_an_HBase_instance_from_a_Python_program_using_a_Thrift2_address)

* [Access an HBase instance from a Go program using a Thrift2 address](https://docs.byteplus.com/en/docs/HBase/Access_an_HBase_instance_from_a_Go_program_via_a_Thrift2_address)


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[StartThrift2](https://docs.byteplus.com/en/docs/HBase/StartThrift2) |Call the StartThrift2 interface to apply for the Thrift2 private network connection address of the instance. |
