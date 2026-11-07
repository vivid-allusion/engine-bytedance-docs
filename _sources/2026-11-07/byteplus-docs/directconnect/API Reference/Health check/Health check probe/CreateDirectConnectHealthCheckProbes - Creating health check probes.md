---
title: "CreateDirectConnectHealthCheckProbes - Creating health check probes"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectHealthCheckProbes"
---

Call the CreateDirectConnectHealthCheckProbes API to create a health check probe.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDirectConnectHealthCheckProbes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|eMCUXq">必选</span> `Example: CreateDirectConnectHealthCheckProbes`

The interface name. The current API name is `CreateDirectConnectHealthCheckProbes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|WSKUxm">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectHealthCheckId ** <span data-label="purple">String </span><span data-api-tag="require|dHfivS">必选</span> `Example: dhc-2752hz4tek****`

The ID of the health check instance.

You can call [DescribeDirectConnectHealthChecks](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectHealthChecks) to query the health check instance ID.



**Region ** <span data-label="purple">String </span><span data-api-tag="require|fiBMit">必选</span> `Example: ap-southeast-1`

The region where the probe is located. Must be the same as the region of the health check instance.



**DirectConnectHealthCheckProbes.N.DirectConnectHealthCheckProbeName ** <span data-label="purple">String </span>`optional` `Example: CheckProbes-01`

The name of the health check probe.


* N represents the sequence number of a probe. You can call a maximum of 10 in a single request.

* Separate multiple names with ampersands (&).

* Must be 1 to 128 characters.

* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-). Cannot start with http:// or https://.

* If you do not pass in this parameter or leave it empty, it defaults to the health check probe ID.



**DirectConnectHealthCheckProbes.N.Description ** <span data-label="purple">String </span>`optional` `Example: This is a checkprobes`

The description of the health check probe.


* N represents the sequence number of a probe. You can call a maximum of 50 in a single request.

* Separate multiple descriptions with ampersands (&).

* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), English commas (,), Chinese commas (，), and Chinese periods (。). Cannot start with http:// or https://.

* Must be 1 to 255 characters.

* If you omit this parameter or set it to an empty value, it defaults to an empty string.



**DirectConnectHealthCheckProbes.N.ProbeTargetIp ** <span data-label="purple">String </span><span data-api-tag="require|ef0yb6">必选</span> `Example: 10.XX.XX.4`

Specify a target IP address for the health check. Currently, only IPv4 addresses are supported.


* N represents the sequence number of a probe. You can call a maximum of 10 in a single request.

* Separate multiple addresses with ampersands (&).



**DirectConnectHealthCheckProbes.N.ProbeInterval ** <span data-label="purple">Integer </span>`optional` `Example: 2`

Specify the interval between consecutive health check packets. Unit: seconds. Default: 2. Values: 2–3.


* N represents the sequence number of a probe. You can call a maximum of 10 in a single request.

* Separate multiple packets with ampersands (&).



**DirectConnectHealthCheckProbes.N.ProbeThreshold ** <span data-label="purple">Integer </span>`optional` `Example: 8`

Specify the number of health check packets to send. Valid values: 3–8. Default: 8.


* N represents the sequence number of a probe. You can call a maximum of 10 in a single request.

* Separate multiple packets with ampersands (&).



**DirectConnectHealthCheckProbes.N.ProbePacketProtocol ** <span data-label="purple">String </span>`optional` `Example: ICMP`

Specify a protocol for the health check packet. Default: ICMP.


* N represents the sequence number of a probe. You can call a maximum of 10 in a single request.

* Separate multiple packets with ampersands (&).



**DirectConnectHealthCheckProbes.N.ProbePort ** <span data-label="purple">Integer </span>`optional` `Example: 88`

Specify a port for the health check packet. Value range: 1\-65535.


* N represents the sequence number of a probe. You can call a maximum of 10 in a single request.

* Separate multiple ports with ampersands (&).



**DirectConnectHealthCheckProbes.N.ProbePacketSize ** <span data-label="purple">Integer </span>`optional` `Example: 56`

Specify a size for the health check packet. Unit: Byte. Value range: 56–8500.


* N represents the sequence number of a probe. You can call a maximum of 10 in a single request.

* Separate multiple packets with ampersands (&).



**ClientToken ** <span data-label="purple">String </span>`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.


* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**DirectConnectHealthCheckProbeIds ** <span data-label="purple">String[] </span>`Example: [dhp-2752hz4****]`

The ID of the health check probe.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=CreateDirectConnectHealthCheckProbes&Version=2020-04-01&DirectConnectHealthCheckId=dhc-2752hz4tek****&Region=ap-southeast-1&DirectConnectHealthCheckProbes.1.DirectConnectHealthCheckProbeName=CheckProbes-01&DirectConnectHealthCheckProbes.1.Description=This is a checkprobes&DirectConnectHealthCheckProbes.1.ProbeTargetIp=10.XX.XX.4&DirectConnectHealthCheckProbes.1.ProbeInterval=2&DirectConnectHealthCheckProbes.1.ProbeThreshold=8&DirectConnectHealthCheckProbes.1.ProbePacketProtocol=ICMP&DirectConnectHealthCheckProbes.1.ProbePort=88&DirectConnectHealthCheckProbes.1.ProbePacketSize=56&ClientToken=123e4567-e89b-12d3-a456-42665544**** HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "CreateDirectConnectHealthCheckProbes",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "ap-southeast-1"
    },
    "Result":{
         "RequestId": "2021062415303301022514515207C4****",
         "DirectConnectHealthCheckProbeIds": {
               [
                  "dhp-2752hz4****"
                ]
     }
     }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDirectConnectHealthCheck.ClusterUnavailable |No available health check cluster. |No available health check clusters exist. |
|400 |InvalidDirectConnectHealthCheck.InvalidStatus |The specified direct connect health check is not in the correct status for the request. |The specified health check cannot respond to this request due to its status. |
|400 |InvalidDirectConnectHealthCheckProbe.CountExceeded |The specified direct connect health check probe count is invalid. |The specified number of health check probes exceeds the limit. Request in batches, with no more than 10 probes per batch. |
|400 |InvalidDirectConnectHealthCheckProbe.Duplicated |The specified direct connect health check probe is duplicated. |The specified health check probe is duplicated. |
|400 |InvalidDirectConnectHealthCheckProbe.InvalidProbe |The specified direct connect health check probe is invalid. |The specified health check probe is invalid. |
|400 |InvalidDirectConnectHealthCheckProbe.InvalidTargetIP |The specified direct connect health check probe target IP is invalid. |The specified target IP of health check probe is invalid. |
|400 |InvalidDirectConnectHealthCheckProbe.ProbeIntervalInvalid |The specified direct connect health check probe interval is invalid. |The specified detection interval of health check probe is invalid. |
|400 |InvalidDirectConnectHealthCheckProbe.ProbePacketProtocolInvalid |The specified direct connect health check probe packet protocol is invalid. |The specified health check probe packet protocol is invalid. |
|400 |InvalidDirectConnectHealthCheckProbe.ProbePacketSizeInvalid |The specified direct connect health check probe packet size is invalid. |The specified packet size of health check probe is invalid. |
|400 |InvalidDirectConnectHealthCheckProbe.ProbePortInvalid |The specified direct connect health check probe port is invalid. |The specified detection port of health check probe is invalid. |
|400 |InvalidDirectConnectHealthCheckProbe.ProbeThresholdInvalid |The specified direct connect health check probe threshold is invalid. |The specified detection threshold of health check probe is invalid. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |QuotaExceeded.DirectConnectHealthCheckProbe |You've reached the limit on the number of probes per direct connect health check that you can create. |The maximum probes that you can create in a single health check have been reached. |
|404 |InvalidDirectConnectHealthCheck.NotFound |The specified direct connect health check does not exist. |The specified health check does not exist. |
|404 |InvalidDirectConnectHealthCheckCluster.NotFound |The specified direct connect direct connect health check cluster does not exist. |The specified health check cluster does not exist. |
