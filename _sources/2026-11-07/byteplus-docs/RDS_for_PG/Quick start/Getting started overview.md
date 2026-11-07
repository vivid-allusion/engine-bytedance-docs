---
title: "Getting started overview"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/use_process"
---

RDS for PostgreSQL is an elastic and reliable relational database service for BytePlus based on the open\-source PostgreSQL database system. This topic introduces the overall procedure for creating instances, databases, and accounts, adding IP allowlists, and connecting to the database in RDS for PostgreSQL.

<span id=".5YeG5aSH5bel5L2c"></span>
## Preparations

BytePlus console provides all\-in\-one functions for deploying and creating PostgreSQL instances. Before you create an instance, please create a BytePlus account first and complete real\-name authentication.

<span id=".5a6e5L6L57G75Z6L"></span>
## Instance types

Supports high\-availability instance types with a classic primary\-standby architecture, suitable for industries such as internet, IoT, retail e\-commerce, logistics, and gaming.

<span id=".5a6e5L6L6KeE5qC8"></span>
## Instance specifications

Parameters of the instance specification include CPU cores, memory size, and max connections. You can choose the appropriate specification for your business needs. For more information, refer to [Instance specifications](https://docs.byteplus.com/en/docs/RDS_for_PG/standard_instance_specification_modification).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

Follow the procedure below to create and use RDS for PostgreSQL instances:


1. **Create instance**: the first step to enable using RDS for PostgreSQL, determining the instance version, instance specification, and more. For instance creation methods, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance).

2. **Create a database and account**: Create the relevant databases and accounts based on business needs, and configure account permissions. For more information, refer to [Creating databases and accounts](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_databases_and_accounts).

3. **Add IP allowlists**: only devices included in the allowlists can access this instance. For details, refer to [Configuring allowlists](https://docs.byteplus.com/en/docs/RDS_for_PG/configuring_an_allowlist).

4. **Connect to the database**: supports multiple connection methods. You can connect to the instance using a client or a command line. For specific connection procedures, refer to [Connecting to the instance](https://docs.byteplus.com/en/docs/RDS_for_PG/connect_instance).
