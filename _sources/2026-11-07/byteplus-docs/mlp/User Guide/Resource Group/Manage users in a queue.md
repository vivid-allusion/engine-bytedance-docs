---
title: "Manage users in a queue"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Manage_users_in_a_queue"
---

A queue can contain multiple administrators and users, and the queue administrator can approve the addition of ordinary users and other administrators, as well as manage the resources in the queue, allocate excess resources, and so on. Ordinary users of the queue can only use the resources in the queue to perform tasks. Users who are not in the queue can apply to join the queue, and the resources in the queue can be used after the administrator approves it.

<span id="相关概念"></span>
# Related concepts


* Queue/queue permissions


<span id="使用前提"></span>
# Premise of use


1. There is \> = 1 queue in [Queue].

2. The main account contains multiple sub\-users.


<span id="申请加入队列"></span>
# Apply to join the queue


1. **Non\-queued users** log in to the Machine Learning Platform and click [Resource Group Management] \- [Queue] in the left navigation bar to go to the list page. Click [Apply to join] in the action area of the queue to be joined and wait for approval.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a2d92084be64e79a9541694156f9157~tplv-goo7wpa0wc-image.image) </span>

2. **The queue administrator** logs into the Machine Learning Platform and clicks [Resource Group Management] \- [Queue] in the left navigation bar to go to the list page. Click the name of the above queue to enter the details page, click [Users in the group], find the above user in the tab and click [Agree] to complete the approval.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5df26111f5cc4d76a190bc67a443b1e4~tplv-goo7wpa0wc-image.image) </span>


<span id="添加用户"></span>
# Add user


1. **The queue administrator** logs into the Machine Learning Platform and clicks [Resource Queues] in the left navigation bar to go to the list page. After clicking Manage Users in the action area of the specified queue and assigning permissions to the new user, the user has joined the queue.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/29f17f301146488d9da96f4d7cbdbd52~tplv-goo7wpa0wc-image.image) </span>


<span id="修改用户权限及用量"></span>
# Modify user permissions and usage

Modify user permissions:


1. **The queue administrator** logs into the Machine Learning Platform and clicks [Resource Queues] in the left navigation bar to go to the list page.

2. Click [Manage Users] in the action area of the specified queue and assigning roles to the user.

3. Modify the **role** of the specified user to complete the change of permissions.

   <span>![图片](blob:https://arcosite.bytedance.net/9e630162-4afc-4850-a49f-16e84e9d959b) </span>


Modify user usage:


4. **The queue administrator** logs into the Machine Learning Platform and clicks [Resource Queues] in the left navigation bar to go to the list page.

5. Click the name of the specified queue to enter the details page, and click [User usage management] to view the corresponding label page.

6. Modify the **upper limit of usage ratio** of the user to limit the amount of resources that the user can use.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dbe6c9bb46ec47c3a37674182db69b32~tplv-goo7wpa0wc-image.image) </span>

<span id="移除用户"></span>
# Remove user


1. **The queue administrator** logs into the Machine Learning Platform and clicks [Resource Group Management] \- [Queue] in the left navigation bar to go to the list page.

2. Click the name of the specified queue to enter the details page, and click [Users in Group] to view the corresponding label page.

3. Find the user to be deleted and click [Remove] to remove the user from the queue. At this time, the user cannot use the queue to submit tasks. If the user wants to use the queue again, he needs to reapply to join or the administrator takes the initiative to add it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5c55494f3f6451aa0524fe8e080ed35~tplv-goo7wpa0wc-image.image) </span>
