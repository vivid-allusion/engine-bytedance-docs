---
title: "Overview"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/connection-drivers-overview"
---

ByteHouse Cloud Data Warehouse Edition provides a wide range of connection driver tools to help you quickly access ByteHouse and carry out data development using different programming languages and frameworks. This article provides an introduction to the core features of the driver, the logic for selecting it, and important notes for its use.

<span id="b0ff8fa6"></span>
# Overview

You can connect ByteHouse and your application through a connection driver, supporting data query, data insertion, management, and other operations. Dimensions to consider when selecting a driver:


* **Development language**: Choose a driver that matches your technology stack, for example, select JDBC drivers for Java.

* **Protocol compatibility**: Must be consistent with the connection protocol of the ByteHouse service (TCP 19000, HTTP 8123, MySQL\-compatible port 3306).

* **Functional requirements**: Consider whether support is needed for ByteHouse custom settings, long connections (KeepAlive), and other features.


<span id="53b8a1a5"></span>
# Driver classification

The following table provides key information for each driver, grouped by development language, to help you select the connection driver you need.


|Language |Driver name |Supported protocols |Recommended version |Default timeout configuration |Is KeepAlive supported |Does ByteHouse support custom settings |
|---|---|---|---|---|---|---|
|Java |[ByteHouse JDBC Driver](https://docs.byteplus.com/docs/bytehouse/docs-bytehouse-jdbc-driver) |TCP（19000） |It is recommended to use the [latest](https://artifact.bytedance.com/repository/releases/com/bytedance/bytehouse/driver-java/) version |ping_timeout：10s<br><br>query_timeout：0s<br><br>send_timeout: Currently inactive<br><br>receive_timeout: Currently inactive<br><br>connect_timeout：0s |Supported by default |Supported |
||[ClickHouse JDBC Driver](https://docs.byteplus.com/docs/bytehouse/docs-clickhouse-jdbc-driver) |HTTP（8123） |It is recommended to use version [0.4.6](https://mvnrepository.com/artifact/com.clickhouse/clickhouse-jdbc/0.4.6). |socket_timeout：30000ms<br><br>connect_timeout：5s |Supported, requires JDK11 |Supported |
||[MySQL JDBC Driver](https://docs.byteplus.com/docs/bytehouse/mysql-jdbc-driver) |TCP（3306） |It is recommended to use version [8.3.0](https://mvnrepository.com/artifact/com.mysql/mysql-connector-j/8.3.0) |connectTimeout：0<br><br>socketTimeout：0 |Supported; requires JDK 11 |Not supported |
|Golang |[ClickHouse Go Driver](https://docs.byteplus.com/docs/bytehouse/docs-clickhouse-go-driver) |TCP（19000）<br><br>HTTP（8123） |We recommend using a V2 version earlier than [v2.30.0](https://github.com/ClickHouse/clickhouse-go/releases/tag/v2.30.0). |TCP：<br><br>dial_timeout：30s<br><br>read_timeout：300s<br><br>HTTP：<br><br>dial_timeout：30s<br><br>read_timeout：300s |TCP (19000): Supported (supported by default)<br><br>HTTP (8123): Supported (supported by default) |Supported |
||[MySQL Go Driver](https://docs.byteplus.com/docs/bytehouse/mysql-go-driver) |TCP（3306） |It is recommended to use version [1.8.1](https://github.com/go-sql-driver/mysql/releases/tag/v1.8.1) |timeout：0s<br><br>readTimeout：0s<br><br>writeTimeout：0s |Ssupported by default |Not supported |
|Python |[ClickHouse Python Driver](https://docs.byteplus.com/docs/bytehouse/docs-ClickHouse-Python-Driver) |TCP（19000） |It is recommended to use version [0.2.9](https://github.com/mymarilyn/clickhouse-driver/releases/tag/0.2.9). |connect_timeout：10s<br><br>send_receive_timeout：300s |Supported |Supported |
||[PyMySQL](https://docs.byteplus.com/docs/bytehouse/pymysql) |TCP（3306） |It is recommended to use version [1.1.2](https://github.com/PyMySQL/PyMySQL/releases/tag/v1.1.2) |connect_timeout：10s<br><br>read_timeout：none<br><br>write_timeout：none |Supported |Not supported |
||[ClickHouse SQLAlchemy Connector](https://docs.byteplus.com/docs/bytehouse/clickhouse-sqlalchemy-connector) |TCP（19000） |Recommended versions:<br><br><br>* SQLAlchemy [v2.0.38](https://pypi.org/project/SQLAlchemy/2.0.38/)<br><br>* Clickhouse Connect [v0.3.2](https://pypi.org/project/clickhouse-sqlalchemy/0.3.2/)<br><br>* Bytehouse Connect [v0.3.2](https://github.com/bytehouse-docs/ecosystem/blob/main/dist/clickhouse-sqlalchemy/clickhouse-sqlalchemy-0.3.2%2Bbytehouse.tar.gz)<br><br>* Python v3.10 |None |Supported |Supported |
||[MySQL SQLAlchemy Conncetor](https://docs.byteplus.com/docs/bytehouse/mysql-sqlalchemy-conncetor-cdw) |None |Recommended versions:<br><br><br>* SQLAlchemy Version [v2.0.41](https://pypi.org/project/SQLAlchemy/2.0.41/)<br><br>* Python v3.12.6 |None |Not supported |Not supported |
|C# |[ClickHouse C# Driver](https://docs.byteplus.com/docs/bytehouse/clickhouse-c-driver) |HTTP（8123） |It is recommended to use v[7.13.0](https://github.com/DarkWanderer/ClickHouse.Client/releases/tag/7.13.0). |Timeout：120s |Not supported |Supported |
|Rust |[ClickHouse Rust (HTTP) Driver](https://docs.byteplus.com/docs/bytehouse/clickhouse-rust-http-driver) |HTTP（8123） |It is recommended to use v[0.13.1](https://crates.io/crates/clickhouse/0.13.1) |send_timeout：None<br><br>end_timeout：None |Support project |Supported |
|PHP |[ClickHouse PHP Driver](https://docs.byteplus.com/docs/bytehouse/docs-bytehouse-php-connection) |HTTP（8123） |It is recommended to use v[1.6.0](https://github.com/smi2/phpClickHouse/releases/tag/1.6.0). |setConnectTimeOut：5s<br><br>setTimeout：20s<br><br>setTimeout: specifies the max_execution_time parameter of ClickHouse |Not supported |Supported |


<span id="1f94db82"></span>
# Other driver tools

In addition to the language\-specific drivers mentioned above, ByteHouse also supports connectors for the following tools/frameworks, which are suitable for specific scenarios:


* [ClickHouse NodeJS](https://docs.byteplus.com/docs/bytehouse/ClickHouse-NodeJS): Suitable for HTTP protocol driver for the Node.js environment and supports server\-side JavaScript development scenarios.

* [Flink Connector Driver](https://docs.byteplus.com/docs/bytehouse/Flink_Connector): Suitable for data synchronization between the Flink real\-time computing engine and ByteHouse, to satisfy streaming data processing requirements;

* [Spark Connector Driver](https://docs.byteplus.com/docs/bytehouse/spark-connector-driver): Suitable for data interaction between the Spark batch processing engine and ByteHouse, adapted for offline big data analysis scenarios.
