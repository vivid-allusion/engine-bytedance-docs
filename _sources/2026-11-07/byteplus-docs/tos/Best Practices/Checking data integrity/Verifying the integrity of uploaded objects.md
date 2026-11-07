---
title: "Verifying the integrity of uploaded objects"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Verify-consistency-of-the-uploaded-object"
---

You can use Content\-MD5, Content\-SHA256, or CRC64 to verify the consistency of the uploaded object. This article introduces the verification flowcharts and example code for different schemes.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background


* For explanations of different verification schemes, refer to [Related concepts](https://docs.byteplus.com/docs/tos/Overview10#.55u45YWz5qaC5b-1).

* For differences among the schemes, refer to [Scheme comparison](https://docs.byteplus.com/docs/tos/Overview10#.5qCh6aqM5LiK5Lyg5a-56LGh55qE5LiA6Ie05oCn).

* For download object consistency verification schemes, refer to [Verifying the integrity of downloaded objects](https://docs.byteplus.com/docs/tos/Verify-the-consistency-of-the-downloaded-object).


<span id=".6YCa6L-HY29udGVudC1tZDU="></span>
## Using Content\-MD5

When calling the TOS API to upload an object or a part, send the Content\-MD5 value calculated on the client for the data to be uploaded via the request header or form field to TOS, ensuring data consistency.

<span id=".5rWB56iL5Zu-"></span>
### Flowchart

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261010092407-1695145968297.jpg) </span>

<span id=".56S65L6L5Luj56CB"></span>
### Example code


<Tabs>
<Tab zoneid="ERntoqdARC" title="Golang">
<TabTitle>Golang</TabTitle>

&nbsp;

```Go
package main

import (
   "bytes"
   "context"
   "crypto/md5"
   "encoding/base64"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func main() {
   var (
      accessKey = "your access key"
      secretKey = "your secret key"
      endpoint  = "your endpoint"
      region    = "your region"
      bucket    = "bucketname"
      key       = "objectname"
   )
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   if err != nil {
      panic(err)
   }

   data := []byte("hello world")
   // Calculate MD5
   hash := md5.New()
   hash.Write(data)
   contentMD5 := base64.StdEncoding.EncodeToString(hash.Sum(nil))

   // upload object with specified Content-MD5
   input := &tos.PutObjectV2Input{}
   input.Bucket = bucket
   input.Key = key
   input.Content = bytes.NewReader(data)
   input.ContentMD5 = contentMD5
   _, err = client.PutObjectV2(context.Background(), input)
   if err != nil {
      panic(err)
   }
}
```





</Tab>
<Tab zoneid="rXzxXApfvL" title="Java">
<TabTitle>Java</TabTitle>

&nbsp;

```Java
package com.volcengine.tos;

import com.volcengine.tos.auth.Credentials;
import com.volcengine.tos.auth.SignV4;
import com.volcengine.tos.auth.StaticCredentials;

import java.io.ByteArrayInputStream;
import java.io.InputStream;
import java.security.MessageDigest;
import java.util.Base64;

public class Main {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String region = "your region";
        String bucket = "bucketname";
        String key = "objectname";

        TOSClient client = new TOSClient(endpoint);
        Credentials c = new StaticCredentials(accessKey, secretKey);
        client.setCredentials(c);
        client.setSigner(new SignV4(c, region));
 
        String data = "hello world";

        try {
            // Calculate MD5
            MessageDigest md5 = MessageDigest.getInstance("MD5");
            md5.update(data.getBytes());
            String contentMD5 = Base64.getEncoder().encodeToString(md5.digest());

            InputStream stream = new ByteArrayInputStream(data.getBytes());
            client.putObject(bucket, key, stream, RequestOptions.withContentMD5(contentMD5));
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```





</Tab>
<Tab zoneid="Hd7ehaGsSb" title="Python">
<TabTitle>Python</TabTitle>

&nbsp;

```Python
import base64
import hashlib

import tos

endpoint = 'your endpoint'
access_key = 'your access key'
secret_key = 'your secret key'
region = 'your region'

bucket = 'bucketname'
key = 'objectname'
data = 'hello world'

# Calculate MD5
hash = hashlib.md5()
hash.update(data.encode())
content_md5 = base64.b64encode(hash.digest()).decode()

client = tos.TosClientV2(access_key, secret_key, endpoint, region)
try:
    resp = client.put_object(bucket, key, content=data, content_md5=content_md5)
    print(resp.status_code)
except Exception as e:
    print(e)
```





</Tab>
</Tabs>


<span id=".6YCa6L-HY29udGVudC1zaGEyNTY="></span>
## Using Content\-SHA256

Similar to the method using Content\-MD5 verification, when calling the TOS API to upload an object or a part, the Content\-SHA256 value of the data to be uploaded, calculated by the client, is passed to TOS via request headers or form fields to ensure data consistency during the upload.

<span id=".5rWB56iL5Zu-"></span>
### Flowchart

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261010092435-165400427861.jpg) </span>

<span id=".56S65L6L5Luj56CB"></span>
### Example code


<Tabs>
<Tab zoneid="OBNAMwwsY2" title="Golang">
<TabTitle>Golang</TabTitle>

&nbsp;

```Go
package main

import (
   "bytes"
   "context"
   "crypto/sha256"
   "encoding/hex"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)


func main() {
   var (
      accessKey = "your access key"
      secretKey = "your secret key"
      endpoint  = "your endpoint"
      region    = "your region"
      bucket    = "bucketname"
      key       = "objectname"
   )
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   if err != nil {
      panic(err)
   }

   data := []byte("hello world")
   // Calculate SHA256
   hash := sha256.New()
   hash.Write(data)
   contentSHA256 := hex.EncodeToString(hash.Sum(nil))

   // upload object with specified Content-SHA256
   input := &tos.PutObjectV2Input{}
   input.Bucket = bucket
   input.Key = key
   input.Content = bytes.NewReader(data)
   input.ContentSHA256 = contentSHA256
   _, err = client.PutObjectV2(context.Background(), input)
   if err != nil {
      panic(err)
   }
}
```





</Tab>
<Tab zoneid="v7DhDUds41" title="Java">
<TabTitle>Java</TabTitle>

&nbsp;

```Java
package com.volcengine.tos;

import com.volcengine.tos.auth.Credentials;
import com.volcengine.tos.auth.SignV4;
import com.volcengine.tos.auth.StaticCredentials;
import com.volcengine.tos.model.object.GetObjectOutput;
import org.apache.commons.codec.binary.Hex;

import java.io.ByteArrayInputStream;
import java.io.InputStream;
import java.security.MessageDigest;

public class Main {

    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String region = "your region";
        String bucket = "bucketname";
        String key = "objectname";

        TOSClient client = new TOSClient(endpoint);
        Credentials c = new StaticCredentials(accessKey, secretKey);
        client.setCredentials(c);
        client.setSigner(new SignV4(c, region));

        String data = "hello world";

        try {
            MessageDigest sha256 = MessageDigest.getInstance("SHA-256");
            sha256.update(data.getBytes());
            String contentSHA256 = Hex.encodeHexString(sha256.digest());

            InputStream stream = new ByteArrayInputStream(data.getBytes());
            client.putObject(bucket, key, stream, RequestOptions.withContentSHA256(contentSHA256));

            GetObjectOutput output = client.getObject(bucket, key);
            output.getContent();

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```





</Tab>
<Tab zoneid="dCLTC6b82W" title="Python">
<TabTitle>Python</TabTitle>

&nbsp;

```Java
import hashlib

import tos

endpoint = 'your endpoint'
access_key = 'your access key'
secret_key = 'your secret key'
region = 'your region'

bucket = 'bucketname'
key = 'objectname'
data = 'hello world'

# Calculate SHA256
hash = hashlib.sha256()
hash.update(data.encode())
content_sha256 = hash.digest().hex()

client = tos.TosClientV2(access_key, secret_key, endpoint, region)
try:
    resp = client.put_object(bucket, key, content=data, content_sha256=content_sha256)
    print(resp.status_code)
except Exception as e:
    print(e)
```





</Tab>
</Tabs>


<span id=".6YCa6L-HY3JjNjQ="></span>
## Using CRC64

After calling the TOS API to upload an object or part, compare the CRC64 of the uploaded data calculated by the client with the CRC64 returned by TOS to ensure data consistency for a single API upload.

In the multipart upload scenario, besides verifying the CRC64 for each part upload, after merging parts, the combined CRC64 of all parts is compared with the CRC64 of the entire object returned by the server to ensure the data consistency of the final object generated by TOS.

<span id=".5rWB56iL5Zu-"></span>
### Flowchart

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261010095622-574968300043.jpg) </span>

<span id=".56S65L6L5Luj56CB"></span>
### Example code


<Tabs>
<Tab zoneid="k2W2GAUKCy" title="Golang">
<TabTitle>Golang</TabTitle>

```Go
package main

import (
   "bytes"
   "context"
   "hash"
   "io"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

type crc64Reader struct {
   r io.Reader
   h hash.Hash64
}

func (cr *crc64Reader) Read(p []byte) (n int, err error) {
   n, err = cr.r.Read(p)
   cr.h.Write(p[:n])
   return n, err
}

func main() {
   var (
      accessKey = "your access key"
      secretKey = "your secret key"
      endpoint  = "your endpoint"
      region    = "your region"
      bucket    = "bucketname"
      key       = "objectname"
   )
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   if err != nil {
      panic(err)
   }

   resp, err := client.CreateMultipartUploadV2(context.Background(), &tos.CreateMultipartUploadV2Input{
      Bucket: bucket,
      Key:    key,
   })
   if err != nil {
      panic(err)
   }

   uploadID := resp.UploadID
   parts := make([]tos.UploadedPartV2, 0, 3)

   var crc64Final uint64
   data := make([]byte, 1024*1024*5)
   for i := 1; i <= 2; i++ {
      // upload object with specified Content-MD5
      input := &tos.UploadPartV2Input{}
      input.Bucket = bucket
      input.Key = key
      input.UploadID = uploadID
      input.PartNumber = i

      crc64Hash := tos.NewCRC(tos.DefaultCrcTable(), 0)
      input.Content = &crc64Reader{
         r: bytes.NewReader(data),
         h: crc64Hash,
      }
      output, err := client.UploadPartV2(context.Background(), input)
      if err != nil {
         panic(err)
      }

      crc64Once := crc64Hash.Sum64()
      if output.HashCrc64ecma != crc64Once {
         panic("crc64 not match")
      }

      crc64Final = tos.CRC64Combine(crc64Final, crc64Once, uint64(len(data)))

      parts = append(parts, tos.UploadedPartV2{
         PartNumber: input.PartNumber,
         ETag:       output.ETag,
      })
   }

   output, err := client.CompleteMultipartUploadV2(context.Background(), &tos.CompleteMultipartUploadV2Input{
      Bucket:   bucket,
      Key:      key,
      UploadID: uploadID,
      Parts:    parts,
   })

   if err != nil {
      panic(err)
   }

   if output.HashCrc64ecma != crc64Final {
      panic("crc64 not match")
   }
}
```





</Tab>
<Tab zoneid="YyvlSryYhh" title="Python">
<TabTitle>Python</TabTitle>

```Python
from io import BytesIO
import os
import tos

endpoint = 'your endpoint'
access_key = 'your access key'
secret_key = 'your secret key'
region = 'your region'
bucket_name = 'bucketname'
key = 'objectname'


class Crc64IO(object):
    def __init__(self, data):
        self.data = data
        self.crc64 = tos.utils.Crc64()

    def __iter__(self):
        return self

    def __next__(self):
        return self.next()

    def next(self):
        content = self.data.read(8 * 1024)
        if content:
            self.crc64.update(content)
            return content
        raise StopIteration


# Local file full path, for example, usr/local/testfile.txt
file_name = 'usr/local/testfile.txt'
client = tos.TosClientV2(access_key, secret_key, endpoint, region, enable_crc=False)
try:
    total_size = os.path.getsize(file_name)
    part_size = 1024 * 1024 * 5
    resp = client.create_multipart_upload(bucket_name, key)
    upload_id = resp.upload_id
    parts = []
    crc64 = tos.utils.Crc64()
    crc64_final = 0

    # Upload part data
    with open(file_name, 'rb') as f:
        part_number = 1
        offset = 0
        while offset < total_size:
            num_to_upload = min(part_size, total_size - offset)
            crc64_io = Crc64IO(SizeAdapter(f, num_to_upload, init_offset=offset))
            part = client.upload_part(bucket_name, key, upload_id, part_number,
                                      content=crc64_io)

            if crc64_io.crc64.crc != part.hash_crc64_ecma:
                raise Exception('crc64 not match')
            crc64_final = crc64.combine(crc64_final, crc64_io.crc64.crc, num_to_upload)
            parts.append(part)
            offset += num_to_upload
            part_number += 1

    resp = client.complete_multipart_upload(bucket_name, key, upload_id, parts)

    if crc64_final != resp.hash_crc64_ecma:
        raise Exception('crc64 not match')

except tos.exceptions.TosClientError as e:
    # Operation failed, capture client exception, usually due to invalid request parameters or network issues
    print('fail with client error, message:{}, cause: {}'.format(e.message, e.cause))
except tos.exceptions.TosServerError as e:
    # Operation failed, capture server exception, detailed error information can be obtained from the response
    print('fail with server error, code: {}'.format(e.code))
    # Request ID can pinpoint specific issues; it is strongly recommended to save it in logs
    print('error with request id: {}'.format(e.request_id))
    print('error with message: {}'.format(e.message))
    print('error with http code: {}'.format(e.status_code))
    print('error with ec: {}'.format(e.ec))
    print('error with request url: {}'.format(e.request_url))
except Exception as e:
    print('fail with unknown error: {}'.format(e))
```





</Tab>
</Tabs>
