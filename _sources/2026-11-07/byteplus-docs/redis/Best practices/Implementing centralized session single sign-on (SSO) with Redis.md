---
title: "Implementing centralized session single sign-on (SSO) with Redis"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/implement_centralized_session_SSO"
---

This article introduces a centralized session single sign\-on solution using Cache for Redis.

## Objective

As enterprise information systems expand and their architectures become more complex, users often need to switch frequently between different business platforms. The traditional independent login mode for multiple systems not only leads to cumbersome operations and fragmented experiences, but may also introduce security risks due to the repeated management of account information. To address these challenges, single sign\-on (SSO) technology emerged and has gradually become a common solution for unified identity authentication and access management.

This solution is designed for multi\-system integration within enterprises and unified identity authentication in microservices architectures. It leverages the centralized session management capabilities of Redis to build an efficient, stable, and scalable SSO system. With this system, users only need to log in once at the auth server to seamlessly access all authorized business systems without re\-authentication. This improves user convenience and enhances the overall security of enterprise systems.

This solution achieves the following objectives:

* Share login status across multiple business systems, allowing users to seamlessly access all authorized services with a single login.

* Use Redis as a centralized session store to ensure session consistency and high availability in a distributed environment.

* Design simple and clear login and logout flows to ensure a secure and reliable authentication process.

* Build a clear and straightforward system architecture and code implementation to facilitate future maintenance and feature expansion.

## Architecture

### Core components

The SSO login system includes the following core components:

* **Auth server**

   As the unified entry point for user authentication, this component receives user log in requests and verifies their identity. After successful authentication, the system generates a unique session ID in Redis and sends it to the client's browser via an HTTP cookie to establish a login session. The auth server also provides logout interface to clear sessions and cookies for unified logout.

* **Centralized session storage with Redis**

   Redis, a high\-performance in\-memory database, centrally stores all login sessions. All service systems access Redis to share the same session data, enabling cross\-system sharing of the login status and ensuring state consistency and efficient access in a distributed environment.

* **Service systems**

   Each service system (such as Service A and Service B) reads the session ID from the client's cookie and queries Redis for the corresponding user information to determine if the user has logged in. If the login is valid, the service system allows the user to access corresponding resources. Otherwise, the user is redirected to auth server's login page to complete the unified authentication process.

The system architecture design for implementing centralized session single sign\-on based on Cache for Redis is shown in the diagram below.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_36f709eb2fa2ebc992a4dcbba5f28fac.png)

### Architecture advantages

This architecture has the following advantages:

* **Centralized session storage**

   Implementing unified storage and management of sessions based on Redis solves the problem of state synchronization of traditional single\-machine sessions in a distributed environment, ensuring that all business systems can obtain the latest user login status in real\-time.

* **Cookie\-based seamless state transfer**

   After a user logs in to the auth server, the system writes session ID to HTTP cookie. The browser then automatically includes this cookie when accessing business systems, enabling seamless transfer of the login state.

* **Unified login and logout process**

   Users only need to log in once at the auth server, and the system shares the login status across all business systems. Upon logout, the auth server clears the session from Redis and the browser cookie. This simultaneously revokes access rights for all business systems, ensuring security.

* **Flexible system extensibility**

   With sessions centrally stored in Redis, new business systems can be quickly integrated into the existing authentication system. They simply need to connect to Redis to validate sessions, which eliminates the need for complex integration and reduces maintenance complexity and costs.

## Implementation

### Preparation

Prepare the following resources and complete the necessary configurations.

|Resource category |Required configuration |
|---|---|
|Redis |This solution requires the following Cache for Redis resources:<br><br><br>* Create Redis 7.0 instance. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/redis/create-instance).<br><br>* Configure an access allowlist for the Redis instance. For specific procedures, refer to [Creating allowlist](https://docs.byteplus.com/en/docs/redis/create-allowlist). |
|ECS |This solution requires the following ECS\-related resources:<br><br><br>* Create ECS instance. For specific procedures, refer to [Purchasing and using ECS instance](https://docs.byteplus.com/en/docs/ecs/Buying-and-using-ECS-instances).<br><br>* Install the Redis Python client and Flask dependency packages on the [ECS](https://console.byteplus.com/ecs/instance) server.<br><br>   > **tip**<br>   <br><br>   > Ensure you are using Python 3.10. You can run the `python --version` command to check the current Python version.<br>   <br><br>* The ports used by the login system in this solution are `5000`, `5001`, and `5002`. Therefore, you must add these three ports to the security group rules for your ECS instance, ensuring that both outbound and inbound rules allow access to these three ports. To configure security group rules, refer to [Adding security group](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules). |

### Procedure

1. Log on to ECS instance where the required environment is installed. For specific procedures on logging on ECS instance, refer to [Logging on to instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-an-instance).

2. In the command\-line window or terminal of ECS instance, execute following command to clone code.

   ```Bash
   git clone https://github.com/byteplus-sdk-samples/cache_for_redis_examples/tree/main/sso_login
   ```

3. Go to the directory of SSO login system project, find `config.py` file, and modify corresponding configuration according to actual situation of your Redis and ECS instances.

   > Description

   * > The following code shows only the configuration for Cache for Redis and ECS instances in the SSO login system project.

   * > You can view the public IP address of specified ECS instance on the list page of the [ECS console](https://console.byteplus.com/ecs/instance). For specific procedures, refer to [Viewing instance information](https://docs.byteplus.com/en/docs/ecs/Instance-overview-1).

   * > You can view the connection address and port number of the instance on Redis console. For specific procedures, refer to [Viewing connection address](https://docs.byteplus.com/en/docs/redis/view-address).

   * > If you forget the password for the default account of your Redis instance, you can reset the password on the console. For specific procedures, refer to [Resetting password](https://docs.byteplus.com/en/docs/redis/reset-password).

   ```Python
   # config
   
   # ESC IP or domain name
   SERVER_HOST = '<Public IP of ECS>'
   
   # auth server configuration
   AUTH_SERVER_PORT = 5000
   
   # Service A configuration
   SERVICE_A_PORT = 5001
   
   # Service B configuration
   SERVICE_B_PORT = 5002
   
   # Redis configuration
   REDIS_HOST = '<Connection address of Redis instance>'
   REDIS_PORT = <Port of Redis connection address, default port 6379>
   REDIS_PASSWORD = <Password for default account in Redis instance>
   
   # Session validity period (seconds)
   SESSION_EXPIRE = 3600
   ```

   The code example is as follows.

   ```Python
   # config
   
   # ESC IP or domain name
   SERVER_HOST = '180.184.***.***'
   
   # auth server configuration
   AUTH_SERVER_PORT = 5000
   
   # Service A configuration
   SERVICE_A_PORT = 5001
   
   # Service B configuration
   SERVICE_B_PORT = 5002
   
   # Redis configuration
   REDIS_HOST = 'redis-cnlfwm1ecuiqv****.redis.ibytepluses.com'
   REDIS_PORT = 6379
   REDIS_PASSWORD = '<your-redis-password>'
   
   # Session validity period (seconds)
   SESSION_EXPIRE = 3600
   ```

4. In the root directory of SSO login system project, execute following command to start service.

   ```Bash
   python3 auth_server.py
   python3 service_a.py
   python3 service_b.py
   ```

5. Open a browser and enter `http://<ECS public IP>:5000/login` in the address bar to access the auth server of the SSO login system.

   The code example is as follows.

   ```Plain Text
   http://180.184.***.***:5000/login
   ```

## Result

> **tip**

> Before you proceed, the login credentials for two users, `user1: password1` and `user2: password2`, are hardcoded in the `login` function of the `auth_server.py` file in the SSO login system project.

1. On the access auth server page of the SSO login system, enter a username (e.g., `user1`) and password (e.g., `password1`), and then click **Login** to authenticate.

2. After successful login, you will be automatically redirected to the service selection page to select **Service A** or **Service B**.

   This example uses Service A. Once selected, you are redirected to the service webpage and logged in without re\-entering your password. This is because the system has already requested the user's session from Redis, which the browser automatically sends via a cookie.

   When a user logs out or their session expires, the system clears the session from Redis. The user must re\-authenticate to log in again.
