---
title: "StopDBInstance"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/stopdbinstance"
---

Call the StopDBInstance API to pause the instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The instance state must be Running.

* Only pay\-as\-you\-go instances can be stopped.

* Instances with blue\-green deployment and disaster recovery instances cannot be stopped.

* When an instance is stopped, its billing items are adjusted. Your account balance must be 100 USD or more, or you cannot pause or start an instance. To top up your account, refer to the [recharging instructions for details](https://docs.byteplus.com/en/docs/6269/100434). For more information on placing orders, refer to [Order Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-orders).

* An instance can be stopped for a maximum of one month. After an instance is stopped for one month, it automatically starts and billing resumes. If an instance does not meet the startup conditions, the stop period is automatically extended.

* After a stop instance operation is initiated, the system creates a full backup for the instance before stopping the instance. When a stopped instance is released due to overdue payments, its backups are retained according to the "Backup retention policy after instance release" set for the instance.

* If the account is in arrears during the instance suspension period, after recharging, the instance will still be in **Stopped**.

* While an instance is stopped:

   * The instance becomes inaccessible, and in the RDS for MySQL console, you can only view its Summary, Connectivity, and Backups pages. Except for starting the instance, downloading backups, restoring to a new instance, and modifying the instance backup policy, no other actions are supported while the instance is stopped.

   * The allowlists associated with the instance cannot be modified or deleted.

   * The instance will no longer provide external services, and its monitoring data may become abnormal, which can trigger alarm policies. In this case, you need to manually deactivate the alarm policies. Before stopping the instance, deactivate its alarm policies and re\-enable them after starting the instance to avoid excessive alarm noise.

   * The basic backup storage space provided for the instance remains free of charge. If we start charging for this storage space, we will make an announcement one month in advance.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=StopDBInstance&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-f30b1e0c\*\*\*\* |Instance ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=StopDBInstance&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-f30b1e0c****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250605211525971049EE8BF66F685294-e60d03",
        "Action": "StopDBInstance",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
