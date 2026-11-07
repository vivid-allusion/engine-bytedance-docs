---
title: "Standard Presigned Signature (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-presignature-java-sdk"
---

By default, when TOSV2Client initiates a request to the server, a signature is included in the request header. The SDK also supports the generation of signed URLs, which can be used to initiate HTTP requests directly or shared with third parties to enable access authorization. This article presents corresponding examples of standard pre\-signatures.

<span id=".55Sf5oiQ55So5LqO5LiL6L2955qE6aKE562-5ZCNLXVybC3npLrkvos="></span>
## **Example of Generating a Pre\-Signed URL for Download**

The following code demonstrates how to generate a pre\-signed URL for access via the GET method.

```Java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.comm.HttpMethod;
import com.volcengine.tos.model.object.PreSignedURLInput;
import com.volcengine.tos.model.object.PreSignedURLOutput;

public class PreSignedUrlGetObjectExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        // Expiration time for the pre-signed URL, in seconds; setting to 3600 seconds means it will expire in one hour
        long expires = 3600;

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            PreSignedURLInput input = new PreSignedURLInput().setBucket(bucketName).setKey(objectKey)
                    .setHttpMethod(HttpMethod.GET).setExpires(expires);
            PreSignedURLOutput output = tos.preSignedURL(input);
            System.out.println("preSignedURL succeed, the signed url is " + output.getSignedUrl());
            System.out.println("preSignedURL succeed, the signed header is " + output.getSignedHeader());
        } catch (TosClientException e) {
            // Operation failed: a client-side exception was caught. Typically, this occurs due to invalid request parameters, and in such cases, the request is not sent.
            System.out.println("preSignedURL failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (Throwable t) {
            // Serves as a fallback to catch other exceptions; this block is generally not expected to be executed.
            System.out.println("preSignedURL failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55Sf5oiQ55So5LqO5LiK5Lyg55qE6aKE562-5ZCNLXVybC3npLrkvos="></span>
## **Example of Generating a Presigned URL for Upload**

The following code demonstrates how to generate a presigned URL for access using the PUT method.

```Java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.comm.HttpMethod;
import com.volcengine.tos.model.object.PreSignedURLInput;
import com.volcengine.tos.model.object.PreSignedURLOutput;

public class PreSignedUrlPutObjectExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        // Expiration time for the pre-signed URL, in seconds; setting to 3600 seconds will cause it to expire after 1 hour
        long expires = 3600;

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            PreSignedURLInput input = new PreSignedURLInput().setBucket(bucketName).setKey(objectKey)
                    .setHttpMethod(HttpMethod.PUT).setExpires(expires);
            PreSignedURLOutput output = tos.preSignedURL(input);
            System.out.println("preSignedURL succeed, the signed url is " + output.getSignedUrl());
            System.out.println("preSignedURL succeed, the signed header is " + output.getSignedHeader());
        } catch (TosClientException e) {
            // Operation failed: a client-side exception was caught, typically due to invalid request parameters; in this case, the request is not sent.
            System.out.println("preSignedURL failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (Throwable t) {
            // Serves as a fallback to catch other exceptions; this block is generally not expected to execute.
            System.out.println("preSignedURL failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="1fca3159"></span>
## **Example of Uploading an Object Using a Pre\-Signed URL**

The following code demonstrates how to upload an object using a generated pre\-signed URL, with okhttp client as an example.

```Java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.comm.HttpMethod;
import com.volcengine.tos.model.object.PreSignedURLInput;
import com.volcengine.tos.model.object.PreSignedURLOutput;
import okhttp3.*;

import java.io.IOException;
import java.util.concurrent.TimeUnit;

public class PreSignedUrlPutObjectWithRequestExample {
    // It is recommended to set OkHttpClient as a static singleton object when using  .
    private static OkHttpClient client;

    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        // Expiration time for the pre-signed URL, in seconds; setting to 3600 seconds means it will expire in 1 hour
        long expires = 3600;

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            PreSignedURLInput input = new PreSignedURLInput().setBucket(bucketName).setKey(objectKey)
                    .setHttpMethod(HttpMethod.PUT).setExpires(expires);
            PreSignedURLOutput output = tos.preSignedURL(input);
            System.out.println("preSignedURL succeed, the signed url is " + output.getSignedUrl());
            System.out.println("preSignedURL succeed, the signed header is " + output.getSignedHeader());
            doPutObject(output.getSignedUrl(), "Hello Volcengine TOS.");
        } catch (IOException e) {
            System.out.println("putObject failed");
            e.printStackTrace();
        } catch (TosClientException e) {
            // Operation failed: a client-side exception was caught, typically due to invalid request parameters; in this case, the request was not sent.
            System.out.println("preSignedURL failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (Throwable t) {
            // This block serves as a fallback to capture other exceptions; it is generally not expected to be executed.
            System.out.println("preSignedURL failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }

    private static void doPutObject(String url, String content) throws IOException {
        if (client == null) {
            ConnectionPool connectionPool = new ConnectionPool(1024, 60000, TimeUnit.MILLISECONDS);
            Dispatcher dispatcher = new Dispatcher();
            OkHttpClient.Builder builder = new OkHttpClient.Builder();
            client = builder.dispatcher(dispatcher)
                    .connectionPool(connectionPool).retryOnConnectionFailure(true).connectTimeout(10000, TimeUnit.MILLISECONDS)
                    .readTimeout(30000, TimeUnit.MILLISECONDS).writeTimeout(30000, TimeUnit.MILLISECONDS)
                    .followRedirects(false).followSslRedirects(false).build();
        }
        Request.Builder builder = new Request.Builder().url(url);
        builder.put(RequestBody.create(MediaType.parse("binary/octet-stream"), content));
        Response response = null;
        try{
            response = client.newCall(builder.build()).execute();
        } finally{
            if (response != null) {
                response.close();
            }
        }
    }
}
```


<span id="8bdd45c7"></span>
## **Example of Downloading an Object Using a Pre\-Signed URL**

The following code demonstrates how to download an object using a generated pre\-signed URL, with okhttp client as an example.

```Java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.comm.HttpMethod;
import com.volcengine.tos.model.object.PreSignedURLInput;
import com.volcengine.tos.model.object.PreSignedURLOutput;
import com.volcengine.tos.model.object.PutObjectInput;
import okhttp3.*;

import java.io.ByteArrayInputStream;
import java.io.ByteArrayOutputStream;
import java.io.IOException;
import java.util.concurrent.TimeUnit;

public class PreSignedUrlGetObjectWithRequestExample {
    // It is recommended to set OkHttpClient as a static singleton object when using .
    private static OkHttpClient client;

    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        // Expiration time for the pre-signed URL, in seconds; set to 3600 seconds to expire after 1 hour
        long expires = 3600;

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            Upload the data first.
            tos.putObject(new PutObjectInput().setBucket(bucketName).setKey(objectKey)
                    .setContent(new ByteArrayInputStream("Hello Volcengine TOS.".getBytes())));

            PreSignedURLInput input = new PreSignedURLInput().setBucket(bucketName).setKey(objectKey)
                    .setHttpMethod(HttpMethod.GET).setExpires(expires);
            PreSignedURLOutput output = tos.preSignedURL(input);
            System.out.println("preSignedURL succeed, the signed url is " + output.getSignedUrl());
            System.out.println("preSignedURL succeed, the signed header is " + output.getSignedHeader());
            String content = doGetObject(output.getSignedUrl());
            System.out.println("getObject to String succeed, the content is " + content);
        } catch (IOException e) {
            System.out.println("getObject to String failed");
            e.printStackTrace();
        } catch (TosClientException e) {
            // Operation failed: a client-side exception was caught, typically due to invalid request parameters; in this case, the request is not sent.
            System.out.println("preSignedURL failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (Throwable t) {
            // Serves as a catch-all for other exceptions; this block is generally not expected to be executed.
            System.out.println("preSignedURL failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }

    private static String doGetObject(String url) throws IOException {
        if (client == null) {
            ConnectionPool connectionPool = new ConnectionPool(1024, 60000, TimeUnit.MILLISECONDS);
            Dispatcher dispatcher = new Dispatcher();
            OkHttpClient.Builder builder = new OkHttpClient.Builder();
            client = builder.dispatcher(dispatcher)
                    .connectionPool(connectionPool).retryOnConnectionFailure(true).connectTimeout(10000, TimeUnit.MILLISECONDS)
                    .readTimeout(30000, TimeUnit.MILLISECONDS).writeTimeout(30000, TimeUnit.MILLISECONDS)
                    .followRedirects(false).followSslRedirects(false).build();
        }
        Request.Builder builder = new Request.Builder().url(url);
        Response response = client.newCall(builder.get().build()).execute();
        if (response == null || response.body() == null) {
            return null;
        }
        ByteArrayOutputStream result = new ByteArrayOutputStream();
        byte[] buffer = new byte[1024];
        int length;
        while ((length = response.body().byteStream().read(buffer)) != -1) {
            result.write(buffer, 0, length);
        }
        result.flush();
        return result.toString("UTF-8");
    }
}
```


<span id="e66401c9"></span>
## **Example of generating a pre\-signed URL for image processing**

The following code demonstrates how to perform image processing using a generated pre\-signed URL, with okhttp client as an example.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.comm.HttpMethod;
import com.volcengine.tos.comm.TosHeader;
import com.volcengine.tos.model.object.PreSignedURLInput;
import com.volcengine.tos.model.object.PreSignedURLOutput;
import okhttp3.*;

import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.util.HashMap;
import java.util.Map;
import java.util.concurrent.TimeUnit;

public class PreSignedUrlImageProcessWithRequestExample {
    // It is recommended to set OkHttpClient as a static singleton object when using.
    private static OkHttpClient client;

    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        // Ensure that the object to be processed already exists
        String objectKey = "image.png";
        String filePath = "example_dir/image.jpg";

        String style = "image/resize,h_100/format,jpg"; //Set the image height to 100px and convert it to JPG format
        Map<String, String> query = new HashMap<>();
        query.put(TosHeader.QUERY_DATA_PROCESS, style);
        // Expiration time for the pre-signed URL, in seconds; set to 3600 seconds to expire after 1 hour
        long expires = 3600;

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try {
            PreSignedURLInput input = new PreSignedURLInput().setBucket(bucketName).setKey(objectKey).setQuery(query)
                    .setHttpMethod(HttpMethod.GET).setExpires(expires);
            PreSignedURLOutput output = tos.preSignedURL(input);
            System.out.println("preSignedURL succeed, the signed url is " + output.getSignedUrl());
            System.out.println("preSignedURL succeed, the signed header is " + output.getSignedHeader());
            doGetObject(output.getSignedUrl(), filePath);
        } catch (IOException e) {
            System.out.println("getObject to String failed");
            e.printStackTrace();
        } catch (TosClientException e) {
            // Operation failed: a client-side exception was caught. Typically, this occurs due to invalid request parameters, and the request is not sent in such cases.
            System.out.println("preSignedURL failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (Throwable t) {
            // Serves as a catch-all for other exceptions; this block is rarely executed.
            System.out.println("preSignedURL failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }

    private static void doGetObject(String url, String filePath) throws IOException {
        if (client == null) {
            ConnectionPool connectionPool = new ConnectionPool(1024, 60000, TimeUnit.MILLISECONDS);
            Dispatcher dispatcher = new Dispatcher();
            OkHttpClient.Builder builder = new OkHttpClient.Builder();
            client = builder.dispatcher(dispatcher)
                    .connectionPool(connectionPool).retryOnConnectionFailure(true).connectTimeout(10000, TimeUnit.MILLISECONDS)
                    .readTimeout(30000, TimeUnit.MILLISECONDS).writeTimeout(30000, TimeUnit.MILLISECONDS)
                    .followRedirects(false).followSslRedirects(false).build();
        }
        Request.Builder builder = new Request.Builder().url(url);
        Response response = client.newCall(builder.get().build()).execute();
        if (response == null || response.body() == null) {
            System.out.println("image process failed");
            return;
        }

        // The following code demonstrates how to download transcoded image data to a local device.
        try (FileOutputStream fileOutputStream = new FileOutputStream(filePath);
             InputStream output = response.body().byteStream()) {
            byte[] buffer = new byte[1024];
            int length;
            while ((length = output.read(buffer)) != -1) {
                fileOutputStream.write(buffer, 0, length);
            }
            System.out.println("image process succeed");
        } catch (IOException e) {
            System.out.println("write data to file failed");
            e.printStackTrace();
        }
    }
}
```


<span id="c0c3c655"></span>
## **Example of Generating a Pre\-Signed URL for Document Preview**

The following code demonstrates how to perform document preview using the generated pre\-signed URL, using okhttp client as an example.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.comm.HttpMethod;
import com.volcengine.tos.comm.TosHeader;
import com.volcengine.tos.model.object.PreSignedURLInput;
import com.volcengine.tos.model.object.PreSignedURLOutput;
import okhttp3.OkHttpClient;

import java.util.HashMap;
import java.util.Map;

public class PreSignedUrlDocProcessWithRequestExample {
    // It is recommended to configure OkHttpClient as a static singleton object when using.
    private static OkHttpClient client;

    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        // Ensure that the object to be processed exists
        String objectKey = "image.png";

        String style = "doc-preview"; //Mark as document preview request
        String sourceType = "docx";  // Original document type: docx
        String destType = "jpg";   // Preview type: jpg
        String docPage = "1";  // Handle page numbers
        Map<String, String> query = new HashMap<>();
        query.put(TosHeader.QUERY_DATA_PROCESS, style);
        query.put("x-tos-doc-src-type", sourceType);
        query.put("x-tos-doc-dst-type", destType);
        query.put("x-tos-doc-page", docPage);

        // Expiration time for the pre-signed URL, in seconds; set to 3600 seconds to expire after 1 hour
        long expires = 3600;

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try {
            PreSignedURLInput input = new PreSignedURLInput().setBucket(bucketName).setKey(objectKey).setQuery(query)
                    .setHttpMethod(HttpMethod.GET).setExpires(expires);
            PreSignedURLOutput output = tos.preSignedURL(input);
            System.out.println("preSignedURL succeed, the signed url is " + output.getSignedUrl());
            System.out.println("preSignedURL succeed, the signed header is " + output.getSignedHeader());
        } catch (TosClientException e) {
            // Operation failed: a client-side exception was caught, typically due to invalid request parameters; in this case, the request is not sent.
            System.out.println("preSignedURL failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (Throwable t) {
            // Serves as a catch-all for other exceptions; this block is generally not executed.
            System.out.println("preSignedURL failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For detailed information on URLs containing signatures, refer to [URLs Containing Signatures](https://docs.byteplus.com/docs/tos/reference-including-a-signature-in-the-url).
