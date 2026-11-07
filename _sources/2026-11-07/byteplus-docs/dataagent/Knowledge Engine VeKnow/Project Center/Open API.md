---
title: "Open API"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Open_API"
---

The enterprise knowledge engine provides unified open capabilities, exporting knowledge bases and other capabilities to the outside world through standard APIs, and controlling the permissions and resource scope of open capabilities through applications, enabling business systems to easily access intelligent question answering, knowledge retrieval, and other capabilities. This article describes how to view the open capabilities of an enterprise knowledge engine, how to manage application calls to OpenAPI, and how to view API usage statistics.

<span id="09dbb536"></span>
# View open capabilities


1. Log in to the Marketing Agent platform.

2. Enter Enterprise Knowledge Engine in the left navigation bar.

3. In the left navigation bar of the Enterprise Knowledge Engine, select **Project Center** \> **Open API** \> **Open Capabilities** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5e6bcf5fadd4ea09864abab4a267114~tplv-goo7wpa0wc-image.image) </span>

4. On the Open Capabilities page, check out the supported OpenAPI information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a64b5f6d9664e4e927e2da004461ab1~tplv-goo7wpa0wc-image.image) </span>


<span id="0c19c694"></span>
# Create an application to call OpenAPI

To call the enterprise knowledge engine OpenAPI, you need to create an application, specify the scope of the API that can be called for the application, and then obtain the application token to call OpenAPI.


1. Log in to the Marketing Agent platform.

2. Enter Enterprise Knowledge Engine in the left navigation bar.

3. In the left navigation bar of the Enterprise Knowledge Engine, select **Project Center** \> **open API** \> **Application Management** .

4. In the upper right corner of the **app management** page, click **New app** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d78274e59de24b259cc129091c1aef8c~tplv-goo7wpa0wc-image.image) </span>

5. On the New App page, complete the following configuration and click **Save** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31390ff984ba43efa01920f8c23eb35b~tplv-goo7wpa0wc-image.image) </span>

   
   |**module** |**configuration item** |**explain** |
   |---|---|---|
   |basic information |app name |A custom name that identifies the current application. |
   ||API available for application |Select the OpenAPI scope of the enterprise knowledge engine that can be invoked by the current application. |
   |Call OpenAPI authentication method |Access to Authorizable Items |Specifies the items that the current app can authorize. |
   ||associated user |Specify the user identity when accessing the API. |
   

6. (Optional) The created app can be viewed in the app list, where you can select the following actions.

   * In the list, you can view the basic information of the application, including the name, associated API, associated user, and other information.

   * In the upper right corner of the page, it is supported to switch the viewing method of the application ( **table** or **card** ).

   * In the **operation** column, click **Edit** to modify the configuration information of the current application.

   * Click **Delete** in the **Actions** column to delete apps that are no longer needed.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Once the application is deleted, it cannot be restored, please operate with caution.      </div>
      

7. In the application list, get the application token.

   Subsequent calls to OpenAPI require passing in the token of the application being used.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6aed604e95b4142bbda4d0afab07e14~tplv-goo7wpa0wc-image.image) </span>


<span id="f660ed08"></span>
# View API usage data


1. Log in to the Marketing Agent platform.

2. Enter Enterprise Knowledge Engine in the left navigation bar.

3. In the left navigation bar of the Enterprise Knowledge Engine, select **Project Center** \> **open API** \> **API usage statistics** .

   In the **API usage statistics** page, the following operations are supported:

   * Select Set **Application** , **Query Time** , and **Statistical Granularity** filters to filter the specified range of data.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c37355a0091d40e39ad4774d6eca4c75~tplv-goo7wpa0wc-image.image) </span>

   * View data indicators and trend graphs such as the cumulative number of applications, the total number of API calls, and the number of successful API calls.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d26dcfa1d77c4c2f8cde2d8549bd28ea~tplv-goo7wpa0wc-image.image) </span>

   * After viewing the specified API metric data, it is supported to download the data locally.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d50ff3d2c5c46248a601d94dfdbfe85~tplv-goo7wpa0wc-image.image) </span>
