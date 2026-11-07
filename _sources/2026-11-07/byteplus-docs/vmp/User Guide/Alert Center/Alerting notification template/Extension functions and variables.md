---
title: "Extension functions and variables"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/variable-structure-and-parameters"
---

You can use preset alert variables in notification templates. This topic describes the structure and parameters of preset alert variables.

<span id=".5pWw5o2u57uT5p6E"></span>
## Data structure

This topic demonstrates the variables, parameters, and data structure contained in the alert information of Vital Managed Service for Prometheus (VMP) by using the following sample JSON code. This helps you understand common Go template syntax and its usage.

```json
{
        "Region": "cn-beijing",
        "AlertingRuleName": "The CPU utilization is greater than 80%",
        "AlertingRuleDescription": "Alert description",
        "AlertingRuleDetailURL": "https://console.volcanicengine.com/prometheus/***3503d49e/detail",
        "Level": "P0",
        "PromQL": "rate(cpu_total[1m])",
        "Comparator": ">",
        "Threshold": "0.8",
        "For": "3m",
        "Alerts": [
          {
                  "Id": "cdwaihonj434390ad",
                  "Labels": {
                          "cluster": "ccmp26s0bjh01jhk860f0",
                          "namespace": "default",
                          "service": "nginx",
                          "pod": "nginx-85996***"
                  },
                  "Value": "0.84",
                  "StartsAt": "2024-02-02 17:13:32.065 +0800 CST",
                  "EndsAt": "2024-02-02 17:13:32.065 +0800 CST",
                  "DetailURL": "https://console.volcanicengine.com/prometheus/***/alert/alerting?detail_id=***"
                }
        ]
}
```


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description

The following table describes the parameters and descriptions of preset variables that can be used in the notification template.


|Variable |Type |Sample Value |Description |
|---|---|---|---|
|Region |String |cn\-beijing |The region where the alert was triggered. Valid values:<br><br><br>* **cn\-beijing**: China (Beijing)<br><br>* **cn\-shanghai**: China (Shanghai)<br><br>* **cn\-guangzhou**: China (Guangzhou)<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more details, refer to <a href="https://docs.byteplus.com/en/docs/vmp/Regions-and-availability-zones">Regions and Availability Zones</a>.</div><br> |
|AlertingRuleName |String |The CPU utilization is greater than 80% |The name of the alerting rule. |
|AlertingRuleDescription |String |Alert description |The description of the alerting rule. |
|AlertingRuleDetailURL |String |https://console.volcanicengine.com/prometheus/\*\*\*3503d49e/detail |The URL of the alerting rule. This URL can redirect you to the corresponding alerting rule. |
|Level |String |P0 |The alert level. Valid values: P0, P1, and P2. |
|PromQL |String |rate(cpu_total[1m]) |The PromQL statement that is used to trigger the alert in the alerting rule. |
|Comparator |String |\> |The alert comparison condition. Valid values:<br><br><br>*  **\>** : greater than<br><br>*  **\>=** : greater than or equal to<br><br>*  **<** : less than<br><br>*  **<=** : less than or equal to<br><br>*  **==** : equal to<br><br>*  **!=** : not equal to |
|Threshold |String |0.8 |The threshold of the alert. |
|For |String |3m |The duration of the alert. |
|Alerts |Object [Alerts](https://docs.byteplus.com/en/docs/88/20187#Alerts) |\- |The details of the alert resource, which is displayed in a nested structure. |


<span id="Alerts"></span>
### Alerts


|Variable |Type |Sample Value |Description |
|---|---|---|---|
|Id |String |cdwaihonj434390ad |The alert ID. |
|Labels |map[string]string |```json```<br>```"cluster": "ccmp26s0bjh01jhk860f0",```<br>```"namespace": "default",```<br>```"service": "nginx",```<br>```"pod": "nginx-85996***"""```<br> |The details of the failed resource in the alert. |
|Value |Float64 |0.84 |The alert value.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter only applies to the <strong>alerting notification</strong> templates and does not apply to the <strong>alerting restoration notification</strong> template.</div><br> |
|StartsAt |time.Time |2024\-02\-02 17:13:32.065 +0800 CST |The start time of the alert. |
|EndsAt |time.Time |2024\-02\-02 17:13:32.065 +0800 CST |The end time of the alert.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter applies to the <strong>alerting restoration notification</strong> templates and does not apply to the <strong>alerting notification</strong> template.</div><br> |
|DetailURL |String |https://console.volcanicengine.com/prometheus/\*\*\*/alert/alerting?detail_id=\*\*\* |The URL of the alert in the console. This URL can redirect you to the corresponding alert. |


<span id=".6YWN572u56S65L6L"></span>
## Extension functions


|Function |Description | |
|---|---|---|
|vkeClusterName |Obtains a cluster name based on the `clusterID` of a Vital Kubernetes Engine (VKE) cluster. |The VKE metrics written through the collection add\-on in a VKE cluster will contain the `cluster` label, whose value is the cluster ID. You can also use the extension function to obtain a cluster name in an alerting notification. You can perform the following configuration to obtain the cluster name:<br><br><br>1. Ensure that the triggered alerts contain the `cluster` label. For example, you can use `sum(up)by(job,cluster)` to achieve aggregation by `cluster` when you configure alerts. In this case, the labels of the alerts will contain the `cluster` label.<br><br>2. When you configure an alerting notification template, use the `vkeClusterName` function to obtain the cluster name. Line 4 of the following sample code shows how to obtain the cluster name.<br><br><br>```Bash```<br>```{{ range $i, $alert := .Alerts -}}```<br>```{{ if lt $i 5 -}}```<br>```No. {{ add1 $i }} resource{{ if $alert.Annotations }}:```<br>```Cluster name: {{ $alert.Labels.cluster \| vkeClusterName }}```<br>```{{- range $key, $value := $alert.Labels }}```<br>```{{ $key }}: {{ $value }}```<br>```{{- end }}```<br>```Current value: {{ $alert.Value }}```<br>```Alert ID: {{ $alert.Id }}```<br>```Alert start time: {{ date "2006-01-02T15:04:05Z07:00" $alert.StartsAt }}```<br>``````<br>```---```<br>``````<br>```{{ else if eq $i 5 -}}```<br>```The details of only top 5 failed resources are displayed. Click [alert content details]({{ $.AlertListConsoleURL }}) to view more details.```<br>```{{- end }}```<br>```{{- end }}```<br> |
|arkEndpointName |Obtains an endpoint name based on `endpointID`. |The metrics written by ModelArk are all added with the `ark_endpoint` label, whose value is an endpoint ID. You can also use the extension function to obtain an endpoint name in an alerting notification. You can perform the following configuration to obtain the endpoint name:<br><br><br>1. Ensure that the triggered alerts contain the `ark_endpoint` label. For example, you can use `sum by(ark_endpoint,api)(rate(ark_api_proxy_request_total{}[2m]))` to achieve aggregation by `ark_endpoint` when you configure alerts. In this case, the labels of the alerts will contain the `ark_endpoint` label.<br><br>2. When you configure an alerting notification template, use the `arkEndpointName` function to obtain the endpoint name. Line 4 of the following sample code shows how to obtain the endpoint name.<br><br><br>```Bash```<br>```{{ range $i, $alert := .Alerts -}}```<br>```{{ if lt $i 5 -}}```<br>```No. {{ add1 $i }} resource{{ if $alert.Annotations }}:```<br>```Endpoint name: {{ $alert.Labels.ark_endpoint \| arkEndpointName }}```<br>```{{- range $key, $value := $alert.Labels }}```<br>```{{ $key }}: {{ $value }}```<br>```{{- end }}```<br>```Current value: {{ $alert.Value }}```<br>```Alert ID: {{ $alert.Id }}```<br>```Alert start time: {{ date "2006-01-02T15:04:05Z07:00" $alert.StartsAt }}```<br>``````<br>```---```<br>``````<br>```{{ else if eq $i 5 -}}```<br>```The details of only top 5 failed resources are displayed. Click [alert content details]({{ $.AlertListConsoleURL }}) to view more details.```<br>```{{- end }}```<br>```{{- end }}```<br> |


<span id=".6YWN572u56S65L6L"></span>
## Configuration example

In addition to the preset alerting templates of the system, you can specify custom content of a notification template based on the data structure of alert variables, Go template syntax, and Markdown syntax. The following section shows the configuration example.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The details of failed resources are obtained through the <code>.Alerts.Labels</code> variable, and the value of the <code>Labels</code> parameter may vary based on different resources. In this example, parameters that contain <code>Labels.*</code> such as <code>$alert.Labels.instance</code>) are used for illustration only. In actual configuration, you need to specify the existing <code>Labels</code> variable of resources.</div>


* <div data-tips="true" data-tips-type="warning">If your notification template includes multiple resource types, you can also choose not to specify a specific <code>Label </code>variable and instead view the details of each failed resource. For the configuration method, refer to the <a href="https://docs.byteplus.com/en/docs/vmp/lark-alerting-notifacation-template#.5qih5p2_56S65L6L6K-05piO">Template example description</a> section of the Creating a notification template topic.</div>



```markdown
**Alert information**:

---

Alert region: {{ .Region }}
Alerting rule name: {{ .AlertingRuleName }}
Alerting rule description: {{ .AlertingRuleDescription }}
Alerting rule URL: {{ .AlertingRuleDetailURL }}
Alert level: {{ .Level }}
PromQL statement of Alerting rule: {{ .PromQL }}
Alert comparison condition: {{ .Comparator }}
Alert threshold: {{ .Threshold }}
Alert duration: {{ .For }}

---
{{- $alertCount := len .Alerts }}
{{- $maxAlerts := 10 }}

**Failed resource details ({{ $alertCount }})**:
{{- range $idx, $alert := .Alerts }}
  {{- if lt $idx 10 }}
    {{- $labels := "" -}}
    <br>
Failed resource ID: {{- $alert.Id }}
Failed resource cluster: {{- $alert.Labels.cluster }}
Failed resource instance: {{- $alert.Labels.instance }}
Failed resource job: {{- $alert.Labels.job }}
Value of failed resource metric: {{- $alert.Value }}
Failure start time: {{- $alert.StartsAt }}
Alert URL: {{- $alert.DetailURL}}
  {{- end }}
{{- end }}

---

{{- if gt $alertCount $maxAlerts }}
**The number of resources has exceeded {{ $maxAlerts }}. For complete alert, go to the console**.
{{- end }}
```
