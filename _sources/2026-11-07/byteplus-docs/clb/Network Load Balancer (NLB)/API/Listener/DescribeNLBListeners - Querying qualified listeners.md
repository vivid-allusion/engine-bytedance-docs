---
title: "DescribeNLBListeners - Querying qualified listeners"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeNLBListeners"
---

Call the DescribeNLBListeners API to query listeners that meet the specified conditions.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeNLBListeners&serviceCode=clb&version=2020-04-01&groupName=)

## Request parameters

When none of the optional parameters in the table below are specified, all listeners under the current account are returned.

**Action ** String必选`Example: DescribeNLBListeners`

Action to execute. Set the value to DescribeNLBListeners.

**Version ** String必选 `Example: 2020-04-01`

Current API version is 2020\-04\-01.

**LoadBalancerId ** String`optional` `Example: nlb-bp1o94dp5i6ea****`

NLB instance ID.

You can call the [DescribeNetworkLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeNetworkLoadBalancers) API to get the NLB instance ID.

**ListenerIds.N ** String`optional Example: lsn-2fek3rgsxhrsw5oxr****`

Listener ID.

* N represents the serial number of the listener, with a value range of 1 to 100.

* Separate listener IDs with ampersands (&).

**ListenerName ** String`optional` `Example: mylistener`

Listener name.

**Protocol ** String`optional` `Example: TCP`

Listener protocol. Valid values:

* TCP

* UDP

* TLS

> The TLS listener is in the invite\-only Beta stage. For trial requests, please contact the account manager.

**TagFilters.N.Key ** String`optional` `Example: k1`

The tag key.

* Parameter N represents the serial number of a tag key. Values: 1\-10.

* Separate multiple tag keys with ampersands ( & ). Multiple tag keys have a logical AND relationship. The query returns listeners tagged with all the specified keys.

**TagFilters.N.Values.N ** String`optional` `Example: v1`

The tag value.

* The first N specifies the serial number of the tag key.

* The second N specifies the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns listeners that have any of the specified tag values for that key.

* Separate multiple tag values with ampersands (&).

> **tip**

* > If this parameter is passed in, `TagFilters.N.Key` must be passed in first.

* > Passing an empty string queries for listeners with an empty tag value.

**NextToken ** String`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

Pagination token used to mark the position in paginated results. Leave this empty for the initial API call. For subsequent queries, set this value to the `NextToken` parameter returned by the previous API call.

**MaxResults ** Integer`optional` `Example: 10`

The number of rows per page for paginated queries. Valid range: 1 to 100. Default value: 10.

## Response parameters

**RequestId ** String`Example: 2024092952539010225146063030****`

Request ID.

**NextToken ** String`Example: caeba0bbb2be03f84eb48b699f0a****`

The query token returned by this API call. An empty value indicates that there is no next page.

**Listeners ** Object[]`Example: --`

Detailed information of listeners that meet the criteria.

**ListenerId ** String`Example: lsn-2fek3rgsxhrsw5oxr****`

Listener ID.

**ListenerName ** String`Example: mylistener`

Listener name.

**LoadBalancerId ** String`Example: nlb-bp1o94dp5i6ea****`

NLB instance ID.

**CreateTime ** String`Example: 2024-08-11T16:37:37Z`

Creation time of listener.

**UpdateTime ** String`Example: 2024-08-11T16:37:37Z`

Last operation time of the listener.

**Description ** String`Example: mylistener`

Description of the listener.

**Status ** String`Example: Active`

Listener status.

* Creating

* Active: Running.

* Deleting

* Disabled

**Enabled ** Boolean`Example: true`

Enable the listener.

* true: Enabled.

* false: Disable.

**Protocol ** String`Example: TCP`

Listener protocol.

* TCP

* UDP

* TLS

> The TLS listener is in the invite\-only Beta stage. For trial requests, please contact the account manager.

**CertificateSource ** String`Example: SSL`

Server certificate source.

* SSL: Certificate Center \- SSL certificate.

* PCALeaf: Certificate Center \- private CA's private certificate.

**CertificateId ** String`Example: cert-3tjuxoukkq3vj0ww****`

The default server certificate, sourced from the BytePlus Certificate Center SSL certificate.

**PCACertificateId ** String`Example: pca_leaf_3tjuxo0ww****`

The default server certificate, sourced from the private certificate of the BytePlus Certificate Center Private CA.

**CAEnabled ** Boolean`Example: true`

Whether to enable mutual authentication.

* true: Yes.

* false: No.

**CACertificateSource ** String`Example: PCARoot`

CA certificate source.

* PCARoot: Private Root CA certificate of the private CA.

* PCASub: Private sub\-CA certificate of the private CA.

**CACertificateId ** String`Example: pca_root_olkf4tgux9fj0lp***`

ID of the CA certificate.

**SecurityPolicyType ** String`Example: custom`

TLS security policy type.

* custom: Custom policy.

* system: System policy.

**SecurityPolicyId ** String`Example: tls_cipher_policy_1_0`

ID of the TLS security policy.

**Port ** Integer`Example: 80`

The port used by the listener to receive requests.

A value of 0 indicates enabling full port listening.

**StartPort ** Integer`Example: 80`

Start port for full port listening.

Only when the parameter `Port` is 0 is this parameter returned.

**EndPort ** Integer`Example: 100`

The end port for full port listening.

Only when the parameter `Port` is 0 is this parameter returned.

**ServerGroupId ** String`Example: rsp-bp1o94dp5i6ea****`

ID of the server group associated with the listener.

**ConnectionTimeout ** Integer`Example: 800`

The connection timeout period of the listener.

**Cps ** Integer`Example: 100`

New connection rate limit value.

* 0 means no rate limiting.

* The new connection rate limiting feature is currently in the invite\-only Beta stage. Contact your account manager for a trial.

**MaxConnections ** Integer`Example: 100`

Max connection rate limit value.

* 0 means no rate limiting.

* Max connections rate limit parameter is in the invite\-only Beta. To request a trial, contact your account manager.

## Request example

```json
GET /?Action=DescribeNLBListeners&Version=2020-04-01&LoadBalancerId=nlb-bp1o94dp5i6ea****&ListenerIds.1=lsn-2fek3rgsxhrsw5oxr****&ListenerName=mylistener&Protocol=TCP&TagFilters.1.Key=k1&TagFilters.1.Values.1=v1&NextToken=caeba0bbb2be03f84eb48b699f0a****&MaxResults=10 HTTP/1.1
Host: clb.cn-beijing.byteplusapi.com.cn
Date: 20260310T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{ 
    "ResponseMetadata": { 
        "RequestId": "20230604110420****100232280022D31", 
        "Action": "DescribeNLBListeners", 
        "Version": "2020-04-01", 
        "Service": "clb", 
        "Region": "cn-beijing" 
    }, 
    "Result": { 
        "Listeners": [ 
            { 
                "Cps": 100, 
                "Port": 80, 
                "Status": "Active", 
                "Enabled": true, 
                "Protocol": "TCP", 
                "CAEnabled": true, 
                "CreateTime": "2024-08-11T16:37:37Z", 
                "ListenerId": "lsn-2fek3rgsxhrsw5oxr****", 
                "UpdateTime": "2024-08-11T16:37:37Z", 
                "Description": "mylistener", 
                "ListenerName": "mylistener", 
                "CertificateId": "cert-3tjuxoukkq3vj0ww****", 
                "ServerGroupId": "rsp-bp1o94dp5i6ea****", 
                "LoadBalancerId": "nlb-bp1o94dp5i6ea****", 
                "MaxConnections": 100, 
                "CACertificateId": "pca_root_olkf4tgux9fj0lp***", 
                "PCACertificateId": "pca_leaf_3tjuxo0ww****", 
                "SecurityPolicyId": "tls_cipher_policy_1_0", 
                "CertificateSource": "SSL", 
                "ConnectionTimeout": 800, 
                "SecurityPolicyType": "custom", 
                "CACertificateSource": "PCARoot" 
            } 
        ], 
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****", 
        "RequestId": "2024092952539010225146063030****" 
    } 
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/NLB-Common-Error-Codes).

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun action. The action has been authorized but has not been executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken format is invalid. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidListenerName.Malformed |The specified ListenerName is malformed. |The specified ListenerName parameter format is invalid. |
|400 |InvalidMaxResult.Malformed |The specified MaxResult is malformed. |The specified MaxResult parameter format is invalid. |
|400 |InvalidMaxResults.Malformed |The specified MaxResults is malformed. |The specified MaxResults parameter format is invalid. |
|400 |InvalidNextToken.Malformed |The specified NextToken is malformed. |The specified NextToken parameter format is invalid. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format of specified pagination parameter is invalid. |
|400 |InvalidProtocol.Malformed |The specified Protocol is malformed. |The specified Protocol parameter format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey parameter format is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue format is invalid. |
|400 |LimitExceeded.ListenerId |You've reached the limit on the number of ListenerId that you can operate. |The maximum number of listeners that can be operated on in a single request has been reached. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |The maximum number of filter tag keys that can be specified in a single request has been reached. |
|400 |LimitExceeded.TagFilterValues |You've reached the limit on the number of tag values that you can filter. |The maximum tag key\-value pairs for filtering in a single request has been reached. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource operation conflicts. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in process. |
