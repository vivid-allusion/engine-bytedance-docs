---
title: "Application scenarios"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Application-scenarios"
---

<span id=".57uR5a6a5LqR5pyN5Yqh5Zmo"></span>
## Access Internet from a single cloud resource

Associate an Elastic IP Address (EIP) with an Elastic Compute Service (ECS) instance to enable communication between the ECS instance and the Internet.

<span id=".57uR5a6a5YWs572RTkFU572R5YWz"></span>
## <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_501601816daec5f92f007e20f6fb05a8.png) </span>

<span id=".57uR5a6a5YWs572RTkFU572R5YWz"></span>
## Access Internet from multiple cloud resources

Associate an EIP with an Internet NAT Gateway and create a SNAT entry or DNAT entry, allowing multiple ECS instances to share the EIP to access the Internet or provide services to the Internet.

<span id="sg28ZyV2"></span>
## <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2852e07685e01d31f72741b3a80b37fc.png) </span>

<span id="sg28ZyV2"></span>
## Achieve high availability via Internet

<span id="CUxbDUtv"></span>
### Associate with Classic Load Balancer

Associate an EIP with a Classic Load Balancer (CLB) instance, enabling client requests from the Internet to be distributed to backend servers according to the specified load balancing policy.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When creating a public CLB, Network Load Balancer (NLB), or other instances, the system automatically creates an EIP to provide Internet services for the instance. This EIP only supports modifying tag information and does not support associating, disassociating, deleting, adding to/removing from the Bandwidth Package, or other actions. Its lifecycle follows the corresponding cloud product instance.</div>


<span id=".57uR5a6a6L6F5Yqp572R5Y2h"></span>
### <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b6b0afec1d8dd3071d2481e28d13db2e.png) </span>

<span id=".57uR5a6a6L6F5Yqp572R5Y2h"></span>
### Associate secondary network interface

Associate an EIP with a secondary network interface, providing multiple EIPs for a single ECS instance. This helps you build a more flexible and higher\-performance network deployment solution.

<span id=".5Yqg5YWl5Yiw5YWx5Lqr5bim5a695YyF"></span>
## <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3549aedbe4196c3fb71cc5af53d1f21f.png) </span>

<span id=".5Yqg5YWl5Yiw5YWx5Lqr5bim5a695YyF"></span>
## Internet cost savings

Add multiple EIPs to a Bandwidth Package instance to share one bandwidth, improving bandwidth utilization and reducing Internet costs.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fb6bf4e9a18c020bf9e8a8e859a69d72.png) </span>
