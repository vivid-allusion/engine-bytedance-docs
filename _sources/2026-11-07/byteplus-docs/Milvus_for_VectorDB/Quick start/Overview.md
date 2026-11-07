---
title: "Overview"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Quick_start_overview"
---

This topic describes the preparations and usage process of Milvus for VectorDB.

<span id="H6EmvfrZ"></span>
## Preparations


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign up and verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* As per the regulations in the Chinese mainland, you must have completed real name registration before you can activate and use cloud services in regions in the Chinese mainland through BytePlus. For more details, refer to [Real name registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration).

* Cross\-service access has been authorized to allow Redis to access other services (such as VPC and EIP). For specific procedures, refer to [Cross-service access authorization](https://docs.byteplus.com/en/docs/redis/cross-service-access-authorization).


<span id="MCRaoIoA"></span>
## Usage process


1. **Cross\-service access authorization**

   Milvus for VectorDB uses other Volcengine services, such as VPCs, subnets, and CloudMonitor. To use the all features of Milvus for VectorDB, cross\-service access authorization is required.

2. **Set permissions for IAM users**

   Each root user can create multiple IAM users and assign different permissions to each IAM user to manage their access to cloud resources. For more information, see [Set permissions for IAM users (optional)](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Set_permissions_for_IAM_users_optional).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you use Milvus for VectorDB as a root user, you can skip this step.   </div>
   

3. **Create an instance**

   1. **Select the architecture type**

   Milvus for VectorDB supports enabling high availability multi\-node deployment. In practical business scenarios, enabling high availability deployment is recommended to ensure continuous service availability.

   2. **Select instance specification**

   Instance specifications refer to the specifications of service nodes and compute nodes, including the number of CPU cores and memory size. You can select appropriate specifications based on your business needs. For more information, see [Product specifications](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Product_specifications).

   3. **Create an instance**

   Create an instance based on the selected architecture type and instance specifications. For more information about how to create an instance, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance).

4. **Connect to the instance**

   Milvus for VectorDB supports connection and usage through clients. For more information about how to connect to an instance, see [Connect to an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Connect_to_the_instance).
