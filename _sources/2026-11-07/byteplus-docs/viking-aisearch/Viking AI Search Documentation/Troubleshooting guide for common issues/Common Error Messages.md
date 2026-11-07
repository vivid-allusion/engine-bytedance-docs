---
title: "Common Error Messages"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Meaning_and_handling_of_common_error_messages"
---

*To experience more Viking AI Search capabilities, visit: * [Viking AI Search, the all-in-one intelligent engine for enterprise search, recommendations, and Q&A](https://www.volcengine.com/product/AI-Search-Rec)


---



To help you quickly resolve issues encountered while using the Viking AI Search platform, this document provides a comprehensive list of common errors. For each error, you will find the trigger scenario, specific meaning, and recommended solution, enabling you to efficiently troubleshoot and maintain your service.

<span id="8c24431c"></span>
# **Common errors and solutions**


|**Trigger scenarios** |**Error message** |**Meaning and recommendation** |
|---|---|---|
|Binding datasets to an application |QuotaExceeded: The specified quota has been exceeded: 'BindUserEventDatasetQuota'.<br><br>error: QuotaExceeded: The specified quota has been exceeded: 'BindUserEventDatasetQuota'. |The application has exceeded the limit for bound user event datasets. Each application can only be bound to one user event dataset.<br><br> |
|Open the Datasets page |The specified resource does not exist: configuration.<br><br> |There are some issues with hidden datasets and applications.<br><br>Contact BytePlus technical support to resolve the issue. |
|When importing data |Line xxx: The data contains field type conflicts. Please check the data and upload again. Problematic fields: '[audience_tag special_element symbol_element_tag visual_feature_tag visual_style_tag]'.<br><br> |The field format of the uploaded document data conflicts with the item dataset configuration. Check the data in line xxx to ensure the data format complies with the configured schema requirements. |
|When importing data |msg:ai search upload_to_dataset error \| [e] 429 Client Error: Too Many Requests for url: |A high volume of data upload requests triggered the limit.<br><br>Contact BytePlus technical support for a solution. |
|Open the Viking AI Search platform. |User is not authorized to perform: aisearch:IsEnabledAccountFunc on |This error occurs because the user account lacks the permission to perform the `aisearch:IsEnabledAccountFunc` action.<br><br>**Solution:** <br><br><br>* Log in to the IAM console and go to the "Access Control" page.<br><br>* On the **Users** page in the IAM console, find the account to be authorized, click **Add permission**, search for and select the policy related to `aisearch:IsEnabledAccountFunc` in **System Policies**, and then confirm to add it.<br><br>* If you are unsure of the specific permissions needed, contact your administrator to request admin permissions, and then configure them yourself. |
|API calls |500 Server Error: Internal Server Error for url<br><br> |A 500 error when invoking an API usually indicates that an unknown error occurred during request processing, such as a backend service timeout, network fluctuations, or other reliability\-related issues.<br><br><br>* Retry later to see if the problem persists.<br><br>* If the problem persists after multiple attempts, provide the complete error log and request ID to BytePlus technical support for troubleshooting. |
|Create index |Create index failed.: Post : context deadline exceeded<br><br> |Failed to create index due to a request timeout.<br><br>Resolution:<br><br><br>* Check the network connection status and ensure the network is stable.<br><br>* Retry creating the index later to avoid service peak hours.<br><br>* If the problem persists, contact the technical support team for further investigation. |
|Create user event dataset |QuotaExceeded: The specified quota has been exceeded: 'Number of user event datasets.'<br><br> |Failed to create the user event dataset because the quota limit was exceeded.<br><br><br>* Standard plan: you can create up to 20 user event datasets per account.<br><br>* Free plan: you can create up to 5 user event datasets per account.<br><br><br>Solution:<br><br><br>* On the Datasets page of the Viking AI Search console, check the number of user event datasets created under the current account to confirm if the quota limit has been reached.<br><br>* On the Datasets page, delete user event datasets that are no longer in use to free up quota space.<br><br>* To get more quota, consider upgrading to a higher service plan. |


&nbsp;


---



*To learn more about Viking AI Search product capabilities, see * [Viking AI Search, an integrated intelligent engine for enterprise search, recommendation, and Q&A](https://www.volcengine.com/product/AI-Search-Rec) *.*
