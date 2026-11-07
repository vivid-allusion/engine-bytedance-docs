---
title: "Sampling configuration"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Sampling_configuration"
---

In some scenarios, only a portion of the data is reported; this is referred to as sampling. This article introduces how to configure sampling in the SDK and platform.

<span id="39fc4ec1"></span>
## Sampling method


* [Configure filtering in the SDK plugin](https://docs.byteplus.com/en/docs/apmplus/Sampling_configuration#a06004e4)

   Generally used for simple sampling requirements.

* [Filter in beforeSend](https://docs.byteplus.com/en/docs/apmplus/Sampling_configuration#6bd67456)

   Common sampling methods are easy to use and highly flexible.

* [Configure the sample field during SDK initialization.](https://docs.byteplus.com/en/docs/apmplus/Sampling_configuration#4e69bc90)

   Commonly used for rule\-based sampling, allowing specification of any event and any rule, and configuration of any sampling rate.

* [Configure sampling on the platform](https://docs.byteplus.com/en/docs/apmplus/Sampling_configuration#54f3f9a9)

   You can also specify any event and any rule, configure any sampling rate, and deliver configurations dynamically without requiring a release.


<span id="a06004e4"></span>
## Configure filtering in the SDK plugin

Some plugins provide filtering options that can filter simple content. If the filter is triggered, the content is not reported directly. For detailed plugin configuration, refer to [Plugin configuration](https://docs.byteplus.com/en/docs/apmplus/Plugin_configuration).

For example, the JavaScript error plugin provides a parameter for filtering based on error message. After completing the following configuration, specified JavaScript errors that meet certain conditions will not be reported.

```TypeScript
import browserClient  from '@apmplus/web'

browserClient('init', {
  ...
  plugins: {
    jsError: {
      ignoreErrors: ['Failed to fetch']
    }
  },
  ...
})
```


<span id="6bd67456"></span>
## Filter in beforeSend

The SDK provides multiple lifecycles, among which the beforeSend lifecycle is commonly used for custom sampling. Every event that needs to be reported goes through the beforeSend lifecycle. If you return false, null, or undefined in the callback, the event will not be reported to the platform.

For example, after completing the following configuration, if the page address contains `test`, JavaScript errors that occur on that page will not be reported.

```TypeScript
 import browserClient  from '@apmplus/web'
 
 browserClient('on', 'beforeSend', (ev) => {
    if(ev.ev_type === 'js_error' && ev.common.url.includes('test')) {
      return false // Reporting discontinued
    }
    return ev // Continue reporting
 })
```


The specific type of ev can be found not only by viewing TypeScript type hints, but also by checking the BrowserSendEvent type exported by @apmplus/web.

<span id="4e69bc90"></span>
## Configure the sample field during SDK initialization.

You can pass in a sample object during init to configure sampling.

<span id="188c56f4"></span>
### Field descriptions


|**Field** |**Type** |**DescriptionS** |
|---|---|---|
|sample_rate |number |The overall sampling rate applies to all events. |
|include_users |string[] |For users who match the allowlist, all fields will be reported directly. |
|sample_granularity |string |Sampling modes.<br><br><br>* session (default): Sampling is performed at the session level.<br><br>* event: Sample at event granularity. |
|rules | |Rule\-based sampling: special configurations for different event types, with the key being the event type.<br><br><br>* pageview<br><br>* http<br><br>* resource<br><br>* ...<br><br><br>All plugin names are event types. To view all possible event type values, refer to [configuration plugins](https://docs.byteplus.com/en/docs/apmplus/Plugin_configuration). |


<span id="8c2e8bdf"></span>
#### sample_granularity description

There are two modes for sampling:


* session: Sampling is performed at session granularity.

* event: Sample at event granularity.


For example, the sampling rate under a certain rule is 1%.


* In session mode, if the current session is selected by the 1% sampling rate, all events within that session that meet the criteria will be reported.

* In event mode, each event recalculates whether it meets the 1% sampling rate. Events that meet the sampling rate are reported, while those that do not are not reported.


To better restore all actions performed by an individual user, the SDK uses session mode by default.

<span id="bde7d744"></span>
#### Description of rules

Rules are commonly used to specify a special sampling rate or special rule\-based sampling for a particular event type. The parameter type of rules is an object, where each key corresponds to a plugin name and each value corresponds to the EventSampleRule type. All plugin names can be found in [Configure plugins](https://docs.byteplus.com/en/docs/apmplus/Plugin_configuration).

The specific types of EventSampleRule are as follows:

```TypeScript
interface EventSampleRule {
  enable: boolean = true // Whether to turn on
  sample_rate: number = 1 // Sampling rate
  conditional_sample_rules?: Array<ConditionalSampleRule> // Conditional sampling rules
}

interface ConditionalSampleRule {
  sample_rate: number // Sampling rate for hit condition events
  filter: FilterCondition // Match filter criteria
}

interface FilterCondition {
  /** or, or and, or rule */
  type: string // 'rule' | 'and' | 'or': 'rule' represents an atomic rule, and 'and' and 'or' indicate logical operations on subrules.
  field?: string // Fields used for filtering and evaluation
  // op represents the matching mode, including 'eq' for equal to | 'neq' for not equal to | 'gt' for greater than | 'gte' for greater than or equal to |
  // 'lt' less than | 'lte' less than or equal to | 'regex' matches regular expression | 'not_regex' does not match regular expression
  op?: string
  values?: Array<string> // Determine the operand; the specific type is determined by the type of the field being judged and the operator.
  children?: Array<FilterCondition> // Subrules
}
```


You can specify the sampling rate for a single event type by configuring the sample_rate for that event, or specify different sampling rates for different rules by configuring conditional_sample_rules.

In conditional_sample_rules, type is used to specify the logical relationship (AND or OR) between multiple child rules (children). For the specific design, refer to [Example description](https://docs.byteplus.com/en/docs/apmplus/Sampling_configuration#d75c26aa).

<span id="d75c26aa"></span>
#### Configuration example

**Scenario 1**: Overall sampling rate is 0.1; pageview events are further sampled at a rate of 0.2.

Actual pageview sampling rate = overall sampling \* single event sampling = 0.1 \* 0.2 = 0.02.

```TypeScript
browserClient('init', {
  ...
  sample: {
    sample_rate: 0.1,
    include_users: [''],
    sample_granularity: 'session',
    rules: {
      pageview: {
        enable: true,
        sample_rate: 0.2,
        conditional_sample_rules: [],
      }
    },
  }
  ...
})
```


**Scenario 2**: A simple rule sampling.

Based on scenario one, add a condition to set the sampling rate to 0.5 for pageview events where pid equals 'login'.

[pid='login'] actual pageview sampling rate = overall sampling rate × rule sampling rate = 0.05.

```TypeScript
browserClient('init', {
  ...
  sample: {
    sample_rate: 0.1,
    include_users: [''],
    sample_granularity: 'session',
    rules: {
      pageview: {
        enable: true,
        sample_rate: 0.2,
        conditional_sample_rules: [
           {
             sample_rate: 0.5, 
             filter: { // PV reporting for the condition where payload.pid is login
               type: 'rule',
               field: 'payload.pid',
               op: '=',
               values: ['login'],
             },
           },
        ],
      }
    },
  }
  ...
})
```


The value of field is the string representation of the BrowserSendEvent reporting type. In this example, payload.pid is equivalent to ev.payload.pid in beforeSend.

**Scenario 3**: Complex rule sampling.

Add another sub\-rule to the previous rule sampling. Sample pageview events at a rate of 0.5 when pid equals 'login' and the release matches the regular expression '0.1012'.

The actual sampling rate for pageview when pid equals 'login' and release matches the regular expression '0.1012' is calculated as total sampling multiplied by rule sampling rate, which equals 0.05.

```TypeScript
browserClient('init', {
  ...
  sample: {
    sample_rate: 0.1,
    include_users: [''],
    sample_granularity: 'session',
    rules: {
      pageview: {
        enable: true,
        sample_rate: 0.2,
        conditional_sample_rules: [
          {
            sample_rate: 0.5, 
             filter: {
               type: 'and',
               children: [
                 {
                  type: 'rule',
                  field: 'payload.pid',
                  op: '=',
                  values: ['login'],
                 }, {
                   type: 'rule',
                   field: 'common.release',
                   op: 'regex',
                   values: ['0.1012'],
                 }
              ]
             },
          },
        ],
      }
    },
  }
  ...
})
```


If multiple sampling rules are configured, they are evaluated one by one in array order. When a rule matches, its corresponding sampling rate is used; if not, the next rule is evaluated, and this process continues until a rule is matched.

From a usage perspective, although the design process is somewhat complex, it is sufficiently flexible to meet the requirements of any scenario. If you find manual configuration too complex or are not confident about configuring it correctly, you can directly configure sampling on the platform. The platform and the SDK use the same set of rules.

<span id="54f3f9a9"></span>
## Configure sampling on the platform

On the platform side, you can configure the sampling rate on the **project setting** page.

Compared to using sample in the SDK for sampling configuration:


* Advantages of platform configuration:

   * No release required; changes take effect upon saving and are delivered dynamically.

   * More user\-friendly interaction, while also supporting multi\-level nesting

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Multi\-level nesting is supported in interactions; however, multi\-level rule nesting within rule sampling is not recommended.      </div>
      

* Drawbacks of the platform configuration

   * Because the sampling mechanism relies on the issuing of settings, there may be occasional request failures, which can result in sporadic reports still occurring even after configuration.


<span id="a6443b2f"></span>
### Verify configuration

You can filter for the settings/get/webpro API in the Network panel and determine from the response body whether the platform's configuration has taken effect.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/694670ce22044a7cb08cbf2cce679510~tplv-goo7wpa0wc-image.image) </span>

<span id="d722fc16"></span>
## Configuration priorities

If both the SDK and the platform have sampling configured, the priority order for merging configurations is as follows: SDK default configuration < platform sampling configuration < sampling configuration provided by the user during SDK initialization.

The merging rule is deep merge, meaning that objects and arrays are merged simultaneously.
