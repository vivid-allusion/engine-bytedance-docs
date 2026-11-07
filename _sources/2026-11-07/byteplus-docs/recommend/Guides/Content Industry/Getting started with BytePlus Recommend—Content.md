---
title: "Getting started with BytePlus Recommend—Content"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-content_standard_getting_started"
---

This section outlines the steps you must take before building your recommendation models.

<span id="Understanding BytePlus Recommend Standard projects"></span>
# Understanding BytePlus Recommend projects

You can perform three main actions on a project: create, edit, and delete. When you edit a project, you change its metadata, including the description, title, and timezone. Deleting a project removes all the data stored within it.

A single BytePlus Recommend project is designed for one specific business. For instance, if you operate two content businesses, Brand_1 and Brand_2, you should create two distinct Recommend projects. You need to provide a unique project name and description for each, and set the timezone accordingly.

Likewise, only one model can be used per project. If you need to use different models for different recommendation scenes, you can create multiple projects catering to each scene. For example, you have a business named Brand_1 with two different recommendation scenes: "Home" and "Suggested for You." You can create two separate projects, dedicating one model to each scene.

<span id="8ab7e3e0"></span>
# Prerequisties

You need to register for a BytePlus console account before proceeding with the following steps. For more information on creating your account, refer [here](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account).

<span id="5d9d72ca"></span>
# Retrieving Recommend credentials

You need to obtain credentials, like a Tenant, Tenant_ID, or Token, to use BytePlus Recommend APIs or SDKs to import data or get model predictions. This is only possible by creating a BytePlus account.

**To retrieve a Tenant or Tenant_ID:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. In the top right corner, click on your username \> **My account**.

   The Account information screen containing the Username and Account ID appears.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/c088097-Recommend_Before_you_begin_Account_information_screen.png) </span>


<span id="52e90407"></span>
## Generating Recommend tokens

You can generate your tokens through the BytePlus Recommend console. The generated SecretAccessKey is your Token for using a BytePlus Recommend API or SDK. You can view your SecretAccessKey later by toggling the show button behind each AccessKey.

**To generate a token:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click your username \> **IAM**.

   The Identity management screen appears.

3. Click **Key Management**.

4. In the Token Management section, click **Create new access key**.

   The security risk alert pop\-up window appears.

5. Click **Continue**.

   An AccessKey is created, and the notification pop\-up window appears.

6. (Optional) Click **Download key certificate** to locally save the certificate of the generated AccessKey.

   For more information, refer to [Managing keys](https://docs.byteplus.com/byteplus-platform/docs/managing-keys).


<span id="Creating BytePlus Recommend Standard projects"></span>
# Creating BytePlus Recommend Standard projects

This section documents how you can create a new project in the Recommend Console.

**To create a Standard project:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

   The Recommendation Projects screen appears.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/d6919d0-RecommendProjects.png) </span>

2. Click **Create new project**.

   The Create New Project screen appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2d6c53dcbc549c4ae80e7b745ec04f3~tplv-goo7wpa0wc-image.image) </span>

3. Enter a Project Name.

4. Enter a Project Description.

5. Under Industry, select **Short\-Video/Image/Doc**.

6. Either select the timezone that your data source is based on or toggle the **Set timezone automatically based on current location** on.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Data import, data validation, and generated data reports will be based on your selected timezone.   </div>
   

7. Select the **Package Type**.

8. In the Project Type, select **Live**.

9. Click **Create**.

   The Create project pop\-up window appears.

10. Click **Create**.

   The project is created.
