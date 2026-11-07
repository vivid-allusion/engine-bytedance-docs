---
title: "Event Tracking, Full Event Tracking"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Event_Tracking_Full_Event_Tracking"
---

<span id="6f84ca65"></span>
# Event Tracking

In user behavior analysis, one or a class of user behavior can be abstracted as an event, such as launching an app, browsing a page, applying for a loan, clicking submit, etc. We can call it an **event**. Through the development of the SDK, the process of writing event logic into the code is called **event tracking**.

And event tracking, I believe you have heard it before: "no event tracking", "full event tracking", "circle selection", "visual event tracking"... all kinds of concept words. From the perspective of the team, how to choose the event tracking form that suits your team's business has become the primary consideration. The various forms of data collection are briefly reviewed and summarized below to help you make decisions.

In the growth analysis (DataFinder) product, we can simply divide event tracking into three categories, which are described in detail below.

<span id="b1ccfe6f"></span>
# Full event tracking (visual circling, heat maps)

Full event tracking, also known as "no event tracking", "no trace event tracking" and "automatic event tracking". Full event tracking is an automatic collection and reporting for standard page browsing and standard element clicking. In the Finder, the full event tracking events collected are bav2b_click button clicks, bav2b_page page browsing. No additional investment in research and development is required, saving time and effort. But at the same time, full event tracking is at the expense of reporting a large amount of data, and can only collect simple PV and UV, which is a bit'powerless' for the collection of rich business data.

Data collected by full event tracking can also be applied to visual event tracking and heat map analysis.

The main application scenario of visual circling event tracking is for business analysts who do not understand code or technology. It can obtain the data they want to analyze at a very low threshold. It is simple and easy to understand. Click the page or button you want to analyze directly on the real interface of the website or mobile application. The system will automatically define the desired event tracking, generate circling events, and realize visual operations. Reference documentation: [Circle Event](https://docs.byteplus.com/docs/DataFinder/Circle_Event).

Heat maps can visualize the behavior of a large number of users, and through a visual interface, show the user's preferences for clicking and staying time. Reference document: [Heat Map Analysis](https://docs.byteplus.com/docs/DataFinder/Heat_Map_Analysis).

<span id="967d8a33"></span>
# Code event tracking

Code event tracking refers to the development engineer, according to business personalized needs, manually write the code to achieve data collection logic. The collection range is wide, and in theory, as long as it is the interaction of the client, it can be collected. At the same time, you can collect complex information of business logic, such as browsing product details page events need to collect information product classification, product price, product name and other attributes, which cannot be done in other event tracking forms.

But it also means that it requires a certain amount of manpower, and it is necessary to check the accuracy of calibration data transmission and the consistency of business logic.

<span id="70446757"></span>
# Preset automatic acquisition event tracking

Preset automatic collection event tracking refers to the default SDK provided by the Finder preset to collect preset events, such as App launch, App exit, etc. According to these basic events, fast access can be realized, and basic metrics such as DAU, MAU, active days, and new users can be easily analyzed. For the relevant preset operation instructions, please refer to: [Preset Property Summary Table](https://docs.byteplus.com/docs/DataFinder/Preset_Property_Summary_Table).

<span id="eae5abae"></span>
# Comparison of event tracking methods supported by DataFinder and suggestions for event tracking planning


|Comparison term |Code event tracking |Full event tracking |
|---|---|---|
|Event tracking |Code event tracking refers to the development engineer, according to business personalized needs, manually write the code to achieve data collection logic. |Full event tracking, also known as "no event tracking", "no trace event tracking" and "automatic event tracking". Full event tracking is automatically collected and reported for the browsing of standard pages and the clicking of standard elements, without the need to develop and develop code for event tracking integration. |
|Capture event |The acquisition range is wide, and theoretically, as long as it is an interactive operation on the application side, it can be collected.<br><br><br>* DataFinder provides you with preset events and properties that you can combine with the supported preset events and properties to supplement with custom code event tracking.<br><br>* For details of supported preset events/properties, see: [Preset Property Summary Table](https://docs.byteplus.com/docs/DataFinder/Preset_Property_Summary_Table). |All event tracking events collected are bav2b_click button clicks, bav2b_page page browsing and other events. For details, see [Full Event Tracking Preset Events and Properties](https://docs.byteplus.com/docs/DataFinder/Full_Event_Tracking_Preset_Events_and_Properties). |
|Applicable scenario |* It is suitable for scenarios where the logic of related fields of the collection and analysis business is tight, and the analysis is more focused.<br><br>* Especially some non\-click, **non\-visual** behavior, non\-code event tracking implementation is not possible<br><br><br>For example: search results return, registration results return, banner, floor, personalized recommendation/thousand people and thousands of faces page |* Applicable to activity pages, landing pages, simple analysis of UV, PV, clicks and other basic indicators;<br><br>* Simple analysis or statistical requirements, events that do not require custom attribute settings such as parameter transfer for event tracking events; |
|Advantage |* Complete business information;<br><br>* Events, properties, reporting timing, etc. can be customized and controlled<br><br>* Capable of fully restoring user behavior links |* No need for developers to enter manually, the least intrusive to business code, **less work++ ++** ;<br><br>* Full event tracking event data is automatically and continuously collected when the SDK is deployed, which means that even if specific events are not explicitly specified to analyze initially, full event tracking's continuous and comprehensive data collection enables **data re\-run** \- that is, past data can be queried and analyzed at any time. |
|Disadvantage |* The event tracking of each control needs to add corresponding code, which is a lot of work and requires developer support and coupling with business code;<br><br>* After the version is launched, the iteration flexibility of event tracking content is low |* Undifferentiated full collection generates invalid data reporting, wasting traffic/storage/computing resources;<br><br>* Unable to collect business\-related properties, automatic collection of all event data, automatic collection of all event data<br><br>* There are some limitations to the development framework, as detailed in the full event tracking section of the [client side](https://docs.byteplus.com/docs/DataFinder/SDK_Feature_List#%E5%AE%A2%E6%88%B7%E7%AB%AF) support scope.<br><br>* If you need to target specific user behavior, you need to combine virtual events or circled event functions to achieve |
|Integrated Operations Guide |* Preset events and properties: You don't need to do any configuration, and the corresponding data will be automatically collected and reported according to the triggering mechanism.<br><br>* Custom code event tracking:<br><br>   * First, according to the business analysis needs, plan the custom event tracking and attributes that need to be collected and reported.<br><br>   * Enter the corresponding event tracking and properties in the DataFinder console, and drop the event tracking and property names into the library first.<br><br>   * When integrating the SDK, refer to the operation guide for reporting code event tracking to configure. |* When integrating the SDK, turn on the full event tracking switch. |
|Stop data reporting |If you don't want to collect and report some code event tracking data, you can disable the corresponding event or attribute in the **Data Management** \> **metadata management** of the DataFinder console. |If you do not want to collect and report full event tracking data, you can turn off the full event tracking switch in the DataFinder console project center \> project management \> SDK settings. No need to modify the full event tracking switch in the integration code. |
|Data analysis |* Heat map and circle event functions can only be used if full event tracking is enabled. ||
