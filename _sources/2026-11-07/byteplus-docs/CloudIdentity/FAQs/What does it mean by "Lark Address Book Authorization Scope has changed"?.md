---
title: "What does it mean by \"Lark Address Book Authorization Scope has changed\"?"
product: "BytePlus Cloud Identity"
product_code: "CloudIdentity"
source: "https://docs.byteplus.com/en/docs/CloudIdentity/What-does-Feishu-mean-by-Address-Book-Authorization-Scope-has-changed"
---

When you select Lark as your identity source to sync users with Cloud Identity Center, your corporate address book information will be read and synced through the Lark Store app "Byteplus" authorized by your Lark administrator.

## Address Book Authorization Scope Configuration Method

#### When installing the app for the first time

During the installation of the Lark Store app "Byteplus", you can select the range of corporate employees you want to sync to Byteplus. You can choose the **installation range ** :

![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261012113700-11349966662.png)

Also specify **certain members ** in the installation scope:

![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261012113722-163261634244.png)

You can sync only some enterprise users to Byteplus.

#### When making changes to an already installed application

If you have completed the installation, or wish to change the installation and synchronization scope later, you can use the administrator user of the Lark tenant to log in to the [Lark admin console ](https://www.larksuite.com/admin/), in the **workbench**\>**Application Management ** Find the Byteplus app and adjust the range of **available members ** .

## Cloud Identity Center Tip: How to deal with "Address Book Authorization Scope Has Changed"

**Please note that ** if you have configured Lark User Synchronization in Cloud Identity Center, you will need to go to the [Byteplus console ](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/userSync/)to process the synchronized data after changing the synchronized address book range in the Lark admin background.

**Please note that user incremental synchronization will be paused until processing is complete.**

When you log in to Cloud Identity Center, the **user synchronization settings ** will prompt you to process user data that has been synced to Cloud Identity Center but is not within the scope of the latest address book authorization. You can choose:

1. **Delete ** : Delete this part of the user data from the Cloud Identity Center, and delete all the SSO authorization tasks corresponding to the user. **Please note that this will affect the corresponding user's login through the original SSO login method. Please confirm that the user no longer needs to use the single sign\-on function to delete it.**

2. **Retention ** : Retain this part of user data and store it in the Cloud Identity Center. The user's corresponding SSO authorization task will not be deleted. **Please note that the retention operation will not cause your permissions to be leaked, and the retained user data will not be updated with the data update of the Lark address book in the future.**
