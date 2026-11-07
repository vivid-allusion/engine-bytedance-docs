---
title: "Creating IAM authentication policy"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Creating_IAM_authentication_policy"
---

If your database account uses IAM verification and you want to use this account to access a MySQL instance, you must first configure an IAM authentication policy. This policy ensures that the IAM user can successfully access the specified MySQL instance using a temporary token.

<span id="y0K5HH9s"></span>
## Prerequisites


* An [IAM user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user) has been created.

* A [database account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_and_managing_an_account?lang=en) has been created, and the verification method is IAM verification.


<span id="GyNaFvzh"></span>
## Procedure


1. Log in to the console using the root account.

2. In the left navigation pane, click **Permission policy**. Go to the **Permission policy** page.

3. On the **Permission policy** page, click [Create Policy](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user-custom-policy) **.**  The syntax is as follows:


```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "rds_mysql:ConnectDatabase"
      ],
      "Resource": [
        "trn:rds_mysql:*:<账号 ID>:instance/<实例 ID>/dbaccountname/<数据库账号>"
      ]
    }
  ]
}
```


Replace the **Account ID**, **Instance ID**, and **Database account** with actual values **.**  You can refer to the permission policy examples and create custom policies based on your specific business scenarios.


4. [Authorize the IAM user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-policies).


<span id="Fu9RdZu4"></span>
## Permission policy examples

<span id="dblk0Nbe"></span>
### Example 1: allowing users to connect to **a database account in a specified instance** by using IAM database verification

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "rds_mysql:ConnectDatabase"
      ],
      "Resource": [
        "trn:rds_mysql:*:21000xxxx:instance/mysql-b469b9axxxx/dbaccountname/testdb"
      ]
    }
  ]
}
```


<span id="RnPteNJq"></span>
### Example 2: allowing users to connect to **multiple database accounts in a specified instance** by using IAM database verification

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "rds_mysql:ConnectDatabase"
      ],
      "Resource": [
        "trn:rds_mysql:*:21000xxxx:instance/mysql-b469b9axxxx/dbaccountname/testdb",
        "trn:rds_mysql:*:21000xxxx:instance/mysql-b469b9axxxx/dbaccountname/testdemo"
      ]
    }
  ]
}
```


<span id="t4jsWE3I"></span>
### Example 3: allowing users to connect to all instances and database accounts by using IAM database verification

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "rds_mysql:ConnectDatabase"
      ],
      "Resource": [
        "trn:rds_mysql:*:21000xxxx:instance/*/dbaccountname/*"
      ]
    }
  ]
}
```


<span id="ncQmxHU8"></span>
### Example 4: allowing users to connect to all instances that contain a specified database account by using IAM database verification

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "rds_mysql:ConnectDatabase"
      ],
      "Resource": [
        "trn:rds_mysql:*:21000xxxx:instance/*/dbaccountname/testdemo"
      ]
    }
  ]
}
```
