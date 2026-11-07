---
title: "Creating a file bucket"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Creating_a_file_bucket"
---

This topic introduces two methods to configure and manage file buckets: in the Supabase console and through the Admin API.

<span id="5bvYzleu"></span>
## Create file bucket in the Supabase console


1. In the Supabase console, click **Storage ** on the left to enter the **Storage** page.

2. On the **Storage** page, click  **+ New bucket**, complete the configuration in the pop\-up **Create a storage bucket** window, then click **Create** to create the bucket.

   
   |**Configuration item** |**Decscription** |
   |---|---|
   |Bucket name<br><br> |Bucket name.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Modifying the bucket name after creating the bucket is not supported.</div><br> |
   |Public bucket |Select whether to set the bucket to public.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Users can read objects in public buckets without any authorization. However, other operations (such as object upload and delete) still require row\-level security (RLS) policies.</div><br> |
   |Restrict file size |Select whether to set a file size limit for the bucket. After configuration, uploading files exceeding the specified size is prohibited.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The bucket file size limit cannot exceed the global file size limit.</div><br> |
   |Restrict MIME types |Set whether to restrict the file types for upload. After configuration, only specified file types can be uploaded to the bucket. |
   


<span id="6G9HNlFN"></span>
## **Create file bucket through Admin API**


* Query file bucket list


```Bash
# curl example to query the bucket list
curl -X GET $SUPABASE_BASE_URL/storage/v1/bucket \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}"
```



* Create a file bucket


```Bash
curl -X POST $SUPABASE_BASE_URL/storage/v1/bucket \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}"
  -H 'Content-Type: application/json' \
  -d '{
       "name": "my-bucket",
       "public": false,
       "file_size_limit": "100MB",
       "allowed_mime_types": ["image/png", "image/jpeg"]
     }'
```


<span id="DB0fwB9a"></span>
## Example \- upload and download through the Supabase Client SDK


* Upload image


```JavaScript
import { createClient } from '@supabase/supabase-js'
const supabase = createClient(
  '<SUPABASE_BASE_URL>',
  '<SUPABASE_ANON_KEY>'
)

// upload image
async function uploadImage(file) {
  const { data, error } = await supabase
    .storage
    .from('pic-bucket') // enter the bucket name
    .upload('images/' + file.name, file, {
      cacheControl: '3600',
      upsert: false // whether to overwrite files with the same name
    })

  if (error) {
    console.log('上传失败:', error.message)
    return
  }

  console.log('上传成功:', data)
  return data
}
```



* Download and convert image


```JavaScript
import { createClient } from '@supabase/supabase-js'
const supabase = createClient(
  "<SUPABASE_BASE_URL>",
  "<SUPABASE_ANON_KEY>")

// download and convert image
async function downloadAndTransformImage() {
  const { data, error } = await supabase
    .storage
    .from('pic-bucket')
    .download('pic.bmp', {
      transform: {
        width: 300,
        height: 300,
        quality: 80,
        format: 'jpg'
      }
    })

  if (error) {
    console.error('failed: ', err.message)
  } else {
    console.log('success: ', data)
  }
}
```
