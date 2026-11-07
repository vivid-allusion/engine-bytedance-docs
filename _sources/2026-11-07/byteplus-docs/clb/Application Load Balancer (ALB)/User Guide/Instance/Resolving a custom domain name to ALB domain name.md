---
title: "Resolving a custom domain name to ALB domain name"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Configuring-domain-name-resolution"
---

This topic describes how to add a CNAME record to point your own domain name to the domain name of an ALB instance.

## Action description

### ALB domain name

After an ALB instance is created, the system assigns it an ALB domain name in the format: *instanceId*.*regionId*.volcenginealb.com. For example: alb\-abc123def456.cn\-beijing.volcenginealb.com.

The BytePlus  does not allow users to **directly** use the default domain name provided by the ALB service for **internet** access. If you need to provide services to the internet through an ALB instance, please use your own domain name and configure a CNAME record to resolve it to the ALB domain name.

### CNAME record

A CNAME record is a type of DNS record used to create an alias for a domain name. It allows one domain name to point to another domain name (rather than directly to an IP address). When a client makes a request using that domain name, the DNS server resolves it to the target domain name specified in the CNAME record.

## Procedures

1. Obtain the instance domain name.

   1. Log in to the [ALB console](https://console.byteplus.com/alb).

   2. In the left navigation pane, click **Instance** to go to the **Instance management** page.

   3. On the **Instance management** page, locate the ALB instance you want to view, then copy the domain name in the **Instance domain** column.

2. Register a domain name.

   If you do not already have one, you need to register a domain name with a domain registrar. You can use BytePlus's Domain Name Service to register a domain.

3. Add CNAME record.

   You need to add the CNAME record at your DNS service provider. As the DNS record management interfaces vary by provider, please consult your specific DNS provider's product documentation or support team for detailed instructions on adding DNS records.

   The table below lists the common fields used in a CNAME record. Note that field names may differ slightly between DNS providers.

   |**Field** |**Explanation** |
   |---|---|
   |Record type |Must be set to CNAME. |
   |Domain name/Host record |Set this field according to your custom domain name and input rules. Typically, this refers to the domain name prefix. |
   |Record value |Record Value: Must be set to the ALB instance domain name you copied. |
   |TTL |TTL: Refers to the expiration time of DNS record caching.<br><br>The smaller the TTL value, the faster the DNS record update takes effect. |

## What to do next

After adding the CNAME record, you can verify if it has taken effect.

### Verify if the CNAME record has taken effect

Typically, a new CNAME record propagates and becomes effective within minutes. However, updates to existing records may take longer to propagate globally due to factors like TTL settings and DNS caching.

You can verify whether the CNAME record has taken effect using the following methods:

#### Method 1: Verify using the **nslookup** command

Run the following command:

```Shell
nslookup -type=CNAME your_custom_domain
```

Replace `your_custom_domain` with your actual custom domain name.

If the returned result displays the corresponding ALB instance domain name, it indicates that the CNAME record has taken effect.

#### Method 2: Verify using the **dig** command

Run the following command:

```Shell
dig -t CNAME your_custom_domain
```

Replace `your_custom_domain` with your actual custom domain name.

If the `ANSWER SECTION` in the returned result displays the corresponding ALB instance domain name, it indicates that the CNAME record has taken effect.

## FAQs

### CNAME record and A record conflict

A domain name cannot have both a CNAME record and an A record simultaneously. When adding a CNAME record for a domain name, if the system prompts a record conflict, check whether an A record has already been configured for that domain name. If an A record exists, delete it first before configuring the CNAME record.
