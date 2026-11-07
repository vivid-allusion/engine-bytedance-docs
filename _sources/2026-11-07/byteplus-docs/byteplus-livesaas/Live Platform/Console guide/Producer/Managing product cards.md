---
title: "Managing product cards"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream"
---

To increase sales during your live streams, you can use product cards to display items and guide viewers to purchase pages. This guide provides step\-by\-step instructions on how to add, configure, and manage product cards, including integrating with external product libraries like Shopify or your own in\-house system.

<span id="683dc3c5"></span>
## What your viewers see


<Tabs>
<Tab zoneid="a7Oh4dZaIq" title="Viewers on PCs">
<TabTitle>Viewers on PCs</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e1e6dcde99549cb83a39391c6f82077~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="uOnTUJtRAD" title="Viewers on mobile devices">
<TabTitle>Viewers on mobile devices</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11c05feb0c524736b2abf05ee9d50b7b~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


<span id="fbb6b85f"></span>
## Prerequisite

A BytePlus account or an IAM user with the following permissions. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


* Producer \> Edit permission: Used to add and configure the menu for product cards.

* Live control \> Edit permission: Used to configure product cards on the **Live control** page.


<span id="Creating a card"></span>
## Procedure

This procedure describes how to add a menu for product cards, how to add product libraries from your own system or Shopify, and finally, how to add products.

<span id="e2390d98"></span>
### Step 1: Add a menu for product cards


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On the live room list, click to open a live room.

3. On the left navigation pane, click **Producer** \> **Menus**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/001115ee5891477097220e74c0b79d7c~tplv-goo7wpa0wc-image.image) </span>

4. Add a menu for product cards.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8035397ebb184ab2bd1c2ffcbc487b0a~tplv-goo7wpa0wc-image.image) </span>

   1. Click **Edit menu**.

   2. In the **Edit menu** dialog box that appears, click **Add**.

   3. Select **Product cards** from the **Menu type** drop\-down list and enter a name for the menu in the **Menu name** field.

   4. (Optional) Drag to adjust the order of menus.

   5. Click **Confirm**.

      You can add at most 5 menus for product cards in a live room.


<span id="0b085a3d"></span>
### Step 2: Configuring the products menu

Configure the basic information of the menu as needed.


* To allow viewers on different platforms to be redirected to different URLs after they click product cards, enable the direct URL feature. You can configure up to 5 environments, each identified by a User Agent, and set a separate direct URL for each environment on every product card.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This feature is only available on mobile devices.   </div>
   

   1. Turn on the **Direct URL** switch.

   2. In the **User Agent for specific environments** field, add up to 5 environments. For each environment, configure the following:

      * **Environment name**: A name to identify the environment, up to 20 characters. This name labels the corresponding direct URL when you configure product cards.

      * **User Agent**: The User Agent string of the target environment, up to 500 characters.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad83d9bb26854dcf874a5b5db6c53ccf~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Direct URL configurations created before this feature was upgraded are automatically migrated to a single environment named <strong>Env1</strong>.   </div>
   

   3. Enter a direct URL for each environment when configuring the product card information.

      When a viewer clicks a product card on a platform whose User Agent contains the value configured for an environment in the **User Agent for specific environments** field, the viewer will be redirected to the direct URL configured for that environment on the product card. If a viewer clicks the product card on a platform that does not match any configured environment, the viewer will be redirected to the product URL of the product card.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a331c10c50045e1aeb3283cfd195775~tplv-goo7wpa0wc-image.image) </span>

* Select where the floating product card is displayed on the viewing page for PCs. By default, the floating product card is displayed in the upper\-right corner of the player.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a733b20a33c4c64bae6a835d3026843~tplv-goo7wpa0wc-image.image) </span>

* Select how the product details page is displayed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e11f14b095f4dd1a3b3e73c7ca42f79~tplv-goo7wpa0wc-image.image) </span>

   * Display on a new page: Opens the product details page in a new browser tab. Viewers cannot watch the video and view the product details simultaneously.

   * Display on a floating page in the live room: A floating page opens in the live room to display the product details page after viewers click the product card. Viewers can watch the video and view the product details page at the same time. This option takes effect only on mobile devices.


<span id="9ad7b1af"></span>
### (Optional) Step 3: Add product libraries of your own system or Shopify

Add product libraries of your own system or Shopify. Then, you can add products from the product library to the live room.


1. Click  **+Add product library**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39859dfdfe9f4703b1776408365b0d14~tplv-goo7wpa0wc-image.image) </span>

2. In the **Product library** dialog box that appears, add one or more product libraries.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21bf3b3d572c4f8f9be7704468647d82~tplv-goo7wpa0wc-image.image) </span>

   1. Modify the product library name. Make sure the name is unique in the live room.

   2. Select the product library type to add a product library of your own system or Shopify.

   * **In\-house system**: Enter the request URL used to get products from the product library.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">You must develop an API according to the specifications to integrate your system with BytePlus Live before adding a product library of your own system. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream#f4985fe1">Integrating your system with BytePlus Live</a>.      </div>
      

   * **Shopify**: Enter the domain name and public access token.

      * **Domain name**: The domain name of your Shopify store.

         To get the domain name, click Settings on the left navigation pane of your Shopify store to view the domain name under the store name. You can also click Settings \> Domains to view the domain name on the Domains page.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0aa4e1b2fc5349e184af839897ce7db9~tplv-goo7wpa0wc-image.image) </span>

      * **Public access token**: The public access token for the Storefront API of your Shopify store.

         To get the token, navigate to the **Headless sales channel** page in your Shopify store.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fcc45a5e3e8b4813b7218b86c6e766be~tplv-goo7wpa0wc-image.image) </span>

         Click **Manage**, and view the public access token on the Storefront API page.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/084b594a5b10486f8af763fe4f1fddfc~tplv-goo7wpa0wc-image.image) </span>

         Click the Save icon.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f44dec36f7a94a829864eecee2d0441d~tplv-goo7wpa0wc-image.image) </span>


<span id="4815086b"></span>
### Step 4: Add product cards from a product library or manually

You can add at most 500 product cards under a menu for product cards.


* Add product cards from the product library

   1. Click **Add from library**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3bd3471936c44ebb97f1e5dc70c37725~tplv-goo7wpa0wc-image.image) </span>

   2. In the Add from library dialog box that appears, select products from the product libraries added in Step 3 and then click Add. Fuzzy search is supported when you search for specific products.

      To hide specific products in your Shopify product library, you must add a specific product metafield in Shopify and set it to True. For more information, see [Hiding specific products in Shopify product library](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream#bd977a0e).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/05e26384d1e04d0fa88f60d9c7308170~tplv-goo7wpa0wc-image.image) </span>

   3. Click **Add**.

* Add product cards manually

   * Add multiple product cards at a time

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/107dc3bbd8a34b40a23ee8a438c4d9ac~tplv-goo7wpa0wc-image.image) </span>

      1. Click **Import**.

      2. In the **Import** dialog box that appears, click **Download template**.

      3. Edit the template as instructed and then upload the updated template.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can only enter text in the template. Images can only be uploaded on the console.      </div>
      

   * Add one product card at a time

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1403fe0cd09941d7b5354eb61a5eb348~tplv-goo7wpa0wc-image.image) </span>

      Click **Add** and complete the following configurations.

      
      |Field |Description |
      |---|---|
      |**Product name** |The name of your product. |
      |**Product description** |The additional information of your product, such as the capacity of a mobile device. |
      |**Product category** |The category of your product, such as clothing. |
      |**Retail price** |The retail price of your product. |
      |**List price** |The list price of your product. |
      |**Product image** |The product image on the left of the product card. You can upload a JPG or PNG file no more than 2 MB. |
      |**Button image** |The button image in the lower\-right corner of the product card. Viewers will be redirected to the product URL or direct URL after clicking the button.<br><br>You can click **Replace** to replace the default image with a JPG or PNG file no more than 2 MB. This action updates the button image for all existing and future product cards. The recommended resolution is 160×60. |
      |**Product URL** |The URL of the product detail page. |
      |**Direct URL** |The direct URL of the product detail page. When the direct URL feature is enabled in step 2, one **Direct URL** field appears for each configured environment, labeled with the environment name (for example, **Env1**). Enter the direct URL for each environment as needed. |
      


<span id="3705e36a"></span>
### (Optional) Step 5: Manage product cards as needed


* Toggle the List switch to the right of a product card to show or hide it on the viewing page.

* Click **Export** to export the information of all product cards.

* Click **Delete** on the right of a product card to delete the product card.

* Click **Pin** on the right of a product card to pin the product card to the top.

* Drag to adjust the order of product cards.


(Optional) On the left navigation pane, click **Live control**. Under the menu for product cards, you can perform the following operations.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/859e93898702476fabe95e3b8fd99052~tplv-goo7wpa0wc-image.image) </span>


* Click **Pin product** to pin the product card to the top of the menu on both the console and the viewing page, and also display the product card in a floating window on the viewing page.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Make sure the product card has a product image configured.   </div>
   

* Click **Unpin product** to revert the product card to its original position on both the console and the viewing page, and stop displaying the product card in a floating window on the viewing page.

* Click **List** or **Unlist** to list or unlist the product card in real time on the viewing page.

* Click the **Pin** icon to pin the product card to the top of the menu on both the console and the viewing page.

* Drag to adjust the display order of product cards on both the console and the viewing page.

* Search for product cards based on the product title or serial number. You can use fuzzy search on the product title.


<span id="bd977a0e"></span>
### Hiding specific products in Shopify product library

To hide specific products in your Shopify product library, you must add a specific product metafield in Shopify and set it to True.

Complete the following steps to add a product metafield.


1. Click **Settings** on the left navigation pane in your Shopify store.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72c09822780247e6a47feea143046604~tplv-goo7wpa0wc-image.image) </span>

2. Click **Metafields and metaobjects** on the left navigation pane, and then click **Products**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe5942dbdf284be4a9571f7f2eb3f7ea~tplv-goo7wpa0wc-image.image) </span>

3. Click **Add definition** in the upper\-right corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31fb82011ab94018853e139082cd71d6~tplv-goo7wpa0wc-image.image) </span>

4. Select **Other** \> **True or false** as the data type and enter **forbid_show_in_byteplus_live** as the name. Make sure the **Namespace and key** field value starts with `custom.`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2f631d91c9a417db06d83e60ed1c530~tplv-goo7wpa0wc-image.image) </span>


If a product in your Shopify store has the **forbid_show_in_byteplus_live** field set to **True**, the product will not be displayed in the Shopify product library added to BytePlus Live.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e71c99b925654c8e8d4c8ca6671df8c9~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After modifying the field value in Shopify, there might be a latency of up to one minute before you can retrieve the latest product list from the Shopify product library.</div>


<span id="230f07c9"></span>
### Configuring direct URLs for Shopify products

If the direct URL feature is enabled and you have configured multiple direct URLs for each environment of each product (see [Step 2: Configuring the products menu](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream#0b085a3d)), you can set a direct URL for each environment of a Shopify product by adding product metafields in Shopify as shown below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15d642b7ad4e4a6ca0fb9b5bad485a94~tplv-goo7wpa0wc-image.image) </span>

Complete the following steps to add direct URL metafields.


1. Click **Settings** on the left navigation pane in your Shopify store.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72c09822780247e6a47feea143046604~tplv-goo7wpa0wc-image.image) </span>

2. Click **Metafields and metaobjects** on the left navigation pane, and then click **Products**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe5942dbdf284be4a9571f7f2eb3f7ea~tplv-goo7wpa0wc-image.image) </span>

3. Click **Add definition** in the upper\-right corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31fb82011ab94018853e139082cd71d6~tplv-goo7wpa0wc-image.image) </span>

4. Select **Single line text** as the data type and enter `direct_url_1` as the name for the first environment. Make sure the **Namespace and key** field value starts with `custom.`. Repeat this step for `direct_url_2` through `direct_url_5` as needed, one per environment.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a5cc66ff0c31473bbbc6cb8daedd796f~tplv-goo7wpa0wc-image.image) </span>

5. Now you can go to your product page and enter the direct URL for the corresponding environment in the matching metafield for each product.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a4cc31c79274f4b9663b3b1e8a9b9b2~tplv-goo7wpa0wc-image.image) </span>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The <code>direct_url_1</code> through <code>direct_url_5</code> metafields in Shopify must map one\-to\-one and in the same order to the environments configured in the <strong>User Agent for specific environments</strong> field on the BytePlus Live console. For example, <code>direct_url_5</code> corresponds only to the fifth environment (and its Direct URL) configured for the product on the console. A mismatch in order will redirect viewers to the wrong URL.</div>


<span id="40b8e98b"></span>
## Learn more

<span id="f4985fe1"></span>
### Integrating your system with BytePlus Live

Before adding a product library of your own system to a live room of BytePlus Live, you must develop the following API according to the specifications to integrate your system with BytePlus Live.

If you have any questions about integration, contact BytePlus Live technical support.

<span id="32f5a471"></span>
#### Process

If the number of products in your system exceeds the specified upper limit, we recommend that you contact BytePlus Live technical support to add your BytePlus account to the allowlist. Otherwise, no products will be returned when you call this API.

The process differs depending on whether your account is on the allowlist.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66eb68e3023b4fd195f2d92f77cffb5e~tplv-goo7wpa0wc-image.image) </span>


1. You configure the request URL of your in\-house system on the BytePlus Live console. This URL is used to receive API calls.

2. The BytePlus Live console sends the configured request URL to the BytePlus Live server.

3. The BytePlus Live server returns the URL configuration status to the BytePlus Live console.

4. You click **Add from library** on the BytePlus Live console or app integrated with the Live Streaming SDK for iOS or Android.

   If your account is on the allowlist, the BytePlus Live server will not call this API.

   If your account is not on the allowlist, the process is as follows:

   1. When you click **Add from library** for the first time on the BytePlus Live console or app, the BytePlus Live server calls this API to load products.

   2. Your server returns all the products in your system.

   3. The BytePlus Live server returns these products to the BytePlus Live console or app.

5. You enter a keyword in the **Add from library** dialog box on the BytePlus Live console or app integrated with the Live Streaming SDK for iOS or Android.

   If your account is on the allowlist, the process is as follows:

   1. BytePlus Live searches for products whose names contain the keyword on the BytePlus Live server.

   2. BytePlus Live calls this API to search for products whose names contain the keyword in your system.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">To avoid timeout or other API errors, we recommend that the API return no more than 5000 results.      </div>
      

   3. Your server returns the search results to the BytePlus Live server.

   4. The BytePlus Live server returns the search results to the BytePlus Live console or app.

      If your account is not on the allowlist, BytePlus Live searches for products whose names contain the keyword among the products returned in step 4, and then displays the search results on the BytePlus Live console or app.


<span id="c3664ca4"></span>
#### Querying products from your own system

**Description**: BytePlus Live can call this API to get products from your own system and display the products on the BytePlus Live console.

**Method**: GET

**Request parameters**

**Query**


|Parameter Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AccountId |Integer |Yes |`<YOUR_ACCOUNT_ID>` |The account ID of your BytePlus account. You can get the ID by clicking the portrait in the upper\-right corner of the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/). |
|Ts |Integer |Yes |`1650778541` |The system time when the API is called in Unix timestamp format. Unit: seconds. |
|FilterName |String |No |Cola |The keyword entered in the **Add from library** dialog box. By using this parameter, you can only return the products whose names contain the keyword in your system.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required and only takes effect when your BytePlus account is added to the allowlist as described in <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream#32f5a471">Process</a>.</div><br> |
|Sign |String |Yes |`c604c2d2df****************ed2f5` |The signature for verification.<br><br>To get the value of `Sign`, you must complete the following steps:<br><br><br>1. Order all the parameters and their values based on the parameter name in lexicographic order.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Include the parameter <code>FilterName</code> only when your BytePlus account is added to the allowlist as described in <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream#32f5a471">Process</a>.   </div><br>   <br><br>2. Concatenate the string in the format of `ParameterNameParameterValueParameterNameParameterValue`.<br><br>3. Add the value of `accountSecret` at the beginning and the end of the string. To get the value of `accountSecret`, contact BytePlus technical support.<br><br>4. Encrypt the concatenated string in MD5 (32\-bit lowercase).<br><br><br>In this example, assume that the `accountSecret` value is `abc`. The concatenated string would then be `abcAccountId310000009Ts1650778541abc`, with the `Sign` value as `c604c2d2df0e982b9506868a891ed2f5`.<br><br>If your BytePlus account is added to the allowlist as described in [Process](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream#32f5a471), the concatenated string would then be `abcAccountId310000009FilterNameColaTs1650778541abc`, with the `Sign` value as `07be033db13866fcea72503355dd3431`. |


**Response parameters**

**Body**


|Parameter Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Code |Integer |`200` |The HTTP status code. |
|Status |Integer |`0` |The service status.<br><br><br>* `0`: Success.<br><br>* `1`: Error. |
|Message |String |`-` |If the value of `Status` is `1`, a detailed error message will be returned and displayed on the console or app integrated with the Live Streaming SDK for iOS or Android. |
|Products |Array of ExternalProduct |`-` |The product list of your own system. |


**ExternalProduct**


|Parameter Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Title |String |`Dress` |The name of your product, which corresponds to the **Product name** field on the console.<br><br>The value must be between 1 and 3315 characters long. |
|Highlight |String |`$800` |The retail price of your product, which corresponds to the **Retail price** field on the console.<br><br>The value is 1\-260 characters in length. |
|IntroduceImage |String |`www.example.com` |The URL of the product image, which corresponds to the **Product image** field on the console. The image is displayed on the left of the product card. |
|RedirectUrl |String |`www.example.com` |The URL of the product detail page, which corresponds to the **Product URL** field on the console. |
|Strikethrough |String |`$1000` |The list price of your product, which corresponds to the **List price** field on the console.<br><br>The value is 1\-260 characters in length. |
|ExternalProductId |String |`20866` |The external product ID. This ID ensures that once the product is added to the menu for product cards, it cannot be added again to the same menu. |
|Description |String |`XL` |The additional information of your product, such as the clothing size. This parameter corresponds to the **Product description** field on the console.<br><br>The value is 1\-3315 characters in length. |
|Category |String |`Clothing` |The product category, which corresponds to the **Product category** field on the console.<br><br>The value is 1\-20 characters in length. |
|ButtonImage |String |`www.example.com` |The URL of the button image, which corresponds to the **Button image** field on the console. The image is displayed in the lower\-right corner of the product card. Viewers will be redirected to the product URL or direct URL after clicking the button.<br><br>The default button image will be used if this parameter does not have a value. |
|DirectUrl |String |`www.example.com` |The direct URL of the product detail page, which corresponds to the Direct URL field on the console.<br><br>This parameter has a value only when the direct URL feature is enabled and you only configure one environment. For more information, see [Step 2: Configuring the products menu](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream#0b085a3d).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If both <code>DirectUrl</code> and <code>DirectUrl1</code> have values, <code>DirectUrl1</code> takes effect.</div><br> |
|DirectUrl1 |String |`www.example.com` |The direct URL for the first configured environment.<br><br>This parameter is used only when the direct URL feature is enabled for multiple environments. For more information, see [Step 2: Configuring the products menu](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream#0b085a3d).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If both <code>DirectUrl</code> and <code>DirectUrl1</code> have values, <code>DirectUrl1</code> takes effect.</div><br> |
|DirectUrl2 |String |`www.example.com` |The direct URL for the second configured environment.<br><br>This parameter is used only when the direct URL feature is enabled for multiple environments. For more information, see [Step 2: Configuring the products menu](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream#0b085a3d). |
|DirectUrl3 |String |`www.example.com` |The direct URL for the third configured environment.<br><br>This parameter is used only when the direct URL feature is enabled for multiple environments. For more information, see [Step 2: Configuring the products menu](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream#0b085a3d). |
|DirectUrl4 |String |`www.example.com` |The direct URL for the fourth configured environment.<br><br>This parameter is used only when the direct URL feature is enabled for multiple environments. For more information, see [Step 2: Configuring the products menu](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream#0b085a3d). |
|DirectUrl5 |String |`www.example.com` |The direct URL for the fifth configured environment.<br><br>This parameter is used only when the direct URL feature is enabled for multiple environments. For more information, see [Step 2: Configuring the products menu](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream#0b085a3d). |


**Samples**

**Sample request**

```Plain
GET https://test.com/get?AccountId=310000009&Ts=1650778541&Sign=c604c2d2df0e982b9506868a891ed2f5;
```


**Sample response**

```JSON
{
    "Code": 200,
    "Status": 0,
    "Message": "",
    "Products": [
        {
            "Title": "Dress",
            "Highlight": "$800",
            "IntroduceImage": "https://www.example.com",
            "RedirectUrl": "https://www.example.com",
            "ExternalProductId": "20866",
            "Strikethrough": "$1000",
            "Description": "XL",
            "Category": "Clothing",
            "ButtonImage": "www.example.com",
            "DirectUrl1": "https://www.example.com/env1/dress",
            "DirectUrl2": "https://www.example.com/env2/dress",
            "DirectUrl3": "https://www.example.com/env3/dress",
            "DirectUrl4": "https://www.example.com/env4/dress",
            "DirectUrl5": "https://www.example.com/env5/dress"
        },
        {
            "Title": "Basketball",
            "Highlight": "$199.99",
            "IntroduceImage": "https://www.example.com",
            "RedirectUrl": "https://www.example.com",
            "ExternalProductId": "20867",
            "Strikethrough": "$300.00",
            "Description": "Ideal for indoor play",
            "Category": "Sports & Outdoors",
            "ButtonImage": "www.example.com",
            "DirectUrl1": "https://www.example.com/env1/basketball",
            "DirectUrl2": "https://www.example.com/env2/basketball",
            "DirectUrl3": "https://www.example.com/env3/basketball"
        }
    ]
}
```
