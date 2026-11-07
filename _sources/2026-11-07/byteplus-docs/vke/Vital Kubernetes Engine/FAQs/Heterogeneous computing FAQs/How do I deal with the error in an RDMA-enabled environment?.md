---
title: "How do I deal with the error in an RDMA-enabled environment?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How_to_deal_with_the_error_ibv_create_cq_allocate_memory_in_a_RDMA_enabled_environment"
---

<span id="pDLIpnBx"></span>
## Issue phenomenon

An NCCL runtime error occurs when containers use RDMA devices to achieve communication among multiple machines.


* ibv_create_cq allocate memory failed.

* ibvwrap.c:106 NCCL WARN Call to ibv_reg_mr failed.

   ```Bash
   ibvwrap.c:106 NCCL WARN Call to ibv_reg_mr failed
   proxy.cc:1519 NCCL WARN [Proxy Service 5] Failed to execute operation Connect from rank 5, retcode 2
   NCCL WARN socketProgress: Connection closed by remote peer master-0.svc.cluster.local<36167>
   ```
   


<span id="boV5RVkq"></span>
## Environment configuration


* Node model: ecs.hpcpni3ln.45xlarge

* NCCL version: 2.18.5


<span id="k6VCavf1"></span>
## Cause analysis

It might be caused by "the default size set by the command ulimit \-l is 64K,  which is insufficient for memlock memory in benchmark scenarios". In that case, please refer to the following solution.

<span id="nU5M1nCL"></span>
## Solution


<Tabs>
<Tab zoneid="fmPE53xMq8" title="Fix it on new nodes">
<TabTitle>Fix it on new nodes</TabTitle>

Go to the page "Edit node pool" and select "Advanced settings", then copy the following script to the textbox "InitializeScript" to overwrite all the existing content. Save the changes to take effect.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">The value of the parameter LimitNOFILE in the script needs to be consistent with that of the same parameter in  <code>/lib/systemd/system/containerd.service</code>.</div>


```Bash
sed -i '/LimitNOFILE=10xxx76/a LimitMEMLOCK=infinity\nLimitSTACK=infinity' /lib/systemd/system/containerd.service && systemctl daemon-reload && systemctl restart containerd
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1d98ef63bb166abe8986f15dc80aac27.png) </span>




</Tab>
<Tab zoneid="CGbtJZj8rb" title="Fix it on existing nodes">
<TabTitle>Fix it on existing nodes</TabTitle>

1. Log in to a node and execute the command `vi /lib/systemd/system/containerd.service`, then add the configuration LimitMEMLOCK=infinity.

2. Execute the command `sudo systemctl daemon-reload && sudo systemctl restart containerd` to reload configuration and restart containerd service.


</Tab>
</Tabs>
