---
title: "GetItem - Get Item Details"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/GetItem_-_Get_Item_Details"
---

***Viking AI Search*** * is an enterprise\-grade AI search product powered by generative AI. It combines the multimodal semantic understanding of large models with ByteDance's years of best practices in information retrieval. This provides customers with an out\-of\-the\-box platform to easily build and integrate end\-to\-end multimodal search and recommendation capabilities for both text and images.* 


---



**Get the details of an item by specifying the dataset ID and item ID. Currently supported:** 


* Item datasets: Get the field details for each item.

* Document datasets: Get the file information for each document.


<span id="2aeccfd9"></span>
## Notes


* **Limitations:** 

   * The body of a single request cannot exceed 10 MB due to HTTP body size limitations.


<span id="40f127ae"></span>
## Request Details


* Request method: POST

* Request URL:



|**Service** |**Region** |**URL** |
|---|---|---|
|BytePlus |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.bytepluses.com/api/v1/dataset/{dataset_id}/get_item` |
|Volcano Engine |North China (Beijing) |`https://aisearch.cn-beijing.volces.com/api/v1/dataset/{dataset_id}/get_item` |
|Volcano Engine |Asia\-Pacific (Johor) |`https://aisearch.cn-beijing.volces.com/api/v1/dataset/{dataset_id}/get_item` |


 *{dataset_id}: The unique ID assigned to a dataset after it is created in the console. You can view and copy it from the dataset details page. Supports both product and document dataset IDs.* 


<columns>
<columnsItem zoneid="YxBJlFqWFd">

<div style="text-align: center">
</div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/fc5b781de31d4097b777a21a52f76964) </span>

<div style="text-align: center">
Item Dataset</div>


</columnsItem>
<columnsItem zoneid="gUrsCfKawi">

&nbsp;

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/7adbdb0580fa4b95b6ac3f292f677e9c) </span>

<div style="text-align: center">
Document dataset</div>


</columnsItem>
</columns>


&nbsp;

<span id="eea41805"></span>
## Request parameters

<span id="fab48576"></span>
### Request body


|**Parameter** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|`_id` |String |Yes |"test_id" |Primary key of the data entry<br><br><br>* Image\-text dataset: The field corresponding to the specified item ID attribute<br><br>* Video dataset: The ID corresponding to the `content_id` field |
|`output_fields`<br><br> |Array<String\> |No |["title", "price", "category"]<br><br> |Specify the fields of item data to return from the target dataset. If you specify return fields, only those fields will appear in the `raw_data` field of the response.<br><br>> If the dataset contains nested objects (Object), only top\-level field names are supported.<br><br>> Fields that do not exist or are nested within an Object will be ignored. |


<span id="4a9ffc03"></span>
### Response body: Product dataset (image\-text)


|**Parameter name** |**Parameter type** |**Example** |**Description** |
|---|---|---|---|
|`item` |`DataItem` object | |A list of queried data items. Each data item contains data fields corresponding to the item ID and processing details. |


`DataItem`


|**Parameter name** |**Parameter type** |**Example** |**Description** |
|---|---|---|---|
|`_id` |String |"test_itemid" |The unique data ID within the dataset. It is returned for all dataset types (items, documents). |
|`raw_data` |Object | |The originally uploaded field content for item dataset (image and text) data. A complete JSON object is returned in string format.<br><br>If output_fields is specified in the request, only the specified fields are returned. |
|`check_status` |String |"normal" |The status of the data quality check, which includes the following:<br><br><br>1. normal: No data quality issues.<br><br>2. warning: The data contains fields with types that do not match their definitions, which may affect storage and retrieval performance.<br><br>3. error: The data quality check failed, blocking subsequent processing. Possible situations include: |
|`process_status` |String |"success" |Data processing status: success, processing, failed |
|`data_status_details` |Array<`DataStatusDetail`\> | |A list of data quality check and processing statuses, including status descriptions for the initial data import and the most recent update. |
|`create_time` |String |"2025\-03\-12T15:01:07+08:00" |Creation time in RFC3339 format. |
|`update_time` |String |"2025\-03\-12T15:01:07+08:00" |Update time in RFC3339 format |


`DataStatusDetail` object


|**Parameter name** |**Parameter type** |**Example** |**Description** |
|---|---|---|---|
|`update_type` |String |"FIRST_UPDATE_SUCCESS" |Update type:<br><br><br>* "FIRST_UPDATE_SUCCESS": The first import and processing were successful<br><br>* "LATEST_UPDATE_SUCCESS": The latest update and processing were successful<br><br>* "UPDATE_FAILED": An exception occurred during the last data update |
|`timestamp` |String |"2025\-03\-12T15:01:07+08:00" |Update time in RFC3339 format |
|`warning_info` |Map[String]String | |Data quality exception information, in the format "Status Code": "Exception Details"<br><br>Data quality exceptions do not affect data processing and indexing, but we recommend fixing them to improve search performance. |
|`error_info` |Map[String]String | |Data validation and processing exception information, formatted as "status code": "exception details"<br><br>Validation and processing exceptions block data at the validation stage, preventing it from being indexed. We recommend reviewing the exception information and re\-uploading the corrected data. |


<span id="3b49e6a5"></span>
### Response body: Product dataset (video)


|**Parameter Name** |**Parameter Type** |**Example** |**Description** |
|---|---|---|---|
|`item` |`DataItem` object | |A list of queried data entries, where each entry contains the data fields and processing details for the corresponding item ID. |


`DataItem`


|**Parameter name** |**Parameter type** |**Example** |**Description** |
|---|---|---|---|
|`_id` |String |"test_itemid" |The data ID, which is unique within the dataset and is returned for all dataset types (such as items and documents). |
|`raw_data` |String | |The original field content of the video dataset. |
|`meta` |`DataItemMeta` | |The processing status and content analysis details of the video. A complete JSON object returned as a string.<br><br>If output_fields is specified in the request, only the specified fields are returned. |
|`process_status` |String |"success" |Data processing status: success, processing, failed |
|`check_status` |String |"normal" |Data check status: normal, warning, error |
|`data_status_details` |Array<`DataStatusDetail`\> | |A list of data quality check and processing statuses, including status descriptions for the initial data import and recent updates. |
|`create_time` |String |"2025\-03\-12T15:01:07+08:00" |Creation time, in RFC3339 format |
|`update_time` |String |"2025\-03\-12T15:01:07+08:00" |Update time, in RFC3339 format |


`DataItemMeta`


|**Parameter name** |**Parameter type** |**Example** |**Description** |
|---|---|---|---|
|`video_meta` |VideoMeta | |Processing and status information for video data |


`VideoMeta`


|**Parameter name** |**Parameter type** |**Example** |**Description** |
|---|---|---|---|
|`content_type` |String |video |Content type: video, collection |
|`video_urls` |Array<String\> |["https://domain.com/file_path.format"] |A list of video URLs |
|`parent_content_id` |String | |The parent content ID. This is returned when the content_type is video and indicates the collection the video belongs to. |
|`sequence_index` |Int | |The sequence number of the video in its collection, returned when the content_type is video. |
|`video_content` |`VideoContent` | |Content from video processing and understanding, returned when the content_type is video. |
|`duration` |Int | |The video duration in seconds, rounded up to the nearest whole second, returned when the content_type is video. |
|`collection_content` |`CollectionContent` | |Processed and understood content of the video series, returned when content_type is collection |


`VideoContent` object


|**Parameter name** |**Parameter type** |**Example** |**Description** |
|---|---|---|---|
|`Title` |String |"Video title" |Generated video title |
|`Summary` |String |"Content summary" |Generated video summary |
|`Insight` |String | |All content returned by video storyline understanding, marshaled from JSON to a string format. |


`CollectionContent` object


|**Parameter name** |**Parameter type** |**Example** |**Description** |
|---|---|---|---|
|`summary` |String | |A video summary of the entire collection, generated after processing each video in the series. |


`DataStatusDetail` object


|**Parameter Name** |**Parameter Type** |**Example** |**Description** |
|---|---|---|---|
|`update_type` |String |"FIRST_UPDATE_SUCCESS" |Update type:<br><br><br>* "FIRST_UPDATE_SUCCESS": The initial import and processing succeeded.<br><br>* "LATEST_UPDATE_SUCCESS": The latest update and processing succeeded.<br><br>* "UPDATE_FAILED": The latest data update failed due to an exception. |
|`timestamp` |String |"2025\-03\-12T15:01:07+08:00" |Update time in RFC3339 format |
|`warning_info` |Map[String]String | |Data quality error information, formatted as "Status Code": "Error Details"<br><br>Data quality errors do not affect data processing and indexing, but we recommend fixing them to improve search results. |
|`error_info` |Map[String]String | |Data validation and processing error information, formatted as "Status Code": "Error Details"<br><br>Validation and processing errors indicate that data is blocked at the validation stage and cannot be indexed. We recommend reviewing the error information and re\-uploading the fixed data. |


<span id="eadcd40f"></span>
### Response body: document dataset


|**Parameter Name** |**Parameter Type** |**Example** |**Description** |
|---|---|---|---|
|`item` |`DataItem` object | |A list of queried data items. Each data item includes data fields corresponding to the item ID and processing details. |


`DataItem`


|**Parameter Name** |**Parameter Type** |**Example** |**Description** |
|---|---|---|---|
|`_id` |String |"test_itemid" |Data ID. Unique within the dataset and returned for all dataset types (items, documents). |
|`raw_data` |String | |The original content of the uploaded file. |
|`check_status` |String |"normal" |The status of the data quality check, which includes the following states:<br><br><br>1. normal: The data quality is good.<br><br>2. warning: The data has field types that are inconsistent with their definitions, which might affect indexing and search performance.<br><br>3. Error: data quality validation exception, blocking subsequent processing, possible cases include |
|`process_status` |String |"success" |Data processing status, such as success, processing, and failed |
|`data_status_details` |Array<`DataStatusDetail`\> | |A list of data quality validation and processing statuses, including status descriptions for the initial data import and recent updates. |
|`create_time` |String |"2025\-03\-12T15:01:07+08:00" |Creation time in RFC3339 format |
|`update_time` |String |"2025\-03\-12T15:01:07+08:00" |Update time in RFC3339 format |


Returned fields for the document dataset in `raw_data` **:** 


|**Parameter name** |**Parameter type** |**Example** |**Description** |
|---|---|---|---|
|`doc_id` |String |"doc_1991040287514935296ab20a55f" |The unique identifier of the document |
|`doc_type` |String |"pdf" |The type of the document |
|`doc_name` |String |"file example.pdf" |Document name |
|`doc_size` |Int |28817 |Document size in bytes |
|`update_time` |String |"2025\-11\-20T14:02:25+08:00" |Document upload time |


`DataStatusDetail` object


|**Parameter name** |**Parameter type** |**Example** |**Description** |
|---|---|---|---|
|`update_type` |String |"FIRST_UPDATE_SUCCESS" |Update type:<br><br><br>* "FIRST_UPDATE_SUCCESS": The initial import and processing succeeded.<br><br>* "LATEST_UPDATE_SUCCESS": The latest update and processing succeeded.<br><br>* "UPDATE_FAILED": an exception occurred during the last data update |
|`timestamp` |String |"2025\-03\-12T15:01:07+08:00" |Update time in RFC3339 format |
|`warning_info` |Map[String]String | |Data quality exception information in the format "Status Code": "Exception Details"<br><br>Data quality exceptions do not affect data processing or indexing, but fixing them is recommended to improve search results. |
|`error_info` |Map[String]String | |Data validation and processing exception details, formatted as "Status Code": "Exception Details"<br><br>A validation and processing exception indicates that data was blocked during validation and could not be indexed. Check the exception details and re\-upload the corrected data. |


<span id="3088ae9c"></span>
### 

<span id="0c19905a"></span>
### Data Status Description

After data is imported, it undergoes quality checks and processing. A data status is generated during this process, which affects how the data is indexed and used. This guide explains the process and status definitions.

<span id="0cb771f3"></span>
#### Data Process Status

The data process status is returned in `DataItem` and includes the following two statuses:


* `process_status`: The data's processing status, which includes:

   * "success": Indicates the data was successfully processed and stored. It is displayed as "Data normal" in the console.

   * "failed": Indicates a critical error that prevented the data from being stored. It is displayed as "Data abnormal" in the console.

   * "processing": Indicates the data is being processed. This status is common for video files due to longer processing times but is rare for images and text. It is displayed as "Data processing" in the console.

* `check_status`: The data's quality check status, which includes:

   * "normal": The data passed all checks, with no format, type, or file errors found in any field.

   * "Warning": indicates data has quality issues, such as type exceptions in non\-preset fields or invalid image links. This does not affect the data ingestion process, but we recommend fixing and retransmitting the data upon receiving this quality status.

   * "Error": indicates data has severe quality issues, such as type exceptions in preset fields or invalid video file links. This affects the data ingestion process. We recommend fixing and retransmitting the data upon receiving this quality status.


<span id="c31b4c5c"></span>
#### Status Details

The `DataStatusDetail` structure returns the status code and detailed status information, displaying processing details for both the initial import and the most recent update:


|**Status Code** |**Description** |
|---|---|
|`Finished` |Data processing complete |
|`Running` |Data processing in progress |
|`InternalError` |Failed to handle internal error |
|`InvalidJsonLineError` |Invalid data JSON format |
|`NonRequiredFieldTypeMismatchError` |The custom field type does not match its definition |
|`DataPrimaryKeyNotFoundError` |Missing data primary key ID |
|`InvalidImageUrlError` |The image URL is inaccessible |
|`ImageDownloadTimeout` |Image retrieval timed out |
|`ImageUnsupportedFileFormat` |Unsupported image file format |
|`ImageSizeTooSmall` |Image is too small to process |
|`ExtremeImageProportion` |The image's aspect ratio exceeds 100:1 and cannot be processed |
|`ImageFileTooLarge` |Image file is too large |
|`ImageBase64UriInvalid` |Invalid base64 encoding format for the image. |
|`DataContentTypeNotFoundError` |Video data must include the content_type field and have a value. |
|`UnsupportedContentTypeError` |Unsupported content_type enum value. Only "video" and "collection" are supported. |
|`DuplicateMediaSequenceIndexError` |Duplicate media sequence index. |
|`MediaCannotBeSetAsParentError` |Media content cannot be set as a parent. |
|`ParentContentMustBeCollectionError` |(Video Data) The parent content must be a series. |
|`ParentContentNotUploadedError` |(Video Data) Parent content not uploaded. |
|`InvalidVideoUrlError` |(Video Data) The video URL is inaccessible. |
|`VideoUrlNotUploadedError` |(Video Data) Video URL not uploaded. |
|`InvalidMediaSequenceIndexError` |(Video Data) Invalid media sequence value. Duplicate sequence numbers exist. |
|`InvalidMediaCoverUrlError` |Video data: the media cover link is inaccessible |
|`RequiredFieldTypeMismatchError` |Video data: incorrect preset field type |
|`ContentTypeNotModifiableError` |Video data: content_type cannot be changed |
|`VideoProcessError` |Video data: video processing error |
|`VideoDurationExceedsLimitError` |Video data: the video duration exceeds the 3\-hour limit |
|`VideoSizeExceedsLimitError` |(Video data) The video size exceeds the 10 GB limit. |


<span id="cd861ab7"></span>
### Error Codes


|**Error code** |**HTTP status code** |**Error message** |**Description** |
|---|---|---|---|
|DatasetNotFound |404 |The dataset not found %s |The dataset does not exist. |
|InvalidParameter |400 |A parameter in the request is not valid: %s |The parameter format is invalid. |
|ErrCodeInvalidRequestBody<br><br> |400 |The request cannot be parsed in JSON format: %s |Request deserialization failed. |
|ErrCodeInternalServiceError<br><br> |500 |Service has some internal Error. Pls Contact With Admin. |An unknown error occurred while processing the request, such as a backend service timeout or network fluctuation. This issue is related to system reliability. |


<span id="c0f997b8"></span>
## Request Example


<Tabs>
<Tab zoneid="f6TL8cA64d" title="CURL">
<TabTitle>CURL</TabTitle>

&nbsp;

```Bash
curl -X POST https://aisearch.cn-beijing.volces.com/api/v1/dataset/{dataset_id}/get_item \
  -H 'Content-Type: application/json' \
  -H 'Authorization: <Header set for Signature/Auth>' \
  -d '{
    "_id": "2"
  }'
```





</Tab>
<Tab zoneid="zW7roBIMUx" title="Python">
<TabTitle>Python</TabTitle>

&nbsp;

```Python
import json
from volcenginesdkcore.rest import ApiException
from volcenginesdkcore import ApiClient, Configuration
from volcenginesdkcore.signv4 import SignerV4


def get_generic_client(access_key: str, secret_key: str, region: str, endpoint: str):
    """创建通用API客户端(适用于任何服务)"""
    try:
        config = Configuration()
        config.ak = access_key
        config.sk = secret_key
        config.region = region
        config.host = endpoint
        config.scheme = "https"
        return ApiClient(config)
    except Exception as e:
        print(f"客户端初始化失败: {str(e)}")
        return None



def call_aisearch_api(client: ApiClient, method: str, path: str, params: dict = None):
    try:
        # Set service name
        service = "aisearch"


        # Set request headers
        headers = {
            "Content-Type": "application/json",
            "Accept": "application/json",
            "Host": client.configuration.host,
        }


        # Serialize the request body
        body = json.dumps(params) if params else ""


        # Manually sign the request
        SignerV4.sign(
            path=path,
            method=method.upper(),
            headers=headers,
            body=body,
            post_params={},
            query={},
            ak=client.configuration.ak,
            sk=client.configuration.sk,
            region=client.configuration.region,
            service=service,
        )


        # Send the request using the REST client
        if method.upper() == "POST":
            response = client.rest_client.POST(
                url=f"https://{client.configuration.host}{path}",
                headers=headers,
                body=json.loads(body) if body else None,
                _preload_content=True,
            )
        else:
            response = client.rest_client.GET(
                url=f"https://{client.configuration.host}{path}",
                headers=headers,
                _preload_content=True,
            )


        # Parse the response
        response_data = json.loads(response.data)


        # Print the status and save the result
        print(f"API调用成功 (状态码: {response.status})")
        return response_data


    except ApiException as e:
        print(f"API调用失败: {e.status} {e.reason}")
        print(f"错误详情: {e.body}")
        return None
    except Exception as e:
        print(f"调用异常: {str(e)}")
        return None



if __name__ == "__main__":
    ACCESS_KEY = "" # Configuration information (replace with actual values)
    SECRET_KEY = ""
    REGION = "cn-beijing"
    ENDPOINT = "aisearch.cn-beijing.volces.com"  # AISearch server endpoint
    DATASET_ID = "" # Dataset ID


    # Create a generic client
    client = get_generic_client(ACCESS_KEY, SECRET_KEY, REGION, ENDPOINT)


    if client is None:
        print("客户端初始化失败，程序退出")
        exit(1)

    item_id = ""  # Ensure the ID exists
    get_path = f"/api/v1/dataset/{DATASET_ID}/get_item"
    get_params = {"_id": item_id}
    get_result = call_aisearch_api(client, "POST", get_path, get_params)
    if get_result:
        with open("get_item.json", "w", encoding="utf-8") as f:
            json.dump(get_result, f, ensure_ascii=False, indent=2)
        print("项目详情已保存到 get_item.json")
```



</Tab>
<Tab zoneid="Jzv35l8Nby" title="Java">
<TabTitle>Java</TabTitle>

&nbsp;

```Python
package com.example;

import java.net.URI;
import java.nio.charset.StandardCharsets;
import java.util.*;
import java.nio.file.Files;
import java.nio.file.Paths;

import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonParser;
import com.google.gson.JsonElement;
import org.apache.http.HttpEntity;
import org.apache.http.HttpResponse;
import org.apache.http.NameValuePair;
import org.apache.http.client.HttpClient;
import org.apache.http.client.config.RequestConfig;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.client.utils.URIBuilder;
import org.apache.http.entity.StringEntity;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.util.EntityUtils;
import com.volcengine.auth.ISignerV4;
import com.volcengine.auth.impl.SignerV4Impl;
import com.volcengine.model.Credentials;
import com.volcengine.service.SignableRequest;


public class App {
    private static final String AK = ""; // your ak
    private static final String SK = ""; // your sk
    private static final String HOST = "aisearch.cn-beijing.volces.com";
    private static final String SERVICE = "aisearch";
    private static final String REGION = "cn-beijing";
    private static final String SCHEMA = "https";
    
    public static class ApiClient {
        private final String accessKey;
        private final String secretKey;
        private final String region;
        private final String host;
        private final String service;
        private final HttpClient httpClient;
        private final Gson gson;
        
        public ApiClient(String accessKey, String secretKey, String region, String host, String service) {
            this.accessKey = accessKey;
            this.secretKey = secretKey;
            this.region = region;
            this.host = host;
            this.service = service;
            this.httpClient = HttpClients.createDefault();
            this.gson = new GsonBuilder().setPrettyPrinting().create();
        }
        
        public String getHost() {
            return host;
        }
        
        public Gson getGson() {
            return gson;
        }
    }
    
    public static class AISearchService {
        private final ApiClient client;
        
        public AISearchService(ApiClient client) {
            this.client = client;
        }
        
        public String callApi(String method, String path, Map<String, Object> params) throws Exception {
            try {
                // 1. 构建请求体
                String requestBody = params != null ? client.getGson().toJson(params) : "";
                
                // 2. 准备签名请求
                SignableRequest signableRequest = prepareRequest(
                    client.getHost(), 
                    path, 
                    method, 
                    new ArrayList<>(), 
                    requestBody, 
                    client.accessKey, 
                    client.secretKey
                );
                
                // 3. 构建最终的 HTTP 请求
                URI uri = signableRequest.getUriBuilder().build();
                HttpPost httpPost = new HttpPost(uri);
                
                // 4. 设置请求头
                httpPost.setHeader("Content-Type", "application/json");
                httpPost.setHeader("Accept", "application/json");
                httpPost.setHeader("Host", client.getHost());
                
                // 5. 复制认证相关请求头
                if (signableRequest.getFirstHeader("Authorization") != null) {
                    httpPost.setHeader("Authorization", signableRequest.getFirstHeader("Authorization").getValue());
                }
                if (signableRequest.getFirstHeader("X-Date") != null) {
                    httpPost.setHeader("X-Date", signableRequest.getFirstHeader("X-Date").getValue());
                }
                if (signableRequest.getFirstHeader("X-Content-Sha256") != null) {
                    httpPost.setHeader("X-Content-Sha256", signableRequest.getFirstHeader("X-Content-Sha256").getValue());
                }
                
                // 6. 设置请求体
                httpPost.setEntity(new StringEntity(requestBody, StandardCharsets.UTF_8));
                httpPost.setConfig(signableRequest.getConfig());
                
                // 8. 发送请求
                HttpResponse response = client.httpClient.execute(httpPost);
                
                // 9. 处理响应
                int statusCode = response.getStatusLine().getStatusCode();
                HttpEntity responseEntity = response.getEntity();
                
                if (responseEntity != null) {
                    String responseBody = EntityUtils.toString(responseEntity, StandardCharsets.UTF_8);
                    
                    if (statusCode >= 200 && statusCode < 300) {
                        System.out.println("API调用成功 (状态码: " + statusCode + ")");
                        return responseBody;
                    } else {
                        System.err.println("API调用失败: " + statusCode);
                        System.err.println("错误详情: " + responseBody);
                        return null;
                    }
                }
                
                return null;
                
            } catch (Exception e) {
                System.err.println("调用异常: " + e.getMessage());
                e.printStackTrace();
                return null;
            }
        }
        
        public String listItems(String datasetId, int maxResults) throws Exception {
            String path = "/api/v1/dataset/" + datasetId + "/list_items";
            Map<String, Object> params = new HashMap<>();
            params.put("max_results", maxResults);
            
            return callApi("POST", path, params);
        }
        
        public String getItem(String datasetId, String itemId) throws Exception {
            String path = "/api/v1/dataset/" + datasetId + "/get_item";
            Map<String, Object> params = new HashMap<>();
            params.put("_id", itemId);
            
            return callApi("POST", path, params);
        }
    }


    public static void main(String[] args) {
        // 配置信息（请替换为实际值）
        String DATASET_ID = "";
        int MAX_RESULTS = 3;
        
        try {
            // 创建通用客户端
            ApiClient client = new ApiClient(AK, SK, REGION, HOST, SERVICE);
            AISearchService service = new AISearchService(client);
            
            String itemId = "";  // 确保ID存在
            String getResult = service.getItem(DATASET_ID, itemId);
            if (getResult != null) {
                // 格式化并保存结果
                JsonElement jsonElement = JsonParser.parseString(getResult);
                String formattedJson = client.getGson().toJson(jsonElement);
                Files.write(Paths.get("get_item.json"), formattedJson.getBytes(StandardCharsets.UTF_8));
                System.out.println("项目详情已保存到 get_item.json");
            }
            
        } catch (Exception e) {
            System.err.println("程序执行异常: " + e.getMessage());
            e.printStackTrace();
        }
    }


    public static SignableRequest prepareRequest(String host, String path, String method, List<NameValuePair> params,
            String body, String ak, String sk) throws Exception {
        SignableRequest request = new SignableRequest();
        request.setMethod(method);
        request.setHeader("Accept", "application/json");
        request.setHeader("Content-Type", "application/json");
        request.setHeader("Host", HOST);
        request.setEntity(new StringEntity(body, "utf-8"));


        URIBuilder builder = request.getUriBuilder();
        builder.setScheme(SCHEMA);
        builder.setHost(host);
        builder.setPath(path);
        if (params != null) {
            builder.setParameters(params);
        }


        RequestConfig requestConfig = RequestConfig.custom().setSocketTimeout(5000).setConnectTimeout(2000).build();
        request.setConfig(requestConfig);


        Credentials credentials = new Credentials(REGION, SERVICE);
        credentials.setAccessKeyID(ak);
        credentials.setSecretAccessKey(sk);


        // 签名
        ISignerV4 ISigner = new SignerV4Impl();
        ISigner.sign(request, credentials);


        return request;
    }
}
```





</Tab>
</Tabs>


<span id="c00dd0cc"></span>
### Response Example


<Tabs>
<Tab zoneid="teM86YK3l3" title="Item Dataset (Images and Text)">
<TabTitle>Item Dataset (Images and Text)</TabTitle>

```JSON
{
  "request_id": "f0821969-7461-48bc-b5dd-beba75c01805",
  "result": {
    "item": {
      "_id": "pd0921HJ9088",
      "raw_data": "{\"spu_id\":\"pd0921HJ9088\",\"image_plp\":[\"http://domain.com/path\"],\"product_name\":\"Women's Silk T-Shirt Korean Style\",\"tags\":[\"Korean Style\",\"Early Spring\",\"Mega Sale\"],\"current_price\":300.00,\"pin_code\":\"889200192\",\"pdp_images\":[\"https://example.com/path\",\"https://example.com/path\"]}",
      "process_status": "success",
      "check_status": "normal",
      "data_status_details": [
        {
          "update_type": "FIRST_UPDATE_SUCCESS",
          "timestamp": "2026-05-12T19:57:23+08:00",
          "warning_info": {
            "ParentContentNotUploadedError": ""
          }
        }
      ],
      "update_time": "2026-05-12T19:57:22+08:00"
    }
  }
}
```



</Tab>
<Tab zoneid="nxoHeMnMZh" title="Item Dataset (Video)">
<TabTitle>Item Dataset (Video)</TabTitle>

```JSON
{
  "request_id": "f0821969-7461-48bc-b5dd-beba75c01805",
  "result": {
    "item": {
      "_id": "30",
      "raw_data": "{\"duration\":\"\",\"video_url\":[\"http://domain.com/path\"],\"language\":\"汉语普通话\",\"content_id\":\"30\",\"sequence_index\":30,\"title\":\"三体\",\"media_link\":\"https://example.com/tv_series/67890/episode_1/\",\"parent_content_id\":\"三体\",\"release_date\":\"\",\"image\":\"https://domain.com/filename.jpg\",\"content_type\":\"video\",\"genres\":\"剧情/科幻\"}",
      "meta": {
        "video_meta": {
          "content_type": "video",
          "video_urls": [
            "http://ai-search-rec-video.byte-test.com/9ecc0045531947d4bd71ff6a890289e6/main.m3u8"
          ],
          "parent_content_id": "三体",
          "sequence_index": 30,
          "video_content": {
            "title": "智子封锁下的科技困局：微观粒子操控与文明存亡博弈",
            "summary": "三体文明通过智子工程展开质子维度操控，将二维平面包裹星球进行集成电路蚀刻，制造出能干扰地球高能加速器的超能计算机。地球科学家发现基础物理停滞源于智子对撞击实验的破坏，科技发展被彻底锁死。三体世界为此承受极寒黑夜，全民脱水贮存以应对漫长工程。人类科学家在绝望中探讨文明对抗本质，以虫子的生存韧性类比人类与三体文明的科技差距，寻找突破封锁的可能性。",
            "insight": "{\"Summaries\":[\"三体文明通过智子工程展开质子维度操控，将二维平面包裹星球进行集成电路蚀刻，制造出能干扰地球高能加速器的超能计算机。地球科学家发现基础物理停滞源于智子对撞击实验的破坏，科技发展被彻底锁死。三体世界为此承受极寒黑夜，全民脱水贮存以应对漫长工程。人类科学家在绝望中探讨文明对抗本质，以虫子的生存韧性类比人类与三体文明的科技差距，寻找突破封锁的可能性。\"],\"Titles\":[\"智子封锁下的科技困局：微观粒子操控与文明存亡博弈\"],\"Clips\":[{\"Title\":\"《三体》开场，宇宙探秘之旅开启\",\"Summary\":\"视频开场展示了出品人、总制片人等信息，随后画面切换到一艘在迷雾中航行的船，标注着林奇、孙忠怀等名字。接着，画面呈现出神秘的宇宙景象，包括悬浮的星球和复杂的机械装置，显示出科幻氛围。最后，镜头转到户外，有几个人在草地上活动，似乎在进行某种探索或讨论，为后续剧情埋下伏笔。\",\"Score\":3.5,\"Dialogue\":\"沪剧审字2023第001号。林奇、孙忠怀，出品人何嵩、白一骢、卢歧、马延琨、中积军、纪敬、胡进、黄杰、夏晓辉、王寒英。李尔云、白一骢、杨星阳、伊简梅、朱智涵、纪毅、朱绍超、黄橙、王宁、刘焱、田咏力、胡海波、徐丹、桑俊、康歆、李潇、闫豪利、吴洋、刘羽丹、章炜、尹秀杰、刘浮、海霞程、王涛、蔡天君、陈正纲、陈晨、刘勇奇、刘屹、周炜强、姜涛、刘屹、灯伟、周炜强、姜涛、男津语、路迪、音乐总监陈雪燃。\",\"Start\":0,\"End\":66.5}... ...]}"
          },
          "collection_content": {},
          "duration": 3288
        }
      },
      "process_status": "success",
      "check_status": "warning",
      "data_status_details": [
        {
          "update_type": "FIRST_UPDATE_SUCCESS",
          "timestamp": "2025-08-06T19:57:23+08:00",
          "warning_info": {
            "ParentContentNotUploadedError": ""
          }
        }
      ],
      "update_time": "2025-08-06T19:57:22+08:00"
    }
  }
}
```



</Tab>
<Tab zoneid="tuHlZHlsoX" title="Document Dataset">
<TabTitle>Document Dataset</TabTitle>

&nbsp;

```JSON
{
    "request_id": "5a095658-87f5-9acc-8235-74e4fee0fa2b",
    "result": {
        "item": {
            "_id": "doc_1764067011552_19897181822007255044729ea93",
            "raw_data": "{\"collection_id\":\"\",\"user_id\":\"1989718182200725504\",\"doc_size\":\"66845\",\"upload_source\":\"homepage_user\",\"doc_id\":\"doc_1764067011552_19897181822007255044729ea93\",\"doc_source\":\"local\",\"doc_path\":\"homepage/unstructured_data/2105638287/20251125183651/二维码.\",\"doc_type\":\"jpeg\",\"doc_name\":\"二维码.jpeg\"}",
            "meta": {
                "video_meta": {}
            },
            "process_status": "success",
            "check_status": "normal",
            "common_process_end_time": "2025-11-25T18:37:03+08:00",
            "update_time": "2025-11-25T18:36:51+08:00"
        }
    }
}
```





</Tab>
</Tabs>


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To explore more of Viking AI's search capabilities, visit: <a href="https://www.volcengine.com/product/AI-Search-Rec">Viking AI Search Engine, the integrated intelligent engine for enterprise search, recommendation, and Q&A</a></div>
