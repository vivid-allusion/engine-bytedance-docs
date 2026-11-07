---
title: "Sending a quiz"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/sending-a-quiz"
---

You can send a quiz to assess the effectiveness of live training, and then provide rewards to viewers who answer correctly as needed.

<span id="37ae0c09"></span>
## Prerequisites


* Make sure the menu for interaction tools is added. For more information, see [Configuring the menu for interaction tools](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-the-interaction-area#f1b04790).

* Send a quiz on the console

   Make sure you have a BytePlus account or an IAM user with Live control \> Edit permission.

* Send a quiz on the live streaming page in a web browser

   * We recommend that you use devices and browsers that meet the specified requirements for live streaming to ensure you can have a smooth live streaming experience. For more information, see [Environmental requirements to start a live stream](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-your-web-browser#d66d12ba).

   * If you enter the live streaming page through the console, make sure you have a BytePlus account or an IAM user with Live control \> Edit permission.

   * If you use a link to enter the live streaming page without the need for logging in, no console permissions are required to send a quiz.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on how to add IAM users, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles">Managing users, organizations, and roles</a>.</div>


<span id="2c162a9e"></span>
## Procedure

<span id="d9a5a6f0"></span>
### Step 1: Enter the Quiz dialog box


* Console

   1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

   2. On the live room list, click to open a live room.

   3. On the **Live control** page, click **Quiz** under the menu for interaction tools.

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86f68a80f87648c5a0c02a33b9c84368~tplv-goo7wpa0wc-image.image" width="1858px" />      </div>
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For a better viewing experience, we recommend that you turn on the <strong>Display menu</strong> switch in the lower\-right corner to display the menu on the viewing page.      </div>
      

   4. Click **Create quiz** in the dialog box that appears.

* Live streaming page in a web browser

   1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

   2. Select **Web browser** as the broadcast method and go to the live streaming page. For more information, see [Live streaming from your web browser](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-your-web-browser).

   3. On the tab for interaction tools, click **Quiz**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2fcc364952d4215a2d2e737663a6fac~tplv-goo7wpa0wc-image.image) </span>


<span id="5283385c"></span>
### Step 2: Configure and send a quiz

The operations are similar on the console and the live streaming page in a web browser. In this step, take the console as an example.


1. In the **Quiz** dialog box that appears, complete the following configurations and click **Save**.

   If this is not the first quiz in the live room, click **Create** and then complete the following configurations.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61820e884be545e9877504a2856f200e~tplv-goo7wpa0wc-image.image) </span>

   * **Quiz type**: Select **Choose one** or **Choose all that apply** to configure whether viewers can select more than one option in the quiz.

   * **Title**: Enter the title of the quiz.

   * **Options**: Enter the options in the quiz.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can configure at most 8 options in a quiz.      </div>
      

   * **Correct answer**: Select the correct answer.

   * **Answer explanation**: Provide an explanation for the answer.

   * **Announce the answer**: Select the timing to announce the answer. Once the answer is announced, viewers cannot submit the quiz.

      * **Automatically after submission**: Viewers can see the correct answer immediately after they submit the quiz. Therefore, the time at which viewers see the answer may vary.

      * **When the time limit ends**: The answer is announced when the quiz countdown ends.

      * **Manually**: The answer is announced manually. You can do this in the **View details** dialog box as described in step 4.

   * **Time limit for answering**: Select the answering time for viewers after the quiz is sent to the viewing page.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">This field is available when the answer is not set to be announced manually.      </div>
      

2. Click **Add to send area** and then click **Send** under the menu for interaction tools to send the quiz to the viewing page.

   If you have multiple unsent quizzes, select the quiz on the left first and then click **Add to send area**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/abd5812423ac4f1b9556380af9a61fdb~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">On the console, you can also click <strong>Quiz</strong> under the menu for interaction tools and select the quiz to be sent in the dialog box that appears. Click <strong>Send</strong> to send the quiz to the viewing page. At most 100 quizzes can exist in the dialog box. If it exceeds 100, you must first delete or withdraw existing quizzes before adding or copying quizzes.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">On the live streaming page in a web browser, select the quiz and click <strong>Send</strong> in the <strong>Quiz</strong> dialog box to send the quiz to the viewing page.   </div>
   

3. (Optional) You can copy, preview, edit, or delete unsent quizzes, as well as copy or delete sent quizzes.

4. (Optional) Under the menu for interaction tools, you can perform the following operations.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a9f549ea9c940fe8b2807a585e4e2b0~tplv-goo7wpa0wc-image.image) </span>

   * Click the **Withdraw** icon to withdraw a sent quiz.

   * Click **View details** to view the quiz results. In the **View details** dialog box that appears, you can perform the following operations:

      * If you select **Manually** in the **Announce the answer** field in step 1, click **Announce the answer** to announce the answer manually.

      * If you select **Automatically after submission** or **When the time limit ends** in the **Announce the answer** field in step 1, you can also click **Announce the answer** to manually announce the answer in advance.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Data is updated every 10 seconds. You can also click <strong>Refresh data</strong> to refresh data manually.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can also view the quiz data on the <strong>Insights</strong> \> <strong>Quiz data</strong> page of the console. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-data-statistics">Viewing data of a live room</a>.      </div>
      


<span id="6f834dba"></span>
## What your viewers see

Viewers can only open the latest manually sent quiz by clicking the quiz icon. However, they can open all the manually sent quizzes in the live room under the menu for interaction tools.

Viewers can submit a quiz in the following steps:


1. Log in to the live room.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Viewers must log in to the live room before participating in quizzes. If <strong>Public</strong> is set as the comment restriction on the <strong>Producer</strong> \> <strong>Viewing restrictions</strong> page, viewers must enter their phone numbers to log in to the live room.   </div>
   

2. After a quiz is sent to the viewing page, the quiz dialog box automatically appears. Then, viewers can select answers and submit the quiz. If the quiz dialog box is closed, they can also manually open it to participate in the quiz.

3. Depending on the timing you select for announcing the answer, the result dialog box automatically appears after viewers submit the quizzes, after the countdown ends, or after you manually announce the answer. If the result dialog box is closed, viewers can also manually open it to view the result.



|Scenario ||On PCs |On mobile devices |
|---|---|---|---|
|Participate in the quiz |By default, the quiz dialog box automatically appears |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fda69afc74f0464781f8756b84ab6b82~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/647e4d8d44664c0e838b5f6cfffb2c62~tplv-goo7wpa0wc-image.image) </span> |
||If the quiz dialog box is closed, viewers can also manually open it to participate in the quiz |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/17735bdf806b49f5bae1c9bd8a5791b2~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ec5eb4987c747438d824780ec26f630~tplv-goo7wpa0wc-image.image) </span> |
|View the result |By default, the result dialog box automatically appears |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b842551b5ed640c3b11f14a480691502~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d1d7ac7ff8f47fd81981fbecd672c67~tplv-goo7wpa0wc-image.image) </span> |
||If the result dialog box is closed, viewers can also manually open it to view the result |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d6cf130f7af4cb496db33dd1604f2b0~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d5eb9747b7c48fbb2e36803889aa226~tplv-goo7wpa0wc-image.image) </span> |
