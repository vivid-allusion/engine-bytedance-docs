---
title: "Connecting to instance via client application"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/connecting_to_an_instance_via_a_client_application"
---

You can establish a connection using any PostgreSQL\-compatible client program. This topic introduces operations for connecting to PostgreSQL instances via client applications.

<span id=".5YeG5aSH5bel5L2c"></span>
## Preparations

Complete the following actions based on the deployment location of the client program.


|Client program deployment location |Procedures to be executed |
|---|---|
|[ESC instance](https://console.byteplus.com/ecs/instance) (recommended) |1. Ensure the ECS instance and the PostgreSQL instance belong to the same VPC network.<br><br>2. Obtain the private IP address of the ECS instance.<br><br>3. Add the ECS instance’s private network IP address to the RDS for PostgreSQL instance’s allowlists For specific procedures, refer to[ Creating an allowlist](https://docs.byteplus.com/en/docs/RDS_for_PG/configuring_an_allowlist). |
|Local device |1. The RDS for PostgreSQL edition provides only private network addresses by default. Local applications must apply for a public network address for the PostgreSQL instance before accessing it. For more information about how to apply for a public address, refer to [Applying for public address](https://docs.byteplus.com/en/docs/RDS_for_PG/enabling_internet_access).<br><br>2. Run the command `curl ipinfo.io \|grep ip` on the device where the local client resides to retrieve the local client’s public network IP address. Example output:<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/4ecf4b1c5be84d75a9ff52ddd50049b6) </span><br><br>3. Add the local client’s public network IP address to the PostgreSQL instance’s IP allowlists. For specific procedures, refer to [Creating an allowlist](https://docs.byteplus.com/en/docs/RDS_for_PG/configuring_an_allowlist). |


<span id=".5aaC5L2V6I635Y-W6L-e5o6l5L-h5oGv"></span>
## How to retrieve connection information

Generally, when connecting to an RDS for PostgreSQL instance through a client program, you need to retrieve the following connection information.


|Information to retrieve |Retrieval method |
|---|---|
|Instance connection address |RDS for PostgreSQL supports multiple types of addresses. We recommend that you use private addresses for connection. For more information about connection address types, refer to [Connection address types](https://docs.byteplus.com/en/docs/RDS_for_PG/type_of_address). |
|Port number |The PostgreSQL instance uses port 5432 by default. |
|Instance account |You need to create an account to use the PostgreSQL instance. For more information about instance accounts, refer to [Creating and managing accounts](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_and_managing_an_account). |
|Account password |Support account and password verification format using `<username> <password>`<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you forget your password, you can reset it. For specific operations, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/resetting_an_account_password">Resetting account password</a>.</div><br> |
