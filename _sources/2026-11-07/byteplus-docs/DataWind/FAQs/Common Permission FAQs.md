---
title: "Common Permission FAQs"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Common_Permission_FAQs"
---

1. If you have project view permission, do you also have permission to view dashboards and datasets under the project? ❌

2. If you have dashboard view permission, do you also have permission to view all datasets referenced by the dashboard? ❌

3. If you have dashboard view permission, can you access the visualization query page for free analysis? ❌

4. If you have dashboard view permission, can you see all charts within the dashboard? Not necessarily

5. If you have dataset permission, do you also have dashboard permission? ❌

6. If you have dashboard permission, do you also have dataset permission? ❌

7. If you have permission to view dashboards or datasets under a project, do you also have permission to view the project? ✅

8. What are the differences and relationships between roles and user groups?


Answer: Roles can be shared across multiple projects and products (via the system console), while user groups are only suitable for the current project.


9. What is the difference between adding management permissions for a project in Project Center—User Group Management, Role Management, and Permission Management, and adding a permission administrator for the project in User Management?


Answer: They are the same; in the end, the corresponding user or users are project administrators.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84ff9454620b464aac03a7639ce6de5b~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/190162e5730b409186767dce02d1632b~tplv-goo7wpa0wc-image.image) </span>


10. [User Group Management] What is the difference between public and non\-public?


Answer: Whether the user group can be searched by people other than the user group administrator.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66f4e35cb97e469ba666b61c132252ac~tplv-goo7wpa0wc-image.image" width="610px" /></div>



11. What is group shielding authorization? In what scenarios is it used?


Answer: When group shielding authorization is enabled, authorization can only be granted to individual users, not to user groups or roles; it is used when the resource is highly confidential.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d8fc3daf1f347bdba63486d9288e49e~tplv-goo7wpa0wc-image.image) </span>


12. If a user group contains both regular users and project administrators, what is the effect of authorization for this user group?


Answer: The permission judgment logic follows the "Permission Judgment Logic Diagram"; if the user group contains project administrators, only regular users other than the project administrators will be subject to the user group's authorization.
