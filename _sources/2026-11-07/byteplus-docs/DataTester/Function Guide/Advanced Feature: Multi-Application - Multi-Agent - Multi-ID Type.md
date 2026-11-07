---
title: "Advanced Feature: Multi-Application/Multi-Agent/Multi-ID Type"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Advanced-Feature-Multi-Application-Multi-Agent-Multi-ID-Type"
---

DataTester version 4.10.0 has added support for multi\-application functions and multi\-ID type functions. Combined with the previously supported multi\-agent functions, DataTester can support the addition and use of multiple applications, multiple subjects, and multiple ID types, which can improve the authenticity and accuracy of experimental data and improve the efficiency of project/application management and experimental creation. This guide introduces you to the use of multi\-application/multi\-agent/multi\-ID types.

<span id="890eacf1"></span>
# Precautions


|Attention segmentation |Detailed description |
|---|---|
|Function switch |This feature is for advanced use and is currently available on demand for customers with relatively complex business needs.<br><br><br>* New customers: Free on\-demand.<br><br>* Purchased customers: Only for environments that use one_id services, if historical data migration is required, manual execution is required. |
|Binding relationship |* A project supports binding multiple applications.<br><br>* An application only supports the option to bind one principal.<br><br>* A principal can be bound by multiple applications.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82ee4a07ef5b468b94161a4c5c12aecc~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Since an app only supports binding one principal, if you need to use the multi\-agent feature to perform data analytics on multiple agents, you need to create multiple apps in your project, each binding one principal.</div><br> |
|Other related products |When using multi\-agent functionality, you also need to simultaneously enable CDP products and deploy Oneid services. |


<span id="6dead6a7"></span>
# Function usage

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">DataTester's multi\-application, multi\-subject, multi\-ID type data reporting logic and application ideas are similar to DataFinder. For details, please refer to the <a href="https://www.volcengine.com/docs/6285/1130146">DataFinder multi\-application/multi\-subject/multi\-ID type help document</a>. The following is an overview of the main points of using DataTester.</div>


<span id="b7a3d1c5"></span>
## Multi\-application

After turning on the multi\-application function, you can add multiple applications to the project, and when you create experiments later, you can switch and choose to conduct experiments in different applications.


* Add multiple applications: You can bind multiple applications to a project in project management.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eeb2029ee83b41e2ac8b76ad1ca6a539~tplv-goo7wpa0wc-image.image) </span>

* Multi\-application authorization: Currently, an application is not authorized separately, but the project permission control shall prevail, that is, the permissions of all applications under the project are the same.

* Data access: The data access operation is similar to a single application scenario. You only need to set the appid to identify which application's data is reported.

* Use the multi\-application function: You can switch between group and project in the upper right corner of the console, switch between different applications in the project in the upper left corner, and choose to carry out experiments in a certain application.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">At present, only the data in the metadata management part is the display project\-level data, and other functional modules, such as experimental creation, diversion and indicators, are displayed in isolation with the application dimension.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/77379f75f1d24f238c510fab0a5a676d~tplv-goo7wpa0wc-image.image) </span>


<span id="9810064b"></span>
## Multi\-ID type


* Add multiple ID types:

   1. After turning on the multi\-subject function, you need to contact the technical support staff to manually configure and add multiple subjects in the background.

   2. After the background addition is completed, when you bind the application for the project, you can bind the corresponding body for the application. An application can only bind to one principal, and a principal can be bound by multiple applications.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/083d58be50194b6b8b65f83b66ea5dc9~tplv-goo7wpa0wc-image.image) </span>

* Data access: When data access, it is necessary to report the ID type (that is, report the id_type related field data) while reporting the ID data, and for the accuracy of the data, report the id_bind relationship at the same time, that is, report the binding relationship between multiple IDs. See the DataFinder [Multi-Application/ Multi-Agent/ Multi-ID Type Overview ](https://docs.volcengine.com/docs/6285/1130146?lang=en)help documentation for more information.

* Use the multi\-ID type function: After enabling and configuring the multi\-ID type, you can switch between different ID types to query user data in user scrutiny and user clustering.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8de814b45526450699598b6556fc235f~tplv-goo7wpa0wc-image.image) </span>


<span id="80ccb6ce"></span>
## Multi\-agent


* DataTester has previously supported multi\-agent functionality, allowing an experiment to be carried out for different subjects. The analysis is unified through the ssid statistical index value, and the experimental analysis itself does not require switching subjects.

* Multi\-agent functionality is available only when a CDP is purchased and one_id service is enabled at the same time.

* An application only supports binding one subject, but one subject can be bound by multiple applications. When data is accessed, it can identify which subject's data is reported by reporting the appid.
