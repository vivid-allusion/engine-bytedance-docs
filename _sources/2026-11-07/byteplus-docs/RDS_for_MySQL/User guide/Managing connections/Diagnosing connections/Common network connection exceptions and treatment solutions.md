---
title: "Common network connection exceptions and treatment solutions"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/connection_diagnosis"
---

This topic lists common connection exceptions in connection diagnosis and corresponding treatment solutions.

## Public network connection diagnosis

* **Exception item**: Exception of MySQL instance state

   **Treatment solution**: The MySQL instance status cannot be **Deleting**, **Waiting for Payment**, **Shutting Down**, **Shut Down**, **Billing Recovery**, **Billing Recycling**, **Recycled**, **Released**, **Destroying**, **Destroyed**, **Creation Failed**, or **Error**.

* **Exception item**: Exception of MySQL allowlist policy

   **Treatment solution**: Confirm that the MySQL allowlist includes the current public IP. For details about modifying the MySQL instance allowlist, refer to [Modifying allowlist](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_an_allowlist).

## Private network connection diagnosis

* **Exception item**: Exception of MySQL instance state

   **Treatment solution**: The MySQL instance status cannot be **Deleting**, **Waiting for Payment**, **Shutting Down**, **Shut Down**, **Billing Recovery**, **Billing Recycling**, **Recycled**, **Released**, **Destroying**, **Destroyed**, **Creation Failed**, or **Error**.

* **Exception item**: Exception of ECS instance status

   **Treatment solution**: Confirm that the ECS instance status is **Running**.

* **Exception item**: Exception of whether ECS and MySQL instances are in the same VPC

   **Treatment solution**: Confirm that the ECS instance and the MySQL instance are in the same Virtual Private Cloud. The private network used by the MySQL instance supports modification. To make changes, refer to [Modifying instance network configuration](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_instance_network_configuration).

* **Exception item**: Exception of ECS security groups policy

   **Treatment solution**: Confirm that the outbound rules allow the passage of the MySQL private network address and connection port. For more information, refer to [Manage security group rules](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules).

* **Exception item**: Exception of ECS and MySQL network type consistency

   **Treatment solution**: Confirm that the ECS IP protocol includes the MySQL IP protocol.

* **Issue**: Exception of MySQL allowlist policy.

   **Solution**: Confirm that the ECS private network IP address has been added to the allowlist of the MySQL instance. For details about modifying the MySQL instance allowlist, refer to [Modifying allowlist](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_an_allowlist).

## caching_sha2_password authentication error

* **Exception item**: When connecting to MySQL 8.0 or later instances (either a direct connection or a connection through the database proxy), caching_sha2_password related authentication errors occur. For example, MySQL Connector/J reports `Public Key Retrieval is not allowed`, MySQL C API / libmysqlclient reports `RSA public key not available`, or the client returns `Access denied for user`.

   **Treatment solution**: This error occurs during the full authentication phase of the caching_sha2_password plugin, typically when a user or client IP address connects to the instance for the first time and the server has not yet cached the authentication credentials. Ensure that at least one of the following conditions is met, then try again:

   * SSL encryption is enabled, and TLS is enabled on the client for data transmission.

   * The client is configured to use a local file containing the RSA public key of the MySQL server.

   * In a trusted network environment, the client is allowed to retrieve the RSA public key from the server when establishing a connection.

   For specific parameter settings for clients in different programming languages (MySQL Connector/J, MySQL Connector/NET, MySqlConnector for .NET, and MySQL C API / libmysqlclient), see [Connect to an instance using caching_sha2_password authentication](https://docs.byteplus.com/en/docs/RDS_for_MySQL/connecting_to_an_instance_via_client_application?lang=en#nhMHsjRW).
