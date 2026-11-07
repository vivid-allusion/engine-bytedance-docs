---
title: "Associating stream pulling and pushing domain names"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/modifyingtheassociationbetweendomains"
---

This article introduces domain name spaces and describes how to update the association between stream pulling domain names and stream pushing domain names by modifying their domain name spaces.

<span id="35c4be99"></span>
## Background

Stream pushing domain names are used to generate push stream addresses, which users (hosts) can use to push live streams to the BytePlus MediaLive Center.

Stream pulling domain names are used to generate pull stream addresses, which users (viewers) can use to pull live streams from the BytePlus MediaLive Center.

If you want to push a live stream to the BytePlus MediaLive Center and pull this live stream for viewing, you need to associate the stream pushing domain names with the stream pulling domain names.

<span id="2180543e"></span>
### Domain name spaces define the association between stream pushing and pulling domain names

A domain name space is a set of stream pushing domain names and stream pulling domain names. It associates the stream pushing domain names with the stream pulling domain names.

The stream pushing domain names and stream pulling domain names used for the pushing and viewing of a live stream must be associated with each other. Once they are associated, you use the stream pushing domain names to push the live stream to the BytePlus MediaLive Center. You can pull and play the live stream using the stream pulling domain names that are associated with the stream pushing domain names.

Different services have different domain name spaces, so connectivity between live streams in different domain name spaces is not possible.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9edf9b991ca94674abb3793a48dad69e~tplv-goo7wpa0wc-image.image) </span>

<span id="4a8ee226"></span>
### Domain name spaces define the configuration of live stream services

The structure of live stream addresses means that all or some streams in the current domain name space can be determined once the domain name, AppName and StreamName are known.

Therefore, we can use the **Domain Name Space**, **Domain name**, **AppName** and **StreamName** to specify the range of valid streams in value\-added feature configurations.

Below is an example of a live stream address.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8878d07015b04a368edb5bed2e017206~tplv-goo7wpa0wc-image.image) </span>

Different services have different domain name spaces. Connectivity between configurations in different domain name spaces is not possible. The image below shows how different levels of configurations apply to different streams in a domain name space.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ca52ea551a74c8cb241f58c6f584b96~tplv-goo7wpa0wc-image.image) </span>


* Domain name space: This value\-added feature configuration applies to all streams in this domain name space.

* Domain name space+ Domain Name: This value\-added feature configuration applies to all streams with this domain name in this domain name space.

* Domain name space + AppName: This value\-added feature configuration applies to all streams with this app name in this domain name space.

* Domain name space + AppName + StreamName: This value\-added feature configuration applies to the stream with this app name and stream name in this domain name space.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Different value\-added configurations apply to different ranges of streams. Refer to their respective descriptions for more details.</div>


<span id="945ca302"></span>
## Procedures

<span id="7d13ae58"></span>
### Adding a domain name to an existing domain name space

When adding a domain name, you can add it to an existing domain name space to associate it with other added domain names.


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, click **Domains**.

3. Click **Add domain name**.

4. Select an existing domain name space under **Associated domain name space**, then add the domain name. For more information on other settings, see [Adding a domain name](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-domain).


<span id="4540ea9c"></span>
### Modifying the domain name space of a domain name

After a domain name is added, you can change its domain name space if necessary.


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, click **Domains**. Click **Settings** to the right of the domain name.

3. In the **Basic** **information** tab, click the Edit icon to the right of **Domain name space** in the **Domain name space** section. Enter a new domain name space in the pop\-up window and click **Confirm**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Domain name spaces without a domain name will be removed.</div>
