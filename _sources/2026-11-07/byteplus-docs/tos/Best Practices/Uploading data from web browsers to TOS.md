---
title: "Uploading data from web browsers to TOS"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Web-direct-upload-practice"
---

You can use the PostObject API to upload content directly from a web browser as an HTML form to TOS. The signature required for the upload can be obtained from the server.

For more information, refer to [PostObject](https://docs.byteplus.com/docs/tos/reference-postobject) and [Pre-signed POST Form (Node.js SDK)](https://docs.byteplus.com/docs/tos/Post-form-presignature-node-js-sdk).

<span id="1d79c5ad"></span>
## Procedure

<span id="fc9088c4"></span>
### Step 1: Create a CORS rule

When data is uploaded from a web browser, a cross\-origin request is sent to TOS. TOS then verifies permissions by checking the bucket’s cross\-origin resource sharing (CORS) rules. To ensure that web browsers can transfer data to TOS correctly, you must set up CORS rules in TOS. For more information, see [Cross-Origin Access Settings](https://docs.byteplus.com/docs/tos/docs-cross-origin-resource-sharing-settings).


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**. On the **Buckets** page, click the target bucket name.

3. In the left navigation pane, select **Permissions \> ** **CORS rules** **.** 

4. On the **CORS rules** page, click **Create rule**.

5. On the **Create CORS rule** page, configure the following parameters.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ed4a6c6ca78e3d536d324bb163b5bd24.png) </span>

&nbsp;

   
   |**Parameter** |**Description** |
   |---|---|
   |Origin |Enter the domain name for browser\-based uploads.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can use a wildcard (\*) to allow all origins.</div><br> |
   |Operation methods |Select **PUT**, **GET**, **POST**, **DELETE**, and **HEAD**. |
   |Allow\-Headers |Enter a wildcard (\*). |
   |Expose\-Headers |Enter ETag, x\-tos\-request\-id, and x\-tos\-version\-id. Multiple entries are permitted, with each entry separated by a carriage return. |
   |Cache Max\-Age |Use the default value. |
   

&nbsp;

6. Click **Create**.


<span id="a79ee8dc"></span>
### Step 2: Configure the server

Refer to the following code to obtain the signature on the server side

```TypeScript
import express from "express";
import TosClient from "@volcengine/tos-sdk";
const app = express();
const PORT = process.env.PORT || 8000; // Service request port number

const getSignature = async (bucket: string,key: string) => {
  const client = new TosClient({
    accessKeyId: "Provide your access key", //  Temporary AccessKey ID obtained from the STS service
    accessKeySecret: "Provide your secret key", //  Temporary AccessKey Secret obtained from the STS service
    stsToken: "Provide your session token", // Temporary security token
    region: "Provide your region", // Specify the region where the bucket is located. For example, for Beijing (North China 2), set this to "cn-beijing".
    endpoint: "Provide your endpoint" // Specify the service endpoint. For example, for Beijing (North China 2), set this to "tos-cn-beijing.bytepluses.com.cn".
  });
  const res = await client.preSignedPostSignature({
    bucket, // Specify your bucket name, for example, examplebucket.
    key,
  });
  return res;
};


app.get("/get_post_signature", async (req, res) => {
  try {
    const key = req.query.key as string; // Retrieve the key from request parameters
    const bucket = req.query.bucket as string; // Retrieve the bucket from request parameters
    const result = await getSignature(bucket, key);
    res.setHeader("Access-Control-Allow-Origin", "*"); // Allow cross-origin requests
    res.setHeader("Access-Control-Allow-Headers", "*"); // Allow headers in cross-origin requests
    res.setHeader("Access-Control-Allow-Methods", "*"); //  Allow methods in cross-origin requests
    res.json(result); //  Return the generated signature data
  } catch (error) {
    console.error("Error generating signature:", error);
    res.status(500).send("Error generating signature");
  }
});


app.listen(PORT, () => {
  console.log(`Server is running on http://127.0.0.1:${PORT}`); 
});
```


You need to replace the following parameters in the sample code according to your actual situation:


|**Parameter** |**Description** |
|---|---|
|accessKeyId |Temporary Access Key ID obtained from Security Token Service (STS).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can create a temporary access credential through the STS service to get temporary keys. For detailed operations, see <a href="https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service">Accessing TOS with temporary credentials of Security Token Service</a>.</div><br> |
|accessKeySecret |Temporary Secret Access Key obtained from STS. |
|stsToken |Temporary access Session Token obtained from STS. |
|region |Region where the bucket is located. |
|endpoint |Access domain name of the bucket.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For detailed information about bucket domain names, see <a href="https://docs.byteplus.com/docs/tos/docs-region-and-endpoint">Regions and endpoints</a>.</div><br> |


<span id="2986f4c2"></span>
### Step 3: Configure the client code

You can refer to the following code to upload files on the client side.

```HTML
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Upload file to TOS</title>
  </head>
  <body>
    <div class="container">
      <form>
        <div>
          <label for="file" class="form-label">Select file:</label>
          <input type="file" id="file" name="file" required />
        </div>
        <button type="submit">Upload</button>
      </form>
    </div>
    <script>
      const form = document.querySelector("form");
      const url = "http://127.0.0.1:8000/get_post_signature"
      const bucket = "example-bucket";
      //Enter the domain name according to the actual Region; here, cn-beijing is used as an example
      const endpoint = "tos-cn-beijing.bytepluses.com.cn"
      form.addEventListener("submit", async (event) => {
        event.preventDefault();
        const fileInput = document.getElementById("file");
        const file = fileInput.files[0];
        if (!file) {
          alert("Please select a file");
          return;
        }
        console.log(file);
        const key = file.name;
        fetch(
          `${url}?key=${key}&bucket=${bucket}`,
          {
            method: "GET",
          }
        )
          .then((response) => {
            return response.json();
          })
          .then((data) => {
            const bucketHost = `${bucket}.${endpoint}`;
            const url = `https://${bucketHost}/${encodeURI(key)}`;
            const formData = new FormData();
            formData.append("key", data.key);
            formData.append("policy", data.policy);
            formData.append('x-tos-algorithm', data['x-tos-algorithm']);
            formData.append('x-tos-credential', data['x-tos-credential']);
            formData.append('x-tos-date', data['x-tos-date']);
            formData.append('x-tos-signature', data['x-tos-signature']);
            formData.append("x-tos-security-token", data["x-tos-security-token"]);
            formData.append("file", file);
            return fetch(url, {
              method: "POST",
              body: formData,
            });
          })
          .then((response) => {
            if (response.ok) {
              console.log("Upload successful");
              alert("File uploaded");
            } else {
              console.log("Upload failed", response);
              alert("Upload failed, please try again later");
            }
          })
          .catch((error) => {
            console.error("An error occurred:", error);
          });
      });
    </script>
  </body>
</html>
```


You need to replace the following parameters in the sample code according to your actual situation:


|**Parameter** |**Description** |
|---|---|
|url |Your server\-side URL. |
|bucket |Name of the bucket where the object needs to be stored. |
|endpoint |The bucket's access domain name.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For detailed information about bucket domain names, see <a href="https://docs.byteplus.com/docs/tos/docs-region-and-endpoint">Regions and endpoints</a>.</div><br> |
