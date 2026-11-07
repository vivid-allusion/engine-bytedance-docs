---
title: "PointCloudCompress"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PointCloudCompress"
---

<span id="1ace590a"></span>
## Description

Point cloud data is an unstructured dataset composed of a large number of three\-dimensional points, widely used in 3D reconstruction, semantic segmentation, autonomous driving, and other fields. Storing and transmitting point cloud data requires substantial storage space and bandwidth, so compression is necessary to reduce costs. This interface is used for point cloud file compression.

<span id="893f98c0"></span>
## Notes


* This interface is in invitation\-only testing. Contact your account manager to use it.

* Point cloud compression supports synchronous processing only (x\-tos\-process method).

* Currently, only pcd format point cloud file compression is supported, with a file size limit of 20MB.

* The default flow control value is 5 QPS.


<span id="31722687"></span>
## Request syntax

```SQL
GET /example.pcd?x-tos-process=pointcloud/compress&format=pcd HTTP/1.1
Host: <bucket_name>.tos-cn-beijing.volces.com
Authorization: authorization_string
```


<span id="179f6321"></span>
## Request parameters and headers 


|**Field name** |**Location **  |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|---|
|x\-tos\-process |Query |String |Yes |pointcloud/compress |This represents the special identifier for point cloud file compression requests, fixed as `pointcloud/compress`. |
|format |Query |String |No |pcd |File format, currently only `pcd` file format is supported. |
|method |Query |String |No |octree: octree |Point cloud file compression method, currently only supports `octree: octree`. |
|fields<br><br> |Query |String |No |xyz |Point cloud data type, currently supports only the `xyz` type.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter requires URL safe encoding, use eHI6 when making requests.</div><br> |
|lib |Query |String |No |pcl<br><br> |The name of the compression library; currently, only `pcl` is supported. |
|point\-resolution |Query |Float |No<br><br> |0.01 |Point cloud resolution. This variable determines the accuracy of point coordinates during encoding. The default value is `0.01`, with a range of [0, 1]. |
|octree\-resolution<br><br> |Query |Float |No<br><br> |0.01 |The minimum block size when partitioning an octree, which is the voxel edge length. The default value is `0.01`, with a range of [0, 1]. |
|down\-sampling |Query |Int<br><br> |No |1 |Whether to use downsampling, default value is `1`.<br><br>`1`: indicates using downsampling.<br><br>`0`: indicates not using downsampling. |


<span id="5fd6897f"></span>
## Request body elements

No elements are used.

<span id="47e8beb0"></span>
## Response headers

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/docs/tos/reference-common-parameters).

<span id="1d08a3fc"></span>
## Response body elements

No elements are used.

<span id="701c8294"></span>
## Sample request

```SQL
GET /example.pcd?x-tos-process=pointcloud/compress&format=pcd HTTP/1.1
Host: <bucket_name>.tos-cn-beijing.volces.com
Authorization: authorization_string
```


<span id="2f1febd5"></span>
## Sample response

```Python
HTTP/1.1 200 OK
Date: Sat, 07 Oct 2023 09:02:23 GMT
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 3515016f6441e0f3696f6441
Content-Type: application/octet-stream
Content-Length: 72650

// Compressed data
[content]
```
