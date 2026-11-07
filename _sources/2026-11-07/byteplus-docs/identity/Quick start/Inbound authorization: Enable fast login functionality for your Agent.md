---
title: "Inbound authorization: Enable fast login functionality for your Agent"
product: "Agent Identity"
product_code: "identity"
source: "https://docs.byteplus.com/en/docs/identity/Enable_fast_login_functionality_for_your_Agent"
---

To add standard, secure login to your Agent application, this guide provides step\-by\-step instructions for integrating with the identity and access management platform for intelligent agents. You will learn how to configure a user pool and client, and then use the standard OIDC protocol to connect your application, enabling users to log in with a centralized account system.

<span id="146f5ed2"></span>
## **Scenario description**

Suppose you have developed an Agent and want users to log in using the account system hosted by the identity and access management platform for intelligent agents, rather than registering a separate account. After configuration is complete, your Agent will have the capability to authenticate user identities.

<span id="aecc5630"></span>
## Prerequisites


* You have enabled the Agent Identity service and completed authorization. For details, see [Enable Agent Identity and complete authorization](https://docs.byteplus.com/docs/identity/89601).

* You have an Agent service under development.


<span id="dd25fbd5"></span>
## Process description

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI3MjVweCIgaGVpZ2h0PSI2NXB4IiB2aWV3Qm94PSItMC41IC0wLjUgNzI1IDY1Ij48ZGVmcy8+PGc+PHBhdGggZD0iTSAxMjIgMzIgTCAxOTUuNjMgMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwN2ZmZiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyMDAuODggMzIgTCAxOTMuODggMzUuNSBMIDE5NS42MyAzMiBMIDE5My44OCAyOC41IFoiIGZpbGw9IiMwMDdmZmYiIHN0cm9rZT0iIzAwN2ZmZiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjMDA3ZmZmIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBjb2xvcj0iI2ZmZmZmZiIgc3R5bGU9ImZvbnQtc2l6ZToxNnB4Ij5DcmVhdGUgdXNlciBwb29sPC9mb250PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAzMjIgMzIgTCAzOTUuNjMgMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwN2ZmZiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA0MDAuODggMzIgTCAzOTMuODggMzUuNSBMIDM5NS42MyAzMiBMIDM5My44OCAyOC41IFoiIGZpbGw9IiMwMDdmZmYiIHN0cm9rZT0iIzAwN2ZmZiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMjAyIiB5PSIyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiMwMDdmZmYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiAyMDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGZvbnQgY29sb3I9IiNmZmZmZmYiPjxzcGFuIHN0eWxlPSJmb250LXNpemU6MTZweCI+Q3JlYXRlIGNsaWVudDwvc3Bhbj48L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDUyMiAzMiBMIDU5NS42MyAzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDA3ZmZmIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDYwMC44OCAzMiBMIDU5My44OCAzNS41IEwgNTk1LjYzIDMyIEwgNTkzLjg4IDI4LjUgWiIgZmlsbD0iIzAwN2ZmZiIgc3Ryb2tlPSIjMDA3ZmZmIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI0MDIiIHk9IjIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iIzAwN2ZmZiIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDQwM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBjb2xvcj0iI2ZmZmZmZiI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxNnB4Ij5DcmVhdGUgdXNlcjwvc3Bhbj48L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2MDIiIHk9IjIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iIzAwN2ZmZiIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDYwM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBjb2xvcj0iI2ZmZmZmZiI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxNnB4Ij5JbnRlZ3JhdGU8L3NwYW4+PC9mb250PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==" />

<span id="85065fac"></span>
## Step 1: Create a user pool

A user pool is a container for storing user accounts. All your user data (usernames, passwords, phone numbers, and more) will be stored here.


1. Log in to BytePlus Identity Agent Console.

2. In the left navigation bar, select **User Pools**.

3. Click **Create User Pool** in the upper right corner.

4. Configure user pool parameters.

   * **User pool name**: Enter an easily identifiable name, for example, `my-web-app-pool`.

   * Other parameters can remain as default.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/463f1825a7044e3685096e7c464920b4) </span>

5. Click **OK**.


<span id="7c83b93f"></span>
## Step 2: **Create a client**

To allow your application to connect to the user pool you just created, you need to register a client.


1. On the returned page, click **Create Client**.

2. Configure basic client information.

   * **Client name**: `my-webapp-client`.

   * **Client type**: Select **Web Application**.

   * **Authorization callback URL**: **Key configuration**. This is the address where Agent Identity will redirect users to your application after successful login.

      * Local debugging example: `http://localhost:8000/callback`

      * Production environment example: `https://agent.com/auth/callback`

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Caution   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The URL configured here must be exactly the same as the Redirect URI configured in your code (including the trailing slash), otherwise a <code>redirect_uri_mismatch</code> error will occur.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ee8944e2b8af49d487a1f47588cb068f) </span>

3. Click **OK**.


<span id="eff7fb18"></span>
## **Step 3: Create a user**

Before integrating the code, create a test account to verify the process.


1. On the returned page, click **Create User**.

2. Configure user information.

   * **Username**: `testuser`.

   * **Phone number**: `+86173********`.

   * **Temporary password**: Set a password that meets the following requirements.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The password must contain numbers, special characters, uppercase and lowercase letters.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The length must be at least 8 characters.      </div>
      

   * **Additional attributes**: Set an additional attribute (for example, last name, first name).

   * Click **OK**.


<span id="d0432d46"></span>
## **Step 4: Integrate configuration in the application**

Return to your Agent code. Agent Identity is compatible with the standard **OIDC** protocol. You can integrate using any language's OIDC client library (such as Python's `authlib` or Node.js's `openid-client`).

<span id="2f303059"></span>
### Obtain parameter configuration

On the Agent Identity user pool details page or client details page, obtain the following information and map it to your OIDC configuration file:


|Console field |Code configuration parameter |Description |
|---|---|---|
|**OIDC discovery endpoint**<br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ee89a5fcf3f143c29ff3b62d20b60e5f) </span> |`ISSUER_URL` / `AUTHORITY` |Root address (Base URL) of the identity service |
|**Client ID**<br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/b1a38fc61611448f834575d26ab2c488) </span> |`CLIENT_ID` |Public unique identifier of the application |
|**Client secret**<br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/1c594fe45ab74e2e81aec9531836d69d) </span> |`CLIENT_SECRET` |This value is security\-sensitive. Use it only on the backend and do not expose it on the frontend. |
|**Authorization callback URL**<br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/70dacd1780bd455e959d50f105a7d938) </span> |`REDIRECT_URI` |Must be consistent with the address entered in Step 2. |


<span id="c5dd38ce"></span>
### Example code

```JSON
{
  "oidc_issuer": "https://identity.byteplus.com/oidc/...",  // Obtain from the discovery endpoint
  "client_id": "cli_xxxxxxxxxxxx",                            // Client ID
  "client_secret": "secret_xxxxxxxxxxxx",                     // Client secret
  "redirect_uri": "http://localhost:8000/callback",           // Authorization callback URL
  "scopes": ["openid"]                                       // Recommended scope of permissions to request
}
```


<span id="46d1e150"></span>
## Verify the configuration


1. Start your Agent service.

2. Click **Log in**. The application should redirect the browser to the unified login page of the Agent Identity Platform.

3. Enter the `testuser` account and password created in **Step 3**.

4. After a successful login, the page will automatically redirect back to your `Redirect URI` and include the authorization code.

5. Your backend service will automatically exchange the code for a token and complete user login.
