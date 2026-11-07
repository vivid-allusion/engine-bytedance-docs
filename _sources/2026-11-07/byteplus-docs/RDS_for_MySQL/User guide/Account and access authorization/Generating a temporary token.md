---
title: "Generating a temporary token"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Generating_a_temporary_token"
---

RDS for MySQL instances support two verification methods for accounts: password verification and IAM verification. If the verification method for an account is IAM verification, you need to acquire a temporary token for the account. This topic describes how to acquire a temporary token by using the console and SDK.

<span id="jehISOwu"></span>
## Prerequisites


* An instance has been created and the instance state is **Running**. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* An account that uses IAM verification has been created. For more information on specific operations, refer to [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_and_managing_an_account).


<span id="HyiFfgGG"></span>
## Obtaining a temporary token from the console


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name.

5. Click the **Accounts** tab on top of the page.

6. On the **Accounts** tab, click **Generate temporary token** in the **Actions** column for the target account.

7. In the **Acquire temporary token** window, set the validity period of the token and click **Generate** to obtain the temporary token for the account.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The maximum validity period of the token is 12 hours. You can use the token to connect to the database within its validity period.</div>


* <div data-tips="true" data-tips-type="default">After the <strong>Acquire temporary token</strong> window is closed, the generated Token cannot be obtained again. Save it immediately.</div>



<span id="WHPNxu9h"></span>
## Generate a temporary token by using an SDK

MySQL supports Python SDK, Go SDK, and Java SDK. You can use one of them based on your business requirements. This topic uses the GO SDK as an example.


1. [Download and install the GO SDK](https://docs.byteplus.com/en/docs/RDS_for_MySQL/overview_3?lang=en#.c2RrLeWIl-ihqA==).

2. [Initialize the client](https://docs.byteplus.com/en/docs/RDS_for_MySQL/client_initialization_3?lang=en).

3. Generate temporary token. Example code:


```Go
import (
        "context"
        "fmt"
        "io/ioutil"
        "net/http"
        "os"

        "github.com/volcengine/volcengine-go-sdk/feature/rds/auth"
        "github.com/volcengine/volcengine-go-sdk/volcengine"
        "github.com/volcengine/volcengine-go-sdk/volcengine/credentials"
        "github.com/volcengine/volcengine-go-sdk/volcengine/session"
)

func main() {
        var (
                ak     string
                sk     string
                region string
        )
        ak = "AKTP0UJUyA5BlHjUpCP5gDgCgyvpVxxxx"
        sk = "jvBjvz2t2CCHPduJmxth1XGdbZJExxxx"
        region = "cn-beijing"
        dbUser := "test"
        instanceId := "mysql-09ad8xxxx"
        expires := 3600
        ctx := context.Background()

        config := volcengine.NewConfig().
                WithCredentials(credentials.NewStaticCredentials(ak, sk, "")).
                WithRegion(region)
        sess, _ := session.NewSession(config)
        token, err := auth.BuildAuthToken(ctx, sess, dbUser, instanceId, expires)
if err != nil {
    fmt.Println("生成Token失败:", err)
    os.Exit(1)
 }                        
fmt.Println("成功生成 MySQL Token:", token)
}
```


Parameter description:


|**Parameter** |**Description** |**Sample value** |
|---|---|---|
|ak |The AccessKey ID (AK) of your BytePlus account. For instructions, refer to [Access Key User Guide](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey). |AKTP0UJUyA5BlHjUpCP5gDgCgyvpVxxxx |
|sk |The Secret Access Key (SK) of your BytePlus Account. For instructions, refer to [Access Key User Guide](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey). |jvBjvz2t2CCHPduJmxth1XGdbZJExxxx |
|region |The Region ID of the MySQL instance. |cn\-beijing |
|dbUser |The Database account in the MySQL instance for which a temporary token needs to be generated. |test |
|instanceId |The Instance ID of the MySQL instance. |mysql\-09ad8xxxx |


&nbsp;
