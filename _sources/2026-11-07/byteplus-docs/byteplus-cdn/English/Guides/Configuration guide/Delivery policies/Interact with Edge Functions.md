---
title: "Interact with Edge Functions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Configure-Edge-Function-Forwarding-Rules"
---

To control which requests trigger your Edge Functions, you can create forwarding rules. This guide provides step\-by\-step instructions on how to associate a function with your domain and configure rules based on request conditions like URL path or file extension. By following these steps, you can precisely manage your edge logic and customize content delivery.

<span id="prerequisites"></span>
## Prerequisites

The function you want to associate must have been fully released at least once.

<span id="steps"></span>
## Steps


1. Log in to the [BytePlus CDN Console](https://console.byteplus.com/cdn).

2. On the **Domain Names** page, find the domain you want to configure and click **Modify** in the **Actions** column.

3. Locate the **Edge Functions** section on the domain details page.

4. If the Edge Functions switch is **Off**, you need to click the switch to set it to **On**.

5. Enter the name of the function, select it from the list, and then click **OK**.

6. Click **Add** in the **Forwarding rules** section.

7. Configure the rule according to the [Configuration description](https://docs.byteplus.com/en/docs/18/20007#configuration-description). Rules are processed in order of priority, from top to bottom. When a request matches a rule, the CDN executes it and stops processing subsequent rules.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a8c193970baecb60657aa187ff90986a.jpeg) </span>

8. After configuration, click **OK** in the bottom right corner of the page.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can change the function assigned to a rule or delete rules based on your business needs.</div>


* <div data-tips="true" data-tips-type="tip">If an domain no longer needs the edge function feature, you can set the edge function switch to <strong>Off</strong>. It's important to note that when you set the edge function switch to <strong>Off</strong>, the association between the domain and the function will not change, but the associated function will no longer be triggered because all configured rules are disabled at this point.</div>



<span id="configuration-description"></span>
## Configuration description


|**Configuration** |**Description** |
|---|---|
|Condition |Represents the matching condition of the rule. When a request matches the condition, the CDN executes the associated edge function. The configuration has the following options:<br><br><br>* **URL Path Extension**: Matches requests for files with specific extensions.<br><br>* **URL Path Directory**: Matches requests for files with specific directory paths.<br><br>* **URL Path** : Matches requests for files with specific URL paths. |
|Patterns |Specifies the pattern to match. The pattern must be no more than 1,024 characters long and must not contain the following characters:<br><br><br>* Double slashes (//), spaces, dollar signs ($), question marks (?).<br><br><br>Additionally,<br><br><br>* If the rule type is **URL Path Extension**, the rule content must be one or more file extensions separated by semicolons (;). File extensions do not need to start with a dot (.). For example: `png;txt`.<br><br>* If the rule type is **URL Path Directory**, the rule content must be one or more directory paths separated by semicolons (;). Directory paths must start and end with a slash (/). For example: `/chs/foods/;/us/birds/`.<br><br>* If the rule type is **URL Path**, the rule content must be one or more file paths separated by semicolons (;). File paths must start with a slash (/) and can include asterisks (\*) to represent one or more characters. For example: `/chs/foods/local*sets;/us/birds/chickadee.` |
|Ignore case |Specifies whether pattern matching is case\-sensitive. The rest of the request URL is not affected by this configuration. The default setting is On. On means that the case is not distinguished.<br><br>Example: For the file extension rule, you set **Ignore case** as Off. You input the rule content as `png;txt`. In this case, the rule can match `HTTPS://www.EXAMPLE.com/byteplus.png`, but it cannot match `https://www.example.com/byteplus.PNG`. |
|Edge function |Specify the function assigned to the rule. |
