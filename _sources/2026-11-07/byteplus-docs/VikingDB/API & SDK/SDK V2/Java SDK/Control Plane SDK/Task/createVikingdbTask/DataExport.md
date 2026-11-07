---
title: "DataExport"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/dataexport"
---

<span id="overview"></span>
# Overview

Batch export data from Collection by specific conditions

Before using, please authorize VikingDB cross\-service access to TOS first: [Authorize](https://console.volcengine.com/iam/service/attach_role/?ServiceName=ml_platform)

<span id="method-definition"></span>
# Method Definition

```Java
public CreateVikingdbTaskResponse createVikingdbTask(CreateVikingdbTaskRequest body) throws ApiException
```


<span id="request-parameters"></span>
# Request Parameters


|Parameter |Sub\-parameter |Type |Required |Description |
|---|---|---|---|---|
|ProjectName | |String |No |Project name |
|CollectionName | |String |Either one is required |Dataset name |
|ResourceId | |String | |Dataset resource ID. The request must specify either ResourceId or CollectionName. |
|TaskType | |String |Yes |data_export |
|TaskConfig | |TaskConfigForCreateVikingdbTaskInput |Yes |Task specific configuration |
| |FileType |String |Yes |File type: json or parquet, required |
| |FilterConds |List[Object] |No |Filter conditions. Reference: https://www.volcengine.com/docs/84313/1791133<br><br><br>* If FilterConds is not filled, regardless of ExportAll, all data will be exported.<br><br>* If FilterConds is filled:<br><br>* If ExportAll is not specified, or ExportAll=false, only data meeting the conditions will be exported by default.<br><br>* If ExportAll=true is specified, all data will be forcibly exported, and FilterConds will not take effect. |
| |TosPath |String |Yes |TOS path, format: {bucket name}/{path}, note this is not a domain name. Required |
| |ExportAll |Boolean |No |Whether to export all data, FilterConds does not take effect when this is set, default is false |


<span id="return-parameters"></span>
## Return Parameters


|Parameter |Type |Description |
|---|---|---|
|taskId |String |Task ID |
|message |String |Operation result information |


<span id="example"></span>
# Example

<span id="request-parameters"></span>
## Request Parameters

```Java
package org.example.newsubproduct.console.task;


import com.volcengine.ApiClient;
import com.volcengine.ApiException;
import com.volcengine.sign.Credentials;
import com.volcengine.vikingdb.VikingdbApi;
import com.volcengine.vikingdb.model.*;


public class CreateVikingdbTaskDataExport {
    public static void main(String[] args) {
        String ak = System.getenv("AK"); // ak
        String sk = System.getenv("SK"); // sk
        String endpoint = "vikingdb.ap-southeast-1.byteplusapi.com"; // Fill in the V2 vector database control plane domain name: https://www.volcengine.com/docs/84313/1792715
        String region = "ap-southeast-1"; // Service region


        ApiClient apiClient = new ApiClient()
                .setEndpoint(endpoint)
                .setCredentials(Credentials.getCredentials(ak, sk))
                .setRegion(region);


        VikingdbApi api = new VikingdbApi(apiClient);


        CreateVikingdbTaskRequest request = new CreateVikingdbTaskRequest()
                .collectionName("test_collection_for_sdk_with_vector")
                .taskType(CreateVikingdbTaskRequest.TaskTypeEnum.DATA_EXPORT)
                .taskConfig(
                        new TaskConfigForCreateVikingdbTaskInput()
                                .fileType(TaskConfigForCreateVikingdbTaskInput.FileTypeEnum.JSON)
                                .tosPath("test-doc1-tos/output.json")
                                .ignoreError(true)
                );


        try {
            CreateVikingdbTaskResponse response = api.createVikingdbTask(request);
            System.out.println("response body: " + response);
            System.out.println();
            System.out.println("response meta RequestId: " + response.getResponseMetadata().getRequestId());
            System.out.println("response meta Service: " + response.getResponseMetadata().getService());
            System.out.println("response meta Region: " + response.getResponseMetadata().getRegion());
            System.out.println("response meta Action: " + response.getResponseMetadata().getAction());
            System.out.println("response meta Version: " + response.getResponseMetadata().getVersion());
        } catch (ApiException e) {
            System.out.println("exception http code: " + e.getCode());
            System.out.println("exception response body: " + e.getResponseBody());
            System.out.println();
            System.out.println("exception RequestId: " + e.getResponseMetadata().getRequestId());
            System.out.println("exception Action: " + e.getResponseMetadata().getAction());
            System.out.println("exception Region: " + e.getResponseMetadata().getRegion());
            System.out.println("exception Service: " + e.getResponseMetadata().getService());
            System.out.println("exception Error.Code: " + e.getResponseMetadata().getError().getCode());
            System.out.println("exception Error.Message: " + e.getResponseMetadata().getError().getMessage());
        }
    }
}
```


<span id="post-processing"></span>
## Post\-processing

<span id="_1-download-files-from-tos"></span>
### 1. Download files from TOS

```Python
import tos
DOMAIN = "api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com"
TOS_ENDPOINT = "tos-ap-southeast-1.bytepluses.com"
REGION = "ap-southeast-1"
AK = "****"
SK = "****"
COLLECTION_NAME = "example"
BUCKET_NAME = "bucket_name"
TOS_DIR = "tos_dir"

def download(client, bucket_name, object_key, local_path):
    file_path = "{}/{}".format(local_path, object_key)
    try:
        client.get_object_to_file(bucket_name, object_key, file_path)
    except tos.exceptions.TosClientError as e:
        # Operation failed, catch client exception, usually illegal request parameters or network exception
        return 'fail with client error, message:{}, cause: {}'.format(e.message, e.cause)
    except tos.exceptions.TosServerError as e:
        return 'fail with server error : {}'.format(e)
    except Exception as e:
        return 'fail with unknown error: {}'.format(e)
    return ''

client = tos.TosClientV2(AK, SK, TOS_ENDPOINT, REGION)
download(client, BUCKET_NAME, TOS_DIR, "./")
```


<span id="_2-parse-parquet-type-data"></span>
### 2. Parse Parquet type data

```Python
import pyarrow.parquet as pq
def process_parquet(file_path):
    parquet_file = pq.ParquetFile(file_path)

    file_data_count = sum(parquet_file.metadata.row_group(i).num_rows for i in range(parquet_file.num_row_groups))
    schema = parquet_file.schema.to_arrow_schema()
    row_iterator = parquet_file.iter_batches(batch_size=100)
    # Iteratively read data
    for batch in row_iterator:
        df = batch.to_pandas()
        for index, row in df.iterrows():
            """
            do what you want
            """
            print(row)
    return ''

process_parquet("1.parquet")
```
