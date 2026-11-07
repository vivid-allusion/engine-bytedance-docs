---
title: "Code examples"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Code_examples_python"
---

This article introduces code examples of NDB for MySQL Python SDK for your reference.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The [Downloading and installing SDK](https://www.byteplus.com/en/docs/NDB_for_MySQL/Downloading_and_installing_SDK_python) has been completed.

* The [Initializing client](https://www.byteplus.com/en/docs/NDB_for_MySQL/Initializing_client_python) has been completed.


<span id=".6K-35rGC6LaF5pe25pe26Ze06K6-572u"></span>
## Request timed out time settings

When calling an interface using the SDK, there is no timeout limit by default. When initiating an API call request, you can add the `_request_timeout` parameter at the end of the code to specify the request timeout (in seconds). If the request is not completed within this time, the request will be terminated immediately and a timeout error will be reported. For example, you can set the timeout to 10 seconds with the following code when calling the [DescribeDBInstanceDetail](https://www.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceDetail) interface.

```python
req = byteplussdkvedbm.DescribeDBInstanceDetailRequest(
    instance_id="your instance id"
)

resp = client.describe_db_instance_detail(req, _request_timeout=10)  # There is a problem with the return value of vcpu
```


<span id=".5Yib5bu6LXZlZGItbXlzcWwt5a6e5L6L"></span>
## Creating an instance

For a detailed description of the parameters in the following example, see [CreateDBInstance](https://www.byteplus.com/en/docs/NDB_for_MySQL/CreateDBInstance#请求参数).

```python
def create_db_instance():
    client = init_client()

    req = byteplussdkvedbm.CreateDBInstanceRequest(
        charge_type="PostPaid",
        db_engine_version="MySQL_8_0",
        db_time_zone="UTC +08:00",
        instance_name="your instance name",
        lower_case_table_names="0",
        node_number=2,
        node_spec="vedb.mysql.x4.large",
        subnet_id="your subnet id",
        super_account_name="your super account name",
        super_account_password="your super account password",
        vpc_id="your vpc id",
        zone_ids="cn-beijing-b",
    )

    resp = client.create_db_instance(req)
    print(resp)
```


<span id=".5p-l6K-iLXZlZGItbXlzcWwt5a6e5L6L5L-h5oGv"></span>
## Query instance information

```python
def describe_db_instance_detail():
    client = init_client()
    req = byteplussdkvedbm.DescribeDBInstanceDetailRequest(
        instance_id="your instance id"
    )

    resp = client.describe_db_instance_detail(req)
    print(resp)
```
