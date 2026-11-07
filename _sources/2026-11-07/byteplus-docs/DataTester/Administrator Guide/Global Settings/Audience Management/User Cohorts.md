---
title: "User Cohorts"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/User-Cohorts"
---

<span id="一-概述"></span>
# Background information

User grouping is a key step for enterprises to conduct data analytics and fine\-grained operations. User grouping refers to the labeling of user information. Users with the same attributes are divided into a group through their historical behavior paths, behavior characteristics, preferences and other attributes, and subsequent analysis is carried out.


* In the A/B experiment, using the user grouping ability to delineate the target user for directional experiments helps to open the effectiveness of experimental goal setting.

* The same application, if users create clusters in a growth analysis (DataFinder) product, also supports the use of clusters when creating experiments in "A/B Testing" products and creating features to select target audiences.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you have also purchased a customer data platform (GMP) product, the user grouping page of DataTester will directly jump to the customer data platform product page. For user grouping operations in this scenario, please refer to the customer data platform help documentation. The following is a guide to user grouping when you have not purchased a customer data platform.</div>


<span id="二-分群列表"></span>
# Go to the user grouping page

After logging in to the DataTester console, click **Global Settings** \> **Audience Settings**\> **User Segmentation** in the left navigation bar to enter the User Segmentation page. The user clustering page shows you the basic situation of clustering, as shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fae1e8122cfc422b82d6bc7d8e16f345~tplv-goo7wpa0wc-image.image) </span>

You can perform the following user grouping operations on the current page


* **Create:**  Click "Create Cluster" in the upper right corner to choose to create a cluster through conditions and files. See the Create Cluster section below for activity details.

* **Search:**  Enter the group name and creator to search for the currently created group.

* **Other administrative actions:**  You can also export, edit, refresh, and delete created user groupings.


<span id="三-创建分群"></span>
# Create user groups

After entering the user grouping page, click the " **+ user grouping**" button in the upper right corner to choose to create a user grouping by circling rules and uploading files.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d06a43c122b4eaeaf3a33f934322ee9~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-通过「规则圈选」创建"></span>
## **Create method 1: Rule creation segment**


1. Configure basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0407697bb1e4131bd619a3fce79e572~tplv-goo7wpa0wc-image.image) </span>

   
   |Configuration item |Configuration instructions |
   |---|---|
   |Cluster Name & Cluster Description |You can directly edit the subgroup name and description information. |
   |Calculation period |After the creation of the user cluster is completed, the subsequent user clusters are routinely recalculated to obtain the latest cluster population data according to the creation rules, or only calculated once, and the subsequent user data of the cluster is manually updated.<br><br><br>* Daily routine: After the creation is completed, the calculation will be carried out, and the previous day's data will be calculated at 6 o'clock every day.<br><br>* Manual update: After the creation is complete, it will be calculated, and it will not be automatically updated after the calculation is completed. If you need to recalculate, please click "Update". |
   

2. Configure the creation rule details for a user cluster.

   1. Sets the time range for each user clustering rule.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99d9c8ca4cfa4dfdaeb67880e94e2682~tplv-goo7wpa0wc-image.image) </span>

      
      |Configuration item |Configuration instructions |
      |---|---|
      |Time frame |Time range Support'same time period '&'different time periods'<br><br><br>* Same time period: The time period for all filters is the same<br><br>* Different time periods: Customize the time period for each filter<br><br>* Maximum support for each time range Select 365 consecutive days |
      

   2. Configure the calculation rules for clustered users.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99ce82f5b43c4001a0657dd2e5e72703~tplv-goo7wpa0wc-image.image) </span>

      
      |Configuration item |Configuration instructions |
      |---|---|
      |Filter condition |You can select certain behaviors of users "done", "not done", "done in turn" & "user is" and "user is not" attributes for user filtering.<br><br><br>* Note: If you select "User Yes", you can only select the final value of the user's attribute (i.e. the latest value for that attribute for that user). If you need to select a dynamic property (such as a property value from 30 days ago), first select the triggering event and select the desired property in the filter criteria.<br><br>* Details of the rules under each filter condition can be found in the following section on the logical description of clustering rules. |
      

   3. Adjust the logical relationship of each filter.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/780f1bbbaa03403386d12390e94ed2b4~tplv-goo7wpa0wc-image.image) </span>

      * Filter conditions support "and/or" switching;

      * Combination conditions support "and/or" switching;

   4. Estimated number of clustered users.

      
      |Configuration item |Configuration instructions |
      |---|---|
      |Estimated number of people |Click the refresh icon to immediately calculate the number of people in the current group |
      


<span id="_3-2-通过「文件上传」创建"></span>
## **Create Method 2: File Upload**

Support to create user groups by uploading user_unique_id, ssid, device_id and other ID types of list files, as shown below:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The private deployment 4.9.0 version starts to support the user ID caliber of ssid and device_id types. From this version, you can upload the corresponding type of user subgroup file to create user subgroups.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b8bbbd5786034a60baa262f3f147d67a~tplv-goo7wpa0wc-image.image) </span>

<span id="四-使用分群"></span>
# Use clustering

When creating experiments and creating features to set your target audience, you can choose to group users. As shown below:

<span id="创建实验中实验"></span>
## Create an experiment in an experiment


* The second step is "Set Effective Policy" \- \> "User Audience Rules";

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e26f31cf1ee43ccb4a2f6d749e3bed4~tplv-goo7wpa0wc-image.image) </span>


<span id="创建feature中使用"></span>
## Use in Creating Features


* Step 3 "Publish Audience \- Custom Audience Rules".


<span id="cf020f0d"></span>
# Reference: User grouping creation logic

The following describes the logic for creating the main cluster. For more information, please refer to the DataFinder's user cluster documentation.

<span id="c0501e9e"></span>
## **Detailed explanation of user grouping rules**


|**Rule condition** |**Rule introduction** |**Calculation condition** |**Value range** |
|---|---|---|---|
|User did |Select the specific event that meets the business requirements. |* Total number of times: The total number of times the event occurred<br><br>* Daily number: The total number of times the event occurs per day<br><br>* Day distribution: The distribution of the number of days that the user triggered the event<br><br>* Consecutive days: The number of consecutive days that the user triggered the event<br><br>* Sum/Maximize/Minimize/Average/Deduplicate by |equal to, greater than, greater than or equal to, less than, less than or equal to, or interval |
|The user has not done it. |A very common scenario in operations is to find users who haven't done something in a while and reach them in a targeted manner. |* Total number of times: The total number of times the event occurred<br><br>* Daily number: The total number of times the event occurs per day<br><br>* Day distribution: The distribution of the number of days that the user triggered the event<br><br>* Consecutive days: The number of consecutive days that the user triggered the event<br><br>* Sum/Maximize/Minimize/Average/Deduplicate by |equal to, greater than, greater than or equal to, less than, less than or equal to, or interval |
|Users did it in turn |Specifies a sequence of event behaviors that will be selected only if the user fires these events in sequence. |||
|User is |Support for selecting user attributes, user groups, and user labels (the latest value is selected by default). ||equal to, not equal to, contain, do not contain, empty, not empty, custom include, regular match |
|User is not |Exclude users for specific user attributes, user groupings, and user labels. ||equal to, not equal to, contain, do not contain, empty, not empty, custom include, regular match |


<span id="36888368"></span>
## **Time of grouping computation**


* The current grouping will start routine calculations at 6 o'clock every day, and usually complete a calculation before 8 o'clock.

* If'today 'is included in the grouping time condition, real\-time calculation will be triggered when the first calculation & refresh is performed; the daily routine task only calculates the data of t\-1 days


It can be seen that the cluster computing strategy of BytePlus growth analysis ensures that the population in the cluster is up\-to\-date whenever users use clusters.

<span id="d8a6bdfa"></span>
## **Building static grouping**


* If your clustering condition contains only static time (e.g. 2022.1.1 \- 2022.2.1); only manual updates are supported

* If you don't need to update the clustering results daily, you can also choose to update manually


<span id="9a02b48e"></span>
# Reference: Effective rules for user grouping in triage

User grouping, as one of the implementation methods of the audience rule of the experiment, takes effect in the process of experimental triage and is consistent with the filtering of the general audience rule. The process of triage is roughly as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f05b43a679a44b2883096528e4bd310f~tplv-goo7wpa0wc-image.image) </span>

It can be seen from the figure that if the user is not a whitelist user, hash bucketing will be performed first when diverting, and then the filtering conditions will be carried out, that is, the audience rule conditions such as user grouping will take effect after bucketing.
