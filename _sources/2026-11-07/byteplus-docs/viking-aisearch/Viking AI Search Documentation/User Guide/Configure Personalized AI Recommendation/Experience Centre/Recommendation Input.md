---
title: "Recommendation Input"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Recommended_Input"
---

The Recommendation **Experience Centre** provides a simulated environment to verify and debug the effectiveness of your recommendation strategies before going live. This ensures results align with your business expectations. It applies to various scenarios, including **Recommendated for You** and **Related Items ** scenarios.

<span id="058a834e"></span>
## Introduction

This guide explains how to simulate real\-world business requests by configuring test users, items, and geographic locations to preview recommendation results.


1. **Access the recommendation experience center:**  navigate to **Experience Center** \> **Recommendation** in the console, and select the target recommendation configuration (such as homepage recommendation or product listing page).

2. **Simulated input configuration:**  Platform supports simulating users, user geographic locations, and parent items.



---



<span id="fb2bca40"></span>
## Configure test users

Configure test users using specified user mode or random user mode. Random user mode selects a user ID randomly for quick recall effect testing. Specified user mode requires entering a test user ID; the user profile displays automatically and is used for personalized recommendations.


<Tabs>
<Tab zoneid="r3HJ4pQyIt" title="Specified User">
<TabTitle>Specified User</TabTitle>

**Steps**


1. Click **Select a Particular User**

2. Enter a known user ID present in the associated user behavior dataset (for example, user_123). If the user ID does not exist, the system cannot retrieve the user profile. 

   If the user has no user profile (No past user event data), the system will display "User data unavailable".


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/e83837233d874baaa124af02dad3f90d" width="400px" /></div>



3. After clicking "OK", the user profile displays automatically. Recommendation results update automatically based on the new user profile. **Hover over "User interest tags"**  **to view tag strength.** 


</Tab>
<Tab zoneid="rk4xrLBdmK" title="Random User">
<TabTitle>Random User</TabTitle>

**Steps**


1. Click **Select a Random User.** 


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/611e8c94c24d410b8e2d8d691828479b" width="340px" /></div>



2. The platform randomly selects a valid user ID from the behavior data set. Recommendation results update automatically based on the new user profile. **Hover over "User interest tags"**  **to view tag strength.** 


</Tab>
</Tabs>


&nbsp;

<span id="8e0a7bde"></span>
## Configure test items

In the **related item ** recommendation scenarios, personalized recommendations also use test items as the parent item to obtain related items. The attributes of test items are used for personalized recommendations.


<Tabs>
<Tab zoneid="FOaEEs52W5" title="Specified item">
<TabTitle>Specified item</TabTitle>

**Steps**


1. Click **Select a Particular Item**

2. Enter the test item ID (for example, item_abc). If the item ID is not in the item dataset, the system will prompt "No matching item found."


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/6ee04bed8dc345d49210c6fc4868e64a" width="350px" /></div>



3. After clicking "OK," the item details will display automatically. Recommended results will also update automatically based on the new test item.


</Tab>
<Tab zoneid="FZrvGG4U0d" title="Random item">
<TabTitle>Random item</TabTitle>

**Steps**


1. Click on **random item**


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a71f231ad9fc45219735a5a433db6d18" width="338px" /></div>



&nbsp;

2. The platform will randomly select an item from the item dataset. Recommended results will also update automatically based on the new test item.


</Tab>
</Tabs>


&nbsp;

<span id="173749e1"></span>
## Configure user geographic location

After configuring boosting and demotion rules related to geographic location, you can verify the rule effects in the Recommendation Experience interface through the following steps to experience recommendation adjustments based on user location (LBS) and item distance.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Prerequisite</div>


<div data-tips="true" data-tips-type="default">At least one "Geolocation Rule" has been added; see details: <a href="https://docs.byteplus.com/docs/393/User_geographic_location-based_ranking_boost_and_demotion">Boost and Demote by User Geo\-location</a>.</div>



&nbsp;

1. **Enter the recommendation experience interface**

   Navigate to "Experience Center" \> "Recommendation" in the console and select the target recommendation scenario.

2. **Simulate user geographic location and item distance**

   In the **Test User** area, use the location features to simulate scenarios where a user's geographic position triggers boosting or demotion rules.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ac1388bbe8b6439bb0679d7e9663e424" width="426px" /></div>



<div style="text-align: center">
</div>


   
   |**Capabilities** |**Description** |
   |---|---|
   |Get My Location |Obtains your current location to simulate user testing. This requires granting location permissions to the browser. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Failed to retrieve location</div><br><br><br><div data-tips="true" data-tips-type="default">If clicking "Get My Location" does not automatically retrieve latitude and longitude, please check:</div><br><br><br><br>1. <div data-tips="true" data-tips-type="default">Whether the computer has location services enabled</div><br><br><br>2. <div data-tips="true" data-tips-type="default">Whether the computer or browser restricts browser location access permissions</div><br><br><br><br><div data-tips="true" data-tips-type="default">If the browser's location permission was previously denied, you must restart the computer to reset the permission restrictions.</div><br> |
   |Specify User Location |Manually enter latitude and longitude coordinates (e.g., `Longitude: 39.9°`, `Latitude: 116.4°`) |
   

3. **View changes in recommendation results**

   Click  **"Recommend again"** . The system will apply configured boosting/demoting rules based on the simulated user location and the actual distance of items (requires item dataset with latitude and longitude configured). For example:

   * **Boost effect for nearby items:**  If the rule sets "boost items within 5 km of the user by 50%," items within this range rank higher in the recommendation list.

   * **Demotion effect for distant items:**  If the rule sets "demote items beyond 20 km from the user by 80%," items beyond this distance rank lower in the recommendation list or receive less exposure.
