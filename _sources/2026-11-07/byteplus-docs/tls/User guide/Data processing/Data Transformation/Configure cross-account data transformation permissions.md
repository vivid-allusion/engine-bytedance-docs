---
title: "Configure cross-account data transformation permissions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Authorization-for-transformation-across-accounts"
---

When transforming log service data in bytepluses account A and writing the results to the log service in bytepluses account B, you need to first create a custom role with cross\-account data transformation permissions as described in this article.

<span id="x4441ZRi"></span>
## Configuration instructions 

To enable cross\-account data transformation, complete the following configuration in bytepluses account B first. 


1. Create a custom permission policy, for example named tls\-etl\-access, which must include query and write permissions for the target Topic. 

2. Create a custom role, for example named TLSCrossAccountTransformation. 

3. Grant permissions to the role by assigning the tls\-etl\-access policy to the TLSCrossAccountTransformation role. 


After granting permissions, you can create transformation tasks in account A. During transformation, the task will assume the above role to transform log service data in account A and write it to the log service in account B. 

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If account B is an IAM account, you must first grant it query and write permissions on the target Topic. </div>


<span id="aeZ4ekCY"></span>
## Procedure 


1. Log in with account B to [Access Control IAM Console](https://console.byteplus.com/iam/identitymanage/user). 

2. Create a custom permission policy. 

   1. In the left navigation pane, click **Permission Policy**. 

   2. On the **Permission Policy** page, click **Create Policy**. 

   3. On the **Create Policy** page, set the **Policy Name** (for example, tls\-etl\-access), enter the following policy script in the JSON editor, then click **Submit**.

      ```JSON
      { 
        "Statement": [ 
          { 
            "Effect": "Allow", 
            "Action": [ 
              "tls:DescribeTopic", 
              "tls:PutLogs" 
            ], 
            "Resource": [ 
              "*" 
            ] 
          } 
        ] 
      } 
      ```
      

3. Create a role. 

   1. In the left navigation pane, click **Role Management**. 

   2. On the **Role Management** page, click **Create New Role**. 

   3. In the **Create New Role** panel, complete the following configuration. 

      1. Set **Select trust identity** to **Account**, set **Select identity** to **Other accounts**, set **Account ID** to the ID of Account A, then click **Next**. 

      2. Set the role name, then click **Next**. 

         The role name must start with TLSCrossAccount, such as TLSCrossAccountTransformation. 

      3. Select the tls\-etl\-access permission policy for the role, then click **Submit**. 

4. Modify the trust relationship of the role. 

   1. On the **Role Management** page, click the role created in the previous step. 

   2. Under the **Trust relationship** tab, click **Edit trust policy**. 

   3. Change **root** in **trn** to **role/ServiceRoleForTLS**, then click **Save**.

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e5e526ba84100d327f8edef152b5c424.png) </span>

5. Record the role TRN. 

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_3dd7a7af212f6372b42aa9b477cd04f1.png) </span>

   When creating a cross\-account data transformation task, you must enter this role TRN. For specific operations, refer to [Create a data transformation task](https://docs.byteplus.com/en/docs/tls/create_a_data_transformation_task).

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9c5a9e6f0a9f223f9bf1999799d84c48.png) </span>
