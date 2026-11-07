---
title: "Connection diagnostics"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/Connection_diagnostics"
---

Cache for Redis provides connection diagnostics feature. When your client cannot connect to the Redis instance through public or private network addresses, you can use this feature to help troubleshoot connection issues.

## Applicable scenarios

Cache for Redis supports private and public network access methods and provides connection diagnosis features for both. Select the appropriate connection diagnosis scenario based on the connection address type your client needs.

> **tip**

> For more details on Redis connection address types, refer to [Viewing connection address](https://docs.byteplus.com/en/docs/redis/view-address).

|Client deployment type |Applicable connection diagnosis scenarios |
|---|---|
|The [ECS instance](https://console.byteplus.com/ecs/instance) where the client is deployed is in the same VPC network and region as the Redis instance. |At this time, you can access the Redis instance through the private connection address (including private address and direct connection address). If access fails, you can use the [Private network connection diagnosis](https://docs.byteplus.com/en/docs/redis/Connection_diagnostics#ygxF8o0j) feature to assist in troubleshooting. |
|* The [ECS instance](https://console.byteplus.com/ecs/instance) where the client is deployed is in the same region as the Redis instance, but not in the same VPC network.<br><br>* The [ECS instance](https://console.byteplus.com/ecs/instance) where the client is deployed is in a different region from the Redis instance.<br><br>* The client is deployed on a local server. |When the client deployment environment is any of the left options, the Redis instance must be accessed through the public network connection address. If public network access fails, you can use the [Public network connection diagnosis](https://docs.byteplus.com/en/docs/redis/Connection_diagnostics#bzWfssRc) feature to assist in troubleshooting. |

## Private network connection diagnosis

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance name.

4. On the instance details page, click on the **Connectivity** tab.

5. On the **Connectivity** tab, in the **Private network access \> Proxy private network access **  / **Direct private network access **  card, click the **Connection diagnosis** entry.

6. In the pop\-up **Connection diagnostics** panel, first confirm the configuration information of the current instance (including instance name, ID, availability zone, VPC, and subnet information), then configure the following settings.

   |Parameters |Description |
   |---|---|
   |Diagnosis type |Default is **Private connection**, no setup required. |
   |Client type |Fixed as **Select ECS instance**, no setup required. |
   |ECS instance |First select the ECS instance where the client is deployed from the dropdown list, then select the private IP addresses to be checked from the selected ECS instances. |

7. Click **Start check**.

## **Public network connection diagnosis**

> **tip**

> Cache for Redis disables public network access by default. To perform connection diagnosis for public network access, you need to manually enable public network access first. For specific procedures, refer to [Applying for public address](https://docs.byteplus.com/en/docs/redis/apply-public-address).

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance name.

4. On the instance details page, click on the **Connectivity** tab.

5. On the **Connectivity** tab, in the **Public network access \> Proxy public network access** / **Direct public network access** card, click the **Connection diagnosis** entry.

6. In the pop\-up **Connection diagnostics** panel, first confirm the configuration information of the current instance (including instance name/ID, availability zone, VPC, and subnet information), then select the corresponding actions based on the client deployment type.

   **Client deployed on ECS instance**

|Parameters |Description |
   |---|---|
   |Diagnosis type |Default is **Public connection**, no setup required. |
   |Client type |Default is **Select ECS instance**, no setup required. |
   |ECS instance |First select the ECS instance where the client is deployed from the dropdown list, then select the public IP addresses to be checked from the selected ECS instances. |

   **Client deployed on local server**

|Parameters |Description |
   |---|---|
   |Diagnosis type |Default is **Public connection**, no setup required. |
   |Client type |Select **Enter IP address**. |
   |IP address |Enter the public IP address used by the local server. |

7. Click **Start check**.

## **Subsequent operations**

1. After the diagnosis is complete, you can directly view the diagnosis results in the **Connection diagnostics** panel and modify relevant settings based on the diagnosis recommendations.

   > **warning**

   > This feature is only used to check whether the client IP address has been correctly added to Redis's access allowlist. If the current IP address passes the diagnosis but still cannot establish a connection, you need to perform further troubleshooting. For specific troubleshooting steps, refer to [What should I do if Redis connection fails](https://docs.byteplus.com/en/docs/redis/what-should-I-do-if-Redis-connection-fails).

   |Diagnosis result |Description |
   |---|---|
   |Diagnosis failed |Indicates that the IP address just checked has not been added to the current instance's allowlist. You can go to the **Allowlists** page and manually add the IP address to the specified allowlist. For specific procedures, refer to [Editing allowlist](https://docs.byteplus.com/en/docs/redis/edit-allowlist). |
   |Diagnosis passed |Indicates that the IP address just checked has been added to the current instance's allowlist. |

2. After the connection diagnosis is complete, you can access the Redis instance on the client using a private or public network address. For specific procedures, refer to:

   * [Connecting to instance via Redis-cli](https://docs.byteplus.com/en/docs/redis/connect-instances-through-redis-cli)

   * [Connecting to instance via client application](https://docs.byteplus.com/en/docs/redis/connect-instance-via-client)

   * [Connecting to instance via direct connection address](https://docs.byteplus.com/en/docs/redis/connect-instance-through-direct-connection-address)
