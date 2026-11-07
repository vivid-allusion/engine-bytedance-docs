---
title: "Associating a host account to a live room"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-adding-a-brand-account"
---

By associating a host account to a live room, viewers can follow the host on the viewing page or be redirected to the host's homepage on other platforms such as TikTok.

<span id="080fb737"></span>
## Prerequisite

A BytePlus account or an IAM user with Marketing toolkits \> Edit permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

<span id="6b547e4a"></span>
## Notes


* The original brand account feature has been upgraded to the host account feature. Viewers can follow the host on the viewing page. For more information, see [What your viewers see](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-a-brand-account#11002b13). If a brand account was added to your live room before, the brand account can still be displayed on the viewing page. You can follow the operations in this topic to associate a host account with your live room to experience more features.

* After enabling the feature of allowing viewers to follow a host, you can perform secondary development to carry out follow\-up operational activities on user following and host management, such as converting viewers who follow the host on the viewing page into followers of the host in the app, pushing live reminders in the app to viewers who follow the host, and compiling live data of the host. If no secondary development is performed, viewers will not be automatically converted into the host's followers in the app after they follow the host on the viewing page.


<span id="0f9cef09"></span>
## Procedure


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On the live room list, click to open a live room.

3. (Optional) To allow viewers to follow a host, click **Producer** \> **Viewing restrictions** on the left navigation pane. Then, select **Custom** as the authentication type or comment restriction. For more information, see [Custom authentication login](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For Web Viewer SDK, Viewer SDK for iOS and Android, make sure the authentication mode is custom mode.   </div>
   

4. On the left navigation pane, click **Marketing toolkits** \> **Promotion**.

5. On the **Host/Brand** account tab, turn on the **Account settings** switch.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f139306b9fd9417891c48eab1e3e5c42~tplv-goo7wpa0wc-image.image) </span>

6. Click **Account library** or **Add account**.

7. In the **Account library** dialog box that appears, click **Add account**. Complete the following configurations and then click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd76b456194e40f2913455a87d75ed9c~tplv-goo7wpa0wc-image.image) </span>

   * **Host/Brand account name**: Enter the host, brand, or company name.

   * **Account avatar**: Click **Upload** to upload your account avatar.

   * **Embedded link**: Enter the homepage link of the account. Viewers can be redirected to the account homepage after they click the account name or avatar on the viewing page.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Contact the customer service personnel of the app where the host account belongs to get the corresponding account homepage link. Make sure the link includes a protocol header.      </div>
      

   * **Account following**: Configure whether to allow viewers to follow the host on the viewing page. To allow viewers to follow the host, complete the following configurations.

      1. Click **Configure request URLs**.

         <div style="text-align: center">
         <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2192208fc274a61af143b61d0eac64a~tplv-goo7wpa0wc-image.image" width="1498px" />         </div>
         

      2. Enter the query and update request URLs. You must develop OpenAPIs for querying whether a viewer is following the host and for updating the following status of a viewer by yourself. For more information, see [Integrating your system with BytePlus Live](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-a-brand-account#fbdefd59).

      3. Select **Supported** from the **Account following** drop\-down list.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Only the BytePlus account or an IAM user with the super administrator role can edit or delete existing host accounts.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can only associate one host account with this live room. If more than one host account is added, select one host account to associate with the live room.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The host accounts you add in this live room can be used across different live rooms.      </div>
      

   * **External platform ID**: Enter the ID on an external platform. The ID can only contain uppercase and lowercase letters and numbers, and cannot exceed 128 characters in length.

8. (Optional) To associate another host account with this live room, click **Switch account**.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db7e84400bbb498e8fdb0810a76077ae~tplv-goo7wpa0wc-image.image" width="1173px" />   </div>
   

9. (Optional) View the number of viewers who follow the host on the viewing page.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e54980296754c748edca71cae0af1a8~tplv-goo7wpa0wc-image.image" width="1173px" />   </div>
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the host account is associated with more than one live room, the total number of viewers who follow the host across different live rooms is displayed here.   </div>
   

<span id="11002b13"></span>
## What your viewers see


<Tabs>
<Tab zoneid="BB6qokv4nD" title="Viewers on PCs">
<TabTitle>Viewers on PCs</TabTitle>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5915e5794a1b46fabf5f2df73f5741f8~tplv-goo7wpa0wc-image.image" width="1659px" /></div>



</Tab>
<Tab zoneid="EsfpYW9quK" title="Viewers on mobile devices">
<TabTitle>Viewers on mobile devices</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac08c2d0d12544c1a3c4713658c1129d~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>



|No. |Description |
|---|---|
|1 |The account avatar and name. Viewers can be redirected to the account homepage after they click the account name or avatar.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">On PCs, viewers can only see the account avatar.</div><br> |
|2 |Viewers can click **Follow** to follow the host or **Followed** to unfollow the host. |


<span id="fbdefd59"></span>
## Integrating your system with BytePlus Live

Before allowing viewers to follow a host on the viewing page, you must develop the following two OpenAPIs according to the specifications to integrate your system with BytePlus Live.

If you have any questions about integration, contact your sales representative. If you do not have a sales representative, click [here](https://www.byteplus.com/en/contact) to fill in the form so that the BytePlus sales team can contact you later.

<span id="e9d9fd70"></span>
### Querying whether a viewer is following the host

Description: BytePlus Live can call this OpenAPI to get whether a viewer is following the host from your own account system, and synchronize the following status and number of followers of the host account from your own account system to BytePlus Live.

Method: GET

<span id="d2a72dcc"></span>
#### Request parameters

<span id="525c1789"></span>
##### Query


|Paramter Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ExternalId |String |Yes |`0` |The user ID in your own account system. |
|ExternalName |String |Yes |`UserA` |The user name in your own account system. |
|Ts |Integer |Yes |`1732534037` |The system time when the OpenAPI is called in Unix timestamp format. Unit: seconds. |
|ActivityId |Integer |Yes |`1111248660938866` |The activity ID of the live room. |
|HostAccountId |Integer |Yes |`3524` |The ID of the host account. |
|HostAccountName |String |Yes |`Host` |The name of the host account. |
|Sign |String |Yes |`0cde1fe04aa48e02ec697734351c785e` |The signature for verification.<br><br>To obtain the value of `Sign`, you must complete the following steps:<br><br><br>1. Order all the parameters and their values based on the parameter name in lexicographic order.<br><br>2. Concatenate the string in the format of `ParameterNameParameterValueParameterNameParameterValue`.<br><br>3. Add the value of `accountSecret` at the end of the string. To obtain the value of `accountSecret`, contact your sales representative.<br><br>4. Convert the string to lowercase.<br><br>5. Encrypt the lowercase string in MD5 (32\-bit lowercase).<br><br><br>In this example, assume that the `accountSecret` value is `yqn234`. The string would then be `activityid1111248660938866externalid0externalnameuserahostaccountid3524hostaccountnamehostts1732534037yqn234`, with the `Sign` value as `0cde1fe04aa48e02ec697734351c785e`. |


<span id="2ea33115"></span>
#### Response parameters


|Paramter Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Code |Integer |`200` |The HTTP status code. |
|Status |Integer |`1` |Indicates whether the viewer is following the host.<br><br><br>* `0`: Not following.<br><br>* `1`: Following.<br><br>* `2`: Error. |
|Message |String |`-` |Returns a detailed error message if the value of `Status` is `2`. |
|Number |Integer |`100` |The number of followers of the host account. |


<span id="4a97a1e6"></span>
#### Samples

<span id="178bcc23"></span>
##### Sample request

```Plain
GET https://test.com/get?ExternalId=0&ExternalName=UserA&Ts=1732534037&ActivityId=1111248660938866&HostAccountId=3524&HostAccountName=Host&Sign=0cde1fe04aa48e02ec697734351c785e
```


<span id="5bdcbc08"></span>
##### Sample response

```JSON
{
    "Code": 200,
    "Status": 1,
    "Message": "",
    "Number": 100
}
```


<span id="59c352d1"></span>
### Updating a viewer's following status for the host

Description: BytePlus Live can call this OpenAPI to synchronize a viewer's following status for the host from BytePlus Live to your own account system.

Method: POST

<span id="84f92614"></span>
#### Request parameters

<span id="8e27c021"></span>
##### Query


|Paramter Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ExternalId |String |Yes |`10300769` |The user ID in your own account system. |
|ExternalName |String |Yes |`UserA` |The user name in your own account system. |
|Ts |Integer |Yes |`1732527267` |The system time when the OpenAPI is called in Unix timestamp format. Unit: seconds. |
|ActivityId |Integer |Yes |`1111248660938866` |The activity ID of the live room. |
|HostAccountId |Integer |Yes |`3524` |The ID of the host account. |
|HostAccountName |String |Yes |`Host` |The name of the host account. |
|Status |Integer |Yes |`1` |Specifies whether the viewer is following the host.<br><br>Valid values:<br><br><br>* `0`: Not following.<br><br>* `1`: Following. |
|Sign |String |Yes |`8c1f72035d6f9897d90ad7352fc4cc0d` |The signature for verification.<br><br>To obtain the value of `Sign`, you must complete the following steps:<br><br><br>1. Order all the parameters and their values based on the parameter name in lexicographic order.<br><br>2. Concatenate the string in the format of `ParameterNameParameterValueParameterNameParameterValue`.<br><br>3. Add the value of `accountSecret` at the end of the string. To obtain the value of `accountSecret`, contact your sales representative.<br><br>4. Convert the string to lowercase.<br><br>5. Encrypt the lowercase string in MD5 (32\-bit lowercase).<br><br><br>In this example, assume that the `accountSecret` value is `yqn234`. The string would then be `activityid1111248660938866externalid10300769externalnameuserahostaccountid3524hostaccountnamehoststatus1ts1732527267yqn234`, with the `Sign` value as `8c1f72035d6f9897d90ad7352fc4cc0d`. |


<span id="68f83f7f"></span>
#### Response parameters


|Paramter Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Code |Integer |`200` |The HTTP status code. |
|Status |Integer |`1` |Indicates whether the viewer is following the host.<br><br><br>* `0`: Not following.<br><br>* `1`: Following.<br><br>* `2`: Error. |
|Message |String |`-` |Returns a detailed error message if the value of `Status` is `2`. |
|Number |Integer |`100` |The number of followers of the host account. |


<span id="3218949d"></span>
#### Samples

<span id="cdd8e05c"></span>
##### Sample request

```JSON
POST https://test.com/get?ExternalId=10300769&ExternalName=UserA&Ts=1732527267&ActivityId=1111248660938866&HostAccountId=3524&HostAccountName=Host&Status=1&Sign=8c1f72035d6f9897d90ad7352fc4cc0d
```


<span id="3c910fb1"></span>
##### Sample response

```JSON
{
    "Code": 200,
    "Status": 1,
    "Message": "",
    "Number": 100
}
```
