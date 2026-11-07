---
title: "Storage-compute separation best practices"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Storage-compute_separation_best_practices"
---

The Lakehouse Edition supports creating storage\-compute separation StarRocks instances. EMR has a built\-in instance profile TOS authentication mode. To create a StarRocks storage\-compute separation instance, select the corresponding TOS address and configure the appropriate access permissions during creation.

After creation, the instance can be used as an open\-source storage\-compute separation StarRocks instance.

<span id="_1-创建存算分离实例"></span>
## 1 Create a storage\-compute separation instance

<span id="_1-1-只有湖仓版支持存算分离，创建时选择湖仓版。"></span>
### 1.1 Only the Lakehouse Edition supports storage\-compute separation. Select the Lakehouse Edition during creation.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0e27a00c228f09cceac32ce837e5da79.png) </span>

<span id="_1-2-配置网络"></span>
### 1.2 Configure the network

Select the correct VPC and subnet according to your network plan. Nodes that need to access the instance must be able to communicate with the selected VPC and subnet.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7c39b397fb74a36d8b0d98e9f8753365.png) </span>

<span id="_1-3-配置存储位置"></span>
### 1.3 Configure the storage location

Select the TOS address for data storage in the TOS address field. You can choose an existing TOS address or create a new TOS bucket for storing storage\-compute separation data. It is recommended to use a dedicated TOS bucket to prevent other applications from modifying the data.

If you do not have permission for the selected TOS address, the interface will prompt for authorization. Click One\-Click Authorization to grant access.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c0df0ca3e84faec834a4e4c96e4e459a.jpg) </span>

<span id="_1-4-设置实例规格"></span>
### 1.4 Set the instance specifications

High availability is strongly recommended. Select the appropriate CN specifications and number of nodes based on your business requirements.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_16d67019f78853b21e6376f7292f00d5.png) </span>

<span id="_1-5-设置实例信息"></span>
### 1.5 Set the instance information

Select a maintenance window for operations management. EMR will perform version upgrades within the window as needed.

For public network access, enable the Public Network button.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91bc03eec9d1d7972787af4947eb9be1.png) </span>

<span id="_1-6-点击下一步完成创建实例"></span>
### 1.6 Click Next to complete instance creation

<span id="_2-数据导入与分析"></span>
## 2 Data import and analysis

<span id="_2-1-使用mysql客户端或工具连接实例"></span>
### 2.1 Connect to the instance using a MySQL client or tool


1. Obtain the connection address

   The connection address can be found in Instance Details \-\> Network Information.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_042171db5e9b02a1e642ef21395ab78a.png) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The client must be able to communicate with the subnet where the instance is located. If communication is not possible, add the corresponding allowlist in Security Management \-\> Allowlist Group to allow the relevant network to access the instance.   </div>
   

2. Add users

   New instance users can be added in User Management \-\> Add User. On the Add User page, set the username, password, user type, and database permissions to add a user. You can then use this username and password to log in to the database and perform other operations.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_888fb2daa3e26a66fe073f9e307c3cb2.png) </span>

3. Configure the allowlist


In Security Management \-\> Allowlist Group, you can configure the list of addresses allowed to access the instance. By default, clients within the same subnet can access the instance. To add a new access allowlist, click "Add Allowlist Group". Both individual IP addresses and network segments in CIDR format are supported.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f3b5fd79dc597e78b91b84834f308097.png) </span>

<span id="_2-2-创建数据库与数据表"></span>
### 2.2 Create a database and table

After connecting to the instance, you can create a database and table.

```sql
create database demo;
use demo;
CREATE TABLE IF NOT EXISTS tb_demo (
    c1  DATE        NOT NULL COMMENT "YYYY-MM-DD",
    c2  TINYINT     COMMENT "range [-128, 127]",
    c3  SMALLINT    COMMENT "range [-32768, 32767] ",
    c4  INT         COMMENT "range [-2147483648, 2147483647]",
    c5  BIGINT      COMMENT "range [-2^63 + 1 ~ 2^63 - 1]",
    c6  LARGEINT    COMMENT "range [-2^127 + 1 ~ 2^127 - 1]"
)
DUPLICATE KEY(c1, c2)
DISTRIBUTED BY HASH(c1, c2)
PROPERTIES (
    "in_memory" = "false"
);

insert into tb_demo values('2023-10-01', 2, 3, 4, 5, 6);

select * from tb_demo;
```


<span id="_2-3-查看tos上数据"></span>
### 2.3 View data on TOS

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_43d42de2e4f3d921a5444d1389cb79c2.png) </span>
