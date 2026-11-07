---
title: "Verifying the integrity of downloaded objects"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Verify-the-consistency-of-the-downloaded-object"
---

This article introduces a scheme and example code to verify the consistency of downloaded objects using CRC64.

<span id=".5pa55qGI6K-05piO"></span>
## Scheme description

In scenarios where the entire object is downloaded in a single operation, after calling the TOS API to complete the download, the client compares the CRC64 of the downloaded data it calculated with the CRC64 returned by TOS to ensure data consistency.

In range download scenarios, after downloading the entire object by Range segments, the CRC64 values of the individual Range segments are combined and compared with the CRC64 of the entire object returned by the server to ensure final data consistency of the downloaded object. For details on CRC64 parameters, see [Related concepts](https://docs.byteplus.com/docs/tos/Overview10#.55u45YWz5qaC5b-1).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the upload object consistency verification scheme, see verify <a href="https://docs.byteplus.com/docs/tos/Verify-consistency-of-the-uploaded-object">Verifying the integrity of uploaded objects</a>.</div>


<span id=".5rWB56iL5Zu-"></span>
## Flowchart

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5145bea3d6e92eedf18a1386f7232917.png) </span>

&nbsp;

<span id=".56S65L6L5Luj56CB"></span>
## Example code


<Tabs>
<Tab zoneid="RwyI216DGw" title="Golang">
<TabTitle>Golang</TabTitle>

&nbsp;

```Python
package main

import (
   "context"
   "hash"
   "io"
   "io/ioutil"

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

   output, err := client.GetObjectV2(context.Background(), &tos.GetObjectV2Input{
      Bucket: bucket,
      Key:    key,
   })

   defer output.Content.Close()
   p := make([]byte, 1024)
   crc64Hash := tos.NewCRC(tos.DefaultCrcTable(), 0)
   reader := &crc64Reader{
       r: output.Content,
       h: crc64Hash,
   }
   for {
       _, err = reader.Read(p)
       if err != nil {
          if err == io.EOF｛
              break
          ｝
          panic(err)
       }
   }

   if output.HashCrc64ecma != crc64Hash.Sum64() {
      panic("crc64 not match")
   }
}
```





</Tab>
<Tab zoneid="VQbQseFxuM" title="Python">
<TabTitle>Python</TabTitle>

&nbsp;

```Python
import tos

endpoint = 'your endpoint'
access_key = 'your access key'
secret_key = 'your secret key'
region = 'your region'
bucket = 'bucketname'
key = 'objectname'

crc64 = tos.utils.Crc64()
client = tos.TosClientV2(access_key, secret_key, endpoint, region)
try:
    resp = client.get_object(bucket, key)
    print(resp.status_code)
    while True:
        chunk = resp.content.read(65536)
        if not chunk:
            break
        crc64.update(chunk)

    if resp.hash_crc64_ecma != crc64.crc:
        raise Exception('crc64 not match')

except Exception as e:
    print(e)
```





</Tab>
</Tabs>
