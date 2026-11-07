---
title: "Configure custom watch lists"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Configure_custom_watch_lists"
---

The LLM Application Firewall includes a built\-in vector watch list for content compliance detection. It also supports creating a custom watch list. A custom watch list does not have block or allow attributes. It uses a **detection category** to associate matched content with effective objects (assets), and determines how detected content is processed based on the specified action. With this asset\-based effective logic, a custom watch list helps you implement flexible and fine\-grained content control.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div>


<div data-tips="true" data-tips-type="warning">If the custom watch list you currently use is an earlier version (an upgrade prompt appears in the upper\-left corner of the console page), we recommend that you upgrade to the new watch list management page as soon as possible. This helps you get a better experience in later version iterations.</div>


<span id="5e95ddc9"></span>
## Process description

You can use the following process to make a custom watch list take effect in a protection policy:


1. **Create a custom detection category**: Create a new detection category, such as "Financial compliance".

2. **Create a custom watch list**: Associate watch lists with similar attributes to the same detection category.

3. **Create a custom rule**:

   1. On the custom detection rule page, create a rule, and select the target asset and the detection category that needs to take effect. Watch lists configured with the same detection category are automatically bound to the target asset.

   2. Configure the expected action in the rule, such as "Allow", "Block", "Secure reply", or "Observe".

4. **Rule takes effect**: After you save the configuration, when user input or model output hits the watch list, the system performs the action that you specified based on the corresponding custom rule, such as block or allow.


<span id="b7632776"></span>
## **Scenario examples**


* **Allowlist scenario**: For example, to ensure that specific industry terms or brand names are not blocked by mistake, you can perform the following operations:

   1. Add these terms to the same watch list.

   2. Associate the watch list that contains these terms with a custom detection category, such as `Financial_industry_allowlist`.

   3. Configure a custom detection rule for the related asset. Select the category that corresponds to the watch list, and set the action to **Allow**.

* **Blocklist scenario**: For example, to block or monitor known non\-compliant content, you can perform the following operations:

   1. Add these terms to the same watch list.

   2. Associate the watch list that contains these terms with a custom detection category, such as `Financial_industry_blocklist`.

   3. Configure a custom detection rule for the related asset. Select the category that corresponds to the watch list, and set the action to **Block**, **Secure reply**, or **Observe**.


<span id="112fd1aa"></span>
## Notes


* If you do not configure any custom watch list, the system uses the preset watch list for content detection by default.

* Limits on the number of custom watch lists:

   * Up to 100 custom watch lists are supported.

   * All watch lists can contain up to 10,000 vocabulary rules in total.

   * Regex matching can contain up to 10 vocabulary rules in total.


<span id="348c8698"></span>
## Procedure


1. Log on to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield).

2. In the left navigation pane, choose **Protection \> Custom protection \> Custom watch list**.

3. Click **Add watch list**. On the configuration page that appears, enter the watch list information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d15c856014584a9b96f4dd0b0fddda3c~tplv-goo7wpa0wc-topic.webp) </span>

&nbsp;

   
   |Parameter |Description |Example value |
   |---|---|---|
   |**Watch list name** |Specify a recognizable name for your watch list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Start with letters, or digits.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Letters, digits, periods ".", underscores "_", and hyphens "\-" are allowed.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The length is 1 to 128 characters.</div><br> |Financial_industry_blocklist |
   |**Description** |Add supplementary information about the watch list usage and scenarios to facilitate subsequent management and understanding. |Used to identify and block inducement\-related terms involving high\-yield financial products and illegal fundraising. |
   |**Detection category** |Specify a detection category for the watch list so that it can be associated in a custom rule.<br><br>You can select an existing category from the drop\-down list. If no existing category applies, click  **+ New category** to create a category.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">After you create a category, you must go to the "Custom detection rule" page to create a rule and bind the category before it can take effect.</div><br> |FinancialCompliance |
   |**Matching method** |You can select the method that best fits your scenario from the following three matching methods:<br><br><br>* **Exact match:**  A hit occurs only when the content to be detected is exactly the same as one entry that you enter here.<br><br>   * Applicable scenario: Suitable for scenarios that require precise control, such as instructions and proper nouns.<br><br>   * Example: If the watch list content is "hello", only content that is exactly "hello" is hit.<br><br>* **Keyword matching:**  A hit occurs when the content to be detected contains the keyword combination that you specify.<br><br>   * **Order not retained (default):**  The text only needs to contain all specified keywords, regardless of their order. Example: The keywords are "principal\-protected" and "zero\-risk". When the content is "This wealth management product is principal\-protected and zero\-risk" or "This wealth management product is zero\-risk and protects your principal", the rule is hit.<br><br>   * **Order retained:**  The text must contain all keywords in the specified order. The keywords are "principal\-protected" and "zero\-risk". The rule is hit only when the content is "This wealth management product is principal\-protected and zero\-risk". The rule is not hit when the content is "This wealth management product is zero\-risk and protects your principal".<br><br>* **Regex matching:**  Allows you to use regular expressions to define complex matching patterns. It is suitable for text that needs to identify specific formats or structures, such as mobile phone numbers, ID numbers, or specific sentence patterns.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">Enter a regular expression that complies with general specifications. To ensure system performance, avoid complex expressions that may cause performance issues, such as expressions that contain excessive backtracking.</div><br><br><br><br>* Example 1: Detect that a user asks about a specific yield forecast. For example, write the expression as `(yield\|return)\s*\d+\s*%`.<br><br>   * Hit: "yield 5%", "return 10%", "annualized return 8%".<br><br>   * Not hit: "yield 5" (no percent sign), "high annualized return" (no specific value).<br><br>* Example 2: Non\-compliant promised returns. For example, write the expression as `(guarantee\|promise\|ensure\|steady\|sure).{0,5}(earn\|profit\|return\|interest\|recover)`.<br><br>   * Hit: "guarantee to recover", "sure profit", "ensure your returns are positive".<br><br>   * Not hit: "*To keep your account secure, do not share your password*" (no benefit\-related keyword appears), "*promise that we will absolutely make huge profit*" (there are more than 5 characters between the two keywords). |Keyword matching (order not retained) |
   |**Prompt** |* Define the specific matching content of the custom watch list here. You can select different matching methods as needed and batch paste input is supported.<br><br>* **Batch paste enhancement**:<br><br>   * You can fill multiple custom entries in a column of an Excel spreadsheet, then copy and paste the column content directly into the input box. The system will automatically split it into multiple independent custom watch list records.<br><br>   * When **Matching type** is selected as **Keyword matching**:<br><br>      * **Single entry (AND logic)** : To configure "Match only when both A and B are included", enter A and B in the same input box (separated by line breaks).<br><br>      * **Multiple entries (OR logic)** : To configure "Match when A or B is included", click the add button and enter A and B in different input boxes. |High yield / zero risk |
   |**Rule switch** |Specify whether to enable the watch list as needed. |Enabled |
   

4. After all configurations are complete, click **OK**.


<span id="11417292"></span>
## Follow\-up operations

After a custom watch list is created, you must associate the watch list with a custom detection rule before it can take effect. For more information, see [Configure custom detection rules](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_custom_detection_policies).

<span id="8af5a190"></span>
## Effect demonstration

To help you better understand how a custom watch list works, the following section uses a financial compliance scenario to show the effective logic under different matching methods.

<span id="9303e3d3"></span>
### Configuration example

&nbsp;


|Configuration |Description |Generated ID |
|---|---|---|
|Custom watch list |* Custom watch list name: Financial_industry_blocklist<br><br>* Detection category: FinancialCompliance<br><br>* Matching condition 1:<br><br>   * Matching method: Exact matching<br><br>   * Matching content: `Query credit card bill`<br><br>* Matching condition 2:<br><br>   * Matching method: Keyword matching (order not retained)<br><br>   * Matching content: `high yield` / `zero risk`<br><br>* Matching condition 3:<br><br>   * Matching method: Regex matching<br><br>   * Matching content: `Recommend a stock with a yield rate of (\d+(\.\d+)?%?)` |thesaurus\-d6en5bjhvcgdavcs\*\*\*\* |
|Custom detection rule |* Rule name: Financial_compliance_detection<br><br>* Protected asset: app\-d5ived60ssmv8r6r\*\*\*\*<br><br>* Effective method: Take effect on both input and output<br><br>* Detection category: FinancialCompliance<br><br>* Action: Block |rule\-d6en68jhvcgau1c6\*\*\*\* |


<span id="fbae615d"></span>
### Test results

<span id="773e0747"></span>
#### Hit the protection policy (block)

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">If the asset is associated with a custom response blocking policy, after the detected content hits the protection policy and is blocked, the client receives the response content configured in the custom response policy.</div>



* **Host**: Replace `****.com` with the protected domain name.

* **URL**: Replace `****.access-bp.llm-shield.omni-shield.ai` with the domain name generated by LLM Application Firewall, and replace `/v1/chat/completions` with the real path.



<Tabs>
<Tab zoneid="gJGR1vu5UU" title="Exact match">
<TabTitle>Exact match</TabTitle>

```Shell
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: */*" \
  -H "Host: ****.com" \
  --write-out "%{http_code}\n" \
  -d '{
    "messages": [  
      {  
        "role": "user",  
        "content": "Query credit card bill"  
      }  
    ] 
  }' \
  http://****.access-bp.llm-shield.omni-shield.ai/v1/chat/completions
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d475b75bd8b24b738852f95cabce680f~tplv-goo7wpa0wc-topic.webp) </span>


</Tab>
<Tab zoneid="o0y3mB3sYt" title="Keyword matching">
<TabTitle>Keyword matching</TabTitle>

```Shell
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: */*" \
  -H "Host: ****.com" \
  --write-out "%{http_code}\n" \
  -d '{
    "messages": [
      {  
        "role": "user",  
        "content": "This stock has high yield and zero risk?"  
      }  
    ]
  }' \
  http://****.access-bp.llm-shield.omni-shield.ai/v1/chat/completions
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/20c994b5d0904f8aa7862166b1ad8986~tplv-goo7wpa0wc-topic.webp) </span>


</Tab>
<Tab zoneid="yw1bUrAMJm" title="Regex matching">
<TabTitle>Regex matching</TabTitle>

```Shell
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: */*" \
  -H "Host: ****.com" \
  --write-out "%{http_code}\n" \
  -d '{
    "messages": [  
      {  
        "role": "user",  
        "content": "Recommend a stock with a yield rate of 20%"  
      }  
    ] 
  }' \
  http://****.access-bp.llm-shield.omni-shield.ai/v1/chat/completions
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d458bd409ff4e56b130bb6080831835~tplv-goo7wpa0wc-topic.webp) </span>


</Tab>
</Tabs>


<span id="8ab045e8"></span>
#### Did not hit the protection policy (allow)


<Tabs>
<Tab zoneid="X2h8yKbjGn" title="Exact match">
<TabTitle>Exact match</TabTitle>

```Shell
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: */*" \
  -H "Host: ****.com" \
  --write-out "%{http_code}\n" \
  -d '{
    "messages": [  
      {  
        "role": "user",  
        "content": "Query my credit card bill"  
      }  
    ] 
  }' \
  http://****.access-bp.llm-shield.omni-shield.ai/v1/chat/completions
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6274bb213c8949d983c9f6ef62b4270e~tplv-goo7wpa0wc-topic.webp) </span>


</Tab>
<Tab zoneid="Ewh5ZQNbDm" title="Keyword matching">
<TabTitle>Keyword matching</TabTitle>

```Shell
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: */*" \
  -H "Host: ****.com" \
  --write-out "%{http_code}\n" \
  -d '{
    "messages": [  
      {  
        "role": "user",  
        "content": "This stock has zero risk?"  
      }  
    ] 
  }' \
  http://****.access-bp.llm-shield.omni-shield.ai/v1/chat/completions
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ebee074218c48cfb1c1395b0ed93596~tplv-goo7wpa0wc-topic.webp) </span>


</Tab>
<Tab zoneid="tBI0XiizdX" title="Regex matching">
<TabTitle>Regex matching</TabTitle>

```Shell
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: */*" \
  -H "Host: ****.com" \
  --write-out "%{http_code}\n" \
  -d '{
    "messages": [  
      {  
        "role": "user",  
        "content": "Recommend a stock with a stable yield rate"  
      }  
    ] 
  }' \
  http://****.access-bp.llm-shield.omni-shield.ai/v1/chat/completions
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/906a084f0fbd464a8d5e4b1cc8f208d1~tplv-goo7wpa0wc-topic.webp) </span>


</Tab>
</Tabs>


<span id="15fccf76"></span>
### Attack logs

On the asset management page in the console, click the target asset name and select **Attack logs**.

Then enter the rule ID `rule-d6en68jhvcgau1c6****` in the advanced filter box to find the log information of the preceding simulated requests.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ccaa09f455e4c01978e580fe81f2bbe~tplv-goo7wpa0wc-topic.webp) </span>

<span id="ebc216b6"></span>
## FAQ

If the custom watch list you use is an earlier version (an upgrade prompt appears in the upper\-left corner of the page), you can refer to the following content to learn about upgrade\-related issues.

<span id="e9b4492a"></span>
### What is the impact if I do not upgrade?

The earlier watch list version no longer supports editing. This affects efficient control and management of custom watch lists and the user experience. We recommend that you upgrade to the new watch list version as soon as possible.

<span id="49d3e690"></span>
### What are the differences between the earlier and new watch list versions?

In the earlier watch list version, positive watch lists and negative watch lists take effect globally. The new watch list version provides more matching methods (supports regex matching) and a more fine\-grained and flexible effective scope (supports asset\-based effect). The following table describes the main differences:

&nbsp;


|**Comparison dimension** |**Earlier watch list version (rigid control)**  |**New watch list version (flexible control)**  |
|---|---|---|
|**Control logic and actions** |**Attribute\-bound actions**:<br><br><br>* **Positive watch list**: Fixed to Allow.<br><br>* **Negative watch list**: Supports Block, Secure reply, or Observe. |**Attributes and actions decoupled**:<br><br><br>* The watch list itself has no positive or negative attributes and is used only as a matching condition.<br><br>* The specific action is determined by the associated custom rule configuration. |
|**Effective scope and configuration** |**Coarse\-grained effect**:<br><br>Positive and negative watch lists take effect for **all global assets**. |**Fine\-grained effect**:<br><br><br>* Supports configuration **by asset**.<br><br>* You must select the target asset and the detection category associated with the watch list in a custom detection rule to implement precise control. |
|**Matching capabilities** |**Basic matching**:<br><br><br>* Exact match<br><br>* Keyword matching |**Enhanced matching**:<br><br><br>* Exact match<br><br>* Keyword matching<br><br>* Regex matching |


<span id="04c6bb40"></span>
### How do I upgrade? How are earlier watch lists handled after upgrade?

The following path describes the upgrade procedure. We ensure smooth migration during the upgrade and ensure that your custom watch list feature is not affected. After the upgrade is complete, your earlier watch lists are retained, but editing is not supported.


1. In the upper\-left corner of the custom watch list page, click **Upgrade watch list**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5885b8ba40d940e1bdcdb281cd956742~tplv-goo7wpa0wc-topic.webp) </span>

2. Map the positive and negative watch lists to different custom detection categories.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If no custom detection category exists, you can click <strong>New category</strong> to create one directly.   </div>
   

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0beba9e166d44d5d93995de039f7ea67~tplv-goo7wpa0wc-topic.webp) </span>


3. After confirmation, click **Upgrade watch list**.

   After the earlier watch list is upgraded to a new watch list, the system automatically creates custom watch lists and custom rules:

* **Watch list changes**: New custom watch lists are generated based on the original watch list attributes and switch states. For example, among the original 4 positive watch lists A, B, C, and D, A and B are enabled, and C and D are disabled. In this case, watch lists A and B are automatically aggregated into new watch list E, and watch lists C and D are automatically aggregated into new watch list F. The same applies to negative watch lists.

* **Rule changes**: The system automatically creates custom detection rules that take effect for different assets based on the detection categories mapped from the earlier watch lists. The execution action of the rule determines whether content that hits the watch list is allowed (earlier positive watch list) or blocked (earlier negative watch list).

4. Confirm the enabled status of the custom rule.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Caution   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">A custom rule takes effect only when both the global switch of custom detection rules and the corresponding rule are enabled.   </div>
   

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ddd9871d69b43fd96b9fbdf9a089650~tplv-goo7wpa0wc-topic.webp) </span>

<span id="e4049c41"></span>
### How do new assets use a custom watch list?

After you complete the watch list switch, its content no longer takes effect for global assets. Therefore, if you need new assets to match custom watch list content, create a new custom detection rule for the asset and associate the rule with the custom detection category that corresponds to the watch list.

<span id="fc7ab8d7"></span>
### Why does the new rule not take effect after the custom watch list is upgraded?

If the custom rule associated with your original watch list is disabled, the corresponding rule remains disabled after the upgrade. Check the enabled status of the upgraded custom rule.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div>


<div data-tips="true" data-tips-type="warning">A custom rule takes effect only when both the global switch of custom detection rules and the corresponding rule are enabled.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5920d0ea1e3347eeb446bcaa7ad67adc~tplv-goo7wpa0wc-topic.webp) </span>
