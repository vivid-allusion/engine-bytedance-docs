---
title: "CreateRules - Adding the forwarding rules to a listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-CreateRules"
---

Call the CreateRules API to add forwarding rules to a listener, forwarding access requests from different domains and URLs to different server groups.

## Instructions

* Submit up to 5 API requests per second.

* This API applies to Basic Edition ALB and Standard Edition ALB:

   * If a parameter is marked "Basic Edition", it is exclusive to Basic Edition ALB.

   * If marked "Standard Edition", it is exclusive to Standard Edition ALB.

   * If unmarked, it is common to both Basic and Standard Edition ALBs.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=CreateRules&groupName=%E8%BD%AC%E5%8F%91%E8%A7%84%E5%88%99&serviceCode=alb&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: CreateRules`

The action that you want to perform. Value: CreateRules.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**Rules.N.RuleActions.N.RewriteConfig.Host ** string[]`optional` `Example: Rules.1.RuleActions.1.RewriteConfig.Host=www.test.com`

(Standard edition) The rewritten domain name.

* The first N: Indicates the serial number of forwarding rule. Value range: 1 to 10000.

* The second N: Indicates the serial number of the forwarding action. Value range: 1\-5.

* If left blank, it defaults to being consistent with the original request's domain name.

* The specified domain name must meet the following requirements:

   * The hostname length must be between 3 and 128 characters. It can only contain lowercase letters a\-z, number, hyphen (\-), period (.), and the wildcard asterisk (\*), equal sign (=), tilde (~), underscore (_), plus sign (+), backslash (\), caret (^), exclamation mark (!), dollar sign ($), ampersand (&), vertical bar (|), parentheses (()), brackets ([]), and question mark (?).

   * A hostname must contain at least one period (.), which cannot appear at the beginning or end.

   * The rightmost domain label can only contain letters and the wildcard asterisk (\*); it cannot contain digits or hyphens (\-). The leftmost domain label is allowed to be an asterisk (\*).

   * A hyphen (\-) cannot appear at the beginning or end of any domain tag. The wildcard asterisk (\*) and the question mark (?) can appear anywhere within a domain label.

**Rules.N.RuleConditions.N.CookieConfig.Values.N.Key ** string[]`optional` `Example: Rules.1.RuleConditions.1.CookieConfig.Values.1.Key=aaa`

(Standard edition) Cookie key.

* The first N: Indicates the serial number of forwarding rule. Value range: 1 to 10000.

* The second N: Indicates the serial number of the forwarding condition. Value range: 1\-10.

* The third N: Indicates the serial number of the cookie. Value range: 1 to 10.

* The key for the cookie cannot be empty.

* Supports 1 to 100 characters.

* Supports visible characters, the wildcard asterisk (\*), and the half\-width question mark (?). If letters are used, they must be lowercase.

* Does not support spaces and `;#\[\]{}\|<>&"`.

* Cannot consist entirely of `*` and `?`.

**Rules.N.RuleActions.N.CorsConfig.AllowHeaders.N ** string[]`optional` `Example: Rules.1.RuleActions.1.CorsConfig.AllowHeaders.1=abc`

(Standard edition) Allowed headers for cross\-origin requests.

* The first N: Indicates the serial number of forwarding rule. Value range: 1 to 10000.

* The second N: Indicates the serial number of the forwarding action. Value range: 1\-5.

* The third N: Indicates the serial number of the cross\-domain header. Value range: 1 to 10.

* You can configure \* or one or more values, with multiple values separated by commas (,).

* A single value may contain only uppercase and lowercase letters, numbers, and underscores (_) or hyphens (\-) that are not at the beginning or end, with a maximum length of 32 characters.

**Rules.N.RuleActions.N.CorsConfig.AllowMethods.N ** string[]`optional` `Example: Rules.1.RuleActions.1.CorsConfig.AllowMethods.1=GET`

(Standard edition) Select the allowed HTTP method for cross\-origin access.

* The first N: Indicates the serial number of forwarding rule. Value range: 1 to 10000.

* The second N: Indicates the serial number of the forwarding action. Value range: 1\-5.

* The third N: Indicates the serial number of the HTTP method allowed for cross\-domain access. Value range: 1 to 10.

* Supports: GET, POST, PUT, DELETE, HEAD, OPTIONS, PATCH.

**Rules.N.RuleConditions.N.SourceIpConfig.Values.N ** string[]`optional` `Example: Rules.1.RuleConditions.1.SourceIpConfig.Values.1=192.168.1.0/24`

(Standard) SourceIP allowlist.

* The first N: Indicates the serial number of forwarding rule. Value range: 1 to 10000.

* The second N: Indicates the serial number of the forwarding condition. Value range: 1\-10.

* The third N: Indicates the serial number of the SourceIP. Value range: 1 to 10.

* Only supports entering IPv4 addresses/IPv4 address ranges, and the IP address must include a mask.

* Does not support address ranges of the 0.0.0.0/x type, where x is any number.

* If a forwarding condition includes SourceIP, only requests whose source matches the specified IP address or CIDR block will match this rule.

* A single rule supports a maximum of 5 values for the SourceIP condition type.

**Rules.N.RuleConditions.N.CookieConfig.Values.N.Value ** string[]`optional` `Example: Rules.1.RuleConditions.1.CookieConfig.Values.1.Value=test`

(Standard edition) Cookie value.

* The first N: Indicates the serial number of forwarding rule. Value range: 1 to 10000.

* The second N: Indicates the serial number of the forwarding condition. Value range: 1\-10.

* The third N: Indicates the serial number of the cookie. Value range: 1 to 10.

* Cookie value cannot be empty.

* Supports 1 to 100 characters.

* Supports visible characters, the wildcard asterisk (\*), and the half\-width question mark (?). If letters are used, they must be lowercase.

* Does not support spaces and `;#\[\]{}\|<>&"`.

* Cannot consist entirely of `*` and `?`.

**Rules.N.RuleActions.N.CorsConfig.AllowOrigin.N ** string[]`optional` `Example: Rules.1.RuleActions.1.CorsConfig.AllowOrigin.1=http://www.test.com`

(Standard edition) Sets the sites allowed to access server resources via browsers.

* The first N: Indicates the serial number of forwarding rule. Value range: 1 to 10000.

* The second N: Indicates the serial number of the forwarding action. Value range: 1\-5.

* The third N: Indicates the serial number of the site. Value range: 1 to 10.

* Supports configuring the wildcard "\*", and allows multiple values separated by commas, up to 32 values.

* Each value must start with http:// or https://, followed by a domain name or a single\-level wildcard domain (\*.test.abc.example.com).

* Each value supports setting a port, with a port range of 1 to 65535.

**Rules.N.RuleActions.N.CorsConfig.ExposeHeaders.N ** string[]`optional` `Example: Rules.1.RuleActions.1.CorsConfig.ExposeHeaders.1=abc`

(Standard edition) The response headers that browsers and JavaScript scripts are allowed to access.

* The first N: Indicates the serial number of forwarding rule. Value range: 1 to 10000.

* The second N: Indicates the serial number of the forwarding action. Value range: 1\-5.

* The third N: Indicates the serial number of the response header. Value range: 1 to 10.

* Can be configured with the wildcard "\*", and allows multiple values separated by commas, up to 32 values.

* Each value only allows uppercase and lowercase letters, numbers, and hyphens "\-" and underscores "_" that are not at the beginning or end, with a maximum length of 32 characters.

**Rules.N.RuleActions.N.CorsConfig.AllowCredentials ** string[]`optional` `Example: Rules.1.RuleActions.1.CorsConfig.AllowCredentials=on`

(Standard edition) Whether to allow carrying credential information.

* The first N: Indicates the serial number of forwarding rule. Value range: 1 to 10000.

* The second N: Indicates the serial number of the forwarding action. Value range: 1\-5.

* Valid values:

   * on: Yes.

   * off (default): No.

**Rules.N.RuleActions.N.CorsConfig.MaxAge** integer[] `optional` `Example: Rules.1.RuleActions.1.CorsConfig.MaxAge=600`

(Standard edition) The maximum cache time for preflight requests in the browser, in seconds.

* The first N: Indicates the serial number of forwarding rule. Value range: 1 to 10000.

* The second N: Indicates the serial number of the forwarding action. Value range: 1\-5.

* Value range: \-1 to 172800.

* \-1 and 0 indicate no caching.

**Rules.N.RuleActions.N.RedirectConfig.Query ** string[]`optional` `Example: Rules.1.RuleActions.1.RedirectConfig.Query=test`

(Standard edition) The query string to redirect to.

* The first N: Indicates the serial number of forwarding rule. Value range: 1\-10000.

* The second N: Indicates the serial number of the forwarding action. Value range: 1\-5.

* The specified query string must meet the following requirements:

   * A maximum of 128 characters is allowed.

   * Does not support spaces and (#[]{}|<\>\"). Must be lowercase letters.

* If you do not specify a query string, the redirect target will use the same query string as the original request.

**Rules.N.RuleActions.N.InsertHeaderConfig.Value ** string[]`optional` `Example: $remote_addr`

(Standard) Header field content for Write Header.

* When the content type is set to SystemDefined, the available values are as follows:

   * $remote_addr: client IP address.

   * $remote_port: client port.

   * $scheme: Protocol of the client request (HTTP or HTTPS).

   * $load_balancer_id: ALB instance ID.

   * $vport: ALB instance listening port.

   * $endpoint_id: Endpoint ID.

   > **tip**

   > $endpoint_id is in invite\-only Beta. For trial requests, please contact your account manager.

* When the content type is set to UserDefined, you can customize the header field content.

   * Length limit: 1\-128 characters.

   * Supports wildcard asterisks (\*), question marks (?), and printable ASCII characters with code values in the range `ch >= 32 && ch < 127`. The characters $ and `"` are not supported.

   * No leading or trailing spaces.

   * Cannot end with `\`.

**Rules.N.RuleActions.N.InsertHeaderConfig.ValueType ** string[]`optional` `Example: SystemDefined`

(Standard) The type of header field content for Write Header. Valid values:

* UserDefined: Custom header field content.

* SystemDefined: System defined header field content.

**Rules.N.RuleActions.N.InsertHeaderConfig.Key ** string[]`optional` `Example: remote-addr`

(Standard) Header field name for Write Header.

* Length limit: 1 to 40 characters.

* Supports uppercase and lowercase letters (a–z), numbers, underscores (_), and hyphens (\-).

* Field name must be unique.

* Regardless of case, the following header names are not supported: x\-real\-ip, x\-forwarded\-for, x\-forwarded\-proto, x\-alb\-waf\-requestid, x\-alb\-waf\-real\-port, upgrade, connection, x\-vport, x\-vip, x\-clb\-cluster, x\-toutiao\-lb\-ip, x\-vni, content\-length, transfer\-encoding, keep\-alive, host, cookie, authority.

**Rules.N.Description ** string[]`optional` `Example: --`

Description of the forwarding rule.

* Parameter \- N: Represents the serial number of the forwarding rule, ranging from 1 to 20.

* Separate multiple forwarding rules with ampersands (&).

* The detailed requirements are as follows:

   * If left blank, this parameter defaults to an empty string.

   * Cannot exceed 255 characters.

   * Must start with an English letter or a Chinese character.

   * Can only contain English letters, Chinese characters, numbers, spaces, and the following special characters`,._=-，。`.

**Rules.N.Url ** string[]`optional` `Example: /`

(Basic edition) Forwarding rule URL.

* Parameter \- N: Represents the serial number of the forwarding rule, ranging from 1 to 20.

* Only absolute paths are supported. ALB allows you to specify either an exact path or use a regular expression to define the path. Regular expression of ALB is currently in invite\-only beta. If you need a trial, please contact your account manager.

* The specified path must meet the following requirements:

   * Exact path:

      * Must start with a forward slash (/).

      * Can only contain letters, numbers, and the following special characters: `- _ / .% ?# &＝`. Consecutive forward slashes are not allowed.

      * A maximum of 128 characters is allowed.

   * Regular expression:

      * A tilde ( ~ ) must be used only once at the beginning.

      * Only English letters, numbers, and the following special characters are allowed`.- _ / ＝ ?~ ^ * $ : ( ) [ ] + |`.

      * `~` at the beginning indicates case\-sensitive matching. `~ *` at the beginning indicates case\-insensitive matching.

      * A maximum of 128 characters is allowed.

> **tip**

* > At least one of Rules.N.Domain and Rules.N.Url must be specified, and the parameter value combination of Rules.N.Domain and Rules.N.Url must be unique within the same listener.

* > If you specify the Rules.N.Domain parameter but do not specify the Rules.N.Url parameter, the Rules.N.Url parameter will use the default value / (the root directory).

* > If you do not specify Rules.N.Domain, the Rules.N.Url value cannot be set to /.

**Rules.N.RuleAction ** string[]`optional` `Example: Rules.1.RuleAction=''&Rules.2.RuleAction=Redirect`

(Basic edition) forwarding action. Valid values:

* Parameter \- N: Represents the serial number of the forwarding rule, ranging from 1 to 20.

* Null (default): Forward to. ALB forwards the request to the backend server group you specified.

* Redirect The ALB redirects the request.

**Rules.N.RewriteEnabled ** string[]`optional` `Example: on`

(Basic edition) Whether to enable "Rewrite" feature.

* Parameter \- N: Represents the serial number of the forwarding rule, ranging from 1 to 20.

* Valid values:

   * on: Enable.

   * off (default): Disable.

> **tip**

* > This parameter can be configured only when the Rules.N.RuleAction value is empty (i.e., the forwarding action is "forward to"). Otherwise, the parameter value is invalid.

* > The forwarding rule rewrite feature is in Invite\-only Beta. For trial requests, please contact your account manager.

**Rules.N.RewriteConfig.RewritePath ** string[]`optional` `Example: Rules.1.RewriteConfig.RewritePath=/{1}/${2}&Rules.2.RewriteConfig.RewritePath=/poo`

(Basic edition) Rewrite path.

* Parameter \- N: Represents the serial number of the domain, ranging from 1 to 20.

* Separate multiple domains with ampersands (&).

* The detailed requirements are as follows:

   * Must start with a forward slash "/".

   * May include letters, numbers, and symbols: '\-', '_', '/', '.', '%', '?', '#', '&', and '='.

   * Length limit is 1 to 128 characters.

   * Support regular expression substitution. The rewrite path must include one or more of the variables `${1}`, `${2}`, or `${3}`. These variables cannot be replaced with other characters.

**Rules.N.RedirectConfig.RedirectProtocol ** string[]`optional` `Example: Rules.1.RedirectConfig.RedirectProtocol=HTTP&Rules.2.RedirectConfig.RedirectProtocol=HTTPS`

(Basic edition) Protocol used for redirection.

* Parameter N: Represents the serial number of the domain, ranging from 1 to 20.

* Separate multiple domains with ampersands (&).

* Valid values:

   * HTTP

   * HTTPS (default).

* When the forwarding rule action is Redirect, the default value is HTTPS if this parameter is not specified.

**Rules.N.RedirectConfig.RedirectHttpCode ** string[]`optional` `Example: Rules.1.RedirectConfig.RedirectHttpCode=301&Rules.2.RedirectConfig.RedirectHttpCode=302`

(Basic edition) Redirect status code.

* Parameter N: Represents the serial number of the domain, ranging from 1 to 20.

* Separate multiple domains with ampersands (&).

* Valid values:

   * 301 (default)

   * 302

   * 307

   * 308

* When the forwarding action is Redirect and this parameter is not specified, the value defaults to 301.

**Rules.N.RedirectConfig.RedirectUri ** string[]`optional` `Example: Rules.1.RedirectConfig.RedirectUri=/&Rules.2.RedirectConfig.RedirectUri=/poo`

(Basic edition) Redirect URI.

* Parameter \- N: Represents the serial number of the domain, ranging from 1 to 20.

* Separate multiple domains with ampersands (&).

* The detailed requirements are as follows:

   * Must start with a forward slash “/”.

   * May include letters, numbers, and symbols: '\-', '_', '/', '.', '%', '?', '#', '&', and '='.

   * Length limit is 1 to 128 characters.

* When the forwarding rule action is Redirect, if this parameter is not specified, it defaults to an empty value, resulting in the redirect URI being the same as the request URI.

**Rules.N.TrafficLimitEnabled ** string[]`optional` `Example: on`

(Basic edition) Forwarding rule QPS rate limiting switch.

* Parameter \- N: Represents the serial number of the forwarding rule, ranging from 1 to 20.

* Valid values:

   * on: Enable.

   * off: Disable (default).

**Rules.N.TrafficLimitQPS ** integer[]`optional` `Example: 100`

(Basic edition) QPS rate limit value.

* Parameter \- N: Represents the serial number of the forwarding rule, ranging from 1 to 20.

* When Rules.N.TrafficLimitEnabled is "on", this field is required.

* Number of requests per second. Value range: 100\-100000.

**Rules.N.RedirectConfig.RedirectDomain ** string[]`optional` `Example: Rules.1.RedirectConfig.RedirectDomain=*.com&Rules.2.RedirectConfig.RedirectDomain=http://www.test.com`

(Basic edition) Redirect domain name.

* Parameter N: Represents the serial number of the domain, ranging from 1 to 20.

* Separate multiple domains with ampersands (&).

* Only exact domain names are supported.

* The detailed requirements are as follows:

   * Must contain at least one ‘.’ but must not start or end with ‘.’.

   * Only letters, numbers, '.', and '\-' are allowed.

   * Length limit is 1 to 128 characters.

   * Exact Domain Name​​: Must comply with domain name specifications (e.g., www.test.com).

* When the action of a forwarding rule is Redirect, that is, redirection, if this parameter is not specified, it will be assigned a default value (empty), and the final effect will be consistent with the requested domain name.

**Rules.N.RedirectConfig.RedirectPort ** string[]`optional` `Example: Rules.1.RedirectConfig.RedirectPort=80&Rules.2.RedirectConfig.RedirectPort=443`

(Basic edition) Redirect port.

* Parameter N: Represents the serial number of the domain, ranging from 1 to 20.

* Separate multiple domains with ampersands (&).

* Value range: 1 to 65535.

* When the forwarding rule action is Redirect, if this parameter is not specified, it defaults to an empty value, which has the same effect as using the request port.

**Rules.N.Domain ** string[]`optional` `Example: Rules.1.Domain=*.com&Rules.2.Domain=www.test.com`

(Basic edition) The domain name of the forwarding condition.

* Parameter \- N: Represents the serial number of the forwarding rule, ranging from 1 to 20.

* Basic requirements:

   * Only English letters, numbers, and the following special characters are allowed ( .\- _ \* ).

   * A domain name must contain at least one period (.), but cannot start or end with a period.

   * A maximum of 128 characters is allowed.

   * Domain names are case insensitive.

* Domain type:

   * Exact domain: Must comply with domain name specifications.

   * Wildcard domain

      * An asterisk (\*) can represent one or more characters.

      * The asterisk (\*) must be at the beginning or the end of the domain name.

      * A domain name can contain at most one asterisk (\*).

      * Characters other than a period (.) are not allowed immediately before or after the asterisk (\*).

* Domain name examples:

   * Valid domain examples: www.test.com, \*.com, www.test.\*.

   * Invalid domain examples: \*aaa.com, www.\*.com.

* Precautions:

   * One of Rules.N.Domain or Rules.N.Url must be specified. The combination of Rules.N.Domain and Rules.N.Url parameter values must be unique within the same listener.

   * If you specify the Rules.N.Url parameter without specifying Rules.N.Domain, the Rules.N.Domain parameter defaults to "\-", meaning any domain name.

**Rules.N.ForwardGroupConfig.StickySessionTimeout ** integer[]`optional` `Example: Rules.1.ForwardGroupConfig.StickySessionTimeout=5000`

(Basic edition) The timeout for session persistence between groups. Unit: seconds.

* Parameter \- N: Represents the serial number of the forwarding rule, ranging from 1 to 20.

* Value range: **1** to **86400**.

* Default: **1000**.

**Rules.N.ForwardGroupConfig.StickySessionEnabled ** string[]`optional` `Example: Rules.1.ForwardGroupConfig.StickySessionEnabled=on`

(Basic edition) Whether to enable session persistence among groups.

* Parameter \- N: Represents the serial number of the forwarding rule, ranging from 1 to 20.

* Valid values:

   * **on**: Enable.

   * **off** (default): Do not enable.

**Rules.N.ForwardGroupConfig.ServerGroupTuples.N.Weight ** integer[]`optional` `Example: Rules.1.ForwardGroupConfig.ServerGroupTuples.2.Weight=50`

(Basic edition) Weight for forwarding to the corresponding backend server group.

* Value range: 0 to 100.

* If the number of server groups is 1 and this parameter is not specified, it will default to 100.

* The first N: Represents the serial number of the forwarding rule, ranging from 1 to 20.

* The second N: Represents the serial number of the server group to forward to, ranging from 1 to 5.

**Rules.N.ForwardGroupConfig.ServerGroupTuples.N.ServerGroupId ** string[]`optional` `Example: Rules.1.ForwardGroupConfig.ServerGroupTuples.2.ServerGroupId=rsp-j7vhgiusf98adf`

(Basic edition) Forward to the backend server group ID.

* The first N: Represents the serial number of the forwarding rule, ranging from 1 to 20. When the action of a forwarding rule is empty, that is, forwarding to a server group, this parameter and `Rules.N.ServerGroupId` must be filled in one of them, and this parameter takes priority over `Rules.N.ServerGroupId`. If this parameter is not empty, `Rules.N.ServerGroupId` will be ignored.

* The second N: Represents the serial number of the server group to forward to, ranging from 1 to 5.

**Rules.N.RuleActions.N.FixedResponseConfig.Content ** string[]`optional` `Example:Rules.1.RuleActions.1.FixedResponseConfig.Content=response_ok`

(Standard edition) Forwarding Rule: Fixed content to be returned.

* The first N: Represents the serial number of the forwarding rule, ranging from 1 to 20.

* The second N: Represents the serial number of the forwarding action, ranging from 1 to 5.

* Maximum length is 1024 characters.

* Only UTF\-8 characters are supported.

**Rules.N.RuleActions.N.FixedResponseConfig.ContentType ** string[]`optional` `Example: Rules.1.RuleActions.1.FixedResponseConfig.ContentType=text/plain`

(Standard edition) Forwarding rule fixed response content format.

* The first N: Represents the serial number of the forwarding rule, ranging from 1 to 20.

* The second N: Represents the serial number of the forwarding action, ranging from 1 to 5.

* Valid values:

   * text/plain

   * text/css

   * text/html

   * application/javascript

   * application/json.

**Rules.N.RuleActions.N.FixedResponseConfig.HttpCode ** string[]`optional` `Example: Rules.1.RuleActions.1.FixedResponseConfig.HttpCode=200`

(Standard edition) HTTP response codes returned by forwarding rules.

* The first N: Indicates the serial number of forwarding rule. Value range: 1\-10000.

* The second N: Indicates the serial number of the forwarding condition. Value range: 1\-10.

* Only numeric strings of the form 2xx, 4xx, 5xx are supported, where x can be any digit.

**Rules.N.RuleConditions.N.MethodConfig.Values.N ** string[]`optional` `Example: Rules.1.RuleConditions.1.MethodConfig.Values.1=GET`

(Standard edition) Request method as a forwarding condition.

* The first N: Indicates the serial number of forwarding rule. Value range: 1\-10000.

* The second N: Indicates the serial number of the forwarding condition. Value range: 1\-10.

* The third N: Indicates the serial number of the key. Value range: 1\-10.

* Values: HEAD, GET, POST, OPTIONS, PUT, PATCH, DELETE.

**Rules.N.RuleConditions.N.QueryStringConfig.Values.N.Key ** string[]`optional` `Example: Rules.1.RuleConditions.1.QueryStringConfig.Values.1.Key=version`

(Standard edition) The query string key of the forwarding condition.

* The first N: Indicates the serial number of forwarding rule. Value range: 1\-10000.

* The second N: Indicates the serial number of the forwarding condition. Value range: 1\-10.

* The third N: Indicates the serial number of the query string key. Value range: 1\-10.

* Length must be 1 to 100 characters.

* Support visible characters, wildcard asterisk (\*), and half\-width question mark (?). If letters are used, they must be lowercase. Spaces and `#[]{}\|<>&"` are not supported.

**Rules.N.RuleConditions.N.QueryStringConfig.Values.N.Value ** string[]`optional` `Example: Rules.1.RuleConditions.1.QueryStringConfig.Values.1.Value=1.0.`

(Standard edition) The query string value of the forwarding condition.

* The first N: Indicates the serial number of forwarding rule. Value range: 1\-10000.

* The second N: Indicates the serial number of the forwarding condition. Value range: 1\-10.

* The third N: Indicates the serial number of the query string value. Value range: 1\-10.

* Length must be 1 to 128 characters.

* Supports lowercase letters, visible characters, wildcard asterisks (\*), and question marks (?). Spaces and the characters `#[]{}\|<>&"` are not supported.

**Rules.N.Priority ** integer[]`optional` `Example: Rules.1.Priority=1&Rules.2.Priority=2`

(Standard edition) Forwarding rule priority.

Parameter \- N: Represents the serial number of the forwarding rule, ranging from 1 to 20.

**Rules.N.RuleConditions.N.Type ** string[]`optional` `Example: Rules.1.RuleConditions.1.Type=Host`

(Standard edition) Type of forwarding condition.

* The first N: Indicates the serial number of forwarding rule. Value range: 1\-10000.

* The second N: Indicates the serial number of the forwarding condition. Value range: 1\-10.

* Value range of forwarding condition types:

   * Host: domain name.

   * Path

   * Header: HTTP header.

   * QueryString

   * Cookie

   * SourceIP

* Each forwarding condition can be configured individually or in combination. When multiple forwarding conditions are configured together, the relationship between them is AND.

* Multiple values can be configured under the same forwarding condition, and these values have an "OR" relationship.

**Rules.N.RuleConditions.N.HostConfig.Values.N ** string[]`optional` `Example: Rules.1.RuleConditions.1.HostConfig.Values.1=www.test.com`

(Standard edition) The domain name of the forwarding condition.

* The first N: Indicates the serial number of forwarding rule. Value range: 1\-10000.

* The second N: Indicates the serial number of the forwarding condition. Value range: 1\-10.

* The third N: Indicates the serial number of the domain name. Value range: 1\-10.

* Separate multiple domain names with ampersands (&). When you specify multiple domain names, the relationship between these domain names is OR.

* Basic requirements:

   * Only English letters, numbers, and the following special characters are allowed ( .\- _ \* ).

   * A domain name must contain at least one period (.), but cannot start or end with a period.

   * A maximum of 128 characters is allowed.

   * Domain names are case insensitive.

* Domain type:

   * Exact domain: Must comply with domain name specifications.

   * Wildcard domain:

      * An asterisk (\*) can represent one or more characters.

      * The asterisk (\*) must be at the beginning or the end of the domain name.

      * A domain name can contain at most one asterisk (\*).

      * Characters other than a period (.) are not allowed immediately before or after the asterisk (\*).

* Domain examples:

   * Valid domain examples: www.test.com,  *.com, www.test.* .

   * Invalid domain examples: *aaa.com, www.* .com.

**Rules.N.RuleConditions.N.PathConfig.Values.N ** string[]`optional` `Example: Rules.1.RuleConditions.1.PathConfig.Values.1=/foo`

(Standard edition) The path of the forwarding condition.

* The first N: Indicates the serial number of forwarding rule. Value range: 1\-10000.

* The second N: Indicates the serial number of the forwarding condition. Value range: 1\-10

* The third N: Indicates the serial number of the path. Value range: 1\-10.

* Separate multiple paths with ampersands (&). When you specify multiple paths, the relationship between these paths is OR.

* Only absolute paths are supported. The ALB allows you to specify paths using either non\-regular expressions or regular expressions. To use regular expressions for path specification, submit a ticket to request access.

* The specified path must meet the following requirements:

   * Non\-regular expressions:

      * Must start with a forward slash (/).

      * Can only contain letters, numbers, and the following special characters: \- _ / .% ?# &＝. Consecutive forward slashes are not allowed.

      * A maximum of 128 characters is allowed.

   * Regular expression:

      * A tilde ( ~ ) must be used only once at the beginning.

      * Only English letters, numbers, and the following special characters are allowed.\- _ / ＝ ?~ ^ \* $ : ( ) [ ] + |.

      * ~ at the beginning indicates case\-sensitive matching. ~\* at the beginning indicates case\-insensitive matching.

      * A maximum of 128 characters is allowed.

**Rules.N.RuleConditions.N.HeaderConfig.Key ** string[]`optional` `Example: Rules.1.RuleConditions.1.HeaderConfig.Key=test`

(Standard edition) The key of the HTTP header in the forwarding condition.

* The first N: Indicates the serial number of forwarding rule. Value range: 1\-10000.

* The second N: Indicates the serial number of the forwarding condition. Value range: 1\-10.

* The third N: Indicates the serial number of the key. Value range: 1\-10.

* Within the same forwarding rule, the key must be unique. The specified keys must meet the following requirements:

   * Can only contain letters, numbers, hyphens (\-), and underscores (_).

   * Cannot be Cookie or Host.

   * A maximum of 40 characters is allowed.

**Rules.N.RuleConditions.N.HeaderConfig.Values.N ** string[]`optional` `Example: Rules.1.RuleConditions.1.HeaderConfig.Values.1=test`

(Standard edition) The value of the HTTP header in the forwarding condition.

* The first N: Indicates the serial number of forwarding rule. Value range: 1\-10000.

* The second N: Indicates the serial number of the forwarding condition. Value range: 1\-10.

* The third N: Indicates the serial number of the HTTP header value. Value range: 1\-10.

* Each key can correspond to multiple values, and the relationship between these values is OR. The specified values must meet the following requirements:

   * Allow printable ASCII characters, asterisks (\*), and half\-width question marks (?).

   * Must not start or end with a space.

   * A maximum of 128 characters is allowed.

**Rules.N.RuleActions.N.Type ** string[]`optional` `Example: Rules.1.RuleActions.1.Type=ForwardGroup`

(Standard edition) Type of forwarding action.

* The first N: Indicates the serial number of forwarding rule. Value range: 1\-10000.

* The second N: Indicates the serial number of the forwarding action. Value range: 1\-5.

* Valid values:

   * ForwardGroup: Forward to. ALB forwards the request to the backend server group you specified.

   * Redirect: Redirect to. The ALB redirects the request.

   * Rewrite ALB rewrites the request path and requests content from the new path on the backend server.

   * TrafficLimit: Rate limiting. When the number of requests exceeds the configured QPS, ALB discards new requests.

   * FixedResponse: Return fixed content. Customize the response status code and response body.

   * Cors: Cross\-domain. Supports cross\-domain requests, i.e., when any of the protocol, domain, or port of the client request differs from the address of the page returned by the server.

   * InsertHeader: Write Header. Add a `key:value` pair to the request header, which will be sent to the backend server along with the request.

* When multiple forwarding actions are configured in combination, the relationship between them is AND.

* Rate limiting and Rewrite must be used together with either Forward to or Redirect to. Cross\-domain and Write Header must be used together with Forward to, Redirect to, or Return fixed response.

**Rules.N.RuleActions.N.ForwardGroupConfig.ServerGroupTuples.N.ServerGroupId ** string[]`optional` `Example: Rules.1.RuleActions.1.ForwardGroupConfig.ServerGroupTuples.1.ServerGroupId=sg-xxx`

(Standard edition) The ID of the backend server group to which requests are forwarded.

* The first N: Indicates the serial number of forwarding rule. Value range: 1\-10000.

* The second N: Indicates the serial number of the forwarding action. Value range: 1\-5.

* The third N: Indicates the serial number of the server group. Value range: 1\-5.

**Rules.N.RuleActions.N.ForwardGroupConfig.ServerGroupTuples.N.Weight ** integer[]`optional` `Example: Rules.1.RuleActions.1.ForwardGroupConfig.ServerGroupTuples.1.Weight=100`

(Standard edition) Weight of the backend server group.

* The first N: Indicates the serial number of forwarding rule. Value range: 1\-10000.

* The second N: Indicates the serial number of the forwarding action. Value range: 1\-5.

* The third N: Indicates the serial number of the server group. Value range: 1\-5.

* Value range: 0\-100.

* If there is only 1 server group and this parameter is not specified, it defaults to 100.

**Rules.N.RuleActions.N.ForwardGroupConfig.ServerGroupStickySession.Enabled ** string[]`optional` `Example: Rules.1.RuleActions.1.ForwardGroupConfig.ServerGroupStickySession.Enabled=on`

(Standard edition) Whether to enable session persistence among server groups.

* The first N: Indicates the serial number of forwarding rule. Value range: 1\-10000.

* The second N: Indicates the serial number of the forwarding action. Value range: 1\-5.

* Valid values:

   * on: Enable.

   * off (default): Do not enable.

**Rules.N.RuleActions.N.ForwardGroupConfig.ServerGroupStickySession.Timeout ** integer[]`optional` `Example: Rules.1.RuleActions.1.ForwardGroupConfig.ServerGroupStickySession.Timeout=1000`

(Standard edition) The timeout for session persistence between server groups. Value range: 1 to 86400. Default: 1000. Unit: seconds.

* The first N: Indicates the serial number of forwarding rule. Value range: 1\-10000.

* The second N: Indicates the serial number of the forwarding action. Value range: 1\-5.

**Rules.N.RuleActions.N.RedirectConfig.Host ** string[]`optional` `Example: Rules.1.RuleActions.1.RedirectConfig.Host=www.test.com`

(Standard edition) The domain name to redirect to.

* The first N: Indicates the serial number of forwarding rule. Value range: 1\-10000.

* The second N: Indicates the serial number of the forwarding action. Value range: 1\-5.

* The specified domain name must meet the following requirements:

   * May include English letters, numbers, half\-width periods (.), and hyphens (\-).

   * Must contain at least one half\-width period (.), but cannot begin or end with a half\-width period (.).

   * Neither the beginning nor the end of each level of a domain name can be a hyphen (\-).

   * A maximum of 128 characters is allowed.

   * Must be an exact domain name that complies with domain name specifications, e.g., www.test.com.

* If you do not specify a domain name, the redirected domain name will be the same as the request's domain name.

**Rules.N.RuleActions.N.RedirectConfig.HttpCode ** string[]`optional` `Example: Rules.1.RuleActions.1.RedirectConfig.HttpCode=302`

(Standard edition) Redirect status code.

* The first N: Indicates the serial number of forwarding rule. Value range: 1\-10000.

* The second N: Indicates the serial number of the forwarding action. Value range: 1\-5.

* Value range:

   * 301 (default)

   * 302

   * 307

   * 308

**Rules.N.RuleActions.N.RedirectConfig.Path** string[] `optional` `Example: Rules.1.RuleActions.1.RedirectConfig.Path=/test`

(Standard edition) Redirect path.

* The first N: Indicates the serial number of forwarding rule. Value range: 1\-10000.

* The second N: Indicates the serial number of the forwarding action. Value range: 1\-5.

* The path must comply with the following specifications:

   * Must start with a forward slash (/).

   * A maximum of 128 characters is allowed.

   * Only English letters, numbers, and the following special characters are allowed: \- _ / .% ?# &＝. Consecutive forward slashes are not allowed.

   * Supports exact paths and regular expressions:

   * Exact path

      * Format:

         * Must start with a forward slash (/).

         * Only letters, numbers, and the following special characters are permitted: \- _ / .% ?# \* & ＝. Consecutive forward slashes are not allowed.

         * By default, exact matching is used. The asterisk (\*) and question mark (?) can also be used as wildcards.

         * A maximum of 128 characters is allowed.

      * Examples:

         * Exact match: If the path is configured as /api/v1/users, a request to /api/v1/users will match successfully.

         * Prefix match: If the path is configured as /api/\*, requests to /api/v1/users and /api/v2 will both match successfully.

   * Regular expression

      * Format:

         * The value must start with a tilde (~), and the tilde can only appear once at the beginning.

         * Only letters, numbers, and the following special characters are allowed: .\- _ / ＝ ?~ ^ \* $ : ( ) [ ] + |.

         * ~ at the beginning indicates case\-sensitive matching. ~\* at the beginning indicates case\-insensitive matching.

         * Example: ~^/api/v[0\-9]+/users/.\*$

      * If you use parentheses ( ) in the path specified in the forwarding condition to create capture groups, you can use placeholders like ${1}, ${2}, ${3}, etc., in the path specified in the forwarding action. These placeholders correspond sequentially to the capture groups (${1} for the first group, ${2} for the second, and so on). When processing the request, ALB replaces these placeholders with the path fragments matched by the corresponding capture groups. Example: Suppose the path in the forwarding condition is /volc/(.\*)/(.\*)/aaa, and the path in the forwarding action is /${1}/${2}. If the request path is /volc/ccc/bbb/aaa, ALB will replace ${1} with ccc and ${2} with bbb. The final redirect path is /ccc/bbb.

**Rules.N.RuleActions.N.RedirectConfig.Port ** string[]`optional` `Example: Rules.1.RuleActions.1.RedirectConfig.Port=443`

(Standard edition) Redirect port.

* The first N: Indicates the serial number of forwarding rule. Value range: 1\-10000.

* The second N: Indicates the serial number of the forwarding action. Value range: 1\-5.

* Value range: 1\-65535.

* If you do not specify a port, the redirected port will be the same as the request port.

**Rules.N.RuleActions.N.RedirectConfig.Protocol ** string[]`optional` `Example: Rules.1.RuleActions.1.RedirectConfig.Protocol=HTTPS`

(Standard edition) Redirect protocol.

* The first N: Indicates the serial number of forwarding rule. Value range: 1\-10000.

* The second N: Indicates the serial number of the forwarding action, value range: 1\-5.

* Value range:

   * HTTP

   * HTTPS (default)

**Rules.N.RuleActions.N.RewriteConfig.Path ** string[]`optional` `Example: Rules.1.RuleActions.1.RewriteConfig.Path=/test`

(Standard edition) The rewritten path.

* The first N: Indicates the serial number of forwarding rule. Value range: 1 to 10000.

* The second N: Indicates the serial number of the forwarding action. Value range: 1\-5.

* The specified path must meet the following requirements:

   * The path length cannot exceed 128 characters.

   * The path must start with a forward slash (/).

   * The path can only include letters, numbers, and the following special characters: \- _ / .% ?# &＝. Consecutive forward slashes are not allowed.

   * If you use regular expressions with capturing groups enclosed in parentheses ( ) in the forwarding condition's path, you can reference the captured content in the forwarding action's path using variables like ${1}, ${2}, and ${3}. Example: Suppose the path in the forwarding condition is /volc/(. *)/(.* )/aaa, and the path in the forwarding action is /${1}/${2}. When a request path is /volc/ccc/bbb/aaa, it will be replaced with /ccc/bbb.

**Rules.N.RuleActions.N.TrafficLimitConfig.QPS ** integer[]`optional` `Example: Rules.1.RuleActions.1.TrafficLimitConfig.QPS=100`

(Standard edition) QPS rate limit value.

* The first N: Indicates the serial number of forwarding rule. Value range: 1 to 10000.

* The second N: Indicates the serial number of the forwarding action. Value range: 1\-5.

* QPS means queries per second. Value range: 100\-100000.

* "Rate limiting" must be used together with "Forward to". When configuring "Rate limiting," set it as the first forwarding action.

**ListenerId ** string必选 `Example: lsn-2fea4ayvu2g3k5oxruuz****`

Listener ID.

**Rules.N.ServerGroupId ** string[]`optional` `Example: Rules.1.ServerGroupId=rsp-bp1o94dp5i6ea****&Rules.2.ServerGroupId=rsp-2fea4bshkqv405oxruuz4****`

(Basic edition) Forward to the backend server group ID.

* Parameter \- N: Represents the serial number of the forwarding rule, ranging from 1 to 20. When the forwarding rule action is empty, it means forwarding to the server group and this parameter is required.

* Separate multiple forwarding rules with ampersands (&).

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** string`Example: 20210811152539010225146063030****`

Request ID.

**RuleIds ** string[]`Example: ["rule-****","rule- ****"]`

The ID of the forwarding rule.

## Request example

```text
GET /?Action=CreateRules&ListenerId=lsn-1g0puwcxuf****ibuxxw2pmf7&Rules.1.Domain=test.com&Rules.1.ServerGroupId=rsp-3ciynvqsspiww****rsz73tzn&Rules.1.Url=/test&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "202108131613570****5146063000AD724",
        "Action": "CreateRules",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021081316135****225146063000AD724",
        "RuleIds": [
            "rule-3ciynwk****b46c6rrt4jszkd"
        ]
    }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request does not contain the required parameter. Please ensure the request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |OperationDenied.AccountArrears |The request on the specified resource is denied due to the account being in arrears status. |The request to operate on this resource was rejected because the account is in an overdue payment state. |
|400 |OperationDenied.RewriteEnabledInRedirectAction |The request on the specified Rule is denied due to the rewrite config is not allowed to be configured in redirect action. |The request to operate on this forwarding rule was rejected because the redirect action does not support the rewrite function. |
|400 |InvalidServerGroup.InvalidStatus |The specified ServerGroup is not in the correct status for the request. |The specified server group is in a status that cannot respond to the request. |
|400 |InvalidLoadBalancer.InvalidStatus |The related LoadBalancer is not in the correct status for the request. |The associated ALB instance is in a state that cannot respond to this request. |
|400 |QuotaExceed.RulePerGroup |You've reached the limit on the number of rules per server group you can associate with, resource xxx, usage xx/xx. |The maximum number of forwarding rules that can be associated with a single server group has been reached. The resource is xxx. Used: xxx. Quota: xxx |
|400 |QuotaExceed.ServerPerInstance |You've reached the limit on the number of backend servers per ALB you can associate with, resource xxx, usage xx/xx. |You have reached the maximum of backend servers attachable per instance. The resource is xxx. Used: xxx. Quota: xxx |
|400 |QuotaExceed.RulePerInstance |You've reached the limit on the number of rules per ALB you can create in, resource xxx, usage xx/xx. |You have reached the maximum of forwarding rules that can be created per instance. The resource is xxx. Used: xxx. Quota: xxx |
|400 |InvalidRules.RewriteConfig.RewritePath.Malformed |The specified Rules.RewriteConfig.RewritePath is malformed. |The specified Rules.RewriteConfig.RewritePath format is invalid. |
|400 |InvalidRules.RewriteEnabled.Malformed |The specified Rules.RewriteEnabled is malformed. |The specified Rules.RewriteEnabled parameter format is invalid. |
|400 |InvalidRules.RuleAction.Malformed |The specified Rules.RuleAction is malformed. |The specified Rules.RuleAction parameter format is invalid. |
|400 |InvalidRules.RedirectConfig.RedirectPort.Malformed |The specified Rules.RedirectConfig.RedirectPort is malformed. |The specified Rules.RedirectConfig.RedirectPort parameter format is invalid. |
|400 |InvalidRules.RedirectConfig.RedirectUri.Malformed |The specified Rules.RedirectConfig.RedirectUri is malformed. |The specified Rules.RedirectConfig.RedirectUri parameter format is invalid. |
|400 |InvalidRules.RedirectConfig.RedirectDomain.Malformed |The specified Rules.RedirectConfig.RedirectDomain is malformed. |The specified Rules.RedirectConfig.RedirectDomain parameter format is invalid. |
|400 |InvalidRules.RedirectConfig.RedirectProtocol.Malformed |The specified Rules.RedirectConfig.RedirectProtocol is malformed. |The specified Rules.RedirectConfig.RedirectProtocol parameter format is invalid. |
|400 |InvalidRules.RedirectConfig.Malformed |The specified Rules.RedirectConfig is malformed. |The specified Rules.RedirectConfig parameter format is invalid. The redirection protocol must be consistent with the listener protocol. At least one of domain, port, or URI must be filled in. |
|400 |InvalidIndexOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |LimitExceed.Rule |You've reached the limit on the number of rules that you can operate at a time. |The maximum number of forwarding rules that can be operated in a single instance has been reached. |
|400 |InvalidRules.TrafficLimitEnabled.Malformed |The specified Rules.TrafficLimitEnabled is malformed. |The specified Rules.TrafficLimitEnabled parameter format is invalid. |
|400 |InvalidRules.TrafficLimitQPS.Malformed |The specified Rules.TrafficLimitQPS is malformed. |The specified Rules.TrafficLimitQPS parameter format is invalid. |
|400 |OperationDenied.DefaultRule |The request on the specified rule is denied due to the default rule can not be added. |The action request for this forwarding rule was denied because the default forwarding rules must not be added manually. |
|400 |InvalidRules.Domain.Malformed |The specified Rules.Domain is malformed. |The specified Rules.Domain format is invalid. |
|400 |InvalidRules.Url.Malformed |The specified Rules.Url is malformed. |The specified Rules.Url format is invalid. |
|400 |InvalidRules.Url.Duplicated |The specified Rules.Url is duplicated. |The specified Rules.Url is duplicated. |
|400 |InvalidRules.Description.Malformed |The specified Rules.Description is malformed. |The specified Rules.Description parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, 'Rules.ServerGroupId'. |This request does not contain the required parameter. Please ensure the request includes all required parameters, such as: Rules.ServerGroupId. |
|400 |InvalidVpcForServerGroup.LoadBalancerMismatch |The specified VPC of ServerGroup and LoadBalancer do not match. |The specified server group and the ALB instance do not belong to the same VPC. |
|400 |InvalidRules.RedirectConfig.RedirectHttpCode.Malformed |The specified Rules.RedirectConfig.RedirectHttpCode is malformed. |The specified Rules.RedirectConfig.RedirectHttpCode parameter format is invalid. |
|400 |LimitExceed.ServerGroupTuple |You've reached the limit on the number of server group tuples that you can associate with the rule. |You have reached the maximum of server groups can be associated with a single forwarding rule. |
|400 |InvalidRules.ForwardGroupConfig.ServerGroupTuples.ServerGroupId.Duplicated |The specified Rules.ForwardGroupConfig.ServerGroupTuples.ServerGroupId is duplicated. |The specified Rules.ForwardGroupConfig.ServerGroupTuples.ServerGroupId is duplicated. |
|400 |InvalidRules.ForwardGroupConfig.Malformed |Either ForwardGroupConfig or ServerGroupID must be specified |For a forwarding rule, at least one of ForwardGroupConfig and ServerGroupId must be specified. |
|400 |InvalidRules.ForwardGroupConfig.StickySessionTimeout.Malformed |The specified Rules.ForwardGroupConfig.StickySessionTimeout is malformed. |The specified Rules.ForwardGroupConfig.StickySessionTimeout parameter format is invalid. |
|400 |InvalidRules.ForwardGroupConfig.ServerGroupTuples.Weight.Malformed |The specified Rules.ForwardGroupConfig.ServerGroupTuples.Weight is malformed. |The specified Rules.ForwardGroupConfig.ServerGroupTuples.Weight parameter format is invalid. |
|400 |InvalidRules.ForwardGroupConfig.StickySessionEnabled.Malformed |The specified Rules.ForwardGroupConfig.StickySessionEnabled is malformed. |The specified Rules.ForwardGroupConfig.StickySessionEnabled parameter format is invalid. |
|400 |InvalidTypeOfRule.LoadBalancerEditionMismatch |The type of Rule and LoadBalancer edition do not match. |The forwarding rule type does not match the instance edition. |
|400 |InvalidRules.Priority.Malformed |The specified Rules.Priority is malformed. |The specified Rules.Priority parameter format is invalid. |
|400 |InvalidRules.Priority.Duplicated |The specified Rules.Priority is duplicated. |The specified Rules.Priority is duplicated. |
|400 |InvalidPriorityOrder.Malformed |The specified priority order is malformed. |The specified priority parameter format is invalid. |
|400 |LimitExceed.Rules.Conditions |You've reached the limit on the number of conditions you can associate with the rule. |The maximum number of forwarding conditions that can be added to a single forwarding rule has been reached. |
|400 |LimitExceed.Rules.Actions |You've reached the limit on the number of actions you can associate with the rule. |The maximum number of forwarding actions that can be added to a single forwarding rule has been reached. |
|400 |LimitExceed.Rules.Wildcard |You've reached the limit on the number of wildcard characters you can use in the rule. |The maximum number of wildcards allowed for a single forwarding rule has been reached. |
|400 |InvalidRules.RuleConditions.HeaderConfig.Key.Malformed |The specified Rules.RuleConditions.HeaderConfig.Key is malformed. |The specified Rules.RuleConditions.HeaderConfig.Key parameter format is invalid. |
|400 |InvalidRules.RuleConditions.HeaderConfig.Values.Malformed |The specified Rules.RuleConditions.HeaderConfig.Values is malformed. |The specified Rules.RuleConditions.HeaderConfig.Values parameter format is invalid. |
|400 |InvalidRules.RuleActions.Type.Malformed |The specified Rules.RuleActions.Type is malformed. |The specified Rules.RuleActions.Type parameter format is invalid. |
|400 |InvalidRules.RuleConditions.Type.Malformed |The specified Rules.RuleConditions.Type is malformed. |The specified Rules.RuleConditions.Type parameter format is invalid. |
|400 |InvalidRules.RuleActions.TrafficLimitConfig.QPS.Malformed |The specified Rules.RuleActions.TrafficLimitConfig.QPS is malformed. |The specified Rules.RuleActions.TrafficLimitConfig.QPS parameter format is invalid. |
|400 |InvalidRules.RuleConditions.HostConfig.Values.Malformed |The specified Rules.RuleConditions.HostConfig.Values is malformed. |The specified Rules.RuleConditions.HostConfig.Values parameter format is invalid. |
|400 |InvalidRules.RuleConditions.PathConfig.Values.Malformed |The specified Rules.RuleConditions.PathConfig.Values is malformed. |The specified Rules.RuleConditions.PathConfig.Values parameter format is invalid. |
|400 |InvalidRules.RuleActions.RedirectConfig.Malformed |The specified Rules.RuleActions.RedirectConfig is malformed. |The specified Rules.RuleActions.RedirectConfig parameter format is invalid. The redirect protocol must match the listener protocol. At least one of domain, port, URI, or query string must be specified. |
|400 |InvalidRules.RuleActions.RedirectConfig.Host.Malformed |The specified Rules.RuleActions.RedirectConfig.Host is malformed. |The specified Rules.RuleActions.RedirectConfig.Host parameter format is invalid. |
|400 |InvalidRules.RuleActions.RedirectConfig.Path.Malformed |The specified Rules.RuleActions.RedirectConfig.Path is malformed. |The specified Rules.RuleActions.RedirectConfig.Path parameter format is invalid. |
|400 |InvalidRules.RuleActions.RedirectConfig.Port.Malformed |The specified Rules.RuleActions.RedirectConfig.Port is malformed. |The specified Rules.RuleActions.RedirectConfig.Port parameter format is invalid. |
|400 |InvalidRules.RuleActions.RedirectConfig.HttpCode.Malformed |The specified Rules.RuleActions.RedirectConfig.HttpCode is malformed. |The specified Rules.RuleActions.RedirectConfig.HttpCode parameter format is invalid. |
|400 |InvalidRules.RuleActions.RedirectConfig.Protocol.Malformed |The specified Rules.RuleActions.RedirectConfig.Protocol is malformed. |The specified Rules.RuleActions.RedirectConfig.Protocol parameter format is invalid. |
|400 |InvalidRules.RuleActions.RewriteConfig.Path.Malformed |The specified Rules.RuleActions.RewriteConfig.Path is malformed. |The specified Rules.RuleActions.RewriteConfig.Path parameter format is invalid. |
|400 |InvalidRules.RuleActions.RewriteConfig.Malformed |The specified Rules.RuleActions.RewriteConfig is malformed.Please specify one rewrite config at least. |The specified Rules.RuleActions.RewriteConfig parameter format is invalid. Specify at least one rewrite configuration. |
|400 |InvalidRules.RuleActions.ForwardGroupConfig.ServerGroupStickySession.Timeout.Malformed |The specified Rules.RuleActions.ForwardGroupConfig.ServerGroupStickySession.Timeout is malformed. |The specified Rules.RuleActions.ForwardGroupConfig.ServerGroupStickySession.Timeout parameter format is invalid. |
|400 |InvalidRules.RuleActions.ForwardGroupConfig.ServerGroupTuples.Weight.Malformed |The specified Rules.RuleActions.ForwardGroupConfig.ServerGroupTuples.Weight is malformed. |The specified Rules.RuleActions.ForwardGroupConfig.ServerGroupTuples.Weight parameter format is invalid. |
|400 |InvalidRules.RuleActions.ForwardGroupConfig.ServerGroupStickySession.Enabled.Malformed |The specified Rules.RuleActions.ForwardGroupConfig.ServerGroupStickySession.Enabled is malformed. |The specified Rules.RuleActions.ForwardGroupConfig.ServerGroupStickySession.Enabled parameter format is invalid. |
|400 |InvalidRules.RuleActions.ForwardGroupConfig.ServerGroupTuples.ServerGroupId.Duplicated |The specified Rules.RuleActions.ForwardGroupConfig.ServerGroupTuples.ServerGroupId is duplicated. |The specified server group ID is duplicated. |
|400 |InvalidRules.RuleConditions.HostConfig.Duplicated |The specified Rules.RuleConditions.HostConfig is duplicated. |The specified Rules.RuleConditions.HostConfig is duplicated. |
|400 |InvalidRules.RuleConditions.PathConfig.Duplicated |The specified Rules.RuleConditions.PathConfig is duplicated. |The specified Rules.RuleConditions.PathConfig is duplicated. |
|400 |InvalidRules.RuleActions.RewriteConfig.Duplicated |The specified Rules.RuleActions.RewriteConfig is duplicated. |The specified Rules.RuleActions.RewriteConfig is duplicated. |
|400 |InvalidRules.RuleActions.TrafficLimitConfig.Duplicated |The specified Rules.RuleActions.TrafficLimitConfig is duplicated. |The specified Rules.RuleActions.TrafficLimitConfig is duplicated. |
|400 |InvalidRules.RuleConditions.HostConfig.Values.Duplicated |The specified Rules.RuleConditions.HostConfig.Values is duplicated. |The specified Rules.RuleConditions.HostConfig.Values is duplicated. |
|400 |InvalidRules.RuleConditions.PathConfig.Values.Duplicated |The specified Rules.RuleConditions.PathConfig.Values is duplicated. |The specified Rules.RuleConditions.PathConfig.Values are duplicated. |
|400 |InvalidRules.RuleConditions.HeaderConfig.Key.Duplicated |The specified Rules.RuleConditions.HeaderConfig.Key is duplicated. |The specified Rules.RuleConditions.HeaderConfig.Key is duplicated. |
|400 |InvalidRules.RuleConditions.HeaderConfig.Values.Duplicated |The specified Rules.RuleConditions.HeaderConfig.Values is duplicated. |The specified Rules.RuleConditions.HeaderConfig.Values is duplicated. |
|400 |OperationDenied.MissingForwardAction |The request on the specified Rule is denied due to the forward\-type action does not exist. |The action request of lacking "Forward" action was rejected due to the forwarding rule. |
|400 |OperationDenied.TrafficLimitMustUsedWithForward |The request on the specified Rule is denied due to the traffic limit rule action must used with forward rule action. |The action request that this rate\-limiting forwarding action must be used together with the "Forward to" action was rejected due to the forwarding rule. |
|400 |OperationDenied.MultipleForwardActions |The request on the specified Rule is denied due to multiple forward actions. |The request to operate on this forwarding rule was rejected because a single forwarding rule contains multiple forwarding\-type actions. |
|400 |InvalidPriority.RuleActionMismatch |The specified priority and action of rule do not match.The traffic\-limit\-type rule action must have the first priority. |The specified forwarding action and priority do not match. The "rate\-limiting" forwarding action must be placed first. |
|400 |InvalidRules.RuleActions.RewriteConfig.Host.Malformed |The specified Rules.RuleActions.RewriteConfig.Host is malformed. |The specified Rules.RuleActions.RewriteConfig.Host parameter format is invalid. |
|400 |InvalidRules.RuleConditions.CookieConfig.Values.Duplicated |The specified Rules.RuleConditions.CookieConfig.Values is duplicated. |The specified Rules.RuleConditions.CookieConfig.Values is duplicated. |
|400 |InvalidRules.RuleConditions.SourceIpConfig.Duplicated |The specified Rules.RuleConditions.SourceIpConfig is duplicated. |The specified Rules.RuleConditions.SourceIpConfig is duplicated. |
|400 |InvalidRules.RuleConditions.SourceIpConfig.Values.Malformed |The specified Rules.RuleConditions.SourceIpConfig.Values is malformed. |The specified Rules.RuleConditions.SourceIpConfig.Values parameter format is invalid. |
|400 |InvalidRules.RuleActions.CorsConfig.AllowOrigin.Malformed |The specified Rules.RuleActions.CorsConfig.AllowOrigin is malformed. |The specified Rules.RuleActions.CorsConfig.AllowOrigin parameter format is invalid. |
|400 |InvalidRules.RuleActions.CorsConfig.AllowMethods.Malformed |The specified Rules.RuleActions.CorsConfig.AllowMethods is malformed. |The specified Rules.RuleActions.CorsConfig.AllowMethods parameter format is invalid. |
|400 |InvalidRules.RuleActions.CorsConfig.AllowHeaders.Malformed |The specified Rules.RuleActions.CorsConfig.AllowHeaders is malformed. |The specified Rules.RuleActions.CorsConfig.AllowHeaders parameter format is invalid. |
|400 |InvalidRules.RuleActions.CorsConfig.ExposeHeaders.Malformed |The specified Rules.RuleActions.CorsConfig.ExposeHeaders is malformed. |The specified Rules.RuleActions.CorsConfig.ExposeHeaders parameter format is invalid. |
|400 |InvalidRules.RuleActions.CorsConfig.AllowCredentials.Malformed |The specified Rules.RuleActions.CorsConfig.AllowCredentials is malformed. |The specified Rules.RuleActions.CorsConfig.AllowCredentials parameter format is invalid. |
|400 |InvalidRules.RuleActions.CorsConfig.MaxAge.Malformed |The specified Rules.RuleActions.CorsConfig.MaxAge is malformed. |The specified Rules.RuleActions.CorsConfig.MaxAge parameter format is invalid. |
|400 |InvalidRules.RuleConditions.CookieConfig.Values.Key.Malformed |The specified Rules.RuleConditions.CookieConfig.Values.Key is malformed. |The specified Rules.RuleConditions.CookieConfig.Values.Key parameter format is invalid. |
|400 |InvalidRules.RuleConditions.CookieConfig.Values.Value.Malformed |The specified Rules.RuleConditions.CookieConfig.Values.Value is malformed. |The specified Rules.RuleConditions.CookieConfig.Values.Value parameter format is invalid. |
|400 |InvalidRules.RuleConditions.SourceIpConfig.Values.Duplicated |The specified Rules.RuleConditions.SourceIpConfig.Values is duplicated. |The specified Rules.RuleConditions.SourceIpConfig.Values is duplicated. |
|400 |InvalidRules.RuleActions.RedirectConfig.Query.Malformed |The specified Rules.RuleActions.RedirectConfig.Query is malformed. |The specified Rules.RuleActions.RedirectConfig.Query parameter format is invalid. |
|400 |QuotaExceed.RulePerInstanceForStandard |You've reached the limit on the number of rules per ALB standard edition you can create in, resource xxx, usage xx/xx. |The maximum number of forwarding rules per Standard Edition instance has been reached. The resource is xxx. Used: xxx. Quota: xxx |
|400 |OperationDenied.ServerGroupTypeMountUnSupported |The request on the specified ServerGroup is denied due to ServerGroup Type does not support. |The operation request for this server group has been rejected because the server group type is not supported. |
|400 |OperationDenied.ServerGroupServiceTypeMountUnSupported |The request on the specified ServerGroup is denied due to ServerGroup ServiceType does not support. |The operation request for this server group has been rejected because the server group service type is not supported. |
|400 |InvalidInsertHeaderSystemDefinedValue.Malformed |Invalid system defined value |Invalid system predefined value |
|400 |InsertHeaderReservedKey.Malformed |Invalid system defined value |Invalid system predefined value |
|400 |InsertHeaderDuplicateKey.Duplicated |Rules.RuleActions.InsertHeaderConfig.Key is duplicated |The specified Rules.RuleActions.InsertHeaderConfig.Key is duplicated |
|400 |OperationDenied.ExtensionLoadBalancerRuleActionInsertHeaderUnSupport |The request on the specified LoadBalancerRule is denied due to Extension LoadBalancer Rule does not support InsertHeader Action. |The operation request for this forwarding rule of the ALB instance with extended capabilities enabled has been rejected because the InsertHeader action is not supported. |
|400 |InvalidRules.RuleActions.InsertHeaderConfig.Key.Duplicated |The specified Rules.RuleActions.InsertHeaderConfig.Key is duplicated. |The specified Rules.RuleActions.InsertHeaderConfig.Key is duplicated. |
|400 |InvalidRules.RuleActions.InsertHeaderConfig.ValueType.Malformed |The specified Rules.RuleActions.InsertHeaderConfig.ValueType is malformed. |The specified Rules.RuleActions.InsertHeaderConfig.ValueType parameter format is invalid. |
|400 |InvalidRules.RuleActions.FixedResponseConfig.ContentType.Malformed |The specified Rules.RuleActions.FixedResponseConfig.ContentType is malformed. |The specified Rules.RuleActions.FixedResponseConfig.ContentType parameter format is invalid. |
|400 |InvalidRules.RuleActions.InsertHeaderConfig.Key.Malformed |The specified Rules.RuleActions.InsertHeaderConfig.Key is malformed. Key uses reserved name. |The specified Rules.RuleActions.InsertHeaderConfig.Key parameter format is invalid. The key uses a reserved name. |
|400 |InvalidRules.RuleActions.InsertHeaderConfig.Key.Malformed |The specified Rules.RuleActions.InsertHeaderConfig.Key is malformed. |The specified Rules.RuleActions.InsertHeaderConfig.Key parameter format is invalid. |
|400 |InvalidRules.RuleActions.InsertHeaderConfig.Value.Malformed |The specified Rules.RuleActions.InsertHeaderConfig.Value is malformed. Invalid system defined value. |The specified Rules.RuleActions.InsertHeaderConfig.Value parameter format is invalid. Invalid system predefined value. |
|400 |InvalidRules.RuleActions.InsertHeaderConfig.Value.Malformed |The specified Rules.RuleActions.InsertHeaderConfig.Value is malformed. |The specified Rules.RuleActions.InsertHeaderConfig.Value parameter format is invalid. |
|403 |Forbidden |You are not authorized to configure rewrite for rule. |You do not have permission to configure rewrites for the specified forwarding rule. |
|403 |Forbidden |You are not authorized to configure rewrite host for rules. |You do not have permission to configure domain rewriting for the specified forwarding rule. |
|403 |Forbidden |You are not authorized to create rules with CookieConfig condition. |You do not have permission to create forwarding rules where the forwarding condition is the Cookie. |
|403 |Forbidden |You are not authorized to create rules with SourceIpConfig condition. |You do not have permission to create forwarding rules where the forwarding condition is the source address. |
|403 |Forbidden |You are not authorized to configure cors for rule. |You do not have permission to configure cross\-origin for the specified forwarding rule. |
|403 |Forbidden |You are not authorized to configure redirect query for rule. |You do not have permission to configure the redirect query string for the specified forwarding rule. |
|403 |Forbidden |You are not authorized to use endpoint_id system defined header. |You do not have permission to use the endpoint_id system predefined header. |
|403 |Forbidden |You are not authorized to configure insert\-header for rule. |You do not have permission to configure Insert Header for the specified forwarding rule. |
|404 |InvalidListener.NotFound |The specified Listener does not exist. |The specified listener does not exist. |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup does not exist. |The specified server group does not exist. |
|409 |InvalidRules.Conflict |The specified Rule already exists. |The specified forwarding rule already exists. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
