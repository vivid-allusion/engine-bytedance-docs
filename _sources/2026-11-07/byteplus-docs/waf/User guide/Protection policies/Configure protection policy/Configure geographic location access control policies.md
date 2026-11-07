---
title: "Configure geographic location access control policies"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/Configure_geographic_location_access_control_policies"
---

The geographic location access control policy refers to setting network access control rules by country or region based on the home of the source IP. This policy can help you detect access behavior from specified region IPs.

<span id="55d72f33"></span>
## Requirements

You have connected the website that needs to be protected to the WAF instance. For related association operations, please refer to [Comparison of website association methods](https://docs.byteplus.com/en/docs/6511/935148).

<span id="d2b00855"></span>
## Steps


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. Select the instance region in the top menu bar.

3. In the left navigation, select **Protection Policy \> Geo\-location Access Control**.

4. Enable geographic location access control for the domain to be protected.

   1. Select the domain to which you want to add the policy.

   2. (Optional) Confirm that the protection mode of the current domain is "Protection enabled". Otherwise, click **Change protection mode** to modify it.

   3. Turn on the policy enable switch.

5. Sets the policy mode.

   * Intercept: Intercept the request and report the request information to the attack log.

   * Observe: Release the request and report the request information to the attack log.

6. Click **Add regions**, select the areas or countries that need to be banned.

7. Click **OK** to complete the banned area configuration.

   Once configured, you can view banned areas in the Geo\-Location Access Control Banned List or delete areas that no longer need to be banned.
