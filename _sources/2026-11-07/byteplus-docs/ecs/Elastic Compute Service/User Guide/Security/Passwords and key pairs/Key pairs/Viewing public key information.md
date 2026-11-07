---
title: "Viewing public key information"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Viewing-public-keys"
---

If you want to specify that a single instance uses multiple public key files but do not have a local backup of the public key files, you can view and obtain public key information by using the three methods described in this topic.

<span id=".5L2_55So5Zy65pmv"></span>
## Applicable scenarios


* Within a Linux instance, you can use the obtained public key information to add multiple key pairs to an instance, allowing login to the same ECS instance by using multiple key pairs. For information about how to add multiple key pairs to an instance, see [Adding or replacing key pairs](https://docs.byteplus.com/en/docs/ecs/Adding-or-replacing-key-pairs-for-instances).

* You can follow the instructions in this topic to [create a key pair](https://docs.byteplus.com/en/docs/ecs/Creating-key-pairs) by **importing an existing public ke**y based on the obtained public key information.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="fcVfWm9Ne6" title="View within an instance">
<TabTitle>View within an instance</TabTitle>

1. [Log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to open the key pair configuration file. You can then view the public key information.

   ```Bash
   vim .ssh/authorized_keys
   ```
   


</Tab>
<Tab zoneid="o0pzBNvGRF" title="Local Windows operating system">
<TabTitle>Local Windows operating system</TabTitle>

1. In the browser on your local Windows host, access [PuTTYgen](https://the.earth.li/~sgtatham/putty/0.76/w64/puttygen.exe), and then download and install PuTTYgen.

2. Double\-click the puttygen.exe file.

3. Select "Type of key to generate \> RSA". Then click "Load".

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_c6e0d045287f9b761e023a22f44892db.png) </span>

4. Select a .ppk or .pem file to display public key information.


</Tab>
<Tab zoneid="udFB2s0lQC" title="Local Linux or macOS operating system">
<TabTitle>Local Linux or macOS operating system</TabTitle>

Execute the following SSH command to view public key information.

```Plain Text
ssh-keygen -y -f <key pair file path>/<key pair name>.pem
```


Public key information similar to the following output is displayed.

```Plain Text
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCxxxxxxMluApvIRol1fqXDJtdeesXwVXFOySC4PzRrehfN1Us2huWo03jS7F6f164PNQDehdxxxxxx+aWBBqsZtcEKUKqVY9Vleuyt8zHHtMq8I0GBxxxxxx+T1WQCQJKe7zxxxxxx/XfNF1lBdyuKbLOAA65fWP4ca8xxxxxx/lUyOiCZxIz4EU8NaJPsK0eprwGXQcitvBZCMx7APNFNixxxxxx/eALjqfh8jo1E5t1uy7C38EPxtST7xxxxxx/HIsmlCM2xVdiJSLiTgXWY9fRvMP1BVXD7Pv0xxxxxx/V118XYkiV0rj0XqtzT7IYlFVKxxxxxx/SoJWJiWHd/
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If no public key information is returned, you can execute the <code>chmod 400 <key pair file path>/<key pair name>.pem</code> command to change the permissions. This ensures that only you can view the file.</div>



</Tab>
</Tabs>


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

After you obtain a public key, you may need to perform the following operations:


* [Adding or replacing key pairs](https://docs.byteplus.com/en/docs/ecs/Adding-or-replacing-key-pairs-for-instances)

* [Creating key pairs](https://docs.byteplus.com/en/docs/ecs/Creating-key-pairs)
