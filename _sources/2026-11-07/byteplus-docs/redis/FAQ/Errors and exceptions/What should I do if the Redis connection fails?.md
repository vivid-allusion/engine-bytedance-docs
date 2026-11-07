---
title: "What should I do if the Redis connection fails?"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/what-should-I-do-if-Redis-connection-fails"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Problem phenomenon

When problems such as being unable to connect to the Redis instance or experiencing connection interruptions even after a successful connection occur, you can refer to the steps in this topic for troubleshooting.

<span id=".5o6S5p-l5q2l6aqk"></span>
## Troubleshooting step


|Troubleshooting step |Solutions |
|---|---|
|1. Connection diagnostics |Cache for Redis provides a connection diagnostics feature to check whether the client IP address has been correctly added to the Redis allowlist. For specific procedures, refer to [Connection diagnostics](https://docs.byteplus.com/en/docs/redis/Connection_diagnostics) to check.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the client IP address changes dynamically, the new IP address needs to be promptly added to the instance allowlist. To avoid frequent modifications, it is recommended to assign a fixed IP to the client.</div><br> |
|2. Confirm network environment |You can use the `PING` command to test the network connection between the Redis instance and ECS. If the PING fails, consider checking the following points:<br><br><br>* If the client accesses the instance through a private IP address, ensure that the Redis instance and the ECS instance you want to connect to are in the same Virtual Private Cloud (VPC). If they are not in the same VPC, you can [modify VPC](https://docs.byteplus.com/en/docs/redis/modify-vpc-or-subnet) for the Redis instance or [enable public network access](https://docs.byteplus.com/en/docs/redis/apply-public-address).<br><br>* Confirm whether the ECS configuration is correct, for example, whether the IP and port settings in the security groups rules are correct, and whether a firewall is set up. For more details, refer to [Viewing and modifying security groups access rules](https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules). |
|3. Confirm connection configuration |You can refer to the following points to check and confirm whether the connection configuration is correct:<br><br><br>* Obtained the correct connection address. Redis provides private and public network connection addresses. Please ensure you use the correct connection address when connecting to the instance. For specific procedures, refer to [Viewing connection address](https://docs.byteplus.com/en/docs/redis/view-address).<br><br>* Correct database account and password were used. When errors such as `ERR NOAUTH Authentication required` or `ERR invalid password` occur, it indicates that the database account password format is incorrect. You can try [resetting password](https://docs.byteplus.com/en/docs/redis/reset-password). |
|4. Is there any upgrade or maintenance event |To continuously improve product performance and stability, the system will perform maintenance operations such as software and hardware upgrades or network upgrades on the machines where Redis instances are located. During the execution of maintenance events, instance node switching may occur, and there may be seconds of unwritable or temporary disconnection during the node switching process. For more details, refer to [Event center](https://docs.byteplus.com/en/docs/redis/event-center) and [Failover](https://docs.byteplus.com/en/docs/redis/failover). |
|5. Other scenarios |If you still cannot connect to the Redis instance after trying the above troubleshooting steps, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support. |
