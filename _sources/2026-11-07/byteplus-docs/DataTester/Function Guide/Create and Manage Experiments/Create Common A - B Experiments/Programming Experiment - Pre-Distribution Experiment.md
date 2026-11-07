---
title: "Programming Experiment - Pre-Distribution Experiment"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Programming-Experiment-Pre-Distribution-Experiment"
---

DataTester's regular experiment is to shunt when the shunt interface is called after the experiment starts and the "experimental exposure event" is reported. In addition, DataTester also provides pre\-shunt experiments. Pre\-shunt experiments refer to experiments that generate shunt results at the beginning of the experiment. It is mainly suitable for scenarios where shunt results are derived in advance, such as push, offline experiments, etc. This article introduces the application scenarios and operation steps of DataTester's pre\-streaming experiment.

<span id="62f63f9c"></span>
# Application scenario

Pre\-shunting experiments are suitable for experimental scenarios such as offline experimental strategies. Usually, after using the AB platform to shunt the crowd, the target group after shunting is obtained, and the offline strategy is affected on the user. Subsequent data collection is used for effect analysis.

For example, a bank pushes customers to buy financial management, which can be promoted through different offline channels and different offline material promotion, so it is possible to create a pre\-diversion experiment to complete the diversion of the corresponding crowd through the AB platform. After that, the results of the diversion are derived, and then the relevant strategies are promoted offline. The follow\-up bank side can also report the relevant data to DataTester in the form of event tracking to analyze the relevant experimental conclusions, so as to adjust the promotion strategy and achieve the goal of improving performance.

<span id="76bb3cd6"></span>
# Usage restrictions


* Pre\-offload experiments only support private deployments.

* The maximum number of shunt target groups selected by the pre\-shunt experiment is 10 million.

* The pre\-shunt experiment is a special server side experiment, and the parent\-child experiment does not support pre\-shunt for the time being.


<span id="fa011ccd"></span>
# Preparation

<span id="e8fcd9f1"></span>
## (Optional) Data access

If you want to see the real metric effect data of each experimental version in the experimental report of DataTester after the pre\-shunting experiment is started, you need to complete the metric tracking event access required for the experiment according to the experimental design before creating the experiment. Detailed activity details of data access can be found at: [Data Access Overview](https://docs.byteplus.com/docs/DataTester/Data-Access-Overview).

<span id="1305c585"></span>
## Create a pre\-distribution population

The pre\-shunt uses the user ssid from the database to DataTester for shunt. You need to create the corresponding pre\-shunt population according to the experimental strategy plan first.


1. Create pre\-triage crowds. You can create pre\-triage crowds on the **Global Settings** \> **Audience Management** \> **User Segmentation** page.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When creating a pre\-distribution crowd, it supports <strong>rule circling</strong> or <strong>file uploading</strong>. If you use the file upload method, the user in the file needs to be active in the volcano (that is, the event has been reported in the volcano, and the user ssid has been warehoused in DataTester). For inactive users, the upload cannot be successful.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9efed39727d466fae9518f696f4edbf~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92bf3c197edd42f2bae7036ffdfad1b7~tplv-goo7wpa0wc-image.image) </span>

   See detailed instructions for creating clusters [User Cohorts](https://docs.byteplus.com/docs/DataTester/User-Cohorts).

2. (Optional) Store crowd information.

   The user ssid who has reported the data has been stored in the DataTester database and does not need to be warehoused again; the user who has never reported the event needs to enter the data first through the server side HTTP API. The configuration points of the data reporting API body are as follows. Please refer to the detailed introduction of the data reporting API [HTTP API](https://docs.byteplus.com/docs/DataTester/HTTP-API).

   ```JSON
   {
       "user": {
           "user_unique_id": "7448158****"   //Need to initialize user id
       },
       "header": {},
       "events": [
           {
               "event": "first_event",    //fixed event name
               "params": "",    //The attribute is empty
               "local_time_ms": 1489573628001   //the timestamp of the event
           }
       ]
   }
   ```
   


<span id="6ce0ffd3"></span>
# Create a pre\-split experiment

Click " **+ Create Experiment**" on the experiment list page, select Programming Experiment, and enter the experiment creation process. The configuration points of the pre\-shunt experiment are as follows. Other configuration operations are consistent with the configuration of ordinary programming experiments. Please refer to the [Programming Experiment](https://docs.byteplus.com/docs/DataTester/Programming-Experiment) documentation for details.


1. Configure basic information. The type of experiment for the pre\-shunt experiment needs to be selected at the server side.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e17450f3ff5f460a9716ed3887f68f80~tplv-goo7wpa0wc-image.image) </span>

2. Configure the effective policy.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2233835aa5fb49489ffe533d3f556281~tplv-goo7wpa0wc-image.image) </span>

   * Distribution Type: Select Pre\-Distribution.

   * Audience rule: Select the pre\-triage experimental population that has been created.

3. The configuration experiment version and the experimental index operation are consistent with the ordinary programming experiment. You can refer to the programming experiment operation document to complete the experiment creation.


<span id="be92379a"></span>
# Debug and start the experiment

After the experiment is created, it can be debugged, and the experiment can be started after there is no problem.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f8572ec971842aeb0a3fd3281eaf5d7~tplv-goo7wpa0wc-image.image) </span>

<span id="d25e8334"></span>
# Export distribution results

After the experiment is opened, you can click **Global Settings** \> **Workflow Management** \> **Pre\-shunt Experiment Management** in the left navigation bar, find the corresponding pre\-shunt experiment, click the button to **export distribution results**, select the id field that needs to be exported, export the shunt results, and then complete the relevant strategy promotion according to the shunt results.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After the experiment is started, it will take about 10 minutes for you to export the shunt results.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d25f1f623e1488188b95644a89c3803~tplv-goo7wpa0wc-image.image) </span>

<span id="5e600705"></span>
# View the experimental report

If you have completed the preparation of data access, after the experiment starts and the offline promotion starts, the user data generated by each promotion channel will be reported to DataTester one after another, and you can view the metric results of the experimental version through the experimental report.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad75eda9ae17441d9d39a31b877dfbfd~tplv-goo7wpa0wc-image.image) </span>
