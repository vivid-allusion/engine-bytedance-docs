---
title: "Sampling configuration"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Sampling_configuration_minipro"
---

In some scenarios, only part of the data is intended to be reported; this is known as sampling. This article describes how to configure sampling on the SDK and the platform.

<span id="39fc4ec1"></span>
## Sampling method


* Configure sampling on the platform (recommended): You can also specify any event and any rule, configure any sampling rate, and deliver changes dynamically without requiring a new release.

* Configure filtering in the SDK plugin: This is generally used for simple sampling requirements.

* Configure filtering in beforeSend: common sampling methods, simple to use and highly flexible.

* Configure the sample field during SDK initialization: This is commonly used for rule\-based sampling, allowing you to specify any event and any rule, and to configure any sampling rate.


<span id="143389e6"></span>
## Configure sampling on the platform

On the platform side, you can configure the sampling rate on the **Project Settings** page.

Compared to using sample to configure sampling in the SDK:


* Advantages of platform configuration:

   * No release required; changes take effect immediately upon saving and are delivered dynamically.

   * Friendlier interaction, with support for multi\-level nesting


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Interactions support multi\-level nesting; however, further multi\-level nesting of rules within rule sampling is not recommended.</div>



* Disadvantages of platform configuration

   * Because sampling relies on the mechanism by which the setting module issues requests, the setting module may occasionally fail to issue requests. As a result, sporadic reports may still occur even after configuration.


<span id="cd8fd332"></span>
### Verify configuration

You can filter the settings/minipro interface in the Network tab of Developer Tools and determine whether the platform configuration has taken effect based on the response body.

<span id="a06004e4"></span>
## Configure filtering in the SDK plugin

Some plugins provide filtering options for simple content. If content matches the filter, it will not be reported directly. For detailed plugin configuration, refer to [Plugin configuration](https://docs.byteplus.com/en/docs/apmplus/Configure_plugins).

For example, the JavaScript error plugin provides a parameter for filtering by error message. By completing the following configuration, you can prevent reporting of specified JavaScript errors that meet the defined criteria.

```TypeScript
client.init({
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

The SDK provides several lifecycle hooks, among which beforeSend is commonly used for custom sampling. Every event that needs to be reported goes through the beforeSend lifecycle hook. If the callback returns false, null, or undefined, the event will not be reported to the platform.

For example, after completing the following configuration, when the page URL contains `test`, JavaScript errors on that page will not be reported.

```TypeScript
client.on('beforeSend', (ev) => {
    if(ev.ev_type === 'js_error' && ev.common.url.includes('test')) {
      return false // No longer reports
    }
    return ev // Continue reporting
 })
```


<span id="4e69bc90"></span>
## Configure the sample field during SDK initialization.

You can pass in a sample object during init to configure sampling.

<span id="188c56f4"></span>
### Field description


|**Field** |**Type** |**DescriptionS** |
|---|---|---|
|sample_rate |number |Overall sampling rate applies to all events. |
|include_users |string[] |For users who are matched on the allowlist, all fields will be reported directly. |
|sample_granularity |string |Sampling modes.<br><br><br>* session (default): Sampling is performed at the session level.<br><br>* event: Sample at event granularity. |
|rules | |Rule\-based sampling applies special configuration for different event types, with the event type as the key.<br><br><br>* pageview<br><br>* http<br><br>* ...<br><br><br>All plugin names are event types. If you want to view all possible values for event types, refer to [configuration plugin](https://docs.byteplus.com/en/docs/apmplus/Configure_plugins). |


<span id="8c2e8bdf"></span>
#### The sample_granularity description

There are two sampling modes:


* Session: Sampling is performed at session granularity.

* event: Sample at the event granularity.


For example, the sampling rate under a certain rule is 1%.


* In session mode, if the current session falls within the 1% sampling rate, all events within the session that meet the criteria will be reported.

* In event mode, each event is recalculated to determine whether it is selected by the 1% sampling rate; if selected, the event is reported; otherwise, it is not reported.


To more accurately reconstruct all actions performed by an individual user, the SDK uses session mode by default.

<span id="bde7d744"></span>
#### Rules description

Rules are commonly used to specify a special sampling rate or special sampling based on rules for a certain event type. The parameter type of rules is in object format, where each key corresponds to a plugin name and each value corresponds to the EventSampleRule type. Please see [Configure plugins](https://docs.byteplus.com/en/docs/apmplus/Configure_plugins) for all plugin names.

The specific types of EventSampleRule are as follows:

```TypeScript
interface EventSampleRule {
  enable: boolean = true // Whether to turn on
  sample_rate: number = 1 // Sampling rate
  conditional_sample_rules?: Array<ConditionalSampleRule> // Conditional sampling rules
}

interface ConditionalSampleRule {
  sample_rate: number // Sampling rate for condition-hit events
  filter: FilterCondition // Filter criteria matched
}

interface FilterCondition {
  /** or or, and or rule */
  type: string // 'rule' | 'and' | 'or' 'rule' represents an atomic rule, while 'and' and 'or' indicate logical operations on subrules.
  field?: string // Fields for filtering and evaluation
  // op represents matching modes, including 'eq' equals | 'neq' not equal | 'gt' greater than | 'gte' greater than or equal to |
  // 'lt' less than | 'lte' less than or equal to | 'regex' matches regular expression | 'not_regex' does not match regular expression
  op?: string
  values?: Array<string> // Determine the operand; the specific type is determined based on the type of the field being checked and the operator.
  children?: Array<FilterCondition> // Subrules
}
```


You can specify the sampling rate for a single event type by configuring the sample_rate for that event, or specify the sampling rate under different rules by configuring conditional_sample_rules.

In conditional_sample_rules, type is used to specify the logical relationship—either 'and' or 'or'—between multiple children (child rules).

<span id="d75c26aa"></span>
#### Configuration example

**Scenario 1**: Overall sampling rate is 0.1, and pageview events are further sampled at a rate of 0.2.

Actual pageview sampling rate = overall sampling × single event sampling = 0.1 × 0.2 = 0.02.

```TypeScript
client.init({
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


**Scenario 2**: Simple rule sampling.

Based on scenario 1, set a condition so that only 50% of pageview events with pid equal to 'login' are sampled.

[pid='login'] actual pageview sampling rate = total sampling \* rule sampling rate = 0.05.

```TypeScript
client.init({
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
             filter: { // PV reporting when payload.pid is login
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


The value of the field is a string representing the MiniProgramSendEvent report type. In this example, payload.pid is equivalent to ev.payload.pid in beforeSend.

**Scenario 3**: Complex rule sampling.

Add another sub\-rule to the previous rule sampling. Sample pageview events at a rate of 0.5 when pid equals 'login' and the release matches the regular expression '0.1012'.

When pid equals 'login' and the release matches the regular expression '0.1012', the actual pageview sampling rate is total sampling multiplied by the rule sampling rate, which is 0.05.

```TypeScript
client.init({
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


If multiple rule sampling configurations are set, they are processed in the order of the array. If the previous rule is matched, the corresponding sampling rate is used; otherwise, the next rule in the array is checked.

From a usage perspective, although it is somewhat complex during the design phase, it is sufficiently flexible to accommodate any scenario. If you find manual configuration too complex or are unsure about configuring it correctly, you can choose to configure sampling on the platform. The platform and SDK use the same set of rules.

<span id="54f3f9a9"></span>
## Configuration priorities

If both the SDK and the platform have sampling configured, the priority order for merging configurations is as follows: SDK default configuration < platform sampling configuration < sampling configuration provided by the user during SDK initialization.

At the same time, the merge rule uses deep merging, meaning that both objects and arrays are merged.
