---
title: "Modifying/Verifying a private DNS name"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Modifying-Verifying-private-DNS-names"
---

After enabling the Private DNS Name for your endpoint service, you must complete verification before you can enable the DNS name for your endpoint.​​ If verification fails, it may be due to an incorrect DNS name configuration. Please modify the settings and retry the verification.​​

## Modify Private DNS name

> **tip**

* > When there is an endpoint associated with the endpoint service whose connection status is **Connected**, modifying the private DNS name is not supported.

* > When all connection statuses of the endpoints associated with the endpoint service are **Pendingacceptance** or **Reject Connection**, the private DNS name can be modified. If you modify the Private DNS Name after accepting endpoint connections, the connections may fail. Please proceed with caution.​​

1. Use the service provider's account to log in to the [Endpoint Service console](https://console.byteplus.com/pl/endpointServices).

2. In the top menu bar, select the target project and region.

3. Click the service ID of target endpoint service.

4. In the **Private DNS name information** zone, click **Modify** after the enable status, and reselect the enable status.

   > **tip**

   > When changing from **Disable** to **Enable**, you must also enter the private DNS name. For the **Private DNS Name**, please enter an internet domain name.​​ If the entered public domain name is a wildcard domain, such as `*.pl.example.com`, it indicates that both the wildcard domain and its root domain, `pl.example.com`, support resolution.

5. Click **Save** to complete the modification.

## Verify private DNS name

### Prerequisites

Please ensure that the private DNS name to be verified has been configured with a TXT resolution record, and that this TXT record can be resolved by the public DNS.

For example: if the private DNS name is `service.example.com` or `*.service.example.com`, configure the TXT record parameters as follows:

|Parameters |Description |Example |
|---|---|---|
|Domain name |The domain name is formed by concatenating the domain verification name of the private DNS and the private DNS name, or the domain verification name and the root domain name of the private DNS name. The specific concatenation format is as follows:<br><br><br>* Domain authentication name.private DNS name<br><br>* Domain authentication name.root domain of the private DNS name |__imo4ypmcr94w8gbssz58f1il.service.example.com or<br><br>_imo4ypmcr94w8gbssz58f1il.example.com |
|Record type |Select **TXT**. |TXT |
|Record value |Enter the **domain verification value** of the private DNS name. |epsvc:imo4yrldvb408gbssz2858rj |

### Action notes

You can initiate verification when the verification status is **Pending verification** or **Verification failed**. When the status is **Verifying** or **Verified**, initiating verification again is not supported.

### Procedures

1. Use the service provider's account to log in to the [Endpoint Service console](https://console.byteplus.com/pl/endpointServices).

2. In the top menu bar, select the target project and region.

3. Click the Service ID of target endpoint service.

4. In the **Private DNS name information** zone, click **Initiate verification** after the verification status, and confirm resource information.

5. Check **I confirm that the TXT record for the domain has been configured and I am ready to validate private DNS ownership**.

6. Click **Confirm** to complete the action.

   After verification, check the verification status to confirm it is successful.​​ If the status shows failure, please check if the Private DNS Name is correct.​​

## Related documents

[ModifyVpcEndpointServiceAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointServiceAttributes)
