---
title: "Get Started With Edge Functions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/doc-Use-Edge-Functions-in-CDN"
---

This tutorial introduces how to use Edge Functions in BytePlus CDN based on a simple example scenario.

<span id="prerequisites"></span>
## Prerequisites

You have activated Edge Functions. See [Activate Edge Functions](https://docs.byteplus.com/docs/byteplus-cdn/activate_byteplus_edge_functions_en).

<span id="example-scenario"></span>
## Example scenario

You have a website with the domain name `www.example.com`. You have added this domain to BytePlus CDN. You want to use Edge Functions to modify the error page returned by the origin server and send a more user\-friendly custom page to users.

<span id="steps"></span>
## Steps

Follow these steps to use Edge Functions in BytePlus CDN.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4ec2d22374c60c6a5b4731c1faf9f87c.jpeg) </span>


1. **Create a function**: Create a function.

2. **Edit and debug code**: Edit and debug code in the function.

3. **Publish your function**: Deploy the function to BytePlus CDN's global edge nodes.

4. **Associate your function with a domain**: Set the function's trigger as a domain trigger and associate the function with your domain in the domain trigger.

5. **Configure forwarding rules**: Configure forwarding rules for your domain. When BytePlus CDN receives a user request that matches the forwarding rules, it will forward the user request to the Edge Function.

6. **Verify your function**: Verify if the actual execution result of the function meets expectations.


<span id="step-1-create-a-function"></span>
## Step 1: Create a function


1. Open the [Functions](https://console.byteplus.com/cdn/edge-function/list) page.

2. On the **Functions** page, click **Create function**.

3. On the **Create function** page, configure the relevant parameters according to the following instructions.

   * **Name**: In this tutorial, set **Name** to `custom-error-page`.

   * **Project**: In this tutorial, set **Project** to `default`.

   * **How to create**: In this tutorial, choose **Create with a template**, then select the **Modify Origin Server Error Response Pages** template.

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_77d37ec3d52395fabc0ddf6cb36e12b6.png) </span>

4. Click **Save** to create the function.


Next, you need to edit and debug the code.

<span id="step-2-edit-and-debug-code"></span>
## Step 2: Edit and debug code


1. Open the [Functions](https://console.byteplus.com/cdn/edge-function/list) page.

2. On the **Functions** page, find the function you created in the **Name** column, then click on the function name.

3. Select the **Code** tab, click **Modify and deploy**.

4. View the `default` file in the code editor. You can modify the code according to your needs. This tutorial uses the code provided by the template.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The code calls <a href="https://docs.byteplus.com/docs/byteplus-cdn/docs-addEventListener">addEventListener()</a> to register an event listener. The parameters passed include <code>fetch</code> and a callback function <code>{event.respondWith(handleResponse(event));}</code>:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>fetch</code> indicates that this event listener will monitor fetch events. If a fetch event is triggered by a domain trigger, the callback function will be called. You will configure the domain trigger for the function in step 4. See <a href="https://docs.byteplus.com/docs/byteplus-cdn/docs-FetchEvent">FetchEvent</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the status code of the origin server's response is 5xx, the callback function will rewrite the origin server's response to your custom HTML page, which is the HTML code in the <code>htmlResponse</code> constant.   </div>
   


```JavaScript
  const htmlResponse = `
  <html>
  
    <head>Error Page</head>
    <body>The server is experiencing some issues, please try again later</body>
  </html>
  `;
  
  // Add an EventListener to listen to fetch event. A domain trigger will trigger a fetch event
  addEventListener('fetch', (event) => {
    event.respondWith(handleResponse(event));
  });
  
  function isErrorStatus(st) {
    return st >= 500;
  }
  
  async function handleResponse(event) {
    const response = await fetch(event.request);
  
    // If the origin server returns a status code >= 500, then return the custom error page
    // Otherwise, return the information from the origin server.
    if (isErrorStatus(response.status)) {
      return htmlResponse;
    } else {
      return response;
    }
  }
```



5. Debug the code. In this tutorial, enter a URL that will return a 5xx status code, click **Send**, and check if the returned result meets expectations. After debugging, click **Save**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You need to send a request to debug the function when the HTTP tab shows a green dot. If you haven't performed any operations for a long time, the debugger will disconnect from the server. At this time, the HTTP tab will show a red dot, and you won't be able to debug. After refreshing the page, the debugger will automatically reconnect, and the HTTP tab will show a green dot.   </div>
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_da5bc439bb2e94fcb306edf1c74c04f7.jpeg) </span>


Next, you need to publish your function.

<span id="step-3-publish-your-function"></span>
## Step 3: Publish your function

You must fully publish the function before you can associate it with a domain.


1. Open the [Functions](https://console.byteplus.com/cdn/edge-function/list) page.

2. On the **Functions** page, find the function you created in the **Name** column, then click on the function name.

3. Select the **Code** tab, click **Modify and deploy**.

4. Click the **Deploy** button.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can perform a canary release before fully releasing the function. See <a href="https://docs.byteplus.com/docs/byteplus-cdn/docs-create-function">Manage Functions</a>.   </div>
   

5. In the **Deploy** dialog box, set **Release type** to **Full release**, then click **OK**.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_dd33c5a72260fa3a0b942faf303e85d5.jpeg) </span>


Next, you need to associate a domain with the function.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Full release of a function generally takes 5 to 10 minutes. You must wait for the function to be fully released before you can associate a domain with it.</div>


<span id="step-4-associate-your-function-with-a-domain"></span>
## Step 4: Associate your function with a domain

In this example, you use a domain trigger to trigger the function execution. Therefore, you need to associate the domain `www.example.com` with the function.


1. Open the [Functions](https://console.byteplus.com/cdn/edge-function/list) page.

2. On the **Functions** page, find the function you created in the **Name** column, then click on the function name.

3. Select the **Triggers** tab, then select the **Domain** tab, click **Add domain**.

4. On the **Add domain** page, select the `www.example.com` domain.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_93e736b9c901601bbccf15b2b535be3e.jpeg) </span>

5. Click **Save**. After the domain association is complete, the function's status will change to **Running**. Since you haven't configured forwarding rules for the domain yet, the domain's status is **Offline**.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_2fa27336b296e4494d05223aaeed66cc.jpeg) </span>


Next, you need to configure forwarding rules for the domain.

<span id="step-5-configure-forwarding-rules-for-the-domain"></span>
## Step 5: Configure forwarding rules for the domain

After you configure forwarding rules for the domain, if BytePlus CDN receives a user request that matches the forwarding rules, it will forward the request to the Edge Function. Moreover, the domain trigger will trigger the fetch event in the function.


1. Open the [Functions](https://console.byteplus.com/cdn/edge-function/list) page.

2. On the **Functions** page, find the function you created in the **Name** column, then click on the function name.

3. Select the **Triggers** tab, then select the **Domain** tab. Click the checkbox in front of your domain `www.example.com`, then click the **Configure forwarding rules** button.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c7d28adecee612089a2f2154fafb50c6.jpeg) </span>

4. In the **Configure forwarding rules** sidebar, configure the **Forwarding rules** parameters according to the table below. This example does not restrict the path of the user request URL, so it will match any path.

   
   |Parameter name |Description |
   |---|---|
   |Filter Type |In this tutorial, you need to set it to **URL Path Directory**. |
   |Patterns |In this tutorial, you need to set it to `/`, which means matching all paths under the domain. |
   |Ignore Case |In this tutorial, you need to keep the default value. |
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_bc5dce3995b1db43bf4d7872f1794485.jpeg) </span>

5. Click **Save**. You need to wait for a few minutes. When the domain's status changes to **Online**, it indicates that the domain trigger has taken effect for that domain. At this point, if a user sends an HTTP/HTTPS request to this domain and the request matches the forwarding rules, the domain trigger will trigger the fetch event in the function associated with that domain.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4613e83cc6870f965bdeaffbb2c2339c.jpeg) </span>

Next, you verify if the function's execution results meet expectations.

<span id="step-6-verify-your-function"></span>
## Step 6: Verify your function

You can access www.example.com and verify:


* When the origin server response code is 5xx, the returned HTML page is the value of the `htmlResponse` constant in the code.

* When the origin server response code is not 5xx, the returned HTML page comes from the origin server.


If the verification is successful, it means your example scenario has been implemented.
