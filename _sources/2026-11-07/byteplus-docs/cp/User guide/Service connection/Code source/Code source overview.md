---
title: "Code source overview"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/An_overview_of_the_code_source"
---

Code source is one of the input sources for the pipeline. Code source is used to manage your repository URL and access credentials. The following types of code source are currently supported:

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">CP has configured by default a network proxy service for the <strong>GitHub</strong> code source, so you can enjoy acceleration without any additional configuration.</div>



|Type |Code source |Service connection |Access key acquisition method |Webhook configuration instructions |
|---|---|---|---|---|
|GitLab |Supported |Supported |[Obtain GitLab token](https://docs.byteplus.com/en/docs/cp/Get_a_GitLab_token) |[Configure Webhook push for GitLab](https://docs.byteplus.com/en/docs/cp/Configure_a_GitLab_webhook) |
|Self\-built GitLab |Supported |Supported |[Obtain self-built GitLab token](https://archives.docs.gitlab.com/16.11/ee/user/profile/personal_access_tokens.html) |[Gitlab Webhooks](https://docs.gitlab.com/user/project/integrations/webhooks/) |
|GitHub |Supported |Supported |[Obtain GitHub token](https://docs.byteplus.com/en/docs/cp/Get_a_GitHub_token) |[Configure Webhook push for GitHub](https://docs.byteplus.com/en/docs/cp/Configure_GitHub_webhook_push) |
|BitbucketCloud |Supported |Supported |[Obtain BitbucketCloud token](https://docs.byteplus.com/en/docs/cp/Get_a_BitbucketCloud_token) |[Configure Webhook push for BitbucketCloud](https://docs.byteplus.com/en/docs/cp/Bitbucket_Cloud_webhook_configuration) |
|Perforce |Supported |Supported |Only supports login via username and key |[Perforce Webhooks](https://help.perforce.com/helix-core/helix-dam/current/Content/HelixDAM-User/using-webhooks.html) |
