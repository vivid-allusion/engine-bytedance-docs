---
title: "Retail Data Validation reports "
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-data_validation_reports"
---

After the data is imported, you can view their data reports and validation results, which helps identify any issues with the imported data sets. Any outstanding problems can then be fixed through metrics such as the data volume and join rate before proceeding to the next step.

You might encounter these types of errors:


* **Import errors**—Errors detected during the data import process are identified through automated data checks. These checks are implemented to validate fundamental aspects of data quality, such as volume, fields, and format. Critical errors that have a significant impact on data quality during the importing stage are considered non\-negotiable; they cannot be skipped. Resolution of these errors is mandatory before proceeding with the data import process to ensure the integrity and accuracy of the imported data.

* **Validation errors**—The errors identified during the validation process. It requires computations, such as join rate or duplication rate analysis, to ensure that the data quality meets the necessary standards for creating a model. While fatal errors are skippable, it is not recommended to bypass them. Addressing fatal errors is advisable to uphold a higher level of data quality and enhance the reliability of the model creation process.


Data reports are available under the Validation tab of each project in the Recommend Console. You can view the data of different events or go by a specified day/range. The Validate data screen has all the information about your imported data, including which field which has a status of **PASS**, **FAIL**, or **WARNING**.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa377d1600234185839f8fd018b7051b~tplv-goo7wpa0wc-image.image" width="864px" /></div>


Data quality is critical to a recommendation model's success. The BytePlus Recommend team will validate a client's imported **Trial** and **Live Mode** data to ensure quality standards are met and do not negatively affect the model training process.

<span id="c1206dbe"></span>
# Data validation status

There are three types of data validation status in the BytePlus Recommend console:


* **PASS**: No errors with the imported data.

* **FAIL**: Fatal error in imported data. You must resolve this error before moving on to the next step.

* **WARNING**: A non\-fatal issue with imported data. You can proceed to the next step if needed.


<span id="bf809814"></span>
# Viewing the error details

You can view the error details through the Validate data dashboard.

**To view the error details:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to view the data validation.

3. On the Configure screen, click **Next**.

4. On the Import screen, click **Next**.

   The Data Validate screen appears.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa377d1600234185839f8fd018b7051b~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

5. Click the right arrow icon.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71a2bceec78e4621b402f60cdbec7424~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

   A more detailed error details screen appears.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca4a9e72cf174464bb11d4fffdb2a751~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

6. For further information on debugging, click on **View details**.

   An expanded details screen appears.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38d5ed11c846491da4c09b891f7ab7da~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   


<span id="5b510aeb"></span>
# Detailed error details screen

You can perform a few actions in the detailed error details screen.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/76ec6db8777f4df085169e052887d4b7~tplv-goo7wpa0wc-image.image" width="864px" /></div>



|**Number** |**Action** |**Description** |
|---|---|---|
|1 |Viewing imported data error graph |Clicking on this icon will bring you to the imported data error. This location may vary, as it could be related to field validation, join rate, or other factors, depending on the type of error.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f84e760cbe054af18edead9239df6e28~tplv-goo7wpa0wc-image.image) </span> |
|2 |Editing threshold settings |You can customize the error threshold by adjusting sliders or inputting specific numerical values in the designated boxes on the error setting page. When you modify the error threshold, you will promptly observe errors either disappearing or emerging based on the defined error ranges. Any adjustments made on this error setting page will be automatically saved once you click the 'Save Configurations' button, ensuring that your chosen error threshold settings are retained for future use.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b12b10399fe741efbbdab6a08ad6678e~tplv-goo7wpa0wc-image.image) </span> |
|3 |View details |Clicking on this displays more information on the imported data file error such as error data samples and troubleshooting instructions. There are troubleshooting instructions and you can also edit threshold settings through this screen.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1039f852555a407685e1f12c2878eab4~tplv-goo7wpa0wc-image.image) </span> |
