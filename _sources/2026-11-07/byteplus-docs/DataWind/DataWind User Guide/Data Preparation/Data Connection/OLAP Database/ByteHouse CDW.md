---
title: "ByteHouse CDW"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/ByteHouse_CDW"
---

This article describes how to integrate ByteHouse CDW to create datasets for BI analysis and report presentation.

<span id="_1-概述"></span>
# Prerequisites

The user must have a [ByteHouse CDW Cloud Warehouse Edition](https://www.byteplus.com/en/product/bytehouse) account.

<span id="8574afe2"></span>
# Preparation


1. Refer to [ByteHouse CDW Cloud Warehouse Edition Quick Started](https://www.volcengine.com/docs/6517/76325) to complete the purchase and activation, set the default compute group, create data objects, and import data.

2. (SaaS version only) Go to 'Tenant Management' \- 'Basic Information', click 'Allowlist Configuration', perform the add allowlist operation, enter the 'DataWind public IP for access' in the allowlist settings area, and grant this IP address permission to access the CDW service. The 'DataWind public IP for access' can be viewed at [Data Connections Overview](https://docs.byteplus.com/docs/DataWind/Data_Connections_Overview).

3. Obtain the access key. Go to 'Tenant Management' \- 'Connection Information', click 'Create', and obtain the API Key.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The generated API Key is displayed only once. Please save it carefully.   </div>
   

4. Obtain the compute group. Go to the 'Compute Group' page to obtain the required compute group name.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Ensure that the current compute group status is "Running" or "Auto Start".   </div>
   

5. Obtain the role. Go to the 'Permission Management' page, click 'Role', and obtain the required role name.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Ensure that the role has SELECT, SHOW, and CREATE permissions on the table in order to use the table in DataWind. For details, refer to <a href="https://www.volcengine.com/docs/6517/1288723">data permission management</a>.   </div>
   

6. Obtain the server. Go to 'Tenant Management' \- 'Basic Information', and obtain the server domain name in the network information section.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The following methods can be used to obtain the ByteHouse CDW connection domain name. If your current environment does not support connecting to ByteHouse CDW via domain name, you need to configure the IP address of ByteHouse CDW. You can contact BytePlus technical support to obtain the corresponding IP address.   </div>
   

7. Obtain the port. Refer to [ByteHouse CDW Regions and Availability Zones](https://www.volcengine.com/docs/6517/76323#%E9%9B%86%E7%BE%A4%E8%BF%9E%E6%8E%A5%E7%AB%AF%E5%8F%A3).

8. Obtain the VPC ID. Go to 'Tenant Management' \- 'Basic Information', in the 'Network Information' section, select the private network domain name, click 'Details', and obtain the VPC ID.


<span id="bb9687e4"></span>
# Create from data connection


1. In BytePlus, go to a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

2. Select ByteHouse CDW on the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54a6e2bcadb744f58245eca53a4717c9~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information, test the connection, and click Save after a successful connection. Multiple connection methods are provided.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9615e60689d44fca917b58e143d1825c~tplv-goo7wpa0wc-image.image) </span>


* The configuration instructions for related parameters are as follows:

   
   |Parameters |Configuration instructions |
   |---|---|
   |Data connection name |Name of the new data connection, used to distinguish between different database connections in the system. The default is Bytehouse_CDW_timestamp. The name can be modified, but please enter a standard name. Only Chinese characters, English letters, numbers, and underscores are allowed, and there must be no spaces at the beginning or end. |
   |Region |Use the default value. |
   |Access key |See [Preparation](https://docs.byteplus.com/docs/DataWind/ByteHouse_CDW#8574afe2) for how to obtain. |
   |Compute group |See [Preparation](https://docs.byteplus.com/docs/DataWind/ByteHouse_CDW#8574afe2) for how to obtain. |
   |Role |See [Preparation](https://docs.byteplus.com/docs/DataWind/ByteHouse_CDW#8574afe2) for how to obtain. |
   |Connection method |The SaaS version provides two connection methods: Volcano Cloud and Server.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd8c8d2508be4969b4848da9396f349d~tplv-goo7wpa0wc-image.image) </span><br><br>For parameter configuration instructions, see below.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5531705be44471bb1948f0fb1de6c5a~tplv-goo7wpa0wc-image.image) </span> |
   

   * The configuration instructions for SaaS version connection methods are as follows:

      
      |Connection method |Configuration instructions |
      |---|---|
      |Volcano Cloud |Applicable to scenarios where the DataWind and ByteHouse CDW region is North China 2 (Beijing).<br><br>vpcMode and VPC ID: Indicates whether VPC mode (private network mode) is used. Only the SaaS version requires these two parameters to be filled in.<br><br>The usage scenarios are as follows:<br><br><br>* **Enable VPC mode**: If your data source is **a BytePlus database or data warehouse product**, **it is recommended to use VPC mode**. Set vpcMode to **Yes** and enter the VPC ID. For how to obtain the VPC ID, see [Preparation](https://docs.byteplus.com/docs/DataWind/ByteHouse_CDW#8574afe2).<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">It is recommended to use VPC mode for BytePlus products to ensure data security and also avoid additional data transfer costs.   </div><br>   <br><br>* **Disable VPC mode**: If your data source has enabled public network access, there is no need to set vpcMode; you can set it to No. |
      |Server |Applicable to other general scenarios.<br><br><br>* Server and port: For how to obtain them, see [Preparation](https://docs.byteplus.com/docs/DataWind/ByteHouse_CDW#8574afe2).<br><br>* vpcMode and VPC ID: Indicates whether VPC mode (private network mode) is used. Only the SaaS version requires these two parameters to be filled in.<br><br>   The usage scenarios are as follows:<br><br>   * **Enable VPC mode**: If your data source is **a BytePlus database or data warehouse product**, **it is recommended to use VPC mode**. Set vpcMode to **Yes** and enter the VPC ID. For how to obtain the VPC ID, see [Preparation](https://docs.byteplus.com/docs/DataWind/ByteHouse_CDW#8574afe2).<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">It is recommended to use VPC mode for BytePlus products to ensure data security and also avoid additional data transfer costs.      </div><br>      <br><br>   * **Disable VPC mode**: If your data source has enabled public network access, there is no need to set vpcMode; you can set it to No. |
      


<span id="59f9e06a"></span>
# Create from dataset


1. In BytePlus, click Data Preparation \-\-\> Dataset, select the 'Create' button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. When selecting the data connection, click Create Configuration.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" />   </div>
   

3. The subsequent steps are the same as steps 2 and 3 of **Create from data connection** described above. After completing the configuration, you will remain at the pop\-up window for selecting a data connection, where you can proceed directly to the next step of dataset creation.


<span id="d5fedd1d"></span>
# Subsequent steps: Create a dataset


1. To create a dataset using a previously created data connection: Click Data Preparation \-\-\> Dataset, then select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. Search for or select the previously created data connection from the dropdown.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6740df52c0e7400597078214cb74ee50~tplv-goo7wpa0wc-image.image" width="450px" /></div>


<span id="5b3e7528"></span>
# Frequently asked questions


* If real\-name authentication is not completed, you will not be able to access the BytePlus ByteHouse (Cloud Data Warehouse Edition) console. Please complete [real-name authentication](https://www.volcengine.com/docs/6261/64935).

* To use the LAS service, cross\-service authorization is required. If you do not need to use it, you can ignore this step.
