---
title: "Configuring cross-border acceleration policy (old version)"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Configuring-cross-border-acceleration-policy-old-version"
---

Cross\-border Public Acceleration is a network acceleration service provided by ArkClaw for the specified domains. You can add target domains based on your business needs. Added domains benefit from accelerated network access. For currently supported domains, see [Target domain list](https://docs.byteplus.com/en/docs/394/106030#Hk8A5uZ4).

<span id="uVnf8hCj"></span>
## Instructions


* All domains using cross\-border acceleration share the same bandwidth cap.

* Cross\-border traffic will be billed on a pay\-as\-you\-go​ basis via Cloud Data Transfer (CDT). For details, see [Billing](https://docs.byteplus.com/en/docs/87633/2307167).


<span id="1I2hEmno"></span>
## Before you begin


* [Public Network Egress](https://docs.byteplus.com/en/docs/ArkClaw/Enabling_or_disabling_access_log_for_public_network_egress) must be enabled.

* Your [Cross-Border Qualification Application](https://console.byteplus.com/cbbp/apply/ChinaUnicom?product=arkclaw) is submitted and approved.


<span id="zYLC7ea7"></span>
## Procedures


1. Log in to the [ArkClaw Enterprise Edition console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. In the Space Egress section, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b4801ed68f363d255f8acaecb67192fa.png) </span>icon to the right of "Public network egress \> Cross\-border public acceleration".

4. Click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_287e5762bcab401334fa8bcb9370a95a.png) </span> or <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a8b532f05699d6f86003b945876da172.png) </span>toggle under "Cross\-border public acceleration" to enable or disable cross\-border acceleration.

5. Add or remove the target acceleration domain in the Acceleration domain​ input field.

6. Click "OK" to complete the action.


<span id="Hk8A5uZ4"></span>
## Target domain list

The following is the list of domains currently supported for acceleration by the cross\-border public acceleration service. It is under continuous update.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">An asterisk (\*) before a domain indicates that all its third\-level subdomains are also supported for access.</div>


* <div data-tips="true" data-tips-type="tip">If the domains in this list do not meet your requirements, please contact your account manager.</div>




<columns>
<columnsItem zoneid="NXBt427y">

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
<columnsItem zoneid="PS1IJPpy">

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
<columnsItem zoneid="QZLU6rbq">

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
