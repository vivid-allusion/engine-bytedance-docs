---
title: "Releasing Thrift2 connection address"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Releasing_Thrift2_connection_address"
---

If you no longer need to access the HBase instance through a Thrift2 connection, you can release the connection address. This topic describes how to release a Thrift2 connection address from the console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A Thrift2 connection address has been requested. For instructions on how to request a Thrift2 connection address, see [Applying for Thrift2 connection address](https://docs.byteplus.com/en/docs/HBase/Applying_for_Thrift2_connection_address).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

After the Thrift2 connection address is released, the HBase instance will no longer support the Apache Thrift protocol, and applications will be unable to access the HBase instance through the Thrift2 connection address. Ensure that the Thrift2 connection address configured in your application is changed to another type, such as a ZK connection address.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click **Connectivity**.

5. In the **Private network access** area, click ** ** the <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_780fa292e1f1e020b9db018da34cb501.jpg)<sub> </sub></span> icon next to the Thrift2 connection address.

6. In the dialog box that appears, click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[StopThrift2](https://docs.byteplus.com/en/docs/HBase/StopThrift2) |Call the StopThrift2 interface to delete the Thrift2 private network connection address of the instance. |
