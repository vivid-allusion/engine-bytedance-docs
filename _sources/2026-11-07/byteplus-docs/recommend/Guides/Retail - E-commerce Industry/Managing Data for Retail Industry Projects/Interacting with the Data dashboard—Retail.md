---
title: "Interacting with the Data dashboard—Retail"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-managing_data_for_retail_industry_projects"
---

After you create a project, you will move on to the BytePlus Recommend's Data dashboard. There are three main processes that you must complete in both the **Trial** and **Live** mode respectively:


|**Step** |**Description** |**Action(s) Needed** |
|---|---|---|
|Configure |The Configuration step enables users to define the schema, scene, attribution, and core metrics for the data. These configurations are essential for setting up the data handling process. |Within the Configure screen, you are required to manage or review the following:<br><br><br>* Data schema<br><br>* Scene<br><br>* Attribution<br><br>* Metrics |
|Import |The Import step allows users to import data into the application. It supports three stages: trial, historical, and incremental import options. |Within the Import screen, you are required to do the following:<br><br><br>* Import trial data<br><br>* Import historical data<br><br>* Import incremental data |
|Validation |The Validation step ensures data integrity and accuracy by performing data validation checks. Users can review the validation report to verify the quality of the imported data. |Within the Validation screen, you are required to do the following:<br><br><br>* Review the import process<br><br>* Identify the errors and rectify them<br><br>* Reimport the data |


<span id="e314120b"></span>
# Data dashboard modes

The Data dashboard operates in two modes: **Trial** Mode and **Live** Mode. Each mode serves different purposes and comes with its own set of rules and restrictions. When you first create your project, you will be in Trial mode by default. You will have to go through the entire process of configuring, importing, and validating your data and ensuring that all fatal errors are resolved before you have the option of switching to Live mode.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/76d8b929666d4825819c402decf1c836~tplv-goo7wpa0wc-image.image" width="864px" /></div>


<span id="70d51ddc"></span>
## Trial Mode


* Trial mode provides users with a sandbox environment to experiment with different configurations and imports. It allows them to check the results through the data validation report.

* Users are encouraged to begin with a smaller subset of data, importing 1\-2 weeks' worth of data, to test their data quality and configurations effectively.

* Any data imported in Trial Mode will be discarded if the user switches to Live Mode.

* Configuration settings made in Trial Mode will be saved and carried over to Live Mode, providing a seamless transition.

* Users have the flexibility to change configurations at any time during Trial Mode.


<span id="6bb6c6b5"></span>
## Live Mode


* Live Mode is the operational mode when users are confident in the data quality based on the validation results.

* Data imported in Live Mode is stored to create and train the model.

* Certain configurations are locked and cannot be changed in Live Mode, including Schema, Scene, Attribution, Join Rate, and Core Metrics.

* However, users can still adjust the Threshold of Error (in the error summary) even while in Live Mode.
