---
title: "Multipart Upload (C SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Sharded-upload-c-sdk"
---

If you need to upload large objects, it is recommended to split them into multiple data blocks (parts) and upload each part separately. Finally, call the merge parts operation to combine the uploaded data blocks into a single object.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Before initiating a multipart upload, you must ensure that your account has the tos:PutObject permission. For detailed instructions, please refer to the [Permission configuration guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* To cancel a multipart upload, you must have the tos:AbortMultipartUpload permission. For detailed instructions, please refer to the [Permission configuration guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* When uploading objects, object names must comply with the naming conventions. For more information, see [Naming conventions for objects](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for large\-scale storage. Its internal partitions store object index data. To maximize the throughput for uploading and downloading objects and to reduce the likelihood of hotspot partitions during horizontal scaling, please avoid using lexicographically incremental object naming. For more information, see [Performance optimization](https://docs.byteplus.com/docs/tos/Performance-optimization-plan).

* If an object with the same name already exists in the bucket, the new object will overwrite the existing one. When versioning is enabled for the bucket, the original object is retained, and a new version number is generated to identify the newly uploaded object.


<span id=".5YiG54mH5LiK5Lyg5q2l6aqk"></span>
## Steps

Multipart upload using the TOS C SDK consists of the following three steps.


1. Initialize a multipart upload

   Call `createMultipartUpload`. The API returns the globally unique `uploadId` created by TOS.

2. Upload the parts

   Call `uploadPart` to upload part data.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For the same multipart upload (identified by <code>uploadId</code>), the part number (<code>partNumber</code>) specifies the relative position of the part within the entire object. If data is uploaded multiple times using the same part identifier, TOS will overwrite the existing data and retain only the data from the most recent upload.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <code>uploadPart</code> API returns the MD5 value of the part data, which can be obtained through the <code>ETag</code> field. When merging parts, you must specify the part number and ETag value for each uploaded part in the current multipart upload.   </div>
   

3. Complete the multipart upload

   After all parts have been uploaded, call `completeMultipartUpload` to merge all parts into a complete object.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id="09de7d48"></span>
### Initialize the client

```C
char* ak = getenv("TOS_ACCESS_KEY");
char* sk = getenv("TOS_SECRET_KEY");
char* sts_token = getenv("TOS_SECRET_TOKEN");

void init_test_config_ak_sk(tos_config_t *config) {
    tos_str_set(&config->endpoint, TEST_ENDPOINT);
    tos_str_set(&config->region, TEST_REGION);
    tos_str_set(&config->access_key_id, ak);
    tos_str_set(&config->access_key_secret, sk);
}

void init_test_config_sts_token(tos_config_t *config) {
    tos_str_set(&config->endpoint, TEST_ENDPOINT);
    tos_str_set(&config->region, TEST_REGION);
    tos_str_set(&config->access_key_id, ak);
    tos_str_set(&config->access_key_secret, sk);
    tos_str_set(&config->sts_token, sts_token);
}

void init_test_tos_client(tos_client_t *client) {
    client->config = tos_config_create(client->pool);

    init_test_config_ak_sk(client->config);
    // init_test_config_sts_token(client->config);

    client->ctl = tos_http_controller_create(client->pool, 0);
}
```


<span id=".5YiG54mH5LiK5Lyg5a6M5pW06L-H56iL"></span>
### Complete multipart upload process

The following code demonstrates the complete process of uploading a local file using multipart upload, with the access control list (ACL) permission set to Private and the storage type specified as Infrequent Access.

<span id="7b951fa6"></span>
#### Multipart upload from file

```C
int test_multipart_upload_from_file() {
    // basic input
    tos_pool_t *p = NULL;
    tos_string_t bucket;
    tos_string_t object;
    tos_client_t *client = NULL;
    tos_error_t *error = NULL;

    // create multipart upload input
    create_multipart_upload_input_t *create_multipart_upload_input = NULL;
    create_multipart_upload_output_t *create_multipart_upload_output = NULL;

    // multipart upload from file input
    upload_part_from_file_input_t *upload_part_from_file_input = NULL;
    upload_part_from_file_output_t *upload_part_from_file_output = NULL;
    tos_file_buf_t *fb = NULL;
    int64_t file_length = 0;
    int64_t pos = 0;
    int part_num = 1;

    // list parts
    list_parts_input_t *list_part_input = NULL;
    list_parts_output_t *list_part_output = NULL;
    upload_part_t *part_content = NULL;

    // complete multipart upload input
    complete_multipart_upload_input_t  *complete_multipart_upload_input = NULL;
    complete_multipart_upload_output_t  *complete_multipart_upload_output = NULL;
    upload_part_t *complete_part_content = NULL;

    tos_pool_create(&p, NULL);
    client = tos_client_create(p);
    init_test_tos_client(client);

    tos_str_set(&bucket, TEST_BUCKET_NAME);
    tos_str_set(&object, TEST_MULTIPART_OBJECT);

    // create multipart upload
    if (create_multipart_upload_input_new(client->pool, &create_multipart_upload_input) != TOSE_OK)
    {
        tos_pool_destroy(p);
        return -1;
    }
    tos_str_set(&create_multipart_upload_input->bucket, bucket.data);
    tos_str_set(&create_multipart_upload_input->key, object.data);
    create_multipart_upload_input->acl = ACL_PRIVATE;
    create_multipart_upload_input->storage_class = STORAGE_CLASS_IA;

    error = create_multipart_upload(client, create_multipart_upload_input, &create_multipart_upload_output);
    if (error == NULL) {
        printf("Init multipart upload succeeded, upload_id:%.*s\n",
               create_multipart_upload_output->upload_id.len,
               create_multipart_upload_output->upload_id.data);
    } else {
        printf("Init multipart upload failed, request_id:%.*s, status_code:%d, message:%.*s, ec:%.*s\n",
               error->request_id.len, error->request_id.data,
               error->status_code,
               error->message.len, error->message.data,
               error->ec.len, error->ec.data);

        tos_pool_destroy(p);
        return -1;
    }

    // upload part from file
    if((fb = tos_create_file_buf(p)) == NULL)
    {
        tos_pool_destroy(p);
        return -1;
    }
    if (tos_open_file_for_all_read(p, TEST_FILE_PATH, fb) != TOSE_OK)
    {
        tos_pool_destroy(p);
        return -1;
    }

    file_length = fb->file_last;
    apr_file_close(fb->file);

    if (upload_part_from_file_input_new(client->pool, &upload_part_from_file_input) != TOSE_OK)
    {
        tos_pool_destroy(p);
        return -1;
    }

    tos_str_set(&upload_part_from_file_input->upload_id, create_multipart_upload_output->upload_id.data);
    tos_str_set(&upload_part_from_file_input->bucket, TEST_BUCKET_NAME);
    tos_str_set(&upload_part_from_file_input->key, TEST_MULTIPART_OBJECT);
    tos_str_set(&upload_part_from_file_input->file_path, TEST_FILE_PATH);

    while (pos < file_length) {
        upload_part_from_file_input->part_number = part_num++;
        upload_part_from_file_input->offset = pos;
        upload_part_from_file_input->part_size = pos + 10 * 1024 * 1024 > file_length ? file_length - pos : 10 * 1024 * 1024;
        pos += upload_part_from_file_input->part_size;
        error = upload_part_from_file(client, upload_part_from_file_input, &upload_part_from_file_output);
        if (error == NULL) {
            printf("Multipart upload part from file succeeded\n");
        } else {
            printf("Multipart upload part from file failed, request_id:%.*s, status_code:%d, message:%.*s, ec:%.*s\n",
                   error->request_id.len, error->request_id.data,
                   error->status_code,
                   error->message.len, error->message.data,
                   error->ec.len, error->ec.data);

            tos_pool_destroy(p);
            return -1;
        }
    }

    // list part
    if (list_parts_input_new(client->pool,&list_part_input) != TOSE_OK)
    {
        tos_pool_destroy(p);
        return -1;
    }
    list_part_input->max_parts = 1000;
    tos_str_set(&list_part_input->bucket,bucket.data);
    tos_str_set(&list_part_input->key,object.data);
    tos_str_set(&list_part_input->upload_id,create_multipart_upload_output->upload_id.data);

    error = list_parts(client,list_part_input,&list_part_output);
    if (error == NULL) {
        printf("List multipart succeeded\n");
        tos_list_for_each_entry(upload_part_t, part_content, &list_part_output->parts, node) {
            printf("part_number = %d, size = %ld, last_modified = %s, etag = %s\n",
                   part_content->part_number,
                   part_content->size,
                   part_content->last_modified.data,
                   part_content->etag.data);
        }
    } else {
        printf("List multipart failed, request_id:%.*s, status_code:%d, message:%.*s, ec:%.*s\n",
               error->request_id.len, error->request_id.data,
               error->status_code,
               error->message.len, error->message.data,
               error->ec.len, error->ec.data);
        tos_pool_destroy(p);
        return -1;
    }

    // complete multipart upload input
    if (complete_multipart_upload_input_new(client->pool,&complete_multipart_upload_input) != TOSE_OK)
    {
        tos_pool_destroy(p);
        return -1;
    }
    tos_list_for_each_entry(upload_part_t, part_content, &list_part_output->parts, node) {
        complete_part_content = create_list_parts_content(p);
        complete_part_content->part_number = part_content->part_number;
        tos_str_set(&complete_part_content->etag, part_content->etag.data);
        tos_list_add_tail(&complete_part_content->node, &complete_multipart_upload_input->parts);
    }
    tos_str_set(&complete_multipart_upload_input->bucket,bucket.data);
    tos_str_set(&complete_multipart_upload_input->key,object.data);
    tos_str_set(&complete_multipart_upload_input->upload_id,create_multipart_upload_output->upload_id.data);

    error = complete_multipart_upload(client,complete_multipart_upload_input,&complete_multipart_upload_output);
    if (error == NULL) {
        printf("Complete multipart upload from file succeeded, key:%.*s\n",
               complete_multipart_upload_output->key.len, complete_multipart_upload_output->key.data);
    } else {
        printf("Complete multipart upload from file failed, request_id:%.*s, status_code:%d, message:%.*s, ec:%.*s\n",
               error->request_id.len, error->request_id.data,
               error->status_code,
               error->message.len, error->message.data,
               error->ec.len, error->ec.data);

        tos_pool_destroy(p);
        return -1;
    }

    tos_pool_destroy(p);
    return 0;
}
```


<span id="ebc4d269"></span>
#### Multipart upload from buffer

```C
int test_multipart_upload_from_buffer() {
    // basic input
    tos_pool_t *p = NULL;
    tos_string_t bucket;
    tos_string_t object;
    tos_client_t *client = NULL;
    tos_error_t *error = NULL;

    // create multipart upload input
    create_multipart_upload_input_t *create_multipart_upload_input = NULL;
    create_multipart_upload_output_t *create_multipart_upload_output = NULL;

    // multipart upload from buffer input
    upload_part_from_buffer_input_t *upload_part_from_buffer_input = NULL;
    upload_part_from_buffer_output_t *upload_part_from_buffer_output = NULL;

    // list parts
    list_parts_input_t *list_part_input = NULL;
    list_parts_output_t *list_part_output = NULL;
    upload_part_t *part_content = NULL;

    // complete multipart upload input
    complete_multipart_upload_input_t  *complete_multipart_upload_input = NULL;
    complete_multipart_upload_output_t  *complete_multipart_upload_output = NULL;
    upload_part_t *complete_part_content = NULL;

    tos_pool_create(&p, NULL);
    client = tos_client_create(p);
    init_test_tos_client(client);

    tos_str_set(&bucket, TEST_BUCKET_NAME);
    tos_str_set(&object, TEST_MULTIPART_OBJECT);

    // create multipart upload
    if (create_multipart_upload_input_new(client->pool, &create_multipart_upload_input) != TOSE_OK)
    {
        tos_pool_destroy(p);
        return -1;
    }
    tos_str_set(&create_multipart_upload_input->bucket, bucket.data);
    tos_str_set(&create_multipart_upload_input->key, object.data);
    create_multipart_upload_input->acl = ACL_PRIVATE;
    create_multipart_upload_input->storage_class = STORAGE_CLASS_IA;

    error = create_multipart_upload(client, create_multipart_upload_input, &create_multipart_upload_output);
    if (error == NULL) {
        printf("Init multipart upload succeeded, upload_id:%.*s\n",
               create_multipart_upload_output->upload_id.len,
               create_multipart_upload_output->upload_id.data);
    } else {
        printf("Init multipart upload failed, request_id:%.*s, status_code:%d, message:%.*s, ec:%.*s\n",
               error->request_id.len, error->request_id.data,
               error->status_code,
               error->message.len, error->message.data,
               error->ec.len, error->ec.data);

        tos_pool_destroy(p);
        return -1;
    }

    for (int i = 1; i <= 3;++i)
    {
       
        char *str = (char *)tos_pcalloc(client->pool, 10*1024*1024);
        if (str == NULL) {
            printf(stderr, "Memory allocation failed\n");
            return -1;
        }
       
        memset(str, 'A', 10*1024*1024 - 1);
        str[10*1024*1024 - 1] = '\0'; 
       
        tos_list_t buffer;
        tos_buf_t* content = NULL;
        tos_list_init(&buffer);
        content = tos_buf_pack(client->pool, str, strlen(str));
        tos_list_add_tail(&content->node, &buffer);

        // upload part from buffer
        if (upload_part_from_buffer_input_new(client->pool, &upload_part_from_buffer_input) != TOSE_OK)
        {
            tos_pool_destroy(p);
            return -1;
        }
        upload_part_from_buffer_input->content = &buffer;
        tos_str_set(&upload_part_from_buffer_input->upload_id,create_multipart_upload_output->upload_id.data);
        tos_str_set(&upload_part_from_buffer_input->bucket,bucket.data);
        tos_str_set(&upload_part_from_buffer_input->key,object.data);
        upload_part_from_buffer_input->part_number = i;

        error = upload_part_from_buffer(client,upload_part_from_buffer_input,&upload_part_from_buffer_output);
        if (error == NULL) {
            printf("Multipart upload part from buffer succeeded\n");
        } else {
            printf("Multipart upload part from buffer failed, request_id:%.*s, status_code:%d, message:%.*s, ec:%.*s\n",
                   error->request_id.len, error->request_id.data,
                   error->status_code,
                   error->message.len, error->message.data,
                   error->ec.len, error->ec.data);
            tos_pool_destroy(p);
            return -1;
        }
    }

    // list part
    if (list_parts_input_new(client->pool,&list_part_input) != TOSE_OK)
    {
        tos_pool_destroy(p);
        return -1;
    }
    list_part_input->max_parts = 1000;
    tos_str_set(&list_part_input->bucket,bucket.data);
    tos_str_set(&list_part_input->key,object.data);
    tos_str_set(&list_part_input->upload_id,create_multipart_upload_output->upload_id.data);

    error = list_parts(client,list_part_input,&list_part_output);
    if (error == NULL) {
        printf("List multipart succeeded\n");
        tos_list_for_each_entry(upload_part_t, part_content, &list_part_output->parts, node) {
            printf("part_number = %d, size = %ld, last_modified = %s, etag = %s\n",
                   part_content->part_number,
                   part_content->size,
                   part_content->last_modified.data,
                   part_content->etag.data);
        }
    } else {
        printf("List multipart failed, request_id:%.*s, status_code:%d, message:%.*s, ec:%.*s\n",
               error->request_id.len, error->request_id.data,
               error->status_code,
               error->message.len, error->message.data,
               error->ec.len, error->ec.data);
        tos_pool_destroy(p);
        return -1;
    }

    // complete multipart upload input
    if (complete_multipart_upload_input_new(client->pool,&complete_multipart_upload_input) != TOSE_OK)
    {
        tos_pool_destroy(p);
        return -1;
    }
    tos_list_for_each_entry(upload_part_t, part_content, &list_part_output->parts, node) {
        complete_part_content = create_list_parts_content(p);
        complete_part_content->part_number = part_content->part_number;
        tos_str_set(&complete_part_content->etag, part_content->etag.data);
        tos_list_add_tail(&complete_part_content->node, &complete_multipart_upload_input->parts);
    }
    tos_str_set(&complete_multipart_upload_input->bucket,bucket.data);
    tos_str_set(&complete_multipart_upload_input->key,object.data);
    tos_str_set(&complete_multipart_upload_input->upload_id,create_multipart_upload_output->upload_id.data);

    error = complete_multipart_upload(client,complete_multipart_upload_input,&complete_multipart_upload_output);
    if (error == NULL) {
        printf("Complete multipart upload from file succeeded, key:%.*s\n",
               complete_multipart_upload_output->key.len, complete_multipart_upload_output->key.data);
    } else {
        printf("Complete multipart upload from file failed, request_id:%.*s, status_code:%d, message:%.*s, ec:%.*s\n",
               error->request_id.len, error->request_id.data,
               error->status_code,
               error->message.len, error->message.data,
               error->ec.len, error->ec.data);

        tos_pool_destroy(p);
        return -1;
    }

    tos_pool_destroy(p);
    return 0;
}
```


<span id=".5YiX5Li-5bey5LiK5Lyg5YiG54mH"></span>
### List uploaded parts

The following code is used to list information about the uploaded parts of a specified object in a bucket.

```C
int list_parts_demo() {
    // basic input
    tos_pool_t *p = NULL;
    tos_string_t bucket;
    tos_string_t object;
    tos_client_t *client = NULL;
    tos_error_t *error = NULL;
    char* upload_id = "<fill_your_upload_id>";

    // list parts
    list_parts_input_t *list_part_input = NULL;
    list_parts_output_t *list_part_output = NULL;
    upload_part_t *part_content = NULL;

    tos_pool_create(&p, NULL);
    client = tos_client_create(p);
    init_test_tos_client(client);

    tos_str_set(&bucket, TEST_BUCKET_NAME);
    tos_str_set(&object, TEST_MULTIPART_OBJECT);

    // list part
    if (list_parts_input_new(client->pool,&list_part_input) != TOSE_OK)
    {
        tos_pool_destroy(p);
        return -1;
    }
    list_part_input->max_parts = 1000;
    tos_str_set(&list_part_input->bucket,bucket.data);
    tos_str_set(&list_part_input->key,object.data);
    tos_str_set(&list_part_input->upload_id,upload_id);

    error = list_parts(client,list_part_input,&list_part_output);
    if (error == NULL) {
        printf("List multipart succeeded\n");
        tos_list_for_each_entry(upload_part_t, part_content, &list_part_output->parts, node) {
            printf("part_number = %d, size = %ld, last_modified = %s, etag = %s\n",
                   part_content->part_number,
                   part_content->size,
                   part_content->last_modified.data,
                   part_content->etag.data);
        }
    } else {
        printf("List multipart failed, request_id:%.*s, status_code:%d, message:%.*s, ec:%.*s\n",
               error->request_id.len, error->request_id.data,
               error->status_code,
               error->message.len, error->message.data,
               error->ec.len, error->ec.data);
        tos_pool_destroy(p);
        return -1;
    }

    tos_pool_destroy(p);
    return 0;
}
```


<span id=".5Y-W5raI5YiG54mH5LiK5Lyg5Lu75Yqh"></span>
### Abort multipart uploads

You can abort a multipart upload via the AbortMultipartUpload API. After a multipart upload is aborted, TOS will delete all previously uploaded part data, and you will no longer be able to perform any operations on the multipart upload.

The following code is used to abort a multipart upload.

```C
int abort_multipart_upload_demo()
{
    // basic input
    tos_pool_t *p = NULL;
    tos_string_t bucket;
    tos_string_t object;
    tos_client_t *client = NULL;
    tos_error_t *error = NULL;
    char* upload_id = "<fill_your_upload_id>";

    // abort abort multipart upload input
    abort_multipart_upload_input_t *abort_multipart_upload_input = NULL;
    abort_multipart_upload_output_t *abort_multipart_upload_output = NULL;

    tos_pool_create(&p, NULL);
    client = tos_client_create(p);
    init_test_tos_client(client);

    tos_str_set(&bucket, TEST_BUCKET_NAME);
    tos_str_set(&object, TEST_MULTIPART_OBJECT);
    
        // abort multipart upload
    if (abort_multipart_upload_input_new(client->pool, &abort_multipart_upload_input) != TOSE_OK)
    {
        tos_pool_destroy(p);
        return -1;
    }
    tos_str_set(&abort_multipart_upload_input->bucket, TEST_BUCKET_NAME);
    tos_str_set(&abort_multipart_upload_input->key, TEST_MULTIPART_OBJECT);
    tos_str_set(&abort_multipart_upload_input->upload_id, "<fill_your_upload_id>");
        error = abort_multipart_upload(client, abort_multipart_upload_input, &abort_multipart_upload_output);
    if (error == NULL) {
        printf("Abort multipart upload succeeded, upload_id:%s\n", upload_id);
    } else {
        printf("Abort multipart upload failed, request_id:%.*s, status_code:%d, message:%.*s, ec:%.*s\n",
               error->request_id.len, error->request_id.data,
               error->status_code,
               error->message.len, error->message.data,
               error->ec.len, error->ec.data);
        tos_pool_destroy(p);
        return -1;
    }

    tos_pool_destroy(p);
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant documents


* For a detailed introduction to the API for initiating multipart uploads, please refer to [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload).

* For a detailed introduction to the API for uploading parts, please refer to [UploadPart](https://docs.byteplus.com/docs/tos/reference-uploadpart).

* For a detailed introduction to the CompleteMultipartUpload API, please refer to [CompleteMultipartUpload](https://docs.byteplus.com/docs/tos/reference-completemultipartupload).

* For a detailed introduction to the API for aborting multipart uploads, please refer to [AbortMultipartUpload](https://docs.byteplus.com/docs/tos/reference-abortmultipartupload).
