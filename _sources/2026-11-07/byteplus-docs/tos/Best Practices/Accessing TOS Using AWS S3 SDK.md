---
title: "Accessing TOS Using AWS S3 SDK"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Accessing_TOS_Using_AWS_S3_SDK"
---

This article provides a comprehensive best practice guide to help you quickly and correctly configure AWS S3 SDKs across major programming languages to connect and operate TOS.

<span id="55e4dfb3"></span>
## Overview

TOS offers an API interface compatible with Amazon S3. This means you can leverage the feature\-rich and well\-supported AWS S3 SDK to seamlessly access and manage storage resources on TOS with simple configuration.


* **Unified technology stack**: manage storage services from different cloud vendors in a multi\-cloud environment using the same AWS S3 SDK, simplifying development and maintenance.

* **Smooth migration**: when migrating applications from AWS S3 or other S3\-compatible storage services to TOS, you only need to modify client configurations without changing business logic code.

* **Leverage a mature ecosystem**: enjoy a stable and efficient development experience with AWS S3 SDKs and access abundant examples and solutions from the community.


<span id="14d0a658"></span>
## Prerequisites


* You have created a standard bucket.

* The recommended signature version for the SDK is `v4` (`s3v4`) to ensure connection security.

* BytePlus TOS domain names compatible with S3 **only support virtual\-hosted style (** `Virtual-hosted Style` **)**  and do not support path style (`Path-style`). Therefore, when configuring the SDK, you must **enforce or default to using virtual\-hosted style**. If the SDK defaults to path style, you need to explicitly disable it. This is crucial to ensure successful connection.


<span id="d3886c65"></span>
## Obtain your access key (AK/SK)


* Region: The region where your TOS bucket is located, for example, `cn-beijing`.

* Access Key: Includes Access Key ID (AK) and Secret Access Key (SK), credentials for accessing TOS API.

* Endpoint: Optional.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For a list of TOS regions and endpoints, see <a href="https://docs.byteplus.com/docs/tos/docs-region-and-endpoint">Regions and endpoints</a>.   </div>
   

<span id="cdf0d3d1"></span>
## Configure access credentials

Before initializing the SDK, you must first set up long\-term access credentials. This process differs depending on the operating system.


<Tabs>
<Tab zoneid="hlGPCC77DP" title="macOS">
<TabTitle>macOS</TabTitle>

1. Open Terminal and run this command to open the file.


```Shell
nano ~/.bash_profile
```



2. Add your access key ID and secret access key at the end of the file.


```Shell
export TOS_ACCESS_KEY=AKTP**********
export TOS_SECRET_KEY=T1dJ**********
```



3. Save the file and exit.

4. Run this command to apply the configuration.


```Shell
source ~/.bash_profile
```



5. Run this command to verify the configuration.


```Shell
echo $TOS_ACCESS_KEY
echo $TOS_SECRET_KEY
```


The following output confirms a successful configuration:

```Shell
AKTP**********
T1dJ**********
```



</Tab>
<Tab zoneid="sxSZbtIzEr" title="Linux">
<TabTitle>Linux</TabTitle>

1. Open Terminal and run this command to open the file.


```Shell
sudo vim /etc/profile
```



2. Add your access key ID and secret access key at the end of the file.


```Shell
export TOS_ACCESS_KEY=AKTP**********
export TOS_SECRET_KEY=T1dJ**********
```



3. Save the file and exit.

4. Run this command to apply the configuration.


```Shell
source /etc/profile
```



5. Run this command to verify the configuration.


```Shell
echo $TOS_ACCESS_KEY
echo $TOS_SECRET_KEY
```


The following output confirms a successful configuration.


```Shell
AKTP**********
T1dJ**********
```



</Tab>
<Tab zoneid="G2JZvDsIjh" title="Windows">
<TabTitle>Windows</TabTitle>

1. Open the command line interface and run this command to enter your access key ID and secret access key.


```Shell
set TOS_ACCESS_KEY=AKTP**********
set TOS_SECRET_KEY=T1dJ**********
```



2. Run this command to apply the configuration.


```Shell
setx TOS_ACCESS_KEY "%TOS_ACCESS_KEY%"
setx TOS_SECRET_KEY "%TOS_SECRET_KEY%"
```



3. Restart the command line interface and run this command to verify the configuration.


```Shell
echo %TOS_ACCESS_KEY%
echo %TOS_SECRET_KEY%
```


If the configuration is successful, the following output appears:


```Shell
AKTP**********
T1dJ**********
```



</Tab>
</Tabs>


<span id="deeccfdf"></span>
## SDK configuration example


<Tabs>
<Tab zoneid="bzqFcVq2xJ" title="Java">
<TabTitle>Java</TabTitle>

We recommend using AWS SDK for Java v2, which offers a more modern API and better performance.

<span id="a5eedda4"></span>
### Environment

Please ensure your development environment has JDK 8 or higher installed.

<span id="3be78ca6"></span>
### Dependency configuration

**Maven**

Add the following dependencies to your `pom.xml` file:

```XML
<dependency>
    <groupId>software.amazon.awssdk</groupId>
    <artifactId>s3</artifactId>
    <version>2.25.27</version>
</dependency>
```


**Gradle**

Add the following dependencies to your `build.gradle` file:

```Plain Text
implementation 'software.amazon.awssdk:s3:2.25.27'
```


<span id="1fc072b1"></span>
#### Complete code example

The following example shows how to initialize S3Client and perform basic operations.

```Java
import software.amazon.awssdk.auth.credentials.AwsBasicCredentials;
import software.amazon.awssdk.auth.credentials.StaticCredentialsProvider;
import software.amazon.awssdk.core.ResponseBytes;
import software.amazon.awssdk.core.sync.RequestBody;
import software.amazon.awssdk.core.sync.ResponseTransformer;
import software.amazon.awssdk.regions.Region;
import software.amazon.awssdk.services.s3.S3Client;
import software.amazon.awssdk.services.s3.model.*;

import java.io.IOException;
import java.net.URI;
import java.nio.file.Files;
import java.nio.file.Paths;

public class TosS3JavaBestPractice {

    public static void main(String[] args) {
        // 1. Configure authentication information and access endpoint
        final String endpoint = "https://tos-s3-cn-beijing.volces.com";
        final String region = "cn-beijing";
        final String accessKey = System.getenv("VOLCENGINE_ACCESS_KEY_ID");
        final String secretKey = System.getenv("VOLCENGINE_SECRET_ACCESS_KEY");

        // 2. Initialize the S3 client
        // Note: AWS SDK for Java v2 uses virtual-hosted style by default
        // To explicitly disable path-style (required for some older versions or special configurations), use .forcePathStyle(false)
        S3Client s3Client = S3Client.builder()
                .endpointOverride(URI.create(endpoint))
                .region(Region.of(region))
                .credentialsProvider(StaticCredentialsProvider.create(
                        AwsBasicCredentials.create(accessKey, secretKey)))
                .build();

        String bucketName = "your-unique-bucket-name-" + System.currentTimeMillis();
        String objectKey = "my-object-key";
        String localFilePath = "local-file.txt";
        String downloadFilePath = "downloaded-file.txt";

        try {
            // Prepare local files
            Files.write(Paths.get(localFilePath), "Hello, Volcengine TOS!".getBytes());

            // 3. Create a bucket
            System.out.println("Creating bucket: " + bucketName);
            s3Client.createBucket(CreateBucketRequest.builder().bucket(bucketName).build());
            System.out.println("Bucket created successfully.");

            // 4. Upload objects
            System.out.println("Uploading object to " + bucketName);
            s3Client.putObject(PutObjectRequest.builder()
                    .bucket(bucketName)
                    .key(objectKey)
                    .build(), RequestBody.fromFile(Paths.get(localFilePath)));
            System.out.println("Object uploaded successfully.");

            // 5. List objects
            System.out.println("Listing objects in bucket: " + bucketName);
            ListObjectsV2Response listObjectsV2Response = s3Client.listObjectsV2(ListObjectsV2Request.builder()
                    .bucket(bucketName).build());
            for (S3Object s3Object : listObjectsV2Response.contents()) {
                System.out.println("- " + s3Object.key());
            }

            // 6. Download objects
            System.out.println("Downloading object: " + objectKey);
            ResponseBytes<GetObjectResponse> objectBytes = s3Client.getObject(
                    GetObjectRequest.builder().bucket(bucketName).key(objectKey).build(),
                    ResponseTransformer.toBytes());
            Files.write(Paths.get(downloadFilePath), objectBytes.asByteArray());
            System.out.println("Object downloaded successfully to " + downloadFilePath);

            // 7. Delete objects
            System.out.println("Deleting object: " + objectKey);
            s3Client.deleteObject(DeleteObjectRequest.builder().bucket(bucketName).key(objectKey).build());
            System.out.println("Object deleted successfully.");

            // 8. Delete bucket
            System.out.println("Deleting bucket: " + bucketName);
            s3Client.deleteBucket(DeleteBucketRequest.builder().bucket(bucketName).build());
            System.out.println("Bucket deleted successfully.");

        } catch (S3Exception | IOException e) {
            System.err.println("Error: " + e.getMessage());
            e.printStackTrace();
        } finally {
            // Clean local files
            try {
                Files.deleteIfExists(Paths.get(localFilePath));
                Files.deleteIfExists(Paths.get(downloadFilePath));
            } catch (IOException ex) {
                System.err.println("Failed to clean up local files: " + ex.getMessage());
            }
            s3Client.close();
        }
    }
}
```



</Tab>
<Tab zoneid="jj1ydVxe9Y" title="Python">
<TabTitle>Python</TabTitle>

Use the `boto3` library to interact with the TOS S3 compatible interface.

<span id="8433d2ff"></span>
### Environment

Ensure your development environment has Python 3.5, 3.6, 3.7, 3.8, or a later version installed.

<span id="8ca0eea6"></span>
### Install boto3

Install `boto3` using pip:

```Bash
pip install boto3
```


<span id="832387f5"></span>
### Complete code example

The following example shows how to initialize the S3 client and perform basic operations.

```Python
import boto3
from botocore.config import Config
from botocore.exceptions import ClientError
import os
import time

def main():
    # 1. configure credentials and access endpoints
    endpoint = "https://tos-s3-cn-beijing.volces.com"
    region = "cn-beijing"
    access_key = os.getenv("VOLCENGINE_ACCESS_KEY_ID")
    secret_key = os.getenv("VOLCENGINE_SECRET_ACCESS_KEY")

    # 2. Initialize the S3 client
    # Key configuration:
    # - endpoint_url: points to the TOS S3 domain
    # - region_name: must be provided even if endpoint_url is specified
    # - config:
    #   - signature_version: 's3v4'
    #   - s3: {'addressing_style': 'virtual'} enforces virtual-hosted–style addressing
    s3_client = boto3.client(
        's3',
        endpoint_url=endpoint,
        aws_access_key_id=access_key,
        aws_secret_access_key=secret_key,
        region_name=region,
        config=Config(
            signature_version='s3v4',
            s3={'addressing_style': 'virtual'}  # Explicitly specify virtual-hosted style
        )
    )

    bucket_name = f"your-unique-bucket-name-{int(time.time())}"
    object_key = "my-object-key"
    local_file_path = "local-file.txt"
    download_file_path = "downloaded-file.txt"

    try:
        # Prepare local files
        with open(local_file_path, "w") as f:
            f.write("Hello, Volcengine TOS!")

        # 3. Create a bucket
        print(f"Creating bucket: {bucket_name}")
        # Do not specify LocationConstraint for the cn-beijing region
        s3_client.create_bucket(Bucket=bucket_name)
        print("Bucket created successfully.")

        # 4. Upload objects
        print(f"Uploading object to {bucket_name}")
        s3_client.upload_file(local_file_path, bucket_name, object_key)
        print("Object uploaded successfully.")

        # 5. List objects
        print(f"Listing objects in bucket: {bucket_name}")
        response = s3_client.list_objects_v2(Bucket=bucket_name)
        if 'Contents' in response:
            for obj in response['Contents']:
                print(f"- {obj['Key']}")

        # 6. Download objects
        print(f"Downloading object: {object_key}")
        s3_client.download_file(bucket_name, object_key, download_file_path)
        print(f"Object downloaded successfully to {download_file_path}")

        # 7. Delete objects
        print(f"Deleting object: {object_key}")
        s3_client.delete_object(Bucket=bucket_name, Key=object_key)
        print("Object deleted successfully.")

        # 8. Delete bucket
        print(f"Deleting bucket: {bucket_name}")
        s3_client.delete_bucket(Bucket=bucket_name)
        print("Bucket deleted successfully.")

    except ClientError as e:
        print(f"Error: {e}")
    finally:
        # Remove a local file
        if os.path.exists(local_file_path):
            os.remove(local_file_path)
        if os.path.exists(download_file_path):
            os.remove(download_file_path)

if __name__ == "__main__":
    main()
```



</Tab>
<Tab zoneid="VykIHgaywb" title="Go">
<TabTitle>Go</TabTitle>

Develop using `aws-sdk-go-v2`.

<span id="9e5718f2"></span>
### Environment

Ensure your development environment has Golang 1.13 or later installed. You can download the installer from the [Golang official website](https://go.dev/).

<span id="38f26b4e"></span>
### configuration and installation

Run the following command to install the required modules for the example:

```Bash
go get github.com/aws/aws-sdk-go-v2/config
go get github.com/aws/aws-sdk-go-v2/credentials
go get github.com/aws/aws-sdk-go-v2/service/s3
```


<span id="29d0a80f"></span>
### complete code example

```Go
package main 
import ( 
        "context" 
        "fmt" 
        "io/ioutil" 
        "os" 
        "strconv" 
        "time" 
 
        "github.com/aws/aws-sdk-go-v2/aws" 
        "github.com/aws/aws-sdk-go-v2/config" 
        "github.com/aws/aws-sdk-go-v2/credentials" 
        "github.com/aws/aws-sdk-go-v2/service/s3" 
        // "github.com/aws/aws-sdk-go-v2/service/s3/types" // [Fix 1] Remove unused package to avoid compile errors
) 
 
func main() { 
        // 1. Configure credentials and access endpoint
        endpoint := "https://tos-s3-cn-beijing.volces.com" 
        region := "cn-beijing" 
        accessKey := os.Getenv("VOLCENGINE_ACCESS_KEY_ID") 
        secretKey := os.Getenv("VOLCENGINE_SECRET_ACCESS_KEY") 
 
        // 2. Initialize the S3 client
        customResolver := aws.EndpointResolverWithOptionsFunc(func(service, r string, options ...interface{}) (aws.Endpoint, error) { 
                 return aws.Endpoint{ 
                 URL: endpoint, 
                 SigningRegion: region, 
                 HostnameImmutable: false, // [Fix 2] must be false! // Otherwise, it will break the Virtual-Hosted addressing mode required by TOS
                 }, nil 
               }) 
 
        cfg, err := config.LoadDefaultConfig(context.TODO(), 
                 config.WithRegion(region), 
                 config.WithCredentialsProvider(credentials.NewStaticCredentialsProvider(accessKey, secretKey, "")), 
                 config.WithEndpointResolverWithOptions(customResolver), 
                ) 
        if err != nil { 
             fmt.Printf("failed to load configuration, %v\n", err) 
             return 
        } 
 
        // Set UsePathStyle to false
        s3Client := s3.NewFromConfig(cfg, func(o *s3.Options) { 
                 o.UsePathStyle = false 
                }) 
 
        bucketName := "your-unique-bucket-name-" + strconv.FormatInt(time.Now().Unix(), 10) 
        objectKey := "my-object-key" 
        localFilePath := "local-file.txt" 
        downloadFilePath := "downloaded-file.txt" 
 
        // Prepare local files
        err = ioutil.WriteFile(localFilePath, []byte("Hello, Volcengine TOS!"), 0644) 
        if err != nil { 
             fmt.Printf("failed to create local file, %v\n", err) 
             return 
           } 
        defer os.Remove(localFilePath) 
 
        // 3. Creating buckets
        fmt.Printf("Creating bucket: %s\n", bucketName) 
        _, err = s3Client.CreateBucket(context.TODO(), &s3.CreateBucketInput{ 
         Bucket: aws.String(bucketName), 
        }) 
        if err != nil { 
         fmt.Printf("failed to create bucket, %v\n", err) 
         return 
         } 
        fmt.Println("Bucket created successfully.") 
 
        // Deleting buckets
         defer func() { 
         fmt.Printf("Deleting bucket: %s\n", bucketName) 
         _, err = s3Client.DeleteBucket(context.TODO(), &s3.DeleteBucketInput{ 
         Bucket: aws.String(bucketName), 
         }) 
         if err != nil { 
         fmt.Printf("failed to delete bucket, %v\n", err) 
         } else { 
         fmt.Println("Bucket deleted successfully.") 
         } 
         }
    
        // 4. Upload objects
        fmt.Printf("Uploading object to %s\n", bucketName) 
        file, err := os.Open(localFilePath) 
        if err != nil { 
         fmt.Printf("failed to open file, %v\n", err) 
         return 
        } 
        defer file.Close() 
 
        _, err = s3Client.PutObject(context.TODO(), &s3.PutObjectInput{ 
         Bucket: aws.String(bucketName), 
         Key: aws.String(objectKey), 
         Body: file, 
        }) 
        if err != nil { 
         fmt.Printf("failed to upload object, %v\n", err) 
         return 
        } 
        fmt.Println("Object uploaded successfully.") 
 
        // Delete objects
         defer func() { 
         fmt.Printf("Deleting object: %s\n", objectKey) 
         _, err = s3Client.DeleteObject(context.TODO(), &s3.DeleteObjectInput{ 
         Bucket: aws.String(bucketName), 
         Key: aws.String(objectKey), 
         }) 
         if err != nil { 
         fmt.Printf("failed to delete object, %v\n", err) 
         } else { 
         fmt.Println("Object deleted successfully.") 
         } 
         }
 
        // 5. List objects
        fmt.Printf("Listing objects in bucket: %s\n", bucketName) 
        listOutput, err := s3Client.ListObjectsV2(context.TODO(), &s3.ListObjectsV2Input{ 
         Bucket: aws.String(bucketName), 
        }) 
        if err != nil { 
         fmt.Printf("failed to list objects, %v\n", err) 
         return 
        } 
        for _, object := range listOutput.Contents { 
         fmt.Printf("- %s\n", *object.Key) 
        } 
 
        // 6. Download objects
        fmt.Printf("Downloading object: %s\n", objectKey) 
        getOutput, err := s3Client.GetObject(context.TODO(), &s3.GetObjectInput{ 
         Bucket: aws.String(bucketName), 
         Key: aws.String(objectKey), 
        }) 
        if err != nil { 
         fmt.Printf("failed to download object, %v\n", err) 
         return 
        } 
        defer getOutput.Body.Close() 
 
        body, err := ioutil.ReadAll(getOutput.Body) 
        if err != nil { 
         fmt.Printf("failed to read object body, %v\n", err) 
         return 
        } 
        err = ioutil.WriteFile(downloadFilePath, body, 0644) 
        if err != nil { 
         fmt.Printf("failed to write downloaded file, %v\n", err) 
         return 
        } 
        defer os.Remove(downloadFilePath) 
        fmt.Printf("Object downloaded successfully to %s\n", downloadFilePath) 
}
```



</Tab>
<Tab zoneid="iwrgBiZNLb" title="C++">
<TabTitle>C++</TabTitle>

Develop using `aws-sdk-cpp`. Note that building and integrating the C++ SDK is relatively complex; be sure to follow the official documentation for environment setup.

<span id="74d9b0bb"></span>
### Environment

Ensure your development environment has C++ 11 or later installed.

<span id="643b941a"></span>
### Configuration and installation

You need to build `aws-sdk-cpp` from source code.


1. Clone the repository: `git clone --recurse-submodules https://github.com/aws/aws-sdk-cpp`

2. Build and install:


```Bash
cd aws-sdk-cpp
mkdir build
cd build
cmake .. -DBUILD_ONLY="s3" -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local
make
sudo make install
```


<span id="6652631c"></span>
### Complete code example

Make sure your `CMakeLists.txt` correctly links to `aws-sdk-cpp`:

```CMake
find_package(AWSSDK REQUIRED COMPONENTS s3)
...
target_link_libraries(your-target PRIVATE ${AWSSDK_LIBRARIES})
```


**Code examples:** 

```C++
#include <iostream>
#include <fstream>
#include <aws/core/Aws.h>
#include <aws/core/auth/AWSCredentialsProvider.h>
#include <aws/core/client/ClientConfiguration.h>
#include <aws/s3/S3Client.h>
#include <aws/s3/model/CreateBucketRequest.h>
#include <aws/s3/model/PutObjectRequest.h>
#include <aws/s3/model/GetObjectRequest.h>
#include <aws/s3/model/ListObjectsV2Request.h>
#include <aws/s3/model/DeleteObjectRequest.h>
#include <aws/s3/model/DeleteBucketRequest.h>
#include <chrono>

int main() {
    Aws::SDKOptions options;
    Aws::InitAPI(options);
    {
        // 1. Configure authentication information and access endpoints
        const Aws::String endpoint = "tos-s3-cn-beijing.volces.com";
        const Aws::String region = "cn-beijing";
        const Aws::String accessKey = std::getenv("VOLCENGINE_ACCESS_KEY_ID");
        const Aws::String secretKey = std::getenv("VOLCENGINE_SECRET_ACCESS_KEY");

        Aws::Client::ClientConfiguration config;
        config.endpointOverride = endpoint;
        config.region = region;
        // The C++ SDK uses Virtual-hosted style by default without additional settings
        
        Aws::Auth::AWSCredentials credentials(accessKey, secretKey);

        // 2. Initialize the S3 client
        Aws::S3::S3Client s3Client(credentials, config, Aws::Client::AWSAuthV4Signer::PayloadSigningPolicy::Never, false);

        auto ms = std::chrono::duration_cast<std::chrono::milliseconds>(
            std::chrono::system_clock::now().time_since_epoch()).count();
        Aws::String bucketName = "your-unique-bucket-name-" + std::to_string(ms);
        const Aws::String objectKey = "my-object-key";
        const Aws::String localFilePath = "local-file.txt";
        const Aws::String downloadFilePath = "downloaded-file.txt";

        // Prepare local files
        std::ofstream localFile(localFilePath);
        localFile << "Hello, Volcengine TOS!";
        localFile.close();

        // 3. Create buckets
        std::cout << "Creating bucket: " << bucketName << std::endl;
        Aws::S3::Model::CreateBucketRequest createBucketRequest;
        createBucketRequest.SetBucket(bucketName);
        auto createBucketOutcome = s3Client.CreateBucket(createBucketRequest);
        if (!createBucketOutcome.IsSuccess()) {
            std::cerr << "CreateBucket error: " << createBucketOutcome.GetError().GetMessage() << std::endl;
            return 1;
        }
        std::cout << "Bucket created successfully." << std::endl;

        // 4. Upload objects
        std::cout << "Uploading object to " << bucketName << std::endl;
        Aws::S3::Model::PutObjectRequest putObjectRequest;
        putObjectRequest.SetBucket(bucketName);
        putObjectRequest.SetKey(objectKey);
        std::shared_ptr<Aws::IOStream> input_data =
            Aws::MakeShared<Aws::FStream>("PutObjectInputStream",
                                          localFilePath.c_str(),
                                          std::ios_base::in | std::ios_base::binary);
        putObjectRequest.SetBody(input_data);
        auto putObjectOutcome = s3Client.PutObject(putObjectRequest);
        if (!putObjectOutcome.IsSuccess()) {
            std::cerr << "PutObject error: " << putObjectOutcome.GetError().GetMessage() << std::endl;
        } else {
            std::cout << "Object uploaded successfully." << std::endl;
        }

        // 5. List objects
        std::cout << "Listing objects in bucket: " << bucketName << std::endl;
        Aws::S3::Model::ListObjectsV2Request listObjectsRequest;
        listObjectsRequest.SetBucket(bucketName);
        auto listObjectsOutcome = s3Client.ListObjectsV2(listObjectsRequest);
        if (listObjectsOutcome.IsSuccess()) {
            for (const auto& object : listObjectsOutcome.GetResult().GetContents()) {
                std::cout << "- " << object.GetKey() << std::endl;
            }
        } else {
            std::cerr << "ListObjects error: " << listObjectsOutcome.GetError().GetMessage() << std::endl;
        }

        // 6. Download objects
        std::cout << "Downloading object: " << objectKey << std::endl;
        Aws::S3::Model::GetObjectRequest getObjectRequest;
        getObjectRequest.SetBucket(bucketName);
        getObjectRequest.SetKey(objectKey);
        auto getObjectOutcome = s3Client.GetObject(getObjectRequest);
        if (getObjectOutcome.IsSuccess()) {
            Aws::OFStream downloadedFile(downloadFilePath.c_str(), std::ios::out | std::ios::binary);
            downloadedFile << getObjectOutcome.GetResult().GetBody().rdbuf();
            std::cout << "Object downloaded successfully to " << downloadFilePath << std::endl;
        } else {
            std::cerr << "GetObject error: " << getObjectOutcome.GetError().GetMessage() << std::endl;
        }

        // 7. Delete objects
        std::cout << "Deleting object: " << objectKey << std::endl;
        Aws::S3::Model::DeleteObjectRequest deleteObjectRequest;
        deleteObjectRequest.SetBucket(bucketName);
        deleteObjectRequest.SetKey(objectKey);
        auto deleteObjectOutcome = s3Client.DeleteObject(deleteObjectRequest);
        if (deleteObjectOutcome.IsSuccess()) {
            std::cout << "Object deleted successfully." << std::endl;
        } else {
            std::cerr << "DeleteObject error: " << deleteObjectOutcome.GetError().GetMessage() << std::endl;
        }
        
        // 8. Delete buckets
        std::cout << "Deleting bucket: " << bucketName << std::endl;
        Aws::S3::Model::DeleteBucketRequest deleteBucketRequest;
        deleteBucketRequest.SetBucket(bucketName);
        auto deleteBucketOutcome = s3Client.DeleteBucket(deleteBucketRequest);
        if (deleteBucketOutcome.IsSuccess()) {
            std::cout << "Bucket deleted successfully." << std::endl;
        } else {
            std::cerr << "DeleteBucket error: " << deleteBucketOutcome.GetError().GetMessage() << std::endl;
        }
        
        // Remove a local file
        remove(localFilePath.c_str());
        remove(downloadFilePath.c_str());
    }
    Aws::ShutdownAPI(options);
    return 0;
}
```



</Tab>
<Tab zoneid="RfaiX6LmPt" title="JavaScript(Node.js)">
<TabTitle>JavaScript(Node.js)</TabTitle>

Use `@aws-sdk/client-s3` (v3).

<span id="c253d73b"></span>
### Environment

Ensure your development environment has Node.js version 10 or higher installed.

<span id="0b75ab10"></span>
### Install the SDK

```Bash
npm install @aws-sdk/client-s3
```


<span id="f451b450"></span>
### Complete code example

```JavaScript
const {
    S3Client,
    CreateBucketCommand,
    PutObjectCommand,
    ListObjectsV2Command,
    GetObjectCommand,
    DeleteObjectCommand,
    DeleteBucketCommand,
} = require("@aws-sdk/client-s3");
const { getSignedUrl } = require("@aws-sdk/s3-request-presigner");
const fs = require("fs");
const { Readable } = require("stream");

// Helper to stream to buffer
const streamToBuffer = (stream) =>
    new Promise((resolve, reject) => {
        const chunks = [];
        stream.on("data", (chunk) => chunks.push(chunk));
        stream.on("error", reject);
        stream.on("end", () => resolve(Buffer.concat(chunks)));
    });


async function main() {
    // 1. Configure authentication information and access endpoint
    const endpoint = "https://tos-s3-cn-beijing.volces.com";
    const region = "cn-beijing";
    const accessKey = process.env.VOLCENGINE_ACCESS_KEY_ID;
    const secretKey = process.env.VOLCENGINE_SECRET_ACCESS_KEY;

    // 2. Initialize the S3 client
    // S3Client V3 requires specifying the forPathStyle parameter as false
    const s3Client = new S3Client({
        endpoint: endpoint,
        region: region,
        credentials: {
            accessKeyId: accessKey,
            secretAccessKey: secretKey,
        },
        forcePathStyle: false, // Key: Must be false to use virtual-hosted-style
    });

    const bucketName = `your-unique-bucket-name-${Date.now()}`;
    const objectKey = "my-object-key";
    const localFilePath = "local-file.txt";
    const downloadFilePath = "downloaded-file.txt";

    try {
        // Prepare local file
        fs.writeFileSync(localFilePath, "Hello, Volcengine TOS!");

        // 3. Create buckets
        console.log(`Creating bucket: ${bucketName}`);
        await s3Client.send(new CreateBucketCommand({ Bucket: bucketName }));
        console.log("Bucket created successfully.");

        // 4. Upload objects
        console.log(`Uploading object to ${bucketName}`);
        const fileStream = fs.createReadStream(localFilePath);
        await s3Client.send(new PutObjectCommand({
            Bucket: bucketName,
            Key: objectKey,
            Body: fileStream,
        }));
        console.log("Object uploaded successfully.");

        // 5. List objects
        console.log(`Listing objects in bucket: ${bucketName}`);
        const listResponse = await s3Client.send(new ListObjectsV2Command({ Bucket: bucketName }));
        if (listResponse.Contents) {
            listResponse.Contents.forEach(obj => console.log(`- ${obj.Key}`));
        }

        // Download the object
        console.log(`Downloading object: ${objectKey}`);
        const getResponse = await s3Client.send(new GetObjectCommand({
            Bucket: bucketName,
            Key: objectKey,
        }));
        if (getResponse.Body instanceof Readable) {
            const bodyBuffer = await streamToBuffer(getResponse.Body);
            fs.writeFileSync(downloadFilePath, bodyBuffer);
            console.log(`Object downloaded successfully to ${downloadFilePath}`);
        }

        // Delete the object
        console.log(`Deleting object: ${objectKey}`);
        await s3Client.send(new DeleteObjectCommand({ Bucket: bucketName, Key: objectKey }));
        console.log("Object deleted successfully.");

    } catch (err) {
        console.error("Error:", err);
    } finally {
        // Delete the bucket
        try {
            console.log(`Deleting bucket: ${bucketName}`);
            await s3Client.send(new DeleteBucketCommand({ Bucket: bucketName }));
            console.log("Bucket deleted successfully.");
        } catch (err) {
             console.error("Error deleting bucket:", err);
        }
        
        // Clean up local files
        if (fs.existsSync(localFilePath)) fs.unlinkSync(localFilePath);
        if (fs.existsSync(downloadFilePath)) fs.unlinkSync(downloadFilePath);
    }
}

main();
```



</Tab>
<Tab zoneid="qS7xuuSZGX" title="PHP">
<TabTitle>PHP</TabTitle>

Use `aws-sdk-php`.

<span id="d916fcd4"></span>
### Environment

Ensure your development environment has PHP version 5.6 or higher installed.

<span id="696fc91f"></span>
### install SDK

Install via Composer:

```Bash
composer require aws/aws-sdk-php
```


<span id="e8e4e1ba"></span>
### Complete code example

```PHP
<?php
require 'vendor/autoload.php';

use Aws\S3\S3Client;
use Aws\S3\Exception\S3Exception;

// 1. Configure authentication information and access endpoint
$endpoint = 'https://tos-s3-cn-beijing.volces.com';
$region = 'cn-beijing';
$accessKey = getenv('VOLCENGINE_ACCESS_KEY_ID');
$secretKey = getenv('VOLCENGINE_SECRET_ACCESS_KEY');

// 2. Initialize the S3 client
// Key: 'use_path_style_endpoint' => false
$s3Client = new S3Client([
    'version' => 'latest',
    'region'  => $region,
    'endpoint' => $endpoint,
    'credentials' => [
        'key'    => $accessKey,
        'secret' => $secretKey,
    ],
    'use_path_style_endpoint' => false // Enforce virtual-hosted style
]);

$bucketName = 'your-unique-bucket-name-' . time();
$objectKey = 'my-object-key';
$localFilePath = 'local-file.txt';
$downloadFilePath = 'downloaded-file.txt';

try {
    // Prepare local files
    file_put_contents($localFilePath, 'Hello, Volcengine TOS!');

    // 3. Create the bucket
    echo "Creating bucket: {$bucketName}\n";
    $s3Client->createBucket(['Bucket' => $bucketName]);
    echo "Bucket created successfully.\n";

    // upload objects
    echo "Uploading object to {$bucketName}\n";
    $s3Client->putObject([
        'Bucket' => $bucketName,
        'Key'    => $objectKey,
        'SourceFile' => $localFilePath,
    ]);
    echo "Object uploaded successfully.\n";

    // list objects
    echo "Listing objects in bucket: {$bucketName}\n";
    $objects = $s3Client->listObjectsV2(['Bucket' => $bucketName]);
    if (!empty($objects['Contents'])) {
        foreach ($objects['Contents'] as $object) {
            echo "- " . $object['Key'] . "\n";
        }
    }

    // download objects
    echo "Downloading object: {$objectKey}\n";
    $result = $s3Client->getObject([
        'Bucket' => $bucketName,
        'Key'    => $objectKey,
        'SaveAs' => $downloadFilePath
    ]);
    echo "Object downloaded successfully to {$downloadFilePath}\n";

    // delete objects
    echo "Deleting object: {$objectKey}\n";
    $s3Client->deleteObject([
        'Bucket' => $bucketName,
        'Key'    => $objectKey,
    ]);
    echo "Object deleted successfully.\n";

    // delete bucket
    echo "Deleting bucket: {$bucketName}\n";
    $s3Client->deleteBucket(['Bucket' => $bucketName]);
    echo "Bucket deleted successfully.\n";

} catch (S3Exception $e) {
    echo "Error: " . $e->getMessage() . "\n";
} finally {
    // clean local files
    if (file_exists($localFilePath)) {
        unlink($localFilePath);
    }
    if (file_exists($downloadFilePath)) {
        unlink($downloadFilePath);
    }
}
```



</Tab>
<Tab zoneid="rKipzQgEtU" title="Rust">
<TabTitle>Rust</TabTitle>

Use `aws-sdk-s3` (v0.34.0 or later).

<span id="d65be1d8"></span>
### Add dependencies

Add the following dependencies to your `Cargo.toml` file:

```TOML
[dependencies]
aws-config = "0.57.0"
aws-sdk-s3 = "0.34.0"
tokio = { version = "1", features = ["full"] }
http = "0.2.9"
```


<span id="c755eca0"></span>
### Complete code example

```Rust
use aws_config::meta::region::RegionProviderChain;
use aws_sdk_s3::{config::Region, meta::PKG_VERSION, Client, Error};
use std::fs::File;
use std::io::Write;
use std::path::Path;
use tokio::fs::File as TokioFile;

#[tokio::main]
async fn main() -> Result<(), Error> {
    // 1. Configure authentication information and access endpoint
    let endpoint = "https://tos-s3-cn-beijing.volces.com";
    let region_str = "cn-beijing";
    let access_key = std::env::var("VOLCENGINE_ACCESS_KEY_ID").expect("VOLCENGINE_ACCESS_KEY_ID not set");
    let secret_key = std::env::var("VOLCENGINE_SECRET_ACCESS_KEY").expect("VOLCENGINE_SECRET_ACCESS_KEY not set");

    let region_provider = RegionProviderChain::first_try(Region::new(region_str));
    let shared_config = aws_config::from_env()
        .region(region_provider)
        .endpoint_url(endpoint)
        .credentials_provider(aws_config::Credentials::new(
            access_key, secret_key, None, None, "default",
        ))
        .load()
        .await;
    
    // 2. Initialize S3 client
    // Rust SDK uses virtual-hosted style by default
    let client = Client::new(&shared_config);

    let bucket_name = format!("your-unique-bucket-name-{}", chrono::Utc::now().timestamp());
    let object_key = "my-object-key".to_string();
    let local_file_path = "local-file.txt";
    let download_file_path = "downloaded-file.txt";

    // Prepare local file
    let mut file = File::create(local_file_path).unwrap();
    file.write_all(b"Hello, Volcengine TOS!").unwrap();

    // 3. create buckets
    println!("Creating bucket: {}", &bucket_name);
    client.create_bucket().bucket(&bucket_name).send().await?;
    println!("Bucket created successfully.");

    // 4. upload objects
    println!("Uploading object to {}", &bucket_name);
    let body = TokioFile::open(local_file_path).await.unwrap().into();
    client
        .put_object()
        .bucket(&bucket_name)
        .key(&object_key)
        .body(body)
        .send()
        .await?;
    println!("Object uploaded successfully.");

    // 5. list objects
    println!("Listing objects in bucket: {}", &bucket_name);
    let mut response = client
        .list_objects_v2()
        .bucket(&bucket_name)
        .into_paginator()
        .send();
    while let Some(result) = response.next().await {
        match result {
            Ok(output) => {
                for object in output.contents().unwrap_or_default() {
                    println!("- {}", object.key().unwrap_or("Unknown"));
                }
            }
            Err(err) => {
                eprintln!("Error listing objects: {:?}", err);
                break;
            }
        }
    }
    
    // 6. download objects
    println!("Downloading object: {}", &object_key);
    let mut object = client
        .get_object()
        .bucket(&bucket_name)
        .key(&object_key)
        .send()
        .await?;
    let mut file = File::create(download_file_path).unwrap();
    while let Some(bytes) = object.body.try_next().await.unwrap() {
        file.write_all(&bytes).unwrap();
    }
    println!("Object downloaded successfully to {}", download_file_path);

    // 7. delete objects
    println!("Deleting object: {}", &object_key);
    client
        .delete_object()
        .bucket(&bucket_name)
        .key(&object_key)
        .send()
        .await?;
    println!("Object deleted successfully.");

    // 8. delete buckets
    println!("Deleting bucket: {}", &bucket_name);
    client
        .delete_bucket()
        .bucket(&bucket_name)
        .send()
        .await?;
    println!("Bucket deleted successfully.");
    
    // clean up local files
    std::fs::remove_file(local_file_path).ok();
    std::fs::remove_file(download_file_path).ok();

    Ok(())
}
```



</Tab>
<Tab zoneid="S5ExepyFcg" title="C#(.NET)">
<TabTitle>C#(.NET)</TabTitle>

Use the `AWSSDK.S3` NuGet package.

<span id="9d3e07fb"></span>
### Environment

Ensure your development environment has .NET Framework 2.0 or higher, or Mono 6.12 or higher installed.

<span id="c45dc96b"></span>
### Install SDK

Install via .NET CLI or NuGet package manager:

```Bash
dotnet add package AWSSDK.S3
```


<span id="96c6973f"></span>
### Complete code example

```C#
using System;
using System.IO;
using System.Threading.Tasks;
using Amazon.S3;
using Amazon.S3.Model;

namespace TosS3DotNetBestPractice
{
    class Program
    {
        static async Task Main(string[] args)
        {
            // 1. Configure authentication information and access endpoint
            var endpoint = "https://tos-s3-cn-beijing.volces.com";
            var region = "cn-beijing";
            var accessKey = Environment.GetEnvironmentVariable("VOLCENGINE_ACCESS_KEY_ID");
            var secretKey = Environment.GetEnvironmentVariable("VOLCENGINE_SECRET_ACCESS_KEY");

            // 2. Initialize the S3 client
            // Key: ForcePathStyle = false
            var config = new AmazonS3Config
            {
                ServiceURL = endpoint,
                RegionEndpoint = Amazon.RegionEndpoint.GetBySystemName(region),
                ForcePathStyle = false, // Force use of virtual-hosted style
            };
            var s3Client = new AmazonS3Client(accessKey, secretKey, config);

            var bucketName = $"your-unique-bucket-name-{DateTimeOffset.Now.ToUnixTimeSeconds()}";
            var objectKey = "my-object-key";
            var localFilePath = "local-file.txt";
            var downloadFilePath = "downloaded-file.txt";

            try
            {
                // Prepare local files
                await File.WriteAllTextAsync(localFilePath, "Hello, Volcengine TOS!");

                // 3. Create buckets
                Console.WriteLine($"Creating bucket: {bucketName}");
                await s3Client.PutBucketAsync(new PutBucketRequest
                {
                    BucketName = bucketName,
                    UseClientRegion = true // Use client-configured region
                });
                Console.WriteLine("Bucket created successfully.");

                // 4. Upload objects
                Console.WriteLine($"Uploading object to {bucketName}");
                await s3Client.PutObjectAsync(new PutObjectRequest
                {
                    BucketName = bucketName,
                    Key = objectKey,
                    FilePath = localFilePath
                });
                Console.WriteLine("Object uploaded successfully.");

                // 5. List objects
                Console.WriteLine($"Listing objects in bucket: {bucketName}");
                var listResponse = await s3Client.ListObjectsV2Async(new ListObjectsV2Request
                {
                    BucketName = bucketName
                });
                foreach (var s3Object in listResponse.S3Objects)
                {
                    Console.WriteLine($"- {s3Object.Key}");
                }

                // Download the object
                Console.WriteLine($"Downloading object: {objectKey}");
                var getResponse = await s3Client.GetObjectAsync(new GetObjectRequest
                {
                    BucketName = bucketName,
                    Key = objectKey
                });
                await getResponse.WriteResponseStreamToFileAsync(downloadFilePath, false, default);
                Console.WriteLine($"Object downloaded successfully to {downloadFilePath}");

                // Delete the object
                Console.WriteLine($"Deleting object: {objectKey}");
                await s3Client.DeleteObjectAsync(new DeleteObjectRequest
                {
                    BucketName = bucketName,
                    Key = objectKey
                });
                Console.WriteLine("Object deleted successfully.");

                // Delete the bucket
                Console.WriteLine($"Deleting bucket: {bucketName}");
                await s3Client.DeleteBucketAsync(new DeleteBucketRequest
                {
                    BucketName = bucketName
                });
                Console.WriteLine("Bucket deleted successfully.");
            }
            catch (Exception e)
            {
                Console.WriteLine($"Error: {e.Message}");
            }
            finally
            {
                // Remove local files
                if (File.Exists(localFilePath)) File.Delete(localFilePath);
                if (File.Exists(downloadFilePath)) File.Delete(downloadFilePath);
            }
        }
    }
}
```



</Tab>
</Tabs>


<span id="9ffc41a9"></span>
## Troubleshooting


1. About `CreateBucket` and `LocationConstraint`

   When creating a bucket outside the US East (Northern Virginia) region `us-east-1`, the S3 API requires providing `LocationConstraint`. TOS’s S3\-compatible interface currently does not require this parameter, even for regions like `cn-beijing` that are not `us-east-1`. You can omit this setting. If the SDK enforces it, pass the same value as the `region`.

2. Certificate validation failed

   * In enterprise intranet or proxy environments, SSL certificate validation may occasionally be intercepted. Ensure your development environment trusts certificates for the domain `*.volces.com`.

   * Some SDKs (such as Python `boto3`) allow disabling SSL certificate validation for debugging via the parameter `verify=False`, but this poses security risks. We strongly recommend resolving this fully in production by configuring the system or CA certificate trust chain.

3. Signature version mismatch

   If a signature verification error occurs when calling the interface, check your SDK initialization settings to ensure the v4 signature algorithm (s3v4) is enforced, as TOS’s S3\-compatible interface strictly requires this version.

4. Virtual host addressing mode configuration error

   The most common configuration mistake during integration. TOS S3 domains do not support Path\-style (`https://tos-s3-cn-beijing.volces.com/bucket-name`). All requests must use Virtual\-hosted style (`https://bucket-name.tos-s3-cn-beijing.volces.com`). Please carefully check the configuration options for the addressing mode in your SDK
