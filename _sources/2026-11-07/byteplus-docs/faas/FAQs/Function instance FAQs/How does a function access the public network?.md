---
title: "How does a function access the public network?"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/How_does_a_function_access_the_public_network"
---

A function supports accessing the public network through two methods: shared NAT gateway and private NAT gateway.


* **Shared NAT gateway**

   In the default scenario, the function accesses the public network through the shared NAT gateway provided by the platform. The outbound IP for this method is dynamically assigned, with none fixed value.

* **Private NAT gateway**

   If the function is configured to associate a VPC network, you can select to access the public network through the private NAT gateway associated with that VPC. After you bind an elastic public IP (EIP) to the NAT gateway, the outbound IP for the public network can be fixed. For details on Actions, see [create a public NAT gateway](https://docs.byteplus.com/en/docs/natgateway/Creating-an-Internet-NAT-gateway).


For details on the function network configuration description, see [network configuration](https://docs.byteplus.com/en/docs/faas/Function_configuration?#.572R57uc).
