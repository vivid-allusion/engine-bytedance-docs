---
title: "Event Property Storage Logic Description"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Event_Property_Storage_Logic_Description"
---

This article introduces the logical explanation of how data is stored in the DataFinder when reporting event properties and event public properties.

<span id="52a8649d"></span>
# Logical description

You first need to understand the process of event property reporting and inventory storage. There are three basic processes: metadata registration, data reporting, and data storage.


1. Metadata registration:

   This process refers to the registration of event properties/event public properties in the DataFinder's metadata repository.

2. Data reporting:

   This process refers to the integration of the data to be collected through the client side, server level SDK, etc. When the subsequent application is used by the end user, once the corresponding event tracking is triggered, the corresponding data will be reported to the DataFinder according to the data reporting policy of each end.

3. Data drop inventory storage:

   This process involves reporting data to the DataFinder and eventually storing it in the DataFinder's database.


See below for a detailed logical description of each process.

<span id="7a31d11d"></span>
## Metadata registration

<span id="1d1f758d"></span>
### General logic


* This process refers to the registration of event properties/event public properties in the DataFinder's metadata repository.

   It is recommended that you plan the event tracking requirements in combination with the business analysis requirements. If there are custom event and property analysis requirements, you can first register the corresponding events and properties in the metadata of the DataFinder.

* There are usually several ways to register metadata:

   
   |Manual registration (recommended) |Automatic registration |
   |---|---|
   |You can manually create event properties/event public properties in DataFinder's console **metadata management** \> **event properties** page before reporting data using client side or server level SDK, etc. After the creation is completed, the registration of the corresponding property is completed in the DataFinder metadata.<br><br>See activity details for manual registration [Event Properties](https://docs.byteplus.com/docs/DataFinder/Event_Properties). |If you have not manually registered a certain property data in the DataFinder metadata page, and then report the data directly to the DataFinder, the DataFinder will first check whether the corresponding metadata has been registered in the metadata database. If it has not been registered before, when receiving the reported data, the DataFinder will automatically register the metadata for you first. |
   |Notes:<br><br><br>* When a property is registered, a property with the same name cannot exist.<br><br>* Automatic registration fails if there is a property with the same name. ||
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After metadata registration, the data in the subsequent actual data access and reporting must be consistent with the results at the time of registration. If adjustments are required during the business analysis process, it is also recommended to modify the registration results of metadata and the SDK code configuration for access and reporting synchronously, and always maintain the same configuration on both sides. Otherwise, it may lead to abnormal data reporting.   </div>
   

<span id="b5c20886"></span>
### Enable event tracking to force acceptance


* Manual registration: Since the manually registered metadata has been registered in the DataFinder metadata, the mandatory acceptance switch has no effect on the manually registered metadata. When the data is reported later, the property properties will be stored in the database after the event tracking acceptance is passed, which has no effect on the registered metadata.

* Automatic registration: If the mandatory acceptance switch is turned on, you need to manually accept it before the automatically registered metadata can take effect, and the data reported after it takes effect can continue to be stored in the inventory; if the acceptance fails, the automatic registration of the metadata cannot be completed.


<span id="d14fa61f"></span>
## Data reporting


* This process refers to the integration of the data to be collected through the client side, server level SDK, etc. When the subsequent application is used by the end user, once the corresponding event tracking is triggered, the corresponding data will be reported to the DataFinder according to the data reporting policy of each end.

* For event properties and event public properties, there is usually a fixed position in the reported data.

   
   |Property data reporting example |Report location description |
   |---|---|
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02c788cb13ea42f6b6872fb9765dac2d~tplv-goo7wpa0wc-image.image) </span> |* Event properties: Usually reported in the `params`that report the data.<br><br>* Event public properties: Typically reported in the `header_custom`of the reported data.<br><br><br>For the specific reporting locations of different types of property data at each end, please refer to the data access document of the corresponding end. |
   


<span id="a2d7610a"></span>
## Inventory storage

This process involves reporting data to the DataFinder and eventually storing it in the DataFinder's database.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In the process of data reporting to the final storage, some types of data include processes such as data stream cleaning, computational optimization, etc. This article will not discuss such processes for the time being, but will focus on the storage logic after the data processing is completed.</div>


<span id="eeb284c0"></span>
### SaaS\-cloud\-native

In SaaS cloud\-native environments, inventory storage can be refined into the following processes:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/05cecf3cbdc44db2b4b7047766782dbf~tplv-goo7wpa0wc-image.image) </span>


1. Metadata validation: The DataFinder will first determine the property type (whether it is an event property or an event public property), and find and verify the property metadata of the corresponding type in the metadata according to the judgment result.

   1. Property type judgment: The main basis for judgment is the code location where the reported data is located:

      * Data reported in the reported `params`is determined as an event property.

      * The data reported in the `header_custom`of the reported data is determined to be a public property of the event.

   2. Metadata Query/Registration: If this property has never been registered before, DataFinder deduces the data type of your current property according to the property data format you reported, and automatically completes the registration of metadata for you according to the derived data type. After automatic registration, it will be stored in the inventory.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If there is a property with the same name, it will automatically fail to register.      </div>
      

   3. Event correlation verification/derivation:

      * For data that is determined to be event properties: DataFinder will also associate the reported event properties with the event, and associate the properties in the `params`of the reported data with the event. If the association has never been registered in metadata before, it will automatically register the association between the registered properties and events for you.

      * For data determined to be event public: Default event public property and all event associations.

   4. Data type verification/derivation: For the registered property data, it will check whether the property data type you reported is consistent with the registered data type. If not, it will be forcibly converted according to the data type set during metadata registration, and then stored in the inventory. If the conversion fails, the data will be discarded and cannot be stored in stock.

2. After metadata verification, DataFinder will store the reported data in the database.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Event properties and event public properties are stored in the same location and manner in the DataFinder database, and properties with the same name cannot exist.   </div>
   

<span id="23bc20e4"></span>
### Privatization

In a privatized environment, inventory storage can be refined into the following processes:


1. Metadata validation: In the privatization scenario, the DataFinder does not pay attention to the property type of the reported data (whether it is an event property or an event public property), but directly finds and verifies the data type in the metadata.

   1. Metadata query/registration:

      * If the reported property has never been registered before, DataFinder deduces the property type and data type of your current property according to the location of the reported property data in the code and the data format, and automatically completes the registration of metadata for you according to the derived results. After automatic registration, it will be stored in the inventory.

         * Data reported in the reported `params`is determined as an event property.

         * The data reported in the `header_custom`of the reported data is determined to be a public property of the event.

      * The property data that has been registered will be checked whether the property data type you reported is consistent with the registered data type. If it is inconsistent, it will be forcibly converted according to the data type set during metadata registration, and then stored in the inventory. Conversion failure will be discarded.

         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="3">warning         </div>
         

         <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">In a privatized environment, if a property has been registered in metadata before, only the consistency of the property data type will be checked during property verification, and the consistency of the property type will not be checked according to the location where the property data is reported.         </div>
         

         <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">For example, property A is registered as an event property when it is registered in metadata, but when the data is actually reported, it is reported in the <code>header_custom</code>of the data code, and finally the DataFinder will report the data normally. The type of property of this property in the metadata is the event property.         </div>
         

   2. Event correlation verification/derivation:

      * For data that is determined to be event properties: DataFinder will also associate the reported event properties with the event, and associate the properties in the `params`of the reported data with the event. If the association has never been registered in metadata before, it will automatically register the association between the registered properties and events for you.

      * For data determined to be event public: Default event public property and all event associations.

2. After metadata verification, DataFinder will store the reported data in the database.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Event properties and event public properties are stored in the same location and manner in the DataFinder database, and properties with the same name cannot exist.   </div>
   

<span id="2d0c199a"></span>
### Enable event tracking to force acceptance


|SaaS\-cloud\-native |Privatization |
|---|---|
|After enabling event tracking to force acceptance, if the property type defined in your metadata is inconsistent with the property type determined based on the position of the actual reported data in the code, the interface will prompt you "property type is inconsistent", the data will not be accepted and the data will not be stored normally. |Since the privatization scenario will not force the verification of the property type, after enabling event tracking to force acceptance, if the property type you define in the metadata is inconsistent with the property type judged based on the position of the actual reported data in the code, you can still check it on the event tracking acceptance interface. After the acceptance is passed, the data can be stored normally according to the property type registered in the metadata. |


<span id="b8d054e8"></span>
# Notes: Modify the event property type

If you modify the type of the event property in **metadata management** \> **event properties**, modify the event property to the event public property, or modify the event public property to the event property, the data reporting and storage logic before and after modification still follows the above logic. The following are a few typical modified scenarios for you to illustrate the impact of the modified property type.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c8c73419d834787abdce531e9022124~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">If you modify the property type in <strong>metadata management</strong> \> <strong>event properties</strong>, please remember to contact the research and development of data access, synchronously modify the access SDK code of data reporting, and synchronously modify the position of property data reporting in the SDK code to the position of corresponding type property data reporting.</div>


* <div data-tips="true" data-tips-type="warning">After modification, please remember to delete the reporting code of the original property type in the SDK code to prevent the property of the same name from being reported in the event property and the event public property at the same time, resulting in data reporting errors.</div>


* <div data-tips="true" data-tips-type="warning">Please note that if you need to modify the property type, it is recommended to modify the property type in <strong>metadata management</strong> \> <strong>event properties</strong> and then synchronously modify the access SDK code. Try not to modify the access SDK code directly without modifying it in the metadata management page to avoid data reporting abnormalities.</div>



<span id="325303bf"></span>
## Example 1: The original property A is an event property and has been registered in metadata, and the data has been reported. Subsequent access to the SDK code changes will report the property as an event public property.


* Example scenario:

   * In this example scenario, the user does not modify the property type on the metadata management page of the DataFinder, but directly modifies the code location reported by the property in the access SDK code.

   * The original event property A has been reported (the reported data is in `params`), and after modifying it to the public event property, it is reported in the public event property (the reported data is in `header_custom`).

* Logical explanation before and after the change:

   
   |comparison term |SaaS\-cloud\-native |Privatization |
   |---|---|---|
   |Modified data reporting logic |DataFinder will check in the properties of metadata whether there is a property named "A" registered before \- because A was registered in metadata as an event property before, it cannot register a property with the same name, so the automatic registration fails, and the reported data after modifying the SDK code cannot be stored normally. |1. After being modified to a public event property and reported, DataFinder will check in the metadata when the modified data is reported to see if any property with the same name has been registered \- since A was registered in the metadata as an event property before and has been registered, DataFinder will register this reported data as an event property.<br><br>2. At the same time, the DataFinder will check the consistency between the data type of the reported property and the data type of the previously registered event property metadata. If there is no consistency, the reported data type will be forcibly converted into the data type registered in the metadata for storage.<br><br>3. After completing the above verification, DataFinder stores the property data into the database. |
   |follow\-up data query |After completing the data storage, when using the analysis tool to query the property data:<br><br><br>* Query time after property modification: data could not be queried.<br><br>* Query time before property modification: the corresponding property data can be queried, and the property type is an event property. |After completing the data storage, when using the analysis tool to query the property data:<br><br><br>* The corresponding property data can be queried.<br><br>* The property type is an event property and does not become an event public property just because it is reported `header_custom`. |
   


<span id="3522c089"></span>
## Example 2: The original property A is an event property and has been registered in metadata. Modify the property type to an event public property on the metadata management page, and it will be reported as an event public property in the access SDK code.


* Example scenario

   * The original event property A has been registered in the metadata management \> event properties page of the console, and then the property is modified to the event public property, and the access SDK code when reporting is modified to the event public property reporting ( `header_custom`).

* Logical explanation before and after the change:

   
   |comparison term |SaaS\-cloud\-native |Privatization |
   |---|---|---|
   |Modified data reporting logic |* After changing to the public event property and reporting, the DataFinder will determine that the currently reported data is the public event property `header_custom`the location of the data report.<br><br>* After determining that it is an event public property, DataFinder will check whether there is a previous event public property named "A" in the event public property of the metadata \- since property A has been modified to the event public property and has been registered in the metadata, so:<br><br>   1. The DataFinder stores this property data as an event public property.<br><br>   2. The DataFinder verifies the reported data type against the data type in the metadata:<br><br>      * Inconsistencies will convert the data type to the data type in the metadata.<br><br>      * If the conversion fails, this piece of data will be discarded and will not be stored in the inventory.<br><br>   3. After completing the verification of the above metadata, DataFinder stores the property data into the database. |1. After being modified to a public event property and reported, DataFinder will check in the metadata when the modified data is reported to see if any property with the same name has been registered \- since property A has been modified to an event public property in the metadata, DataFinder will put this reported data into storage as an event public property.<br><br>2. At the same time, the DataFinder will check the consistency between the data type of the reported property and the data type of the previously registered event property metadata:<br><br>   * Inconsistencies will convert the data type to the data type in the metadata.<br><br>   * If the conversion fails, this piece of data will be discarded and will not be stored in the inventory.<br><br>3. After completing the above verification, DataFinder stores the property data into the database. |
