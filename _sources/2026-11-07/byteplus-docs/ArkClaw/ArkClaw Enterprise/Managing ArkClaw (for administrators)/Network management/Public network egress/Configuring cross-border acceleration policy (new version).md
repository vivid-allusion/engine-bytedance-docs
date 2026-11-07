---
title: "Configuring cross-border acceleration policy (new version)"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Configuring-cross-border-acceleration-policy-new-version"
---

For cross\-border access scenarios, ArkClaw provides a Cross\-Border Acceleration​ service. You can add a cross\-border acceleration rule​ to your Web access policy based on your business needs. Once configured, cross\-border traffic to the specified domains will be accelerated.

<span id="xJE2zRJC"></span>
## Instructions


* Only one​ cross\-border acceleration rule can be created per Web access policy.

* Currently, the cross\-border service cannot be disabled once enabled.

* All domains using cross\-border acceleration share the same bandwidth cap.

* After the rule is configured, cross\-border traffic will be billed on a pay\-as\-you\-go​ basis via Cloud Data Transfer (CDT). For details, see [Billing](https://docs.byteplus.com/en/docs/87633/2307167).


<span id="zWOK9Hn7"></span>
## Before you begin


* [Public Network Egress](https://docs.byteplus.com/en/docs/ArkClaw/Enabling_or_disabling_access_log_for_public_network_egress) must be enabled and [Web Access Policy is activated](https://docs.byteplus.com/en/docs/ArkClaw/Configuring-Web-access-policy-for-public-private-network-egress-non-cross-border).

* Your [Cross-Border Qualification Application](https://console.byteplus.com/cbbp/apply/ChinaUnicom?product=arkclaw) is submitted and approved.


<span id="KIrewhS3"></span>
## Procedures

<span id="tKYTReD4"></span>
### Step 1: Enable cross\-border service


1. Log in to the [ArkClaw Enterprise Edition console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. On the Network Configuration page, click the "Space Egress" tab.

4. In the "Public network egress" section, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_49a09136752b92229c5f1da6b4850aac.png) </span>toggle of "Configuration \> Cross\-border service".

5. Click "OK" to complete the action.


<span id="Dh0DDn2y"></span>
### Step 2: Configure cross\-border acceleration rule


1. In the "Public network egress" section, click "Security controls \> Web access policy".

2. Click "Add Rule".

3. Click the “Custom rule” tab and configure the cross\-border acceleration rule.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Name |The name of the cross\-border acceleration rule. |Cross\-border acceleration rule |
   |Priority |Cross\-border acceleration rules have the highest priority among all Web access rules. Custom priority settings do not apply. |\- |
   |the action to perform |Specify **Allow** for the action to perform. |Allow |
   |Egress region |The egress region of the cross\-border acceleration rule must be **Asia Pacific**. |Asia Pacific |
   |Source |The source of the cross\-border acceleration rule must be set to **All**. |All |
   |Destination |Enter the target acceleration domain name. Up to 500 acceleration domains are supported. Currently, supported domains are listed in the [Target domain list](https://docs.byteplus.com/en/docs/394/106029#MtxPFQ86). |api.openai.com |
   

4. Click "OK" to complete the action.

   Once the cross\-border acceleration rule is successfully added, ArkClaw​ provides accelerated network access for all domains specified in the "Destination" field (e.g., api.openai.com).


<span id="MtxPFQ86"></span>
## Target domain list

The following is the list of domains currently supported for acceleration by the cross\-border public acceleration service. It is under continuous update.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">An asterisk (\*) before a domain indicates that all its third\-level subdomains are also supported for access.</div>


* <div data-tips="true" data-tips-type="tip">If the domains in this list do not meet your requirements, please contact your account manager.</div>




<columns>
<columnsItem zoneid="t58Ot2YXNy">

**LLM Services and Ecosystem**


* platform.openai.com

* auth.openai.com

* api.openai.com

* \*.openai.com

* platform.claude.com

* auth.anthropic.com

* api.anthropic.com

* \*.anthropic.com

* aistudio.google.com

* generativelanguage.googleapis.com

* oauth2.googleapis.com

* console.x.ai

* api.x.ai

* \*.x.ai

* \*.mistral.ai

* api.groq.com

* \*.groq.com

* api.cohere.ai

* api.cohere.com

* \*.cohere.ai

* \*.fal.media

* \*.fal.run

* openrouter.ai

* \*.openrouter.ai

* \*.ai.cloudflare.com

* clawhub.ai

* \*.clawhub.ai




</columnsItem>
<columnsItem zoneid="U6NTSdp3rv">

**Development Tools**


* go.dev

* golang.org

* go.opentelemetry.io

* pkg.go.dev

* registry.npmjs.com

* registry.npmjs.org

* registry.npmmirror.com

* registry.replicated.com

* registry.terraform.io

* rubygems.org

* sum.golang.org

* registry.k8s.io

* dl.k8s.io

* cdn.dl.k8s.io

* k8s.io

* apache.org

* \*.apache.org

* github.com

* \*.github.com

* \*.githubusercontent.com

* gitlab.com

* \*.gitlab.com

* pypi.org

* \*.pypi.org

* pythonhosted.org

* \*.pythonhosted.org

* quay.io

* \*.quay.io

* rust\-lang.org

* \*.rust\-lang.org

* sass\-lang.com

* \*.sass\-lang.com

* svc.ms

* \*.svc.ms

* visualstudio.com

* \*.visualstudio.com

* mysql.com

* \*.mysql.com

* docker.com

* \*.docker.com

* docker.io

* \*.docker.io




</columnsItem>
<columnsItem zoneid="ceQwREwMCK">

**Media and Social**


* discord.com

* discord.gg

* gateway.discord.gg

* discordapp.com

* \*.discordapp.com

* discordapp.net

* \*.discordapp.net

* graph.facebook.com




</columnsItem>
</columns>


&nbsp;
