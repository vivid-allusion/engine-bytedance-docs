---
title: "Code repository access control"
product: "TRAE"
product_code: "trae"
source: "https://docs.byteplus.com/en/docs/trae/code-repository-access-control"
---

To protect your code and comply with the security rules of your enterprise, you can add code repositories containing sensitive information, core algorithms, or non\-open\-source projects to the access restriction list.

Once added, all AI features of TRAE (including chat, code completion, codebase indexing, and more) will not be able to access or use the contents of these repositories. This restriction applies to all operations performed through TRAE IDE and TRAE Plugin.

If a member attempts to reference or operate on a restricted repository when using AI features, the system will display a clear prompt to block the operation.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/44ca827713344de0b8b6a30084ffb332) </span>

<span id="cd03b0e4"></span>
## Use cases


* **Protect core code assets**: Prevent repositories containing trade secrets, core algorithms, or critical configurations from being inadvertently accessed or referenced by AI features, reducing the risk of sensitive information leakage.

* **Meet compliance and security requirements**: Comply with the security and compliance policies of your enterprise or the entire industry to ensure that the scope of AI usage is valid.

* **Isolate experimental projects**: Prevent unstable code that is still under development or testing from contaminating AI's context or generated results.


<span id="9d8045dd"></span>
## Limitation

No more than 200 code repositories can be added.

<span id="885b5d12"></span>
## Add code repositories to the access restriction list


1. Log in to the [TRAE Enterprise Console](https://console.enterprise.trae.ai/).

2. Go to **Enterprise Setup** \> **Security Settings**.

3. In the upper\-right corner of the **Isolation Repository** tab, click the **Add Repository** button.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/4e9140cecb274548a58456e27ff2ca14) </span>

4. In the **Add Repository** popup, enter the address of the Git repository (supports HTTPS or Git protocol), then click the **Save** button.


<span id="0d2c2bf9"></span>
## Remove code repositories from the access restriction list


1. In the access restriction list on the **Isolation Repository** tab, find the target repository.

2. In the **Actions** column corresponding to that repository, click the **Remove** button.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/b9f849d1e3684789beba78d882ef377d) </span>

3. In the confirmation popup, click the **Remove** button.
