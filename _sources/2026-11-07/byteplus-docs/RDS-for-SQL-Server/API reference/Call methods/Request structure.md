---
title: "Request structure"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/request-structure"
---

This topic describes API request structure information for RDS for SQL Server.

<span id="service-address"></span>
## **Service address**

The regions where RDS for SQL Server has been opened are as follows.


|Regions |RegionId |**Endpoint** |
|---|---|---|
|China (Beijing) |cn\-beijing |rds\-mssql.cn\-beijing.byteplusapi.com |
|China (Shanghai) |cn\-shanghai |rds\-mssql.cn\-shanghai.byteplusapi.com |
|China (Guangzhou) |cn\-guangzhou |rds\-mssql.cn\-guangzhou.byteplusapi.com |
|China (Hong Kong) |cn\-hongkong |rds\-mssql.cn\-hongkong.byteplusapi.com |
|Asia Pacific (Johor) |ap\-southeast\-1 |rds\-mssql.ap\-southeast\-1.byteplusapi.com |
|Asia Pacific(Indonesia） |ap\-southeast\-3 |rds\-mssql.ap\-southeast\-3.byteplusapi.com |


<span id="communication-protocol"></span>
## **Communication protocol**

Support for request communication via HTTP or HTTPS, and it is recommended to use a more secure HTTPS method to send requests.

<span id="request-method"></span>
## **Request method**

Supports the HTTP POST request method, where the `Content-Type` type supported by the POST request is application/JSON (recommended).

<div data-tips="true" data-tips-type="tip">tip</div>


<div data-tips="true" data-tips-type="tip">Requests must use the Volcano <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/signature-mechanism">Signature mechanism</a>.</div>


<span id="request-parameters"></span>
## **Request parameters**

Each API request contains the following two types of parameters:


* Public request parameters: The parameters that each API interface needs to use are public request parameters. For more information about public parameters, see [Common parameters](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/common-parameters).

* Interface request parameters: The parameters specific to each API interface are interface requests. For the request parameters for each interface, see the detailed description of each interface in the [API overview](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/api-references).


<span id="character-encoding"></span>
## **Character encoding**

All use `UTF-8` encoding.
