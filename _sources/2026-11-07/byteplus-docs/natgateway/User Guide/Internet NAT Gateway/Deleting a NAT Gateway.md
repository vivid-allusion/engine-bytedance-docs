---
title: "Deleting a NAT Gateway"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Deleting-a-NAT-gateway"
---

When the Internet NAT Gateway is no longer needed, follow this topic to delete it.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

To delete the Internet NAT Gateway by the following procedure, ensure all the following conditions are met:


* The Internet NAT Gateway is Pay\-as\-you\-go, or the Subscription Internet NAT Gateway has expired. Deleting is not supported before a Subscription Internet NAT Gateway expires. To release it early, see [Unsubscription](https://docs.byteplus.com/en/docs/natgateway/Unsubscription).

* No SNAT entries exist under the Internet NAT Gateway. If any SNAT entries exist, [delete the SNAT entries](https://docs.byteplus.com/en/docs/natgateway/Managing-SNAT-rules#.5Yig6ZmkU05BVOinhOWImQ==) first.

* No DNAT entries exist under the Internet NAT Gateway. If any DNAT entries exist [delete the DNAT entries](https://docs.byteplus.com/en/docs/natgateway/Managing-DNAT-rules#.5Yig6ZmkRE5BVOinhOWImQ==) first.

* Internet NAT Gateway has no Elastic IP Address (EIP) associated. If have, [disassociate the EIP](https://docs.byteplus.com/en/docs/natgateway/Associating-or-disassociating-an-EIP#.6Kej57uR5YWs572RSVA=) first.

* Internet NAT Gateway is not managed by other cloud services. If managed, confirm it is no longer in use according to the management system tag and corresponding cloud service, then remove management.

   > When the Internet NAT Gateway is managed by a cloud service, the cloud service can use its features and control its permissions; users can only view and modify the managed Internet NAT Gateway, but cannot delete it.

   > When the Internet NAT Gateway is managed by a cloud service, a management system tag with the `tag key` `volc:{ServiceCode}:ServiceManaged` is added, such as `volc:vke:ServiceManaged`.   
   

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the Internet NAT Gateway list, click  **… \> Delete** to the right of the target Internet NAT Gateway.

4. Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[DeleteNatGateway](https://docs.byteplus.com/en/docs/natgateway/DeleteNatGateway): Delete an Internet NAT Gateway.
