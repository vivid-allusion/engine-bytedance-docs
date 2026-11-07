---
title: "Seat and member management"
product: "TRAE"
product_code: "trae"
source: "https://docs.byteplus.com/en/docs/trae/manage-members"
---

The first TRAE account registered after purchasing a TRAE Enterprise plan is by default designated as the super administrator of the enterprise. The super administrator can manage members for the enterprise, including inviting members, adding seats, transferring the super administrator role, and removing members.

<span id="9a43a4b6"></span>
## Invite members

You can invite members to join your enterprise.


1. Log in to the [TRAE Enterprise Console](https://console.enterprise.trae.ai/).

2. Go to **Enterprise Management** \> **Member Management**.

3. In the upper\-right corner of the page, click the **Invite Members** button.

4. Select a desired invitation method from the list, fill in the required information, and then send the invitation. The available invitation methods are as follows:

   
   |**Invitation Method** |**Description** |
   |---|---|
   |Invite Via email |In the **Invite Via Email** popup, enter the email addresses of the members to be invited, set their roles (member/admin), and then send the invitation.<br><br>***Note***: One email address can only join one enterprise. It is recommended to invite members via their enterprise email addresses. |
   |Batch Upload Members |In the **Bulk Add** popup, download the template CSV file, fill in the email addresses and roles of the members to be invited, then upload the file and send the invitation.<br><br>***Note***: Up to 1,000 members can be invited at one time. |
   |Invite Via Link |In the **Invite Via Link** popup, enable the enterprise unified invitation link, set the link validity period, then copy the link and send it to the people to be invited. |
   

   After the invitation is sent, you can view the invited members and their roles, status, invitation time, and other information on the **Inviting** tab.


<span id="7891d7a2"></span>
## Add seats

If the current seats are not enough for your enterprise, you can add more seats.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">If the enterprise purchases additional seats during the subscription period, the newly added seats will share the same expiration date as the original order.</div>



1. Log in to the [TRAE Enterprise Console](https://console.enterprise.trae.ai/).

2. Go to **Enterprise Management** \> **Member Management**.

3. In the upper\-right corner of the page, click the **Add Seats** button.

   This directs you to the BytePlus TRAE Console, and the seat purchase popup appears automatically.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/6ec8df4c6e3d45eebfbc7a99f8163189) </span>

5. In the **Purchase additional seats for TRAE Enterprise version** popup, complete the following steps:

   1. Fill in the number of seats to purchase.

   2. Read the agreement and check the **I agree to TRAE** ** ** **Terms of ** **Service** checkbox.

   3. Click the **Buy now** button.

   This directs you to the payment page.

6. Complete the payment.


<span id="476de887"></span>
## Transfer the Super Admin role

If you are currently the super administrator of the enterprise but do not want to continue in this role, you can transfer the role to another person.


1. Log in to the [TRAE Enterprise Console](https://console.enterprise.trae.ai/).

2. Go to **Enterprise Management** \> **Member Management**.

3. In the **Enterprise Member** list, find yourself.

4. In the **Actions** column, click  **···**  \> **Transfer Super Admin Role**.

5. In the **Transfer Super Admin Role** popup, select the member to whom you want to transfer the role, and then click the **Confirm** button.


<span id="dfb730f9"></span>
## Remove members

The super administrator of the enterprise can remove members.


1. Log in to the [TRAE Enterprise Console](https://console.enterprise.trae.cn/).

2. Go to **Enterprise Management** \> **Member Management**.

3. Remove members:

   * **Remove individually**: In the member list, find the member you want to remove, then click  **···**  \> **Remove Personnel ** in the **Actions** column.

   * **Remove by batch**: In the member list, select multiple members you want to remove, then click the **Batch Removal** button at the bottom of the list.


<span id="dd0807b0"></span>
## About seat release

After removing a member, whether the seat is released depends on the member's token usage in AI chat for the current month. The rules are as follows:


* **Usage ≤ 1 million**: The seat will be released immediately, and you can invite a new member to join.

* **Usage \> 1 million**: The seat will not be released until the following month, at which point you can invite a new member to join.


**For example**:

On January 1, two seats are purchased with a validity period of three months, and John Doe and Jane Doe have already joined the enterprise. 

John Doe has used more than 1,000,000 Tokens before January 5. If John Doe is removed on January 5, you cannot invite others to join before February 1 (the start of the next subscription cycle); starting from February 1, the seat occupied by John Doe will be released, and a new member can be invited to join.

&nbsp;
