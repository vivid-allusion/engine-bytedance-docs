---
title: "Circle Events"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Circle-Events"
---

You can create a new web or mobile circled event in the circled event and view the details of all the circled events.

<span id="596a013f"></span>
# Prerequisite

Before using this function, please ensure that full event tracking has been enabled, that is, the full event tracking switch has been turned on in the SDK on the web or App side. For the full event tracking function switch configuration of each end SDK, please refer to the data access SDK documentation on each end.

<span id="页面介绍"></span>
# Page introduction

The "Circle Events" page is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb76dd94626640ec9cf8f87462e10c7f~tplv-goo7wpa0wc-image.image) </span>


* You can enter the event name/event description to search for the event you want to find, and you can manually switch the sorting method of circled events, such as recent attention, creation date, and number of included events;

* You can select web end circling events and mobile end circling events.


<span id="网页端圈选"></span>
## Circle

**Step 1: Click "+ New Circle Event" \- websites;** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c082e65e149142228d6fa9c2e1e8698a~tplv-goo7wpa0wc-image.image) </span>

**Step 2: Enter the address of the circled URL and click "Confirm";** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4f654f760fb47c783a75fb9210501d5~tplv-goo7wpa0wc-image.image) </span>

Tip: If you click Submit and the Circle toolbar does not appear, please check if full event tracking is enabled.

**Step 3: Circle the elements.** 

① If the entered website has circled the event tracking sdk before, you can open the page corresponding to the address on the new tab page, and there will be a floating toolbar at the top, as shown below (circle the event tracking page):

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/691a3f0c2bf24d9bb8dcac8d6179fb1b~tplv-goo7wpa0wc-image.image) </span>


* "Browse, circle, heat map" View switch:

   * "Circle selection" is selected by default, and the circle selection function is used normally;

   * Clicking "Browse" will change to browse the website mode, and circling related functions is not available;

   * Click "heat map", you need to select a page or page group.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f463deb97204f3c81357184765b6857~tplv-goo7wpa0wc-image.image) </span>

* Click the "Define Page" button to define the entire current page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e733c46332f4c1cb8eaa82e0bb0ffb7~tplv-goo7wpa0wc-image.image) </span>

* The checkbox "Highlight defined events" is turned off by default. After opening, all the circled front\-end control elements will be displayed on the entire page, and the color is different from the newly circled one;

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2adc519a5cf4a1dbbeb784c8c6b32a8~tplv-goo7wpa0wc-image.image) </span>

* Click the drop\-down box "This page has marked xx elements" to expand the drop\-down list, which lists all the element\-type events that have been defined on the current page;

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a6c8f126e4945e2ae655e5c96e46126~tplv-goo7wpa0wc-image.image) </span>

* Click the "Close" button to exit the circled mode and turn it into normal browsing mode, and the floating toolbar disappears.


② When the mouse moves on the page, a green floating layer mark will appear. After clicking, enter the element circle selection, as shown below:


* Fill in the event name, select the page to which it belongs, and tick the qualification;

* The bottom is the hour level of the currently selected element (the last 48 hours, real\-time data), the number of triggers, and the number of triggers changes;

* Click Save to successfully save the element.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c21828ff0d264652abe25457821b9914~tplv-goo7wpa0wc-image.image) </span>


* Element event groups are divided into the following two cases:

   * For the same events that belong to different pages, such as buttons in the navigation bar, first define the corresponding page group with the wildcard path, and then select the page group when defining the element event.

   * For similar events in lists belonging to the same page, just ignore the "Match Location" and "Match Content" options.


**Step 4: Define the page.** 


* New pages/page groups can be defined.

   * Fill in the page name, domain name (there are three values: \*/http/https, \* is selected by default), more settings, etc.;

   * Under "Define a new page/page group", display the page class events/page groups defined on the current page, select any one to view the defined configuration, and only modify the page name;

   * The bottom right is the hour level of the currently selected element (the last 48 hours, real\-time data), the number of triggers and the number of triggers change;

   * Click Save to successfully save the page.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c157463190a74906be2ec91fb85cb788~tplv-goo7wpa0wc-image.image) </span>

The definition of a page group is divided into the following two cases:


* Wildcard path, such as defining a page group containing: `http://www.example.com/product/123456.html`, you can set the page path to: `http://www.example.com/product/\ *`

* Limit parameters, such as defining events: car e\-commerce \- search SUV, links that meet the definition include `xxx.com/search?keyword=SUV&tab=1`and `xxx.com/search?keyword=SUV&tab=2`, you need to set the query parameters to `"keyword = SUV &\ *"`.


**Step 5: After event circling, you can select and use it in various analysis functions, and the usage method is basically the same as that of general events; you can also view and manage it in "Data Management \- Circling Events".** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef96e4994c244fc38134a34acb1ff332~tplv-goo7wpa0wc-image.image) </span>

<span id="移动端圈选"></span>
## Mobile end selection

You can create a newly circled event. **Scan the code to start the circle selection, as follows:** 

**Step 1: Click "+ New Circle Event" \- mobile end;** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3313948e1a8f4e3384646eaf1e943dfb~tplv-goo7wpa0wc-image.image) </span>

**Step 2: WeChat scan code;** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e43bbe72aae406db3238244d5541453~tplv-goo7wpa0wc-image.image) </span>

**Step 3: Open it in the mobile browser.** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06b7a12889b84e408cce5e9ce42ec387~tplv-goo7wpa0wc-image.image) </span>

**Step 4: Select the circling method;** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b99e3a78a2143dbba2ab1485886a2fe~tplv-goo7wpa0wc-image.image) </span>


* If there is an error in circling startup, the following image will be displayed:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/deedf61f0665460090d455852db5603a~tplv-goo7wpa0wc-image.image) </span>

* If the loop starts successfully, you can start the loop event tracking.

   * Click the mouse to start circling, as shown below:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e3c993cb48f4e6c90e116b3e4bc6040~tplv-goo7wpa0wc-image.image) </span>

   * Define the circled element, the selected element presents a green thick border and a transparent base color, and can perform operations such as event naming and selecting the page to which it belongs;

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ba2d2641a344de492f0180d13d55fe7~tplv-goo7wpa0wc-image.image) </span>

* You can click on the card of the circled event to enter the circled event details.

   * The circled event details are shown below, including information about the circled elements, thumbnails, data previews, event details, and more.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd6f852959554735ab1b2787952c03d8~tplv-goo7wpa0wc-image.image) </span>


**Reminder:** 


* The circled event will be displayed in the event configuration options for event analysis, retention analysis, conversion analysis, user path, and user grouping, as shown below:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67e81d4d848242f1a0531f8c151566f8~tplv-goo7wpa0wc-image.image) </span>



---



Note: DataFinder is a former name for BytePlus Growth Analytics.
