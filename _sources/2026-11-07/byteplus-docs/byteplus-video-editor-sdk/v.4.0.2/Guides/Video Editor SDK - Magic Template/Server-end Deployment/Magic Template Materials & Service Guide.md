---
title: "Magic Template Materials & Service Guide"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-magic-template-materials-service-guide-v.4.0.2"
---

<span id="Structure overview of CutSame template files"></span>
## **Structure overview of CutSame template files**

```Ruby
--template+Customer name+Date.zip/ # The name of the delivered file package.

|

|---type.json/ # The information about template categories. This file has a mapping relationship with the id.json file.

|

|---id.json/   # The basic descriptive information about a single template. This file has a mapping relationship with the xxxxx folder.

|  

|---xxxxxx/   # The folder that contains detailed information about a template.

|    |---cover.jpg (png/jepg/tiff...) # The thumbnail picture.

|    | 

|    |---effectresource/  # The folder that contains effect asset files.

|    |    ｜-----xxxx.zip # The information about an effect asset. Users do not need to know the specific file content.

|    |     

|    |---modelresource/  # The folder that contains model asset files.

|    |    ｜-----xxxx.zip #  The information about a model asset. Users do not need to know the specific file content.

|    |  

|    |---xxxxxx.mp4/ # The preview video of the template.

|    |    

|    |---template.zip/# The detailed information about the template, including resource files of audio, videos, and pictures. Users do not need to know the specific file content.

|    |    

|    |---model.json/ #  The model mapping table.   Users do not need to know the specific file content.
```


<span id="Delivery process"></span>
### **Delivery process**

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/87ae42813bf449d69175ffaa09cc81c4~tplv-em5hxbkur4-noop.image?width=2106&height=186) </span>

<span id="Step 1 Query the information about template categories"></span>
#### **Step 1 Query the information about template categories**

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/4f5cfd05038e4682a70977a61dcfea5b~tplv-em5hxbkur4-noop.image?width=602&height=1294) </span>

You need to obtain the names of all template categories based on the mapping relationship between the type.json file and id.json files and then create unique category IDs. Each ID can be used to query all the suggested descriptive information in the corresponding id.json file.

```JSON
{

  "data": {

    "category_list": [

      {

        "id": 0,

        "name": "其他"

      },

      {

        "id": 1,

        "name": "纪念日"

      }

    ]

  }

}
```


<span id="Step 2 Fetch corresponding model preview information of template categories"></span>
#### **Step 2 Fetch corresponding model preview information of template categories**

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/9c4d3bbe7b1545ddad9c5eb1cbe7d050~tplv-em5hxbkur4-noop.image?width=622&height=1342) </span>

Before requesting basic template information on a client, you need to convert the local storage URLs in the id.json files into BOS URLs. The client directly uses these BOS URLs for template display and preview.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/ca1d654d547342cfaacc509236ab7137~tplv-em5hxbkur4-noop.image?width=1558&height=454) </span>

After receiving the category list delivered by the server, the client uses the category IDs to fetch the corresponding id.json files that contain information such as thumbnail pictures, basic information, and preview videos.

<span id="Step 3 Obtain the details of single templates"></span>
#### **Step 3 Obtain the details of single templates**

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/bd0d04beca6949519d708c4a99f3831a~tplv-em5hxbkur4-noop.image?width=568&height=1218) </span>

Convert the template URLs in the id.json files into BOS URLs.

Template details are fetched based on the template URLs in the id.json files and are downloaded as the template.zip data package.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/db839e36855f427aa189f12e2f3c0ed7~tplv-em5hxbkur4-noop.image?width=1772&height=312) </span>

**Notes**

After the local storage URLs are converted into BOS URLs, the client can use the BOS URLs to directly display templates without downloading them.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/a30e13fc6cba4127bb3b99cd97433b19~tplv-em5hxbkur4-noop.image?width=1018&height=904) </span>

<span id="Service deployment"></span>
### **Service deployment**

Interface nameDeployment modeDescriptionRequiredtype.jsonSeparate deploymentSeparately fetches the information about the category tabs to be displayed on a clientYesid.jsonSeparate deploymentBased on the selected category tabs, fetches the corresponding id.json files that contain basic template informationYestemplate.zipIndependent deploymentFetches template details for combining selected assets on a clientYeseffectresource/Independent deployment through .zip packagesFetches effect asset details for combining selected assets on a clientYesmodel.jsonIndependent deploymentFetches the model table information for combining selected assets on a clientNomodelresource/Independent deploymentFetches model resources for combining selected assets on a clientNo

<span id="Integration guide"></span>
## **Integration guide**

<span id="Development protocol"></span>
### **Development protocol**

The following parameters are required in the SDK.


* Parameters about the external entity that integrates the SDK

   * The external entity determines how parameters are put into a request string. The parameters can be processed directly as GET/POST requests or be integrated to requests as the header.

   * HTTPS and HTTP are supported.

   * GET and POST requets are supported.

* // URL instances to be added.


Encoding format: UTF\-8

Call methods: HTTPS and GET

Data format: application/x\-www\-form\-urlencoded

Parameter combination: Required parameters in the SDK+Custom parameters of your app

<span id="Interfaces"></span>
## **Interfaces**

<span id="Formats of common uplink and downlink parameters"></span>
#### **Formats of common** **uplink** **and downlink parameters**

Uplink parameters

Common parameters in the SDK

ParameterTypeDescriptionRequiredcutsamesdkversionstringThe version of the current CutSame SDK. This parameter is used for basic filtering.Yesdevice_platformstringThe operating system into which the SDK is integrated. Valid values are "android" and "ios". This parameter is used for basic filtering.Yesos_versionstringThe version of the operating system.Yes

Common response parameters for business services

ParameterTypeDescriptionRequiredretlongReturns status codes. (Visit the “Status codes” section in this article.)YeserrmsgstringReturns error descriptions.YesdataDepends on the actual data field

Sample response

```JSON
header:

x-log-id // The log ID on the server.



body// json

{

    "ret": "0",

    "errmsg": "success",

    "data": {

        ......   // Business services return response results.

    }

}
```


<span id="Fetch the information about template categories"></span>
#### **Fetch** **the** **information about template categories**

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/1ce77fe015984115bb9dd8b1dd084741~tplv-em5hxbkur4-noop.image?width=544&height=1174) </span>

SDK input parameters

None. Common uplink parameters are acceptable.

<span id="Preview the template list on the feed page"></span>
#### **Preview the template list on the feed page**

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/5002b0e3f6e04055bcc3f7a21fa5d18f~tplv-em5hxbkur4-noop.image?width=464&height=1000) </span>

SDK input parameters

ParameterTypeDescriptionRequiredcategory_idstringA list of templates to be previewed.Yes

```Plain
templateFetcher.loadTemplateList(TEMPLATE_LIST_PATH, category, nextCursor, callback = object :

    TemplateLoadCallback {

    override fun onSuccess(

        templateList: List<TemplateItem>,

        hasMore: Boolean,

        nextCursor: Int

    ) {

         // The template list is obtained.

        this@TemplateNetPageModel.nextCursor = nextCursor

        hasMoreTemplate.postValue(hasMore)

        val oldValue = templateItems.value ?: ArrayList()

        if (refresh) {

            templateItems.postValue(templateList)

        } else {

            templateItems.postValue(oldValue + templateList)

        }

    }



    override fun onError(errorCode: String, errorMsg: String) {

        Log.d(TAG, "loadFeedList: error $errorCode $errorMsg")

        // Failed to obtain the template list.

        templateItems.postValue(emptyList())

    }

})
```


Sample response

```JSON
{

  "data": {

    "has_more": false,

    "template_list": [

      {

        "cover": { // The preview picture.

          "url": "shengrikuaile_6959437645714604039/cover.png", // The URL of the preview picture.

          "height": 1280, // The height of the preview picture.

          "width": 720 // The width of the preview picture.

        },

        // The fragment information required by the template.

        "extra": "{\"align_mode\":\"align_video\",\"fragments\":[{\"video_width\":450,\"video_height\":800,\"duration\":12713,\"is_cartoon\":false,\"material_id\":\"payload_DFF8696D-7222-4B27-94B2-62F764076170\"}]}",

        // The number of fragments required by the template.

        "fragment_count": 1,

        // The template ID.

        "id": "6959437645714604039",

        // The earliest version supported by the template.

        "limit": {

          "sdk_version_min": 170000

        },

        "short_title": "生日快乐?", // The short title of the template.

        "template_url": "shengrikuaile_6959437645714604039/template.zip", // The link for downloading the template.

        "title": "祝你生日快乐?祝你幸福?祝你快乐?", // The description of the template.

        // The URL of the template preview video.

        "video_info": {

          "url": "shengrikuaile_6959437645714604039/shengrikuaile_6959437645714604039.mp4"

        },

        "md5": "c36668687aca2b0aa2c1c95df8fceb4e"  // The MD5 hash value of the .zip template file.

      }

    ]

  }

}
```


<span id="Download the ZIP package of a template"></span>
#### **Download the ZIP package of a template**

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/45fb987862d6446ba017b98e86cc01f3~tplv-em5hxbkur4-noop.image?width=458&height=998) </span>

Click a template on the feed page to enter the details page of the template. On the details page, select and combine assets and then download them as a ZIP package.

Application\-level input parameters

ParameterTypeDescriptionRequiredidstringThe template ID.Yes

Sample response

```Java
template.zip Data in the package.
```


<span id="Model files"></span>
#### **Model files**


* Application\-level input parameter: get


This parameter obtains the corresponding BOS URL in the model mapping table.


* Delivery format


? Model files.

<span id="Obtain effect assets"></span>
#### **Obtain effect assets**

Application\-level input parameters

ParameterTypeDescriptionRequiredpanelstringThe panel that specifies conditions for asset searching.Yesresource_idsarrayAn array of effect asset IDs. Example: {5500, 6000}.Yes

Sample response

```JSON
"data": {

        "effect_list": [

            {

                "id":"",//effect id

                "resource_id": // The resource ID.

                "name":"", // The effect name.

                

                "uri":"",// The MD5 hash value of the effect asset file. This value is the unique identifier of the effect asset file and is used for download verification and local storage.

                "url_list":[

                "cdn 链接1",// The link for downloading the effect asset file.

                "cdn 链接2"

                   ],

             "need_unzip":true,// A boolean value that indicates whether the downloaded package requires unzipping.

             "model_names":"",// The algorithm models that the effect asset file depends on. The value of this parameter is a JSON string in the format of Map<String and List<String>>.

             "requirements":[// The algorithm units that the effect asset file depends on. During download, the algorithm models that the algorithm units depend on are found.

                 "",

                 ""

              ],

              "extras": "Other fields are stored here and passed by the SDK to you for JSON parsing."

            },

            {

              "id": "636071",

              "resource_id": "6791652175668843016",

              "name": "",

              "uri": "a7d2e4892e25fbce01d2c1e8ffa53aac",

              "url_list": [

                    "shengrikuaile_6959437645714604039/effectresource/4fa65e60217a4c719ef9b11c23d94c87.zip"

               ],

              "need_unzip": true,

              "model_names": "",

              "requirements": [],

              "extras": ""

            }    

         ]

    }
```


<span id="Status codes"></span>
## **Status codes**


|**Status codes** |**Description** |**Retun message** |**Solution** |
|---|---|---|---|
|0 |The request is successfully processed. |success | |
|1000 |The parameter is invalid. |invalid parameter | |
|1001 |A common error occurred. |common error | |
|1002 |Failed to obtain the category list. |fail to get category list | |
|1003 |Failed to obtain the template of the category. |fail to get category templarte list | |
|1004 |Failed to obtain the template details. |fail to pack template | |
