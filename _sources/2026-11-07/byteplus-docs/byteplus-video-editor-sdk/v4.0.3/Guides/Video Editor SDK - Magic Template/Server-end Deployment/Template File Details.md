---
title: "Template File Details"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-template-file-details"
---

<span id="Template files"></span>
# **Template files**

<span id="Content of delivered template files"></span>
## **Content of delivered template files**

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/67966c263277488abc6e74fa29e58885~tplv-em5hxbkur4-noop.image) </span>

This section describes the types of data in each delivered template file.

<span id="type.json"></span>
### **type.json**

This file contains a list of categories to be displayed on the feed homepage on a client.

```JSON
{
   data : {
     category_list : [
      {
         id : 0, // The category ID.
         name :  其他  // The category name.
      },
      {
         id : 1, 
         name :  纪念日 
      }
    ]
  }
}
```


<span id="1.json, 2.json"></span>
### **1.json, 2.json**

After a file of this type is obtained on a client, the category ID is used to obtain the corresponding template list. The server delivers the corresponding data structure based on the category ID. The following code shows a sample data structure.

```JSON
{
   data : {
     template_list : [
      {
         author : {},// The author. This parameter isn’t required in the demo. If no author is specified, set this parameter to {}.
         counter_data : {},// The creation time. This parameter isn’t required in the demo. If no creation time is specified, set this parameter to {}.
         cover : {
           url :  jilu2020_6959540106912317448/cover.png , // The URL of the preview picture. This parameter is required in the demo.
           height : 1280, // The height of the preview picture. This parameter is required in the demo.
           width : 720 // The width of the preview picture. This parameter is required in the demo.
        },
        // The slot information about the template, which is required for accessing the photo album. This parameter is required in the demo.
         extra :  {\ fragments\ :[{\ material_id\ :\ payload_BB59A070-7F7C-40E2-9D27-E83490A5C01A\ ,\ video_width\ :828,\ duration\ :1608,\ is_cartoon\ :false,\ video_height\ :828},{\ material_id\ :\ payload_583C0B6C-50DF-4F80-B4F2-9CE8692686F7\ ,\ video_width\ :600,\ video_height\ :600,\ duration\ :2587,\ is_cartoon\ :false},{\ video_height\ :2160,\ is_cartoon\ :false,\ video_width\ :2160,\ duration\ :356,\ material_id\ :\ payload_FFDFBA5A-E3FE-4018-AC70-7D9D1CA78B4D\ },{\ material_id\ :\ payload_79CE4B1C-F195-4F64-A29F-8F1AD10BEC77\ ,\ duration\ :357,\ video_height\ :991,\ video_width\ :991,\ is_cartoon\ :false},{\ video_height\ :1080,\ video_width\ :1080,\ material_id\ :\ payload_EEAAECCA-3419-440A-A2EF-B69315D64325\ ,\ is_cartoon\ :false,\ duration\ :360},{\ is_cartoon\ :false,\ duration\ :357,\ video_width\ :1080,\ video_height\ :1080,\ material_id\ :\ payload_DE568422-2F95-4E99-9186-79C2883849AD\ },{\ video_height\ :2160,\ is_cartoon\ :false,\ material_id\ :\ payload_81BAB873-B4E2-48DC-870F-BDFBB6A89988\ ,\ video_width\ :2160,\ duration\ :353},{\ video_width\ :2160,\ is_cartoon\ :false,\ duration\ :355,\ video_height\ :2160,\ material_id\ :\ payload_9D091B57-CF35-4B38-A7F6-16ABD109F9C5\ },{\ material_id\ :\ payload_E12D2DD4-6001-4D2B-A150-BA4272C7FEF8\ ,\ video_width\ :1036,\ duration\ :360,\ is_cartoon\ :false,\ video_height\ :1036},{\ duration\ :357,\ video_height\ :1901,\ material_id\ :\ payload_4C20F0B2-8D1E-44F9-A780-F8B7304C3BA3\ ,\ is_cartoon\ :false,\ video_width\ :1901},{\ duration\ :353,\ video_height\ :1431,\ is_cartoon\ :false,\ video_width\ :1431,\ material_id\ :\ payload_C8BB1E0C-F139-4B8A-A1F0-75C5A3F36CA7\ },{\ video_width\ :1884,\ video_height\ :1884,\ material_id\ :\ payload_DF03B9A9-D8E3-4D24-937C-240ACCB7B9A3\ ,\ duration\ :364,\ is_cartoon\ :false},{\ duration\ :353,\ material_id\ :\ payload_BF6DEBC2-2673-42F7-BE07-D9E2C1F8CA74\ ,\ is_cartoon\ :false,\ video_width\ :2160,\ video_height\ :2160},{\ video_width\ :2160,\ video_height\ :2160,\ is_cartoon\ :false,\ material_id\ :\ payload_654D4CC5-CCB3-48C0-830B-428D3FBF4889\ ,\ duration\ :364},{\ duration\ :353,\ video_height\ :2160,\ material_id\ :\ payload_70529997-B3F9-4AD4-AB92-81838941F88F\ ,\ is_cartoon\ :false,\ video_width\ :2160},{\ duration\ :350,\ material_id\ :\ payload_2CBFC8BB-D934-4F37-9F02-AFC75C30EEBA\ ,\ video_height\ :1982,\ video_width\ :1982,\ is_cartoon\ :false},{\ video_height\ :1242,\ is_cartoon\ :false,\ video_width\ :1242,\ duration\ :357,\ material_id\ :\ payload_58024C07-C096-476A-857D-3AC18106AF62\ },{\ video_width\ :1860,\ is_cartoon\ :false,\ duration\ :353,\ video_height\ :1860,\ material_id\ :\ payload_245B3F63-1A83-4AEF-BFE5-941F504563D2\ },{\ material_id\ :\ payload_52F1BBB8-7D9E-4783-804D-C772C106D839\ ,\ video_width\ :440,\ duration\ :370,\ video_height\ :440,\ is_cartoon\ :false},{\ duration\ :375,\ video_width\ :2160,\ is_cartoon\ :false,\ video_height\ :2160,\ material_id\ :\ payload_0D8C0AE7-41B3-45F8-99EA-003B0EB8124C\ },{\ material_id\ :\ payload_9791AFC0-2558-48E9-A2D0-D5C0EE8A14D2\ ,\ is_cartoon\ :false,\ video_width\ :2024,\ video_height\ :2024,\ duration\ :373},{\ material_id\ :\ payload_A946A389-03BC-490B-A6AB-7A547D2B52D4\ ,\ video_width\ :2160,\ duration\ :371,\ video_height\ :2160,\ is_cartoon\ :false},{\ video_width\ :2160,\ duration\ :374,\ video_height\ :2160,\ is_cartoon\ :false,\ material_id\ :\ payload_E1AD041D-0BF8-4A0B-B198-8F07CDFC827E\ },{\ video_width\ :1549,\ video_height\ :1544,\ material_id\ :\ payload_3740A1E8-6523-4BF2-B157-582DA9D515DB\ ,\ duration\ :334,\ is_cartoon\ :false},{\ video_width\ :1080,\ is_cartoon\ :false,\ duration\ :372,\ material_id\ :\ payload_D45868C8-38DA-4BD8-A414-5B49D49D1294\ ,\ video_height\ :1080},{\ is_cartoon\ :false,\ duration\ :372,\ video_height\ :1085,\ video_width\ :1085,\ material_id\ :\ payload_26B2F56C-7D05-4945-986E-F34FC13F56D6\ },{\ video_height\ :2100,\ is_cartoon\ :false,\ duration\ :375,\ video_width\ :2100,\ material_id\ :\ payload_22A9BE8D-9D5F-43C4-955D-748793980FFF\ },{\ material_id\ :\ payload_07A7FC05-0F96-4A12-AEBE-C3DA9A86B9EE\ ,\ is_cartoon\ :false,\ video_width\ :1872,\ duration\ :374,\ video_height\ :1872},{\ material_id\ :\ payload_458A9FA8-3D3C-4F8F-9145-4EAF018067EE\ ,\ is_cartoon\ :false,\ video_width\ :1536,\ duration\ :376,\ video_height\ :1536},{\ material_id\ :\ payload_D4828A0F-8180-44AE-8FC6-2B808E8E1AD8\ ,\ duration\ :375,\ video_height\ :2160,\ is_cartoon\ :false,\ video_width\ :2160},{\ video_height\ :1631,\ material_id\ :\ payload_459D9E5E-CC13-4FD4-AA32-B1580416B861\ ,\ is_cartoon\ :false,\ duration\ :376,\ video_width\ :1631},{\ video_width\ :2160,\ material_id\ :\ payload_12F2D424-0945-4206-BC4B-CACE96866F89\ ,\ is_cartoon\ :false,\ video_height\ :2160,\ duration\ :368},{\ video_width\ :1710,\ video_height\ :1710,\ duration\ :375,\ is_cartoon\ :false,\ material_id\ :\ payload_330295F9-1E9B-4785-B012-39CB4A8BAD60\ },{\ video_height\ :2160,\ is_cartoon\ :false,\ video_width\ :2160,\ material_id\ :\ payload_B8FC91BB-D0D2-400C-8513-21F9019900EC\ ,\ duration\ :366},{\ duration\ :260,\ video_width\ :2160,\ material_id\ :\ payload_E919326B-2028-4D99-AA3F-7532E719621B\ ,\ is_cartoon\ :false,\ video_height\ :2160}],\ align_mode\ :\ align_canvas\ } ,
         fragment_count : 35,// The number of slots in the template. This parameter is required in the demo.
         id :  6959540106912317448 ,// The template ID. This parameter is required in the demo.
         limit : {
           // The earliest SDK version supported by the template. This parameter isn’t required in the demo.
           sdk_version_min : 190000
        },
        // The URL of the original template video. This parameter isn't required in the demo.
         origin_video_info : {
           url :  jilu2020_6959540106912317448/jilu2020_6959540106912317448.mp4 
        },
         short_title :  {template short title} ,// The short title of the template. This parameter is required in the demo.
         status : 1,// The data status of the template. This parameter isn't required in the demo.
         template_tags :  {template tags} ,// The tag of the template. This parameter isn't required in the demo.
         template_url :  jilu2020_6959540106912317448/template.zip ,// The link for downloading the ZIP template data package.
         title :  {template title} ,// The template title. This parameter is required in the demo.
        // The URL of the template video. This parameter is required in the demo.
         video_info : {
           url :  jilu2020_6959540106912317448/jilu2020_6959540106912317448.mp4 
        },
        // The MD5 hash value of the ZIP template data package. This parameter is required in the demo.
         md5 :  fb3bee51c89815fcec857ec0d82f47cb 
      }
    ]
  }
}
```


<span id="effect"></span>
### **effect**

During the effect playback of a template, the SDK parses the template protocol file, obtains the information about the corresponding effect assets, and then downloads the effect assets. The effect file contains all effect description files that are required by the delivered template.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/f9185d421a2f4f3ba9ef1d47e126ceca~tplv-em5hxbkur4-noop.image) </span>

<span id="Details of a description file"></span>
#### **Details of a description file**

6874487735059485198.json

```JSON
{
   id :  923591 , // The file ID, which is used only for internal indexing and does not have a specific meaning.
   resource_id :  6874487735059485198 ,// The ID of the effect asset.
   name :  小陀螺 II,// The name of the effect asset.
   uri :  23c89003824b72f78e57e4b7b3225ef6 ,// The MD5 hash value of the effect file 923591.zip.
   url_list : [
      // The link for downloading the effect file. This link indicates the path of the effect file in the data package. You can find the effect file based on this path and deploy the effect file to the server.
     xiyixinbing_6959439775582093348/effectresource/923591.zip 
  ],
   need_unzip : true,// This parameter indicates whether the downloaded file requires unzipping.
   model_names :   ,// The name of the algorithm models that the file depends on.
   requirements : [],// The link for downloading the algorithm models that the file depends on.
   extras :   // Custom business information.
}
```


This data is delivered when the client fetches a list of effect assets during the effect playback of a template.

For example, the template A contains 3 video effects. The IDs of the effect assets are 6865579178599649806, 6874487656969933325, and 6874487735059485198. When a client fetches the effect assets, the interaction process between the client and server is as follows:

Parameters:


|**Parameter** |**Type** |**Description** |**Required** |
|---|---|---|---|
|panel effect2 fi |string |The panel that specifies conditions for asset searching. |Yes |
|resource_ids 6739752823140913675 |array |An array of effect asset IDs, for example, {6874487735059485198, 6874487735059485198}. |Yes |


Request:

```Plain
http://xxxxx/api/effectlist?panel=video&resource_ids=6874487735059485198,6874487656969933325,6865579178599649806
```


Response: After receiving the request, the server delivers a list of description data about the requested effect assets.

```JSON
{
     ret :0,
     errmsg : success ,
     data :{
         effect_list :[
            {
                 id : 923591 ,
                 resource_id : 6874487735059485198 ,
                 name : \u5c0f\u9640\u87ba II ,
                 uri : 23c89003824b72f78e57e4b7b3225ef6 ,
                 url_list :[
                     http://xxx/xiyixinbing_6959439775582093348/effectresource/923591.zip 
                ],
                 need_unzip :true,
                 model_names :  ,
                 requirements :[

                ],
                 extras :  
            },
            {
                 id : 923592 ,
                 resource_id : 6874487656969933325 ,
                 name : \u5c0f\u9640\u87ba ,
                 uri : 0f9b2169d02f8376f70e40b335789de0 ,
                 url_list :[
                     http://xxx/iyixinbing_6959439775582093348/effectresource/923592.zip 
                ],
                 need_unzip :true,
                 model_names :  ,
                 requirements :[

                ],
                 extras :  
            },
            {
                 id : 898332 ,
                 resource_id : 6865579178599649806 ,
                 name : \u56db\u683c\u7ffb\u8f6c II ,
                 uri : 98e51279afefac659426263e896eb8a4 ,
                 url_list :[
                     http://xxx/shengrijilukadianmoban_7002470461230219278/effectresource/898332.zip 
                ],
                 need_unzip :true,
                 model_names :  ,
                 requirements :[

                ],
                 extras :  
            }
        ]
    }
}
```


After receiving the data list, the SDK on the client downloads the effect assets.

<span id="Template-related data"></span>
### **Template\-related data**

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/b1b92eb8d7f245258045e4a12934954c~tplv-em5hxbkur4-noop.image) </span>

<span id="Data interaction between the CutSame demo on a client and the server"></span>
# **Data interaction between the CutSame demo on a client and the server**

The current demo has 3 interfaces for interaction with the server.


* **category_list**


<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/1336012ed9844d938545099b6cef167f~tplv-em5hxbkur4-noop.image) </span>

The return results of this interface are as follows. For more information, visit the type.json file in delivered template files.

```JSON
{
     ret :0,
     errmsg : success ,
     data :{
         category_list :[
            {
                 id :0,
                 name : 其他 
            },
            {
                 id :1,
                 name : 纪念日 
            }
        ]
    }
}
```


**template_list**

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/f6642433b7e04a1ca46d8ecac463ca33~tplv-em5hxbkur4-noop.image) </span>

The return results of this interface are as follows. For more information, visit the 0.json and 1.json files in delivered template files.

```JSON
{
     ret :0,
     errmsg : success ,
     data :{
         has_more :false,
         next_cursor :101,
         template_list :[
            {
                 author :Object{...},
                 counter_data :Object{...},
                 cover :Object{...},
                 extra : {\ fragments\ :[{\ material_id\ :\ payload_BB59A070-7F7C-40E2-9D27-E83490A5C01A\ ,\ video_width\ :828,\ duration\ :1608,\ is_cartoon\ :false,\ video_height\ :828},{\ material_id\ :\ payload_583C0B6C-50DF-4F80-B4F2-9CE8692686F7\ ,\ video_width\ :600,\ video_height\ :600,\ duration\ :2587,\ is_cartoon\ :false},{\ video_height\ :2160,\ is_cartoon\ :false,\ video_width\ :2160,\ duration\ :356,\ material_id\ :\ payload_FFDFBA5A-E3FE-4018-AC70-7D9D1CA78B4D\ },{\ material_id\ :\ payload_79CE4B1C-F195-4F64-A29F-8F1AD10BEC77\ ,\ duration\ :357,\ video_height\ :991,\ video_width\ :991,\ is_cartoon\ :false},{\ video_height\ :1080,\ video_width\ :1080,\ material_id\ :\ payload_EEAAECCA-3419-440A-A2EF-B69315D64325\ ,\ is_cartoon\ :false,\ duration\ :360},{\ is_cartoon\ :false,\ duration\ :357,\ video_width\ :1080,\ video_height\ :1080,\ material_id\ :\ payload_DE568422-2F95-4E99-9186-79C2883849AD\ },{\ video_height\ :2160,\ is_cartoon\ :false,\ material_id\ :\ payload_81BAB873-B4E2-48DC-870F-BDFBB6A89988\ ,\ video_width\ :2160,\ duration\ :353},{\ video_width\ :2160,\ is_cartoon\ :false,\ duration\ :355,\ video_height\ :2160,\ material_id\ :\ payload_9D091B57-CF35-4B38-A7F6-16ABD109F9C5\ },{\ material_id\ :\ payload_E12D2DD4-6001-4D2B-A150-BA4272C7FEF8\ ,\ video_width\ :1036,\ duration\ :360,\ is_cartoon\ :false,\ video_height\ :1036},{\ duration\ :357,\ video_height\ :1901,\ material_id\ :\ payload_4C20F0B2-8D1E-44F9-A780-F8B7304C3BA3\ ,\ is_cartoon\ :false,\ video_width\ :1901},{\ duration\ :353,\ video_height\ :1431,\ is_cartoon\ :false,\ video_width\ :1431,\ material_id\ :\ payload_C8BB1E0C-F139-4B8A-A1F0-75C5A3F36CA7\ },{\ video_width\ :1884,\ video_height\ :1884,\ material_id\ :\ payload_DF03B9A9-D8E3-4D24-937C-240ACCB7B9A3\ ,\ duration\ :364,\ is_cartoon\ :false},{\ duration\ :353,\ material_id\ :\ payload_BF6DEBC2-2673-42F7-BE07-D9E2C1F8CA74\ ,\ is_cartoon\ :false,\ video_width\ :2160,\ video_height\ :2160},{\ video_width\ :2160,\ video_height\ :2160,\ is_cartoon\ :false,\ material_id\ :\ payload_654D4CC5-CCB3-48C0-830B-428D3FBF4889\ ,\ duration\ :364},{\ duration\ :353,\ video_height\ :2160,\ material_id\ :\ payload_70529997-B3F9-4AD4-AB92-81838941F88F\ ,\ is_cartoon\ :false,\ video_width\ :2160},{\ duration\ :350,\ material_id\ :\ payload_2CBFC8BB-D934-4F37-9F02-AFC75C30EEBA\ ,\ video_height\ :1982,\ video_width\ :1982,\ is_cartoon\ :false},{\ video_height\ :1242,\ is_cartoon\ :false,\ video_width\ :1242,\ duration\ :357,\ material_id\ :\ payload_58024C07-C096-476A-857D-3AC18106AF62\ },{\ video_width\ :1860,\ is_cartoon\ :false,\ duration\ :353,\ video_height\ :1860,\ material_id\ :\ payload_245B3F63-1A83-4AEF-BFE5-941F504563D2\ },{\ material_id\ :\ payload_52F1BBB8-7D9E-4783-804D-C772C106D839\ ,\ video_width\ :440,\ duration\ :370,\ video_height\ :440,\ is_cartoon\ :false},{\ duration\ :375,\ video_width\ :2160,\ is_cartoon\ :false,\ video_height\ :2160,\ material_id\ :\ payload_0D8C0AE7-41B3-45F8-99EA-003B0EB8124C\ },{\ material_id\ :\ payload_9791AFC0-2558-48E9-A2D0-D5C0EE8A14D2\ ,\ is_cartoon\ :false,\ video_width\ :2024,\ video_height\ :2024,\ duration\ :373},{\ material_id\ :\ payload_A946A389-03BC-490B-A6AB-7A547D2B52D4\ ,\ video_width\ :2160,\ duration\ :371,\ video_height\ :2160,\ is_cartoon\ :false},{\ video_width\ :2160,\ duration\ :374,\ video_height\ :2160,\ is_cartoon\ :false,\ material_id\ :\ payload_E1AD041D-0BF8-4A0B-B198-8F07CDFC827E\ },{\ video_width\ :1549,\ video_height\ :1544,\ material_id\ :\ payload_3740A1E8-6523-4BF2-B157-582DA9D515DB\ ,\ duration\ :334,\ is_cartoon\ :false},{\ video_width\ :1080,\ is_cartoon\ :false,\ duration\ :372,\ material_id\ :\ payload_D45868C8-38DA-4BD8-A414-5B49D49D1294\ ,\ video_height\ :1080},{\ is_cartoon\ :false,\ duration\ :372,\ video_height\ :1085,\ video_width\ :1085,\ material_id\ :\ payload_26B2F56C-7D05-4945-986E-F34FC13F56D6\ },{\ video_height\ :2100,\ is_cartoon\ :false,\ duration\ :375,\ video_width\ :2100,\ material_id\ :\ payload_22A9BE8D-9D5F-43C4-955D-748793980FFF\ },{\ material_id\ :\ payload_07A7FC05-0F96-4A12-AEBE-C3DA9A86B9EE\ ,\ is_cartoon\ :false,\ video_width\ :1872,\ duration\ :374,\ video_height\ :1872},{\ material_id\ :\ payload_458A9FA8-3D3C-4F8F-9145-4EAF018067EE\ ,\ is_cartoon\ :false,\ video_width\ :1536,\ duration\ :376,\ video_height\ :1536},{\ material_id\ :\ payload_D4828A0F-8180-44AE-8FC6-2B808E8E1AD8\ ,\ duration\ :375,\ video_height\ :2160,\ is_cartoon\ :false,\ video_width\ :2160},{\ video_height\ :1631,\ material_id\ :\ payload_459D9E5E-CC13-4FD4-AA32-B1580416B861\ ,\ is_cartoon\ :false,\ duration\ :376,\ video_width\ :1631},{\ video_width\ :2160,\ material_id\ :\ payload_12F2D424-0945-4206-BC4B-CACE96866F89\ ,\ is_cartoon\ :false,\ video_height\ :2160,\ duration\ :368},{\ video_width\ :1710,\ video_height\ :1710,\ duration\ :375,\ is_cartoon\ :false,\ material_id\ :\ payload_330295F9-1E9B-4785-B012-39CB4A8BAD60\ },{\ video_height\ :2160,\ is_cartoon\ :false,\ video_width\ :2160,\ material_id\ :\ payload_B8FC91BB-D0D2-400C-8513-21F9019900EC\ ,\ duration\ :366},{\ duration\ :260,\ video_width\ :2160,\ material_id\ :\ payload_E919326B-2028-4D99-AA3F-7532E719621B\ ,\ is_cartoon\ :false,\ video_height\ :2160}],\ align_mode\ :\ align_canvas\ } ,
                 fragment_count :35,
                 id : 6959540106912317448 ,
                 limit :Object{...},
                 origin_video_info :Object{...},
                 short_title : \u8bb0\u5f552020 ,
                 status :1,
                 template_tags : \u5176\u4ed6 ,
                 template_url : http://xxx/jilu2020_6959540106912317448/template.zip ,
                 title : \u8bb0\u5f552020\u5361\u70b9\u6a21\u677f ,
                 video_info :{
                     url : http://xxx/jilu2020_6959540106912317448/jilu2020_6959540106912317448.mp4 
                },
                 md5 : fb3bee51c89815fcec857ec0d82f47cb 
            }
        ]
    }
}
```


<span id="effect_list"></span>
## **effect_list**

This interface is called to obtain a list of effect assets during the effect playback of a template. For more information of the return results of this interface, visit the .json effect files in delivered template files.

```JSON
{
     ret :0,
     errmsg : success ,
     data :{
         effect_list :[
            {
                 id : 923591 ,
                 resource_id : 6874487735059485198 ,
                 name : \u5c0f\u9640\u87ba II ,
                 uri : 23c89003824b72f78e57e4b7b3225ef6 ,
                 url_list :[
                     http://xxx/xiyixinbing_6959439775582093348/effectresource/923591.zip 
                ],
                 need_unzip :true,
                 model_names :  ,
                 requirements :[

                ],
                 extras :  
            },
            {
                 id : 923592 ,
                 resource_id : 6874487656969933325 ,
                 name : \u5c0f\u9640\u87ba ,
                 uri : 0f9b2169d02f8376f70e40b335789de0 ,
                 url_list :[
                     http://xxx/iyixinbing_6959439775582093348/effectresource/923592.zip 
                ],
                 need_unzip :true,
                 model_names :  ,
                 requirements :[

                ],
                 extras :  
            },
            {
                 id : 898332 ,
                 resource_id : 6865579178599649806 ,
                 name : \u56db\u683c\u7ffb\u8f6c II ,
                 uri : 98e51279afefac659426263e896eb8a4 ,
                 url_list :[
                     http://xxx/shengrijilukadianmoban_7002470461230219278/effectresource/898332.zip 
                ],
                 need_unzip :true,
                 model_names :  ,
                 requirements :[

                ],
                 extras :  
            }
        ]
    }
}
```


To learn more about specific interface protocols and deployment descriptions, visit [CutSame template assets and service documents](https://bytedance.feishu.cn/docs/doccnDPbfcn5JQPPwmdwqJ9PaWc) .

<span id="Notes"></span>
# **Notes**

<span id="category_list"></span>
## **category_list**

This interface is used mainly for UI display. You can customize data delivery as needed. Currently, the UI display of the demo depends on the preceding data structures. If you need to use the UI display of the demo but the server doesn’t deliver data based on the preceding data structures, you must manually adjust the data structure.

<span id="template_list"></span>
## **template_list**

This interface is used mainly for UI display. You can customize data delivery as needed. Currently, the UI display of the demo depends on the preceding data structures. If you need to use the UI display of the demo but the server doesn’t deliver data based on the preceding data structures, you must manually adjust the data structure.

<span id="extra field of the template_list interface"></span>
## **extra field of the template_list interface**

This field indicates the slot information about the template. This field must be parsed before you can access the photo album and select assets.

<span id="effect_list"></span>
## **effect_list**


* This interface is called within the SDK. This interface requires two request parameters (panel and resource_ids) and uses fixed data structures for parsing. Therefore, the structure of data returned by the server must be consistent with the preceding data structures.
