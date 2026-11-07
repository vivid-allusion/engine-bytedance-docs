---
title: "Circle Event"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Circle_Event"
---

You can create a new web or mobile circled event in the circled event and view the details of all the circled events.

<span id="d781903b"></span>
# Prerequisite

Before using this feature, make sure that full event tracking is enabled:


* The full event tracking switch has been turned on in the SDK of the Web or App side. For the full event tracking function switch configuration of the SDK of each end, please refer to the SDK documentation of each end data access.

* The full event tracking function switch is turned on on the Circle Events page in the DataFinder console.


<span id="页面介绍"></span>
# Page introduction

The "Circle Events" page is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5e3723bbca548fabf1d6fc141a05304~tplv-goo7wpa0wc-image.image) </span>


* You can enter the event name/event description to search for the event you want to find, and you can manually switch the sorting method of circled events, such as recent attention, creation date, and number of included events;

* You can select web end circling events and mobile end circling events.


<span id="网页端圈选"></span>
## Circle


1. **Step 1: Click "+ New Circle Event" \- web page;** 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f228990cfd34c93bc1e1c059916eded~tplv-goo7wpa0wc-image.image) </span>

2. **Step 2: Enter the address of the circled URL and click "Confirm";** 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/03704649eaa4454383f35d5e40d9784b~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you click <strong>Confirm</strong> and the Circle toolbar does not appear, check if full event tracking is enabled.   </div>
   

3. **Step 3: Circle the elements.** 

   1. If the entered website has circled the event tracking sdk before, you can open the page corresponding to the address on the new tab, and there will be a floating toolbar at the top, as shown below (circle the event tracking page):

      <span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/e02c73e7b0a14eb09741af02d99b44b2~tplv-em5hxbkur4-noop.image?width=2876&height=1394) </span>

      * "Browse, circle, heat map" View switch:

         * "Circle selection" is selected by default, and the circle selection function is used normally;

         * Clicking "Browse" will change to browse the website mode, and circling related functions is not available;

         * Click "heat map", you need to select a page or page group.<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/fba1b55979c44c7692f5d9f9b11208c7~tplv-em5hxbkur4-noop.image?width=1982&height=554) </span>

      * Click the "Define Page" button to define the entire current page.<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/eb9969aa296445c3b7e17125f23458e2~tplv-em5hxbkur4-noop.image?width=1984&height=1242) </span>

      * The checkbox "Highlight defined events" is turned off by default. After opening, all the circled front\-end control elements will be displayed on the entire page, and the color is different from the newly circled one;<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/76ad4fb5ba0e46149d3ef37da5dd7755~tplv-em5hxbkur4-noop.image?width=2426&height=1216) </span>

      * Click the drop\-down box "This page has marked xx elements" to expand the drop\-down list, which lists all the element\-type events that have been defined on the current page;<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/969a7fcc6cd3442780ccf89dca0ea6c0~tplv-em5hxbkur4-noop.image?width=2378&height=602) </span>

      * Click the "Close" button to exit the circled mode and turn it into normal browsing mode, and the floating toolbar disappears.

   2. When the mouse moves on the page, a green floating layer mark will appear. After clicking, enter the element circle selection, as shown below:

      * Fill in the event name, select the page to which it belongs, and tick the qualification;

      * The bottom is the hour level of the currently selected element (the last 48 hours, real\-time data), the number of triggers, and the number of triggers changes;

      * Click Save to successfully save the element.

         <span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/5fed2dc6f2d8465889f3e04a5dba250a~tplv-em5hxbkur4-noop.image?width=2420&height=1248) </span>

      * Element event groups are divided into the following two cases:

         * For the same events that belong to different pages, such as buttons in the navigation bar, first define the corresponding page group with the wildcard path, and then select the page group when defining the element event.

         * For similar events in lists belonging to the same page, just ignore the "Match Location" and "Match Content" options.

4. **Step 4: Define the page.** 

   New pages/page groups can be defined.

   * Fill in the page name, domain name (there are three values:  */http/https, selected by default* ), more settings, etc.;

   * Under "Define a new page/page group", display the page class events/page groups defined on the current page, select any one to view the defined configuration, and only modify the page name;

   * The bottom right is the hour level of the currently selected element (the last 48 hours, real\-time data), the number of triggers and the number of triggers change;

   * Click Save to successfully save the page.

       **<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/bb02986d65fe4f5da384c8de6a8f06e8~tplv-em5hxbkur4-noop.image?width=2838&height=1244) </span>** 

      The definition of a page group is divided into the following two cases:

   * Wildcard path, such as defining a page group containing: `http://www.example.com/product/123456.html`, you can set the page path to: `http://www.example.com/product/\ *`

   * Limit parameters, such as defining events: car e\-commerce \- search SUV, links that meet the definition include `xxx.com/search?keyword=SUV&tab=1`and `xxx.com/search?keyword=SUV&tab=2`, you need to set the query parameters to `"keyword = SUV &\ *"`.

5. **Step 5: After event circling, you can select and use it in various analysis functions, and the usage method is basically the same as that of general events; you can also view and manage it in "Data Management \- Circling Events".** 

   <span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/27ce6adaa38743cd86417336f2889eb3~tplv-em5hxbkur4-noop.image?width=1172&height=1000) </span>


<span id="移动端圈选"></span>
## Mobile end selection

You can create a new circled event. **Scan the code to start the circle selection, as follows:** 


1. **Step 1: Click "+ New Circle Event" \- mobile end;** 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57ab753ac05b4d06abcdd775424ebb3c~tplv-goo7wpa0wc-image.image) </span>

2. **Step 2: WeChat scan code;** 

   <span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/762e3cdabd9144f1ba3b88b19a1e21ee~tplv-em5hxbkur4-noop.image?width=651&height=329) </span>

3. **Step 3: Open it in the mobile browser.** <span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/f57e2b9510eb486da9e8ca0ab499639e~tplv-em5hxbkur4-noop.image?width=1235&height=591) </span>

4. **Step 4: Select the circling method;** <span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/e05570067b9e4ddf89576058447dc99e~tplv-em5hxbkur4-noop.image?width=2433&height=1122) </span>

   * If there is an error in circling startup, the following image will be displayed:<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/ce213e277638427ea5768327ccc46d47~tplv-em5hxbkur4-noop.image?width=5229&height=2340) </span>

   * If the circling starts successfully, you can start circling event tracking

      * Click the mouse to start circling, as shown below:<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/9f70434481bb4a3a8a36787d1b454d2f~tplv-em5hxbkur4-noop.image?width=1018&height=630) </span>

      * Define the circled element, the selected element presents a green thick border and a transparent base color, and can perform operations such as event naming and selecting the page to which it belongs;<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/25a02bcd8754448f8f0310cf8d76ca77~tplv-em5hxbkur4-noop.image?width=1030&height=603) </span>

   * You can click on the card of the circled event to enter the circled event details.

      * The circled event details are shown below, including information about the circled elements, thumbnails, data previews, event details, and more.<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/79974bfc93c24c24b8799768b4b01d3f~tplv-em5hxbkur4-noop.image?width=2322&height=1196) </span>


**Reminder:** 

The circled event will be displayed in the event configuration options for event analysis, retention analysis, conversion analysis, user path, and user grouping, as shown below:<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/fe8185687fe34b5ebc46ca3c54463218~tplv-em5hxbkur4-noop.image?width=2376&height=962) </span>


---



Note: DataFinder is a former name for BytePlus user growth.
