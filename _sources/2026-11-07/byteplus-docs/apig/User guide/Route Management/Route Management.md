---
title: "Route Management"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Managing_route"
---

After adding a route, you can manage it. This article introduces you to related operations in route management.

<span id=".5p-l55yL6Lev55Sx"></span>
## View Route

Supports viewing basic information, specific matching rules, and connected upstream information of a route.


1. Log in to the [API Gateway Console](https://console.byteplus.com/veapig).

2. In the top navigation bar, select the target region.

3. In the left navigation bar select **Route Management \> Route List**. In the route list, supports searching for and viewing basic information of routes.

   * In the dropdown menus under **instance**, **service** and **Upstream**, selecting filter options allows you to filter routes based on these options.

   * The route list displays basic information about the routes, including: name/ID, status, priority, domain name, route path, etc.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Between multiple filter options, there is an <strong>and</strong> relationship, meaning only routes that meet all filter options will be filtered out.</div>



4. Click on the target route name to enter the overview page of the route. You can view the basic information of the route, matching rule(s), and information connected to Upstream.


<span id=".57yW6L6R6Lev55Sx"></span>
## Edit route

Supports modification of the route's matching rule(s), information connected to Upstream, and advanced routing policy.


1. Log in to [API Gateway Console.](https://console.byteplus.com/veapig)

2. In the top navigation bar, select the target region.

3. In the left navigation bar select **Route Management \> Route List**. In the route list, select the route to be modified and click **Edit** in the **Actions** column.

4. Modify the route information as needed, after finishing, click **Confirm**.


<span id=".5Yig6Zmk6Lev55Sx"></span>
## Delete route

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">Once a route is deleted, it cannot be restored, please proceed with caution.</div>



1. Log in to the [API Gateway Console](https://console.byteplus.com/veapig).

2. In the top navigation bar, select the target region.

3. In the left navigation bar select **Route Management \> Route List**. In the route list, select the route to be deleted, click **Delete** in the **Actions** column.

4. In the pop\-up confirmation dialog, confirm the relevant information. After confirming, click **Delete**.


<span id=".5LiK57q_L-S4i-e6v-i3r-eUsQ=="></span>
## Publish/Unpublish route

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>[Beta · Apply for Trial]</strong>: This feature is currently in the <strong>beta</strong> stage, please contact your account manager if you wish to use it.</div>


Supports publishing or unpublishing routes, facilitating users in managing the status of route effectiveness.


1. Log in to [API Gateway Console](https://console.byteplus.com/veapig).

2. In the top navigation bar, select the target region.

3. In the left navigation bar select **Route Management \> Route List**. In the route list, select the target route, click the **Publish** or **Unpublish** in the  **actions** column. This will enable or disable that route.


<span id=".5aSN5Yi26Lev55Sx"></span>
## Copy Route

Supports copying existing route information, including the service, matching rule(s), connected Upstream information, and advanced routing policy, etc. Facilitates users in modifying based on existing route information to quickly create new routes.


1. Log in to the [API Gateway Console](https://console.byteplus.com/veapig).

2. In the top navigation bar, select the target region.

3. Select **Route management \> Service list (Domain name)**  from the left navigation bar. In the service list, click on the target service name to enter the service Overview page.

4. In the route list, select the route to be copied, then click the **Copy** in the **Actions** column.

5. You can modify the service and the properties of the route itself; after modifying, click **Confirm**.
