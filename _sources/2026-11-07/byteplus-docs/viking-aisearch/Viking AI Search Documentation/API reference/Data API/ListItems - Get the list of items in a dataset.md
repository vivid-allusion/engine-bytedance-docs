---
title: "ListItems - Get the list of items in a dataset"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/ListItems_-_Get_the_list_of_items_in_a_dataset"
---

***Viking AI Search*** * is an enterprise\-level AI search product based on generative AI. It leverages the multi\-modal semantic representation and understanding of large models, combined with ByteDance's best practices in information retrieval, to provide an out\-of\-the\-box AI search platform. This platform helps customers easily build and integrate end\-to\-end multi\-modal search and recommendation capabilities for images and text.* 


---



Gets the list of imported items for a specified dataset. Pagination is supported.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Description</div>


<div data-tips="true" data-tips-type="default">Only list queries for item datasets are supported. Queries for behavior datasets are not currently supported.</div>


<span id="aef5f353"></span>
## Notes


* **Usage Limits:** 

   * The body of a single request cannot exceed 10 MB.


<span id="9c7df7dd"></span>
## Request Description


* **Request Method**: POST

* **Request URL**:



|**Service** |**Region** |**URL** |
|---|---|---|
|BytePlus |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.bytepluses.com/api/v1/dataset/{dataset_id}/list_items` |
|Volcano Engine |North China (Beijing) |`https://aisearch.cn-beijing.volces.com/api/v1/dataset/{dataset_id}/list_items` |
|Volcano Engine |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.volces.com/api/v1/dataset/{dataset_id}/list_items` |



---



 *{dataset_id}: The unique ID for a dataset, assigned by the system after you create it in the console. You can view and copy it from the dataset details page.* 

&nbsp;

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/128992460e3d4f3da5096aa74215a374) </span>

&nbsp;

Request Parameters

<span id="78f55836"></span>
### Request Body


|**Parameter Name** |**Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|
|`filter` |Filter structure |No | |Filtering conditions for querying batch records |
|`max_results`<br><br> |Int<br><br> |No<br><br> |10 |The number of results to get per page. The default value is used if not specified. Values: \- Minimum: 1 \- Maximum: 100 \- Default: 10 |
|`output_fields`<br><br> |Array<String\> |No |["title", "price", "category"]<br><br> |Specifies the fields of item data to return for the queried dataset. When return fields are specified, the `raw_data` field in the API response includes only those fields.<br><br>> If the dataset contains nested objects, only top\-level field names are supported.<br><br>> Non\-existent fields or fields within a nested object will be ignored. |
|`next_token` |String |No |MHwxMDY4MzAzMDNfOTM4Njk4NDM4NTAyMzEwNDkx |String used to retrieve the next page of content. |


`Filter`


|**Parameter Name** |**Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|
|`_id` |String |No |"test_id" |The primary key of the data entry. Filter criteria. No filter is applied by default.<br><br><br>* Image\-text dataset: the field that corresponds to the item ID attribute you specified.<br><br>* Video dataset: the ID corresponding to the `content_id` field. |
|`process_status`<br><br> |Array<**String**\><br><br> |No<br><br> |["success", "processing", "failed"] |Processing status of data entries: "success" means the data is valid, "processing" means it is being processed, and "failed" means there is an error. Returns all statuses by default. |


<span id="52da3f73"></span>
### Response Body


|**Parameter name** |**Parameter type** |**Example** |**Description** |
|---|---|---|---|
|`next_token` |String |MHwxMDY4MzAzMDNfOTM4Njk4NDM4NTAyMzEwNDkx |A string used to retrieve the next page of content. An empty value indicates the last data entry. |
|`items` |Array<DataItem\> structure | |A list of retrieved data items, where each item contains the data fields corresponding to the item ID and the processing details. |


`DataItem`


|**Parameter Name** |**Parameter Type** |**Example** |**Description** |
|---|---|---|---|
|`_id` |String |"test_itemid" |The primary key of the data record, which is unique within the dataset. |
|`raw_data` |String | |The content of all fields in the imported raw data. |
|`meta` |DataItemMeta structure | |For video datasets, this returns the data's processing and status information. |
|`process_status` |String |"success" |Data processing status: success, processing, or failed |
|`check_status` |String |"normal" |Data check status: normal, warning, or error |
|`data_status_details` |Array<DataStatusDetail\> | |A list of data quality check and processing statuses, including status descriptions for the initial import and latest update. |
|`create_time` |String |"2025\-03\-12T15:01:07+08:00" |Creation time, in RFC3339 format |
|`update_time` |String |"2025\-03\-12T15:01:07+08:00" |Update time, in RFC3339 format |


**DataItem response for video datasets:** 

`DataItemMeta`


|**Parameter name** |**Parameter type** |**Example** |**Description** |
|---|---|---|---|
|`video_meta` |VideoMeta | |Video data processing and status information |


`VideoMeta`


|**Parameter name** |**Parameter type** |**Example** |**Description** |
|---|---|---|---|
|`content_type` |String |video |Content type: video, collection |
|`video_urls` |Array<String\> |["https://domain.com/file_path.format"] |Video URL list |
|`parent_content_id` |String | |Parent content ID |
|`sequence_index` |Int | |Sequence index |
|`video_content` |VideoContent | |Video processing and understanding content |
|`collection_content` |CollectionContent | |Video collection processing and understanding content |
|`duration` |Int | |Video duration in seconds, rounded up to the nearest whole number. |


`VideoContent`


|**Parameter Name** |**Parameter Type** |**Example** |**Description** |
|---|---|---|---|
|`Title` |String |"Video title" |The generated video title. |
|`Summary` |String |"Content summary" |Generated video summary |
|`Insight` |String | |All content returned by the video storyline analysis, with the JSON marshaled into a string. |


`CollectionContent`


|**Parameter name** |**Parameter type** |**Example** |**Description** |
|---|---|---|---|
|`summary` |String | |A video summary generated by summarizing the entire collection after processing each video in the series. |


`DataStatusDetail`


|**Parameter name** |**Parameter type** |**Example** |**Description** |
|---|---|---|---|
|`update_type` |String |FIRST_UPDATE_SUCCESS |Update type:<br><br><br>* FIRST_UPDATE_SUCCESS: first import and processing succeeded<br><br>* LATEST_UPDATE_SUCCESS: latest update and processing succeeded<br><br>* UPDATE_FAILED: an error occurred during the latest data update |
|`timestamp` |String |2025\-03\-12T15:01:07+08:00 |Update time in RFC3339 format |
|`warning_info` |Map[String]String | |Data quality exception details in the format "Status Code": "Exception Details"<br><br>Data quality exceptions do not affect data processing or indexing, but fixing them is recommended to improve search performance. |
|`error_info` |Map[String]String | |Data validation and processing exception details in the format "Status Code": "Exception Details"<br><br>Validation and processing exceptions indicate that data was blocked during the validation stage and could not be processed or indexed. Review the exception details and re\-upload the corrected data. |


<span id="eafc9bc9"></span>
### Data Status Description

After data is imported, it undergoes quality checks and processing. Data statuses are generated during this process and affect data indexing and usage. The following sections describe the process and status definitions.

<span id="b135611f"></span>
#### Data Processing Status

The data processing status is returned in `DataItem` and includes 2 statuses:


* `process_status`: The processing status of the data, which includes the following:

   * "success": Indicates that the data has been processed and stored successfully, corresponding to "Data normal" displayed on the console.

   * "failed": Indicates a blocking exception that caused the data import to fail. The console displays "Data exception".

   * "processing": Indicates that the data is being processed. This status usually applies to video files, which have longer processing times, and is less common for image and text data that are processed quickly. The console displays "Data processing".

* `check_status`: The quality validation status of the data, which includes:

   * "normal": The data has passed all validation checks, and there are no format, type, or file exceptions in any fields.

   * "warning": Indicates a data quality issue, such as a type exception in a non\-preset field or an invalid image link. This issue does not affect the data import process, but we recommend you fix and resubmit the data upon receiving this status.

   * "error": Indicates a serious data quality issue, such as a type exception in a preset field or an invalid video file link. This issue affects the data import process, and we recommend that you fix and resubmit the data upon receiving this status.


<span id="62247fa8"></span>
#### Status Details

The `DataStatusDetail` structure returns the status code and detailed status information for the initial import and the most recent update:


|**Status Code** |**Description** |
|---|---|
|`Finished` |Data processing complete |
|`Running` |Processing data |
|`InternalError` |Failed to handle internal error |
|`InvalidJsonLineError` |Invalid JSON data format |
|`DataPrimaryKeyNotFoundError` |A primary key field with a value is required. |
|`InvalidImageUrlError` |The image link is inaccessible |
|`ImageDownloadTimeout` |Image download timed out |
|`ImageUnsupportedFileFormat` |Unsupported image file format |
|`ImageSizeTooSmall` |The image is too small to be processed |
|`ExtremeImageProportion` |The image aspect ratio exceeds 100:1 and cannot be processed |
|`ImageFileTooLarge` |The image file is too large. |
|`ImageBase64UriInvalid` |Invalid image Base64 encoding format. |
|`DataContentTypeNotFoundError` |The content_type field is required for video data and must have a value. |
|`UnsupportedContentTypeError` |Unsupported content_type value. Only "video" and "collection" are supported. |
|`DuplicateMediaSequenceIndexError` |Duplicate media sequence index. |
|`MediaCannotBeSetAsParentError` |Media content cannot be set as a parent |
|`ParentContentMustBeCollectionError` |Parent content must be a collection |
|`ParentContentNotUploadedError` |The parent content has not been uploaded |
|`InvalidVideoUrlError` |The video URL cannot be accessed |
|`InvalidImageUrlError` |The image URL cannot be accessed |
|`VideoUrlNotUploadedError` |(Video data) Video URL not uploaded |
|`InvalidMediaSequenceIndexError` |(Video data) Invalid media sequence number. Duplicate sequence numbers exist. |
|`InvalidMediaCoverUrlError` |(Video data) The media cover URL is inaccessible. |
|`RequiredFieldTypeMismatchError` |(Video data) Incorrect preset field type. |
|`NonRequiredFieldTypeMismatchError` |Incorrect custom field type. |
|`ContentTypeNotModifiableError` |(Video data) The content_type cannot be modified. |
|`VideoProcessError` |(Video data) Video processing error. |
|`VideoDurationExceedsLimitError` |(Video data) The video duration exceeds the 3.5\-hour limit. |
|`VideoSizeExceedsLimitError` |(Video data) The video size exceeds the 10 GB limit. |


<span id="5baf22de"></span>
### Error Code


|**Error code** |**HTTP status code** |**Error message** |**Description** |
|---|---|---|---|
|DatasetNotFound |404 |The dataset not found %s |The dataset does not exist. |
|InvalidParameter |400 |A parameter in the request is not valid: %s |The parameter format is invalid. |
|ErrCodeInvalidRequestBody<br><br> |400 |The request cannot be parsed in JSON format: %s |Request deserialization failed. |
|ErrCodeInternalServiceError<br><br> |500 |Service has some internal Error. Pls Contact With Admin. |A reliability\-related unknown error occurred during request processing, such as a backend service timeout or network fluctuations. |


<span id="eaaa1332"></span>
## Request Example

<span id="a5180538"></span>
## Request Sample Code


<Tabs>
<Tab zoneid="Y5Y9vNHilU" title="CURL">
<TabTitle>CURL</TabTitle>

&nbsp;

```Java
curl -X POST https://aisearch.cn-beijing.volces.com/api/v1/dataset/{dataset_id}/list_items \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <Header set for Signature/Auth>' \
  -d '{
    "max_results": 2
  }'
```



</Tab>
<Tab zoneid="MwKdLoIWIO" title="Python">
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
        # Set the service name
        service = "aisearch"

        # Set the request header
        headers = {
            "Content-Type": "application/json",
            "Accept": "application/json",
            "Host": client.configuration.host,
            "Authorization": f"Bearer {API_KE}"
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

        # Print the status and save the results
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
    API_KEY = "" # Configuration information (replace with actual values)
    REGION = "cn-beijing"
    ENDPOINT = "aisearch.cn-beijing.volces.com"  # AISearch server endpoint
    DATASET_ID = "" # Dataset ID

    # Create a general-purpose client
    client = get_generic_client(ACCESS_KEY, SECRET_KEY, REGION, ENDPOINT)

    if client is None:
        print("客户端初始化失败，程序退出")
        exit(1)


    list_path = f"/api/v1/dataset/{DATASET_ID}/list_items"
    list_params = {"max_results": 3}
    list_result = call_aisearch_api(client, "POST", list_path, list_params)
    if list_result:
        with open("list_items.json", "w", encoding="utf-8") as f:
            json.dump(list_result, f, ensure_ascii=False, indent=2)
        print("列表结果已保存到 list_items.json")

```





</Tab>
<Tab zoneid="cKiqrP4Imo" title="Java">
<TabTitle>Java</TabTitle>

&nbsp;

```Java
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
                // 1. Build the request body
                String requestBody = params != null ? client.getGson().toJson(params) : "";
                
                // 2. Prepare the signed request
                SignableRequest signableRequest = prepareRequest(
                    client.getHost(), 
                    path, 
                    method, 
                    new ArrayList<>(), 
                    requestBody, 
                    client.accessKey, 
                    client.secretKey
                );
                
                // 3. Build the final HTTP request
                URI uri = signableRequest.getUriBuilder().build();
                HttpPost httpPost = new HttpPost(uri);
                
                // 4. Set the request headers
                httpPost.setHeader("Content-Type", "application/json");
                httpPost.setHeader("Accept", "application/json");
                httpPost.setHeader("Host", client.getHost());
                
                // 5. Copy the authentication request headers
                if (signableRequest.getFirstHeader("Authorization") != null) {
                    httpPost.setHeader("Authorization", signableRequest.getFirstHeader("Authorization").getValue());
                }
                if (signableRequest.getFirstHeader("X-Date") != null) {
                    httpPost.setHeader("X-Date", signableRequest.getFirstHeader("X-Date").getValue());
                }
                if (signableRequest.getFirstHeader("X-Content-Sha256") != null) {
                    httpPost.setHeader("X-Content-Sha256", signableRequest.getFirstHeader("X-Content-Sha256").getValue());
                }
                
                // 6. Set the request body
                httpPost.setEntity(new StringEntity(requestBody, StandardCharsets.UTF_8));
                httpPost.setConfig(signableRequest.getConfig());
                
                // 8. Send the request
                HttpResponse response = client.httpClient.execute(httpPost);
                
                // 9. Handle the response
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
        // Configuration information (replace with actual values)
        String DATASET_ID = "";
        int MAX_RESULTS = 3;
        
        try {
            // Create a generic client
            ApiClient client = new ApiClient(AK, SK, REGION, HOST, SERVICE);
            AISearchService service = new AISearchService(client);
            
            System.out.println("=== 列出数据集项目 ===");
            String listResult = service.listItems(DATASET_ID, MAX_RESULTS);
            if (listResult != null) {
                // Format and save the results
                JsonElement jsonElement = JsonParser.parseString(listResult);
                String formattedJson = client.getGson().toJson(jsonElement);
                Files.write(Paths.get("list_items.json"), formattedJson.getBytes(StandardCharsets.UTF_8));
                System.out.println("列表结果已保存到 list_items.json");
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


        // Signature
        ISignerV4 ISigner = new SignerV4Impl();
        ISigner.sign(request, credentials);


        return request;
    }
}
```





</Tab>
</Tabs>


<span id="223419f9"></span>
## Response Sample

```JSON
{
  "request_id": "0cbab6b2-b17e-4ef6-885b-ed9b9099569a",
  "result": {
    "next_token": "MTc1NDQ4MTQ0MTkyM3wxMDcxNTEwNDdfNTc3MzE4NDA0NDcwNTQ5NjIzfDEwNzE1MTA0Nw==",
    "items": [
      {
        "_id": "30",
        "raw_data": "{\"duration\":\"3288\",\"video_url\":[\"http://domain.com/path\"],\"language\":\"English\",\"content_id\":\"30\",\"sequence_index\":30,\"title\":\"Stranger Things\",\"media_link\":\"https://example.com/tv_series/67890/season_1/episode_8/\",\"parent_content_id\":\"Stranger Things\",\"release_date\":\"2016-07-15\",\"image\":\"https://domain.com/filename.jpg\",\"content_type\":\"video\",\"genres\":\"Drama/Sci-Fi/Horror\"}",
        "meta": {
          "video_meta": {
            "content_type": "video",
            "video_urls": [
              "http://domain.com/path"
            ],
            "parent_content_id": "Stranger Things",
            "sequence_index": 30,
            "video_content": {
              "title": "The Upside Down: The Battle of Hawkins Lab and the Demogorgon",
              "summary": "Joyce and Hopper venture into the Upside Down to rescue Will, braving the toxic atmosphere and the shadow monster's lair. Meanwhile, Eleven faces her past at Hawkins Lab, using her telekinetic powers to protect her friends from the pursuing agents and the lethal Demogorgon. The boundary between dimensions thins as the boys wait in the school, realizing that survival requires a final, desperate stand against the supernatural forces unleashed by the gate.",
              "insight": "{\"Summaries\":[\"Joyce and Hopper enter the Upside Down to find Will, discovering the biological growth overtaking the alternate dimension. Eleven confronts the Demogorgon in a final showdown at the middle school, sacrificing herself to save Mike and the group. The episode concludes with Will's return, though he shows lingering effects of his time in the dark realm.\"],\"Titles\":[\"Dimension Breach: The Vanishing of Will Byers and the Final Stand\"],\"Clips\":[{\"Title\":\"Stranger Things
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To experience more of Viking AI's search capabilities, visit <a href="https://www.volcengine.com/product/AI-Search-Rec">Viking AI Search, an all\-in\-one intelligent engine for enterprise search, recommendation, and Q&A</a>.</div>
