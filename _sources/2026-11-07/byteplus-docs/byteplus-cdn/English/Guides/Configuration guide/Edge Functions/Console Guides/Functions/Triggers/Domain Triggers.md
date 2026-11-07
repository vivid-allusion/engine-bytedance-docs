---
title: "Domain Triggers"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-domain-triggers"
---

This document describes how to configure domain triggers for functions.

When a user accesses a function\-associated domain name via HTTP/HTTPS requests, and the user request matches the domain's forwarding rules, the domain trigger will trigger the fetch event in the function code. You need to listen for and handle the fetch event in your code.

<span id="usage-limitations"></span>
## Usage limitations

A function can be associated with a maximum of 100 domain names, and a domain name can be associated with a maximum of 50 functions.

<span id="configure-domain-triggers"></span>
## Configure domain triggers

You need to complete the following tasks to configure domain triggers for a function.


* [Step 1: Associate a domain name with the function](https://docs.byteplus.com/en/docs/18/17372#step-1-associate-a-domain-name-with-the-function)

* [Step 2: Configure forwarding rules for the domain name](https://docs.byteplus.com/en/docs/18/17372#step-2-configure-forwarding-rules-for-the-domain-name)

* [Step 3: Listen for fetch events in the function code](https://docs.byteplus.com/en/docs/18/17372#step-3-listen-for-fetch-events-in-the-function-code)


<span id="step-1-associate-a-domain-name-with-the-function"></span>
### Step 1: Associate a domain name with the function

<span id="prerequisites"></span>
#### Prerequisites


* Your function has been fully released, and the function's status is **Running** or **Unassociated**.

* Your domain name has been added to BytePlus CDN, and the **Status** of the domain is **Enabled**. See [Add Your Domain Name](https://docs.byteplus.com/docs/byteplus-cdn/docs-add-your-domain-name).


Follow these steps to associate a domain name with a function.


1. Open the [Functions](https://console.byteplus.com/cdn/edge-function/list) page.

2. On the **Functions** page, find the function you created in the **Name** column, then click on the function name.

3. Select the **Triggers** tab, then select the **Domain names** tab, and click **Add domain**.

4. In the **Add domain** dialog box, select one or more domain names you want to associate, then click **Save**.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_42acbc934ed66b35369cadb0a628fc96.jpeg) </span>


After the domain name is successfully associated, you can view the domain name on the **Triggers** tab. Since the added domain name has no forwarding rules configured, its status is **Offline**.

<span id="step-2-configure-forwarding-rules-for-the-domain-name"></span>
### Step 2: Configure forwarding rules for the domain name

After adding a domain name to the function, you need to configure forwarding rules for the domain name.


1. Open the [Functions](https://console.byteplus.com/cdn/edge-function/list) page.

2. On the **Functions** page, find the function you created in the **Name** column, then click on the function name.

3. Select the **Triggers** tab, then select the **Domain names** tab.

4. In the domain name list under the **Domain names** tab, select the domain name for which you want to configure forwarding rules. If you want to configure the same forwarding rules for multiple domain names under this function, check multiple domain names.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_be799c05b1f42bb02ed4a3556c67ea4d.png) </span>

5. Click **Configure forwarding rules** below the domain name list.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can only incrementally configure one forwarding rule at a time on the <strong>Domain names</strong> tab. Multiple configurations will result in multiple forwarding rules. You can view all forwarding rules associated with the domain name on the <strong>Domain Names</strong> page of BytePlus CDN. See <a href="https://docs.byteplus.com/docs/byteplus-cdn/docs-Configure-Edge-Function-Forwarding-Rules">Interact With Edge Functions</a>.   </div>
   

6. On the **Configure forwarding rules** page, configure the forwarding rules according to the following table.

   
   |Parameter |Description |
   |---|---|
   |Domain name |The domain name for which forwarding rules are to be configured. |
   |Function name |The name of the current function, which cannot be modified. |
   |Forwarding rules |User requests that match the forwarding rules will be forwarded by BytePlus CDN to the edge function.<br><br><br>* **Filter Type**<br><br>   Select a type of rule. The configuration values are as follows:<br><br>   * URL Path Extension: The rule applies to all files with the specified suffix.<br><br>   * URL Path Directory: The rule applies to all files in the specified directory.<br><br>   * URL Path: The rule applies to the specified file.<br><br>* **Patterns**<br><br>   Enter the rule content according to the specified **Filter Type**. The rule content cannot exceed 1024 characters. You can enter one or more configurations, separated by semicolons (;). The requirements for rule content are as follows:<br><br>   * If the type is **URL Path Extension**, enter one or more file extensions. For example, `xlsx` or `png;txt`. File extensions can contain English letters and numbers.<br><br>   * If the type is **URL Path Directory**, enter one or more directory paths. Directory paths must start and end with a slash (/). For example, `/www/img/byte/;/www/doc/`. Directory paths cannot contain consecutive slashes (//), percent signs (%), or spaces. To specify all directories under the domain name, enter `/`.<br><br>   * If the type is **URL Path**, enter one or more complete paths. Paths start with a slash (/). For example, `/www/img/byteplus.png;/doc/study.docx`. File paths cannot contain consecutive slashes (//), percent signs (%), or spaces.<br><br>* **Ignore Case**<br><br>   Set whether CDN distinguishes between uppercase and lowercase when using **Patterns** to match user\-requested files. The rest of the request URL is not affected by this configuration. The default setting is on. On means case\-insensitive. |
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_7b46ba1fd505b0731f9b760cc286da2f.jpeg) </span>

7. After configuring the forwarding rules, click **Save**.


You need to wait a few minutes. When the domain name's status changes to **Online**, it indicates that the domain trigger is effective for that domain name. At this point, if a user sends an HTTP/HTTPS request to that domain name and the request matches the forwarding rules, BytePlus CDN will forward the user request to the edge function, and the domain trigger will trigger the fetch event in the function associated with that domain name.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4ef941416ad8ad182705a06bd1d41879.jpeg) </span>

<span id="step-3-listen-for-fetch-events-in-the-function-code"></span>
### Step 3: Listen for fetch events in the function code

You need to listen for fetch events in the function code to handle user requests. The following sample code demonstrates how to register an event listener to listen for fetch events and call a callback function to return a custom response to the user when a fetch event is triggered.

```JavaScript
// Register an event listener to listen for fetch events
addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request));
})
// This function is called when fetch event fires
async function handleRequest(request) {
    return new Response('Hello World!', { status: 200 });
}
```


<span id="disassociating-a-function-from-a-domain-name"></span>
## Disassociating a function from a domain name

<span id="prerequisites"></span>
### Prerequisites

The domain name status on the **Triggers** tab is **Offline**.

<span id="steps"></span>
### Steps

Follow these steps to disassociate a domain name from a function.


1. Open the [Functions](https://console.byteplus.com/cdn/edge-function/list) page.

2. On the **Functions** page, find the function you created in the **Name** column, then click on the function name.

3. Select the **Triggers** tab, then select the **Domain names** tab.

4. In the domain name list under the **Domain names** tab, find the domain name you want to disassociate, and click **Remove** in the **Actions** column.

5. Click **OK** in the pop\-up dialog box.


After disassociation, the domain name will no longer appear in the domain name list.
