---
title: "Label Template"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Label_Template"
---

<span id="_1-功能概述"></span>
# 1. Function Overview

CDP has preset the Tag Template for the automotive industry. Users can quickly map corresponding data based on the built\-in table template and tag system, apply tag templates, and construct a tag system that meets business scenarios.

<span id="_2-使用限制"></span>
# 2. Usage Restrictions


1. To use the tag template function, you need to first configure the **table template data**, which can be done by going to the **Data Fusion\-Metadata Management** module.

2. Editing permissions for the **Metadata Management** module are required.


<span id="_3-操作步骤"></span>
# 3. Operation Steps

The usage process of this function is as follows:

`Project administrators configure data connections-->Configure ID graph-->Complete table template data mapping in metadata management-->Click on label template in the labeling system, enable corresponding labels.`

The **operation steps** are as follows:


1. Click on **Data Connection** to access and integrate attribute and behavioral data in this module.

2. Click on **Data Fusion \- ID Graph Construction** to complete the ID Mapping configuration in this module.

3. Click **Data Fusion\-Metadata Management\-Table Templates**, then click **Configure Mapping**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The table template is a structure with defined headers and rules; users need to configure the mapping of specific data content based on actual situations.</div>


<div data-tips="true" data-tips-type="tip">Currently, the table template only provides templates in two forms: behavior and attribute.</div>


<span id="_3-1-配置用户属性表"></span>
## 3.1 Configure User Attribute Table


1. If you choose the mapping configuration of **User Attribute Table**, users need to search and select the registered user attribute table from the dropdown list.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Unable to change after initial configuration.</div>


<div data-tips="true" data-tips-type="warning">Baseid defaults to the ID information in the data source registration and cannot be modified.</div>



2. When **configuring fields**, users can select appropriate fields from the table based on the fields and types in the template for mapping.

3. Click **Save** to complete the configuration. The system will output the **User Full Table** data based on the template and mapping, retaining only the latest imported data for each field.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In terms of system ID mapping, if there are multiple user records, one will be randomly retained. If a user has two phone numbers that correspond to different genders, the system id mapping will randomly retain one gender.</div>


<span id="_3-2-配置用户行为表"></span>
## 3.2 Configure User Behavior Table


1. If you choose the mapping configuration of **User Behavior Table**, users need to search and select the registered user behavior table from the dropdown list.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Unable to change after initial configuration.</div>


<div data-tips="true" data-tips-type="warning">Baseid defaults to the ID information in the data source registration and cannot be modified.</div>



2. Complete the **Behavior Table Mapping** according to the table template requirements.

   * Event Occurrence Time: Display the event occurrence time registered in the data source.

   * Event: Display the event registered in the data source.

   * Event Parameters: Display the event parameters registered in the data source, with multiple values.

3. Based on the template event, configure the corresponding **event fields and attributes**, and select the source event from the dropdown list.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_12add48997c81bb82ff6659e8d226c6b.png) </span>


4. After the source event configuration is completed, you also need to configure the corresponding event attributes. Click **Configure Attributes** to configure the attributes based on the template in the page that pops up on the right side.

5. Click **OK** to finish the configuration.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c54e2c5bd3161a8d3a5c02efa866701a.png) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Final format: Behavioral data increment table, synchronize new data to daily partitions daily.</div>


<div data-tips="true" data-tips-type="warning">System id mapping: If there are multiple user records, they will all be retained. If a user has two phone numbers that correspond to different business records, the system id mapping will retain both records.</div>


<span id="_4-应用标签模板"></span>
# 4. Apply Tag Templates


1. After the template mapping is set up, users click on **Tag System\>Tag Templates**.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1f79a855bf033271d2f52cfcf5533fe0.png) </span>


2. Select the **tags** that need to be created.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5bc8436ea70dc782342eab8452c58df5.png) </span>3. Click **OK** to enable the creation rules for the corresponding tag and quickly generate the tag.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_47fe3cab21d8d989898c32ca9c719049.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Grayed\-out tags indicate that the tags have already been created and cannot be recreated.</div>


* <div data-tips="true" data-tips-type="tip">Once the tags are activated, corresponding tag levels and tags will appear in the tagging system, with the remark "(system template)" appended to the tags.</div>


* <div data-tips="true" data-tips-type="tip">Tags can be copied and deleted, but cannot be renamed.</div>
