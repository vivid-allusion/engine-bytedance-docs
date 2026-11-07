---
title: "Failure to install the monitoring add-on"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Handling-errors"
---

<span id="9949a260"></span>
## **Issue description**

If the DNS server addresses used by the VPC where the target instance is located are not the default addresses provided by the platform, the monitoring add\-on cannot be installed. The error message is as follows:

```Bash
Could not resolve host: tos-s3-cn-beijing.ivolces.com; Unknown error
```


<span id="TqA2Gg4q"></span>
## **Solution**

Log in to the ECS instance and run the `cat /etc/resolv.conf` command to view the DNS server addresses.


* If the default DNS server addresses are used, the response is as follows.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/bc832c5a8c1d41228daaaf571bebcb3f.png) </span>

* If the default DNS server addresses are not used, modify the DNS server addresses of the VPC and then reinstall the monitoring add\-on. For details, see [Custom VPC DNS](https://docs.byteplus.com/en/docs/vpc/Customizing-the-private-DNS).
