---
title: "Event Properties"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Event-Properties"
---

<span id="aa4be2dd"></span>
# 1. Overview

<span id="9e6b5eb9"></span>
## 1.1 What are event properties?

Properties are used to describe dimensional information when the event occurs, including user information (user_id), device information (app version, device number, ip address, device model, etc.), business custom information (custom parameters reported to params), etc.

<span id="7aa6c3a4"></span>
## 1.2 Event property classification


1. Event properties: Also known as Params, different events have different event properties. The same event tracking can define multiple properties. Take the "play video" event as an example, it contains the following event properties: enter_from (page where the action took place), video_id (video id), etc.

2. Event Public property: Also known as Header, a general property that is reported by every event. The Data Access SDK presets the fields of the Device Information class into the Header.


<span id="9d8254b5"></span>
## 1.3 Event property Status Description


* Enabled: Available properties, data will be updated normally.

* Disable: Unavailable properties, data will be discarded, and cannot be viewed in the system.

* Not displayed: The data is updated normally, but it is not available in the system. It is usually applicable to the properties consumed in the background of the system.


<span id="7e5169eb"></span>
# 2. Function description

<span id="3632f1ea"></span>
## 2.1 Added event properties

You can register event properties when registering event tracking (general events), or you can register event properties separately. If you need to register event properties separately or for event public properties, you can do the following:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Common device, time and other common parameters, the data access SDK has provided you with preset event properties, you do not need to manually create repeatedly. It is recommended that you check the supported preset events and preset properties before creating custom event properties. If the business meaning is the same, try to reuse the preset fields to avoid flooding the system with fields after arbitrary definition.</div>



1. Select **Metrics Management \> Metadata Management \> Event Properties** , enter the Event Properties page, and click the **Add Event Properties** button.

2. Configure property parameters on the New Event Properties page that pops up.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4ab2736e46b41c893360bb9ee4b2385~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |Property name |When naming event properties, be specific, and use generalized parameter names carefully, such as time (what time? Is it timestamp or duration?), name (what's the name?), positive examples such as order time, it is recommended to name order_time. |
   |Event public property |* If you register a general event property (params), do not check the event public property, you need to associate the property with a specific event (there are events that report this property), if the event is not associated, the event property cannot be used when querying the event.<br><br>* If you register the event public property (header), be sure to check the event public property, which does not need to be associated with a specific event. Each event can use event public properties. |
   

3. Click the **OK** button to complete adding event properties.


<span id="5f314605"></span>
## 2.2 Property approval

The event property list only displays the accepted/registered event properties. For unaccepted properties, you can click the "Property approval" button to view and complete the approval on the "Data Approval" page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac74ce458be541329e34a56fd6372cad~tplv-goo7wpa0wc-image.image) </span>

You can also manage the event property blacklist on the "Data Approval" page, adding or removing required event properties from the blacklist.

<span id="1c1690ae"></span>
## 2.3 Modifying the data type of a custom property

If you previously registered the wrong data type or changed to a new type, you can modify the data type field in the list.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/361a6464523d4c42860ff65a7b1a4e4e~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Change types are divided into compatible and incompatible changes. Large types transfer historical data to small types without losing historical data (such as string \- \> int), and small types transfer historical data to large types (such as int \- \> float). Please choose your data type carefully.</div>


<span id="8ccc8762"></span>
## 2.4 Edit display name and property description

Support to modify the display name and property description of event properties. Support batch modification. If you want to complete the information in batches, you can filter out the event with empty display name and property description, package and export it as a csv format document, fill it out in the csv document and click the **Modify Information** button to upload and import, and realize batch modification/registration of display and description information.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94ce9443107749b0b41128ba42bfb283~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The batch import function only supports modifying the display name and property description, and other fields do not support batch modification.</div>


<span id="871fc58b"></span>
# 3. Frequently Asked Questions FAQ

<span id="caf2bc1e"></span>
## 3.1 How to delete event properties?

Deleting the registered/accepted event property is not supported. If you no longer need the property, you can modify the status to disable it. The disabled event property will no longer build data and cannot be viewed in the analysis module.

<span id="e53c84da"></span>
## 3.2 What is the difference between event properties and user properties?

Event properties record various dimensional information describing the event, such as operating system, software version, software channel, etc., and can also be article ID, article title, article author, etc.; user properties are properties of the user's own state, such as gender, age, etc.

<span id="b7b43597"></span>
## 3.3 What is the difference between event property approval and addition?

The effect of adding event properties is the same as that of accepting event properties. Both register events property information in the Data Management\-Event property List so that it can be used in advanced analysis. The difference is that the approval property needs to report the data first, and the system can only accept it after detecting the report; while the new event property can be registered before and after the data is reported, you can register the event property in the event tracking design stage, so that the event tracking does not need to be accepted after going online, and can be used directly.
