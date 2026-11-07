---
title: "Content Data Validation reports "
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-content_data_validation_reports"
---

After the data is imported, you can view their data reports and validation results, which helps identify any issues with the imported data sets. Any outstanding problems can then be fixed through metrics such as the data volume and join rate before proceeding to the next step.

You might encounter these types of errors:


* **Import errors**—Errors detected during the data import process are identified through automated data checks. These checks are implemented to validate fundamental aspects of data quality, such as volume, fields, and format. Critical errors that have a significant impact on data quality during the importing stage are considered non\-negotiable; they cannot be skipped. Resolution of these errors is mandatory before proceeding with the data import process to ensure the integrity and accuracy of the imported data.

* **Validation errors**—The errors identified during the validation process. It requires computations, such as join rate or duplication rate analysis, to ensure that the data quality meets the necessary standards for creating a model. While fatal errors are skippable, it is not recommended to bypass them. Addressing fatal errors is advisable to uphold a higher level of data quality and enhance the reliability of the model creation process.


Data reports are available under the Validation tab of each project in the Recommend Console. You can view the data of different events or go by a specified day/range. The Validate data screen has all the information about your imported data, including which field which has a status of **PASS**, **FAIL**, or **WARNING**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3426f96c43a741fab6ef50238e490465~tplv-goo7wpa0wc-image.image) </span>

Data quality is critical to a recommendation model's success. The BytePlus Recommend team will validate a client's imported **Trial** and **Live Mode** data to ensure quality standards are met and do not negatively affect the model training process.

<span id="f2b45158"></span>
# Data validation status

There are three types of data validation status in the BytePlus Recommend console:


* **PASS**: No errors with the imported data.

* **FAIL**: Fatal error in imported data. You must resolve this error before moving on to the next step.

* **WARNING**: A non\-fatal issue with imported data. You can proceed to the next step if needed.


<span id="2d08cca2"></span>
# Viewing the error details

You can view the error details through the Validate data dashboard.

**To view the error details:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to view the data validation.

3. On the Configure screen, click **Next**.

4. On the Import screen, click **Next**.

   The Data Validate screen appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96d84fe46baf4bf3aa741f704ce690c9~tplv-goo7wpa0wc-image.image) </span>

5. Click the right arrow icon.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/085ba00b0b9c4de0bf3c42462e6d837f~tplv-goo7wpa0wc-image.image) </span>

   A more detailed error details screen appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c0dae93151049b7a821a4eb24f970ad~tplv-goo7wpa0wc-image.image) </span>

6. For further information on debugging, click on **View details**.

   An expanded details screen appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/28d64589d34c4f0e9984024a9ff62388~tplv-goo7wpa0wc-image.image) </span>


<span id="97fec752"></span>
# Detailed error details screen

You can perform a few actions in the detailed error details screen.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d265d9b7d3d54acfab04a214ddaf9cc4~tplv-goo7wpa0wc-image.image) </span>


|**Number** |**Action** |**Description** |
|---|---|---|
|1 |Viewing imported data error graph |Clicking on this icon will bring you to the imported data error. This location may vary, as it could be related to field validation, join rate, or other factors, depending on the type of error.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a859e7931a84dad8b79503b31baf045~tplv-goo7wpa0wc-image.image) </span> |
|2 |Editing threshold settings |You can customize the error threshold by adjusting sliders or inputting specific numerical values in the designated boxes on the error setting page. When you modify the error threshold, you will promptly observe errors either disappearing or emerging based on the defined error ranges. Any adjustments made on this error setting page will be automatically saved once you click the 'Save Configurations' button, ensuring that your chosen error threshold settings are retained for future use.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b12b10399fe741efbbdab6a08ad6678e~tplv-goo7wpa0wc-image.image) </span> |
|3 |View details |Clicking on this displays more information on the imported data file error such as error data samples and troubleshooting instructions. There are troubleshooting instructions and you can also edit threshold settings through this screen.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9a3236fdde14086a16c13596fae4b10~tplv-goo7wpa0wc-image.image) </span> |
