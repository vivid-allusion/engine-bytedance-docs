---
title: "Identity and permission configuration"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Identity_and_permission_configuration"
---

When using Proton to operate object storage, you need to configure the IAM identity information for performing operations and ensure that the user or role executing the operations has the corresponding permissions; otherwise, issues such as insufficient permissions may occur. Proton supports multiple methods for configuring identity information. The following is a brief explanation.

<span id="eec30c1f"></span>
## IAM identity information configuration

Proton supports setting IAM identity information for operating object storage through environment variables, configuration files, and EMR ECS internal services. Users can select the method that best suits their business scenario from the options below.

<span id="99d736d9"></span>
### TOS scenario

<span id="e973da99"></span>
#### Environment variables

Configure the following parameters in the `core-site.xml` file

```XML
<configuraiton>
    <property>
        <name>fs.tos.credentials.provider</name>
        <value>io.proton.common.object.tos.auth.EnvironmentCredentialsProvider</value>
    </property>
</configuraiton>
```



|Environment variables |Required |
|---|---|
|TOS_ACCESS_KEY_ID |Yes |
|TOS_SECRET_ACCESS_KEY |Yes |
|TOS_SESSION_TOKEN |No |


<span id="4754c7ef"></span>
#### core\-site.xml configuration file

Configure the following parameters in the `core-site.xml` file. In this mode, you can configure dedicated identity information for different Buckets. When Proton reads identity information, it first checks whether the corresponding Bucket has dedicated identity information, and then checks the global configuration information.

```XML
<configuraiton>
    <property>
        <name>fs.tos.credentials.provider</name>
        <value>io.proton.common.object.tos.auth.SimpleCredentialsProvider</value>
    </property>
    <!-- Global configuration -->
    <property>
        <name>fs.tos.access-key-id</name>
        <value>xxxxxxxxxxxxxx</value>
    </property>
    <property>
        <name>fs.tos.secret-access-key</name>
        <value>xxxxx</value>
    </property>
    
    <!-- Optional -->
    <property>
        <name>fs.tos.session-token</name>
        <value>xxxxx</value>
    </property>
    
    <!-- Bucket-level configuration -->
    <property>
        <name>fs.tos.bucket.bucketA.access-key-id</name>
        <value>xxxxxxxxxxxxxx</value>
    </property>
    <property>
        <name>fs.tos.bucket.bucketA.secret-access-key</name>
        <value>xxxxx</value>
    </property>
    <property>
        <name>fs.tos.bucket.bucketA.session-token</name>
        <value>xxxxx</value>
    </property>
</configuraiton>
```


<span id="ceacd206"></span>
#### Custom XML configuration file

Configure the following parameters in the `core-site.xml` file. In this mode, you can configure dedicated identity information for different Buckets. When Proton reads identity information, it first checks whether the corresponding Bucket has dedicated identity information, and then checks the global configuration information.

```XML
<configuraiton>
    <property>
        <name>fs.tos.credentials.provider</name>
        <value>io.proton.common.object.tos.auth.FileCredentialsProvider</value>
    </property>
    <property>
        <name>fs.tos.credentials.file.path</name>
        <value>/xxxxxxx/xxx.xml</value>
    </property>
    <!-- File content refresh interval -->
    <property>
        <name>fs.tos.credentials.file.refresh.interval</name>
        <value>5000</value>
    </property>
</configuraiton>
```


Content of the custom XML file

```XML
<configuraiton>
    <property>
        <name>fs.tos.access-key-id</name>
        <value>xxxxxxxxxxxxxx</value>
    </property>
    <property>
        <name>fs.tos.secret-access-key</name>
        <value>xxxxx</value>
    </property>
    
    <!-- Optional -->
    <property>
        <name>fs.tos.session-token</name>
        <value>xxxxx</value>
    </property>
    
    <!-- Bucket-level configuration -->
    <property>
        <name>fs.tos.bucket.您的bucket.access-key-id</name>
        <value>xxxxxxxxxxxxxx</value>
    </property>
    <property>
        <name>fs.tos.bucket.您的bucket.secret-access-key</name>
        <value>xxxxx</value>
    </property>
    <property>
        <name>fs.tos.bucket.您的bucket.session-token</name>
        <value>xxxxx</value>
    </property>
</configuraiton>
```


<span id="5f731c6f"></span>
#### EMR cluster ECS internal service

When the runtime environment is Volcano EMR, you can configure the following parameters in the `core-site.xml` file. The EMR cluster will use the ECS role (such as VEECSforEMRRole) to access TOS. In EMR out\-of\-the\-box mode, when using this authentication method, you must ensure that the corresponding ECS role has permission to operate TOS data.

```XML
<configuraiton>
    <property>
        <name>fs.tos.credentials.provider</name>
        <value>io.proton.common.object.tos.auth.IAMInstanceCredentialsProvider</value>
    </property>
</configuraiton>
```


<span id="f5cae9be"></span>
## IAM identity permission configuration

When Proton operates TOS, the following actions are involved. You need to authorize the IAM identity performing the operations according to your business requirements. For details, refer to [TOS IAM policy overview](https://www.volcengine.com/docs/6349/102131).


|Action |HDFS use cases |Required |
|---|---|---|
|HeadBucket |Obtain bucket information, such as bucket type |Yes |
|ListBucket |List directories/files |No |
|GetObjectTagging |Set attribute\-related information ||
|PutObjectTagging |||
|DeleteObjectTagging |||
|GetFileStatus |GetFileStatus use cases ||
|HeadObject |||
|GetSymlink | ||
|GetSymlink | ||
|GetObject |Read file content ||
|PutObject |Write files, create directories ||
|AppendObject |||
|CreateMultipartUpload |||
|UploadPart |||
|CompleteMultipartUpload |||
|AbortMultipartUpload |||
|ListMultipartUploadParts |||
|RenameObject |Rename directories, rename files ||
|CopyObject |||
|UploadPartCopy |||
|DeleteObject |Delete directories, delete files ||
|DeleteObjects |||
|SetObjectMeta |Set directory/file metadata, such as ACL, group, owner, time, and so on ||
|RestoreObject |Restore cold storage data using Proton CLI ||


<span id="1c0a8737"></span>
### Authorization examples

<span id="bb881722"></span>
#### Authorize an IAM user with all permissions for the storage bucket `test`

```JSON
{ 
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tos:*"
            ],
            "Resource": [
                "trn:tos:::test",
                "trn:tos:::test/*"
            ]
        }
    ]
 }
```


<span id="758296b1"></span>
#### Grant an IAM user read\-only permission for the storage bucket `test`

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "tos:Head*",
        "tos:List*",
        "tos:Get*",
      ],
      "Resource": [
        "trn:tos:::test",
        "trn:tos:::test/*"
      ]
    }
  ]
}
```


<span id="5bb924cd"></span>
#### Grant an IAM user all permissions for the `abc` directory and its subdirectories within the storage bucket `test`

```JSON
{ 
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tos:*"
            ],
            "Resource": [
                "trn:tos:::test/abc",
                "trn:tos:::test/abc/*"
            ]
        }
    ]
 }
```


<span id="9732b081"></span>
#### Grant IAM users all permissions in bucket `test` except for the `abc` directory

```JSON
{ 
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tos:*"
            ],
            "Resource": [
                "trn:tos:::test",
                "trn:tos:::test/*"
            ]
        },
        {
            "Effect": "Deny",
            "Action": [
                "tos:*"
            ],
            "Resource": [
                "trn:tos:::test/abc",
                "trn:tos:::test/abc/*"
            ]
        }
    ]
 }
```
