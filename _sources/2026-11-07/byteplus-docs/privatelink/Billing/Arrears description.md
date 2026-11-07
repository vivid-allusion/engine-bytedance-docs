---
title: "Arrears description"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Arrears"
---

This topic describes how overdue payments affect PrivateLink services.

> **tip**

* > When your account has an overdue payment, the platform will send you SMS/email/internal message reminders based on your settings.

* > After your account becomes overdue, regardless of whether your instance resources are suspended or released, any fees reflected in issued bills must be settled accordingly. The specific suspension time is subject to the actual situation.

## Endpoint account overdue

* **The payer account is the Endpoint account**

   Endpoint resources will be affected. The status and operational restrictions of endpoint resources during different periods are shown in the figure below.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c4d2116b80ccdef77d8fd4a37d582acc.png)

* **The payer account is the Endpoint Service account**

   The PrivateLink service itself remains unaffected and continues to operate normally.

## Endpoint service account overdue

* **The payer account is the Endpoint account**

   The pay\-as\-you\-go CLB instances associated with the endpoint service will be affected, which may result in partial unavailability of endpoint connections. It is recommended to recharge the service provider account promptly. For a detailed explanation of the status of service resources after an account becomes overdue, see respective documentation based on the service resource type: [CLB arrears](https://docs.byteplus.com/en/docs/clb/Billing-07), [ALB arrears](https://docs.byteplus.com/en/docs/clb/Overdue-payments).

   > **tip**

   > The ALB service resource support for PrivateLink is in beta stage. For trial requests, contact your account manager.

* **The payer account is the Endpoint Service account**

   The endpoint service and its associated resources will be affected. The status and operational restrictions of endpoint service resources during different periods are shown in the figure below.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9c50f16cf80131fa59a7547b5b5f7aea.png)
