---
title: "Miracle Data"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Miracle_Data"
---

Users can connect the magic behavior data and metadata to the enterprise knowledge engine for subsequent tag creation, clustering, etc., which includes historical total data, metadata, as well as incremental data and metadata. This article shows you how to connect your data.

<span id="3f77439d"></span>
# Conditions of use

Users need to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to use this function.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="b10a28a8"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. In the **data connection** interface, select **Application Data Source \- Miracle Data** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2fb7526abdf14023aa801cd06d091aef~tplv-goo7wpa0wc-image.image) </span>

3. On the edit page, configure the corresponding parameters.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/03abbd325ee0424585ae141eefe13466~tplv-goo7wpa0wc-image.image) </span>

   
   |parameter |explain |
   |---|---|
   |data connection name |Required item, connection name _ year, month, day, hour, second, such as ftp_sftp_xxx |
   |data type |Selectable event table only (transaction table) |
   |Kafka server address/topic |Fill in the Miracle server address and topic, and verify the connectivity sample data example. |
   |Extract sample data |Sample data can be extracted after successful verification |
   |data mapping settings |The value of the attribute field can only be selected as string, integer type (short, int, long,....), floating point type (float, double), array type, timestamp type |
   |ID\- Mapping Type |Divided into real\-time conversion and real\-time generation |
   |subject |Select the principal to be configured |
   


<span id="a1e371ed"></span>
# Common problem


1. The data samples of the Miracle data source support input customization, but need to conform to the Miracle event message format, refer to [Data Format](https://docs.sensorsdata.com/sa/docs/tech_knowledge_layout/).

2. The Miracle data source automatically generates access tasks according to the system template, and does not support viewing/modifying task processing logic by default. If there are special needs, you can provide support.

3. The Miracle data source is a dataset automatically generated according to the system template. The current version does not support viewing imports for offline tasks.
