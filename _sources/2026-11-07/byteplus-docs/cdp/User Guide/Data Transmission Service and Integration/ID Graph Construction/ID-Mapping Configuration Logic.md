---
title: "ID-Mapping Configuration Logic"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/ID-Mapping_Configuration_Logic"
---

<span id="d456fafd"></span>
# 1. Function Overview

IDMapping is a functional module that uses **association rules and fusion algorithms** to identify and connect the same user from different channels, serving as the fundamental foundation of VeCDP data.

For example, a user's data pool may include order or behavioral data from WeChat Official Accounts, WeChat Enterprise Accounts, TikTok Stores, and various proprietary apps. Each channel acquires user data with different identifiers (e.g., WeChat has UnionID, External_UserID, while proprietary apps have DeviceID, EmailID, WebID, and business UseID, etc.). Normally, inconsistency in user primary keys prevents data correlation and analysis. IDMapping is designed to resolve such issues, enabling seamless integration of data from various channels, creating more comprehensive data profiles and portraits, facilitating precise insight analysis and marketing applications.

<span id="1e10c7a9"></span>
# 2. Basic Definitions

<span id="da4b698d"></span>
## 2.1 Subject

Also known as object, individual, entity, the target object that needs IDMapping, such as a person, vehicle, or store, typically possessing the following attributes:


* Has active behavioral log data/operational logs, meaning objects that actively generate data, like people/stores/leads/vehicles

* Undergoes complete lifecycle changes, indicating objects that are not static and evolve with certain processes, like product brands/categories


**Common subject explanations:** 


|**Subject Classification** |**Explanatory Notes** |
|---|---|
|Person (User) |**Evaluation Criteria:** <br><br><br>* Whether they have the same (or similar) behavioral paths and user attributes.<br><br>> Such as sharing the same app usage, both being served (managed) objects.<br><br><br>* Whether user data segregation and separation need to be done according to business units.<br><br>> Meeting the first condition, but users from different business units must be completely separated and independently operated.<br><br><br>**Definition of Combination:** <br><br><br>* Having the same (similar) behavior + No need to split = The same subject. Scenes like **ordinary users, member users**, etc., often define users of different levels as one subject.<br><br>* Having the same (similar) behavior + Need to split = Different subjects. Scenes like financial management, credit card customers with absolute isolation are often defined as different subjects.<br><br>* Not having the same (similar) behavior = Different subjects. Scenes like **B\-side brokers and C\-side users**, one being the management target and the other the service target, where various data have no commonalities, need to split into different subjects.<br><br><br>Scenario Explanation: If a financial institution has users of different apps, consider defining the subject based on how customers manage users.<br><br><br>1. If users of different apps are considered as group assets, each department can cross\-explore user value to drive flow diversion, then users of different apps are suggested to be defined as the same subject.<br><br>2. If users of different apps are unique assets of each department, and departments are unwilling to share customer resources, then users of different apps are suggested to be defined as different subjects. |
|Car |With the intelligent transformation of cars, a car is equivalent to a mobile phone representing an end user. Car data comes relatively single and fixed (Vin code), generally does not require ID linkage, only VinID configuration is needed. |
|Store |In the process of operating a store, there is a complete operational data file, such as store revenue, operating status, and accessible marketing touchpoints, such as the store owner's mobile phone, store app, or end\-point operating tools (such as a cash register). The store's identity is relatively fixed, usually only requiring configuration of ShopID. |
|Product Category |When goods are the subject, it is recommended to take the SKC product category as the minimum granularity of the goods. Categories have inventory, revenue, sales, and other operational data in the business management process, which will be used in applications that link multiple entities in human\-goods\-scene, forming data linkage in supply recommendations, targeted marketing, and other business strategies.<br><br>Consumer Goods Direction: For common shoe categories, such as Nike AJ1, it is recommended to treat it as a single entity. It is not advisable to treat every barcode ID as a separate entity since there won't be additional business value after selling the barcode ID.<br><br>Financial Direction: Common types of financial products, such as a certain financial product, can be sold to many people, having business value.<br><br>Cross\-Internet Direction: Common material or content IDs, but for content IDs, it is advisable to research specific application scenarios clearly, otherwise the data may expand indefinitely. |


<span id="785a134b"></span>
## 2.2 OneID

Also known as BaseID, the benchmark ID, is the ultimate product of IDMapping fusion, representing a unique user identifier integrated around a certain subject, typically defined as a natural person.

> For the purchase of DataFinder or DataTester products, OneID = SSID, reusing a unified set of IDM services in the background (except for users who purchased Finder separately before June 2022).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Attention:</div>


<div data-tips="true" data-tips-type="tip">OneID (internally known as Baseid) is a unique identity generated through IDMapping. VeCDP data files and labeling systems are built on Baseid as the primary key in the data model. In cases where analysis requires other ID types, the system will convert them to corresponding IDs based on the ID\-OneID mapping relationship. The number of converted IDs may be greater than the number of OneIDs (multiple IDs correspond to one OneID).</div>


<div data-tips="true" data-tips-type="tip">OneID is the representation of a unique identifier. When querying the OneID with different IDs, you will only get one result, <strong>there won't be one ID corresponding to multiple OneIDs!</strong> <strong>(The most basic principle is that one person cannot have two IDs)</strong></div>


<span id="22e4fa4a"></span>
## 2.3 ID Types

Also known as user identifiers, are user tag data reported on different channels, such as device IDs, Email IDs.

**Common ID types across different channels:** 


|**ID type (channel identification)**  |**ID identification Code** |**ID type name** |**ID type description** |**Source type** |**Recommended priority** |
|---|---|---|---|---|---|
|UID |UID |User ID |User ID generated by the actual registration on the business side |Subject ID |1 |
|VIN_ID |VINID |Vehicle ID |Unique identifier for the vehicle logo on the business side, commonly used Vin code |||
|Shop_ID |SHOPID |Merchant ID |Unique identifier corresponding to the subject of the business entity on the business side |||
|Item_ID |ITEMID |Product ID |Unique identifier corresponding to the subject of the business\-side commodity |||
|Phone |PHONE |Mobile Phone Number |Mobile phone number, the phone number displayed in plain text |Phone Number Authentication |2 |
|Phone_SHA256 |PHONE(SHA256) |Phone number (SHA256 encryption) |Phone number, encrypted using the SHA256 algorithm |||
|Phone_MD5 |PHONE(MD5) |Phone number (MD5 encryption) |Phone number, encrypted using the MD5 algorithm |||
|IDFA |IDFA |Advertiser Identifier (IDFA) |Advertiser Identifier (IDFA) is a unique combination of letters and numbers for each iOS device, which mobile advertising networks can use to track users and deliver targeted ads |Device Identifier |3 |
|IDFA_MD5 |IDFA(MD5) |Advertiser Identifier (IDFA) \- MD5 Encryption |Advertiser Identifier (IDFA) uses MD5 encryption, a unique combination of letters and numbers for each iOS device that mobile advertising networks can use to track users and deliver targeted ads |||
|IMEI |IMEI |IMEI, mobile serial number |IMEI (International Mobile Equipment Identity) is also known as the mobile serial number, or "IMEI." It is a globally unique number that identifies a specific mobile device |||
|IMEI_MD5 |IMEI(MD5) |IMEI, mobile serial number (MD5 encryption) |IMEI (International Mobile Equipment Identity) encrypted with MD5, is also known as the mobile serial number, or "IMEI." It is a globally unique number that identifies a specific mobile device |||
|OAID |OAID |OAID, anonymous device number |Open Anonymous Device Identifier (OAID) is an Android platform device identifier jointly developed by the Mobile Security Alliance, the China Academy of Information and Communications Technology, and terminal manufacturers in accordance with the Alliance Standard "Mobile Smart Terminal Supplementary Device Identification System Specification." |||
|OAID_MD5 |OAID(MD5) |OAID anonymous device ID (MD5 encrypted) |Open Anonymous Device Identifier (OAID), encrypted using MD5, is an Android platform device identifier defined in the Alliance Standard "Mobile Smart Terminal Supplementary Device Identification System Specification" jointly developed by the Mobile Security Alliance, China Academy of Information and Communications Technology, and terminal manufacturing companies |||
|DeviceID |DEVICEID |Device ID |Device fingerprint calculated by the client through the device identifier |||
|ByteId |BYTEID |BYTEID |BYTEID |TikTok ecosystem |4 |
|DY_UnionID |DY_UNIONID |TikTok Application Identity UnionID |Openid is the identity ID of TikTok users in different types of products, which is the unique identifier of users in TikTok account, TikTok Store, mini\-programs, etc., in the current application. |||
|DY_MpID_OpenID |DY_MPID_OPENID |TikTok MpID + OpenID combination ID |MpID: Media platform ID, such as Toutiao (54), Watermelon (117), and iYouteng, etc. |||
|DY_MpID_OpenID_MD5 |DY_MPID_OPENID(MD5) |TikTok MpID + OpenID combination ID (MD5 encryption) |MpID: Media platform ID, such as Toutiao (54), Watermelon (117), and iYouteng, etc. |||
|DouDian_AppID_OpenID |DOUDIAN_APPID_OPENID |TikTok AppID + OpenID combination ID |Openid TikTok user unique identifier |||
|WX_UnionID |WX_UNIONID |Subject of WeChat Official Account Users UnionID |For the same user, the UnionID is the same for different applications under the same WeChat Open Platform account. The UnionID is the unique identifier of the user on the WeChat Open Platform, including mini\-programs, public accounts, etc. The UnionID of the same user is consistent. |WeChat Official Account |5 |
|WX_AppID_OpenID |WX_APPID_OPENID |Subject of WeChat Official Account Users AppID_OpenID Combination |OpenID is the unique identifier of the user in the mini\-program, meaning each WeChat account corresponds to a unique OpenID for each public account. |||
|WX_External_UserID |WX_EXTERNAL_USERID |Open Platform |unionid + openid = External UserID, i.e., Service Provider UserID |Enterprise WeChat |5 |
|WX_GROUP_CHAT_ID |WX_GROUP_CHATID |Enterprise WeChat Group ID |Enterprise WeChat Group ID |||
|PrivateID |PRIVATEID |Custom ID |In cases where the stock ID cannot meet the requirements, a custom ID type is defined |Custom ID |6 |


**For the purchase of DataFinder products, DataFinder contains some unique ID types:** 

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When reporting <ins>user ID (user_unique_id)</ins> and <ins>custom ID</ins> on DataFinder, please do not report different types of ID data to the same ID type, such as reporting phone numbers and user IDs to <ins>user ID (user_unique_id)</ins> simultaneously</div>


* <div data-tips="true" data-tips-type="tip">DataFinder has functions for single\-caliber and multi\-caliber, representing the number of ID types reported by customers. Reporting only <ins>user ID (user_unique_id)</ins> is single\-caliber, while additional reporting of <ins>custom ID</ins> is multi\-caliber</div>




|**ID type (channel identifier)**  |**ID Identifier Code** |**ID type name** |**ID type description** |
|---|---|---|---|
|PrivateID |finder_uid |User ID (user_unique_id) |Business user ID, set by customers, scenarios include account, phone number, email, etc.<br><br>User reporting, ID type can be specified as needed |
|PrivateID |finder_did |Device ID (device_id) |Mobile device ID, also known as Anonymous ID, is an identifier that remains the same for a device across different apps. For security reasons, the publicly exposed ID is the bytedance device ID, which can be understood as a device ID encrypted through the app ID.<br><br>DataFinder System Generated |
|PrivateID |finder_webid |Web ID（web_id） |Web ID, also known as Anonymous ID<br><br>DataFinder System Generated |
|PrivateID |finder_anonid |Anonymous ID (anonymous_id) |Client\-side custom device IDs, also known as anonymous IDs, can be generated by the client system backend or existing device IDs from history<br><br>User reporting |
|Custom ID |PRIVATEID |\-\- |Use the same custom ID reported by the user, such as phone number, as the user ID<br><br>User reporting |


<span id="e26e4546"></span>
## 2.4 ID Priority and Reference Relationship


* **Priority**: With multiple ID types on different channels, the process of generating OneID requires defining the order in which IDs participate in the generation.

* **Reference Relationship**: The key to integrating IDs is to establish a connection between **IDs**, where IDs with connections can be defined as a OneID. In this case, this connection is the reference relationship. Typically, the reference relationship is used in combination with priority to jointly define the order of OneID generation and fusion rules.


For example, the user subject has DeviceID, mobile ID, based on different priority and reference relationship scenarios:


|**Scene** |**Example image** |**DeviceID** |**Mobile phone ID** |**OneID** |**Description** |
|---|---|---|---|---|---|
|* Priority:<br><br><br>DeviceID \> Mobile phone ID<br><br><br>* Reference: None |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aba96f08bb1644048948468a3f642446~tplv-goo7wpa0wc-image.image) </span> |1 |*  |BaseID1 |No reference relationship, DeviceID and Mobile phone ID indicate no mapping relationship, each DeviceID and each Mobile phone ID represent a user, a total of 5 users according to the example |
|||2 |*  |BaseID2 ||
|||*  |AA |BaseID3 ||
|||*  |BB |BaseID4 ||
|||*  |CC |BaseID5 ||
|* Priority:<br><br><br>DeviceID on the device \> Phone number ID<br><br><br>* <br><br><br>Reference: One DeviceID is associated with multiple phone numbers |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/34d084a7d07a452395ea34ef4b87b886~tplv-goo7wpa0wc-image.image) </span> |1 |AA |BaseID1 |For low\-priority AA/BB phone numbers, refer to the high\-priority 1 device Device ID, where these two phone numbers represent one person. |
|||1 |BB |BaseID1 ||
|||2 |CC |BaseID2 ||
|* Priority:<br><br><br>Device ID \> Phone Number ID<br><br><br>* Reference: One Phone Number ID associates with multiple Device IDs |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84587da8303c4ffba5e908e897acf601~tplv-goo7wpa0wc-image.image) </span> |1 |AA |BaseID1 |The AA with low priority in data presentation is mapped to two 1/2 devices with DeviceID, but in the actual process of generating OneID, the priority 1 and 2 generate OneID first (BaseID1/BaseID2), when the lower priority is referenced for reusing OneID, only one can be reused. Therefore, mobile number A can only belong to one of BaseID1/BaseID2, and which one it belongs to can be defined by the OneID generation and reference strategy. |
|||2 |*  |BaseID2 ||


<span id="bffbc6c2"></span>
## 2.5 OneID Generation Policy & Reference Policy (optional)

<span id="f486d99f"></span>
##### OneID Generation Policy: Mandatory one\-to\-one (default off, i.e., no need for mandatory one\-to\-one)


* **Explanation**: Regardless of how the ID of a certain channel is integrated, <ins>each ID is required to correspond to one person</ins>. There is no scenario where multiple IDs are merged into one person. When querying the ID through OneID, it can only be defined to a specific ID value without exception.

* **Example**: If a mandatory one\-to\-one setting is applied to a mobile number, and a person has two mobile numbers, before the setting, the same DeviceID may be bound to the same OneID based on the same reference. After the setting, each mobile number will correspond to a OneID.

* **Scenario Suggestions**:

   * Scenario 1: All low\-priority IDs reference the highest priority ID, in this case, the default setting can be maintained \- off.

   * Scenario 2: The highest priority ID refers to the low\-priority IDs, in this case, the highest priority ID is set to mandatory one\-to\-one.

   * Scenario 3: For example, if member ID \- mobile number = 1:N, where priority member ID \> mobile number, and the requirement is that one member can only correspond to one mobile number, in this case, the member ID and mobile number can be set to mandatory one\-to\-one when the mobile number references the member ID with a reference policy.


<span id="d45c53c3"></span>
##### OneID Generation Policy: Offline reference real\-time (default on, i.e., real\-time priority by default)


* When the ID data sources include offline data and real\-time data, the offline side retains all reference relationships, which are more precise but less timely. The real\-time data relies more on whether the real\-time reported data contains rich data relationships. If it does not contain them, there may not be much integration. The offline data supplements the real\-time missing relationships the next day, resulting in potentially different OneIDs generated by offline and real\-time data. Therefore, it needs to be determined whether you prefer a more accurate OneID or better data concatenation.

   * Offline ID data: The ID reference relationship is compared with the full data, which is comprehensive and accurate, but lacks timeliness, usually T\-1.

   * Real\-time ID data: The ID reference relationship depends on real\-time data reporting, which in most cases does not include all data; it has good timeliness, usually at T\-0.

* **Purpose**：

   * When the same ID conflicts in the Baseid calculations between the offline and real\-time sides, determine whether the business ID maps to the offline or real\-time Baseid through the "Offline Reference Real\-time" configuration.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc5dce9081534d7c8510339bf341271c~tplv-goo7wpa0wc-image.image" width="513px" /></div>



* **For example: The offline real\-time fusion scenario is generally used for new user scenarios**


For example, customers have two acquisition channels, online and offline. Online users register on the APP with their phone numbers, while offline marketing conducts real\-name registration, obtaining users' phone numbers and ID numbers. The ID number takes precedence over the phone number. Multiple channels may register multiple times simultaneously, resulting in one ID number linked to multiple phone numbers.

Low\-priority IDs should refer to high\-priority IDs first and then consider reusing existing OneIDs


|**Time** |**ID Card Number** |**Mobile Number** |**OneID** |**Description** |
|---|---|---|---|---|
|Real\-time data reporting within T days |*  |123 |BaseID1 | |
|Real\-time data reporting within T days |*  |234 |BaseID2 | |
|Offline on the T\-th day |AA |*  |BaseID0 | |
|Offline on the (T + 1)\-th day |AA |123 |BaseID0 |When the phone number is turned off [offline reference to real\-time], phone numbers 123 and 234 are both linked to BaseID0 via ID card AA. |
|Offline on the (T + 1)\-th day |AA |234 |BaseID0 ||
|Offline on the (T + 1)\-th day |AA |123 |BaseID1 |When the phone number enables [Offline Reference Real\-time], the phone numbers 123 and 234 are bound to BaseID1 and BaseID2 respectively based on real\-time side data. |
|Offline on the (T + 1)\-th day |*  |234 |BaseID2 ||



* **Scenario Suggestion**: It is recommended that the real\-time configuration of reporting IDs on Finder takes precedence, with offline configuration of reporting IDs on Finder being secondary.

   * Assuming there are Finder_uid and uid with the priority order as Finder_uid \> uid:



|The type of ID reported by the buried point |Whether to report the ID relationship in real\-time (through the Idbind interface) |Recommend turning on offline reference real\-time IDs |Recommend turning off offline reference real\-time IDs |Can meet |Cannot meet |
|---|---|---|---|---|---|
|Finder_uid |*  |Finder_uid |uid |The Finder_uid has the same baseid in the real\-time side on the T\-th day, the real\-time side on the (T + 1)\-th day and the offline side in the new customer scenario, and the behaviors are concatenated. |*  |
|uid |Report the association between Finder_uid and uid. |Finder_uid、uid |*  |The uid has the same baseid in the real\-time side on the T\-th day, the real\-time side on the (T + 1)\-th day and the offline side in the new customer scenario, and the behaviors are concatenated. |In the scenario of new customers, due to the reporting of the real\-time association relationship between Finder_uid and uid through the event tracking reporting points, the offline association relationship between these two is not effective. Eventually, the baseids generated by the two may be inconsistent with the offline measurement relationship. |
||*  |uid |Finder_uid |The uid has the same baseid in the real\-time side on the T\-th day, the real\-time side on the (T + 1)\-th day and the offline side in the new customer scenario, and the behaviors are concatenated. |In the scenario of new customers, since the baseid of uid has been generated on the real\-time side, the reference relationship between Finder and uid in the offline measurement is not effective. As a result, even if there is a reference relationship in the offline measurement, the baseids generated by the two after calculation are inconsistent. |
|Finder_uid/uid multi\-caliber reporting |*  |Finder_uid、uid |*  |The baseids of both Finder_uid and uid are consistent on both the offline side and the real\-time side, as well as on the T\-th day and the (T + 1)\-th day respectively. |The reference relationship of Finder_uid and uid on the offline side is not effective, that is, the baseids generated by the two are inconsistent. |
||Report the association relationship between Finder_uid and uid |Finder_uid、uid |*  |The baseids of Finder_uid and uid on the offline side and the real\-time side are consistent on both the T\-th day and the (T + 1)\-th day. |*  |


<span id="029e55f4"></span>
##### OneID generation strategy: Is OneID changeable (enabled by default, i.e., change allowed by default)


* **Description:**  Considering the stability of ID data, if you do not want the OneID corresponding to the ID to change, you can turn off the switch that allows OneID to change

   * Benefits after turning off: The OneID corresponding to the ID will no longer change due to reference relationships, priority configurations, etc., ensuring data stability

   * Drawbacks after turning off: If there is a subsequent fusion relationship with the ID, OneID consolidation will not be performed, which could affect the long\-term accuracy of OneID consolidation

* **Scenario**:

   * Highest priority, IDs without reference relationships but not the highest priority can <ins>disable OneID changes</ins>

   * Offline reference relationships and ID generation are established almost simultaneously. There will be minimal changes later, so you can <ins>disable OneID changes</ins>

   * Example: In cases where behavioral data from anonymous login is converted to real\-name registration and there is rich anonymous behavioral data worth mining, and there is a desire to link the anonymous and real\-name data, you can set the device ID of the anonymous user to disable OneID changes to ensure the continuity of behavior before and after anonymity. (If the anonymous\-to\-real\-name conversion cycle is relatively short within 3 days, you can also use the "OneID Correction" feature to retroactively link the behaviors)

* **Attention**:

   * Do not perform one\-on\-one and close the OneID change simultaneously, as it may lead to abnormal ID mapping, affecting data consistency and integration results.


<span id="b7c6d17c"></span>
##### OneID Reference Strategy


* **Purpose**: When referring to IDs mutually, if the referenced ID has a one\-to\-many relationship, to reference the most reasonable ID corresponding to OneID, the strategy field and logic need to be specified. If not configured, the system default strategy will randomly select one ID as the reference ID.

* **Example**: For instance, when "Device ID" refers to "Mobile ID," with one Device ID corresponding to multiple Mobile IDs, setting the Mobile ID with the latest usage time as the reference Mobile ID. Here, usage time is the strategy field, and latest is the strategy logic.

* **Attention**: Reference strategies are typically set when there are many\-to\-many or many\-to\-one relationships between two IDs that strictly need to be converted to one\-to\-one references.


<span id="00356422"></span>
##### ID Unbinding Operation Between IDs


* **Purpose**: During OneID generation, firstly check for referenced IDs, then check if the ID itself has an already generated OneID. If two IDs had a reference relationship the previous day and reused the same OneID, on the following day, the relationship dissolves. The high\-priority ID can continue reusing the original OneID, while the low\-priority ID, although no longer referencing the high\-priority ID, will reuse the historically generated OneID. In this case, the corresponding OneIDs of the two IDs are still the same, which may not meet expectations in certain scenarios. Therefore, when the relationship is broken in the second step, the high\-priority ID should be given priority to generate a new OneID instead of reusing the historically existing OneID.

* **Example**: **Suppose there is a scenario where a member ID is linked to a phone number, supporting the operation of changing the linked phone number. In this case, the phone number that has been changed should not be associated with the original member.** 

   * ID Types and Priority: Member ID \> Phone Number. Phone numbers reference member IDs based on binding relationships.



| |Member ID |Phone number |Not started binding transfer |Start binding transfer |
|---|---|---|---|---|
|T\-1 day |1 |A |baseid1 |baseid1 |
|T day |\-\- |A |baseid1 |baseid2 |
||1 |B |baseid1 |baseid1 |


<span id="4a886e53"></span>
##### Cross\-Entity Transformation Relationship

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Attention: The subject conversion relationship and the reference relationship are two completely different concepts</div>


<div data-tips="true" data-tips-type="tip">The subject conversion relationship is used for <strong><ins>multiple subjects</ins></strong> to perform subject conversion, such as the human\-vehicle purchase relationship</div>


<div data-tips="true" data-tips-type="tip">The reference relationship is used for <strong><ins>a single subject with multiple IDs</ins></strong> to generate OneID, such as the phone number referring to the device ID</div>



* The **function**：The main body conversion relationship is the relationship data used when two entities switch between each other. It has a specific business meaning and, at the data level, will store at least two columns: one for the ID of the first entity and the other for the ID of the second entity. When both appear in the same row, it indicates their business mapping relationship, which will be applied in scenarios such as cross\-entity selection, cross\-entity insight analysis, and cross\-entity query services.

* **Scenario**：Taking the example of two entities, people and cars. People and cars have multiple business relationships such as preference relationships, purchase relationships, and maintenance relationships. Each relationship represents a main body conversion relationship. For instance, when selecting target users strictly based on the tags of people and cars, it heavily relies on relationship data as the query condition.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/081eaf8e960e48709b25ef1d1f8db417~tplv-goo7wpa0wc-image.image" width="2118px" /></div>
