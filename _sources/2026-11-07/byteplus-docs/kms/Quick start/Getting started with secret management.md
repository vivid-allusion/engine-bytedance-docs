---
title: "Getting started with secret management"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/Getting_started_with_secret_management"
---

**Step 1: Activate the service**

Prerequisites: You have registered a BytePlus account and passed real\-name authentication.


1. Go to the [Secret Manager console](https://console.byteplus.com/kms/region:kms+ap-southeast-1/secrets). On the left navigation pane, click **Secret manager**.

2. On the **Open application** page, click **Open immediately**.

3. Select the region where you need to activate the service, read the description and select **I agree**, and then click **Buy now**.


Note: Key Management Service (KMS) and the Secret Manager service need to be separately activated.

**Step 2: Create a secret**

Prerequisites: The Secret Manager service is activated.


1. Click **Create Secret**.

2. On the **Create Secret** panel, select a secret type from the **Secret type** drop\-down list. Supported secret types: generic secrets, Identity and Access Management (IAM) secrets, Elastic Compute Service (ECS) secrets, RDS secrets, and Cache for Redis secrets.

3. Specify the basic information and configure the key/value of the secret. The required parameters vary depending on the secret type. For more information, refer to [User guide - Secret management](https://docs.byteplus.com/en/docs/kms/ECS_secret_management).

4. Click **Create**.


**Step 3: View the information about the secret**

Prerequisites: The secret is created.


1. In the search box in the secret list, you can search for a secret based on the secret name, type, state, and other information.

2. Find the secret and click **Detail** in the **Actions** column.

3. On the list page or details page, you can edit the description of the secret.


Note: The parameters and operation buttons displayed on the secret details page vary depending on the type of the secret.

Notes for version management:


1. If the secret is not a generic secret, you can store up to two secret versions. One secret value is in the CURRENT state and the other is in the OLDER state. The secret value that was rotated most recently is marked as the CURRENT state.

2. If the secret is a generic secret, you can store up to 20 secret versions. One secret value is in the CURRENT state and the other 19 secret values are in the OLDER state. The secret value that was stored most recently is marked as the CURRENT state.


&nbsp;

**Step 4: Rotate the secret**

Prerequisites: The secret is created.


1. Rotating a generic secret involves storing a new secret value. Secrets can be rotated only manually via the console or APIs. You can store a secret value by specifying the key/value or entering the value as text.

2. Other types of secrets can be either manually or automatically rotated.


For example, when a user performs immediate rotation on an RDS secret, the Secret Manager service automatically generates a strong password and changes the account password for the RDS instance.

In addition, the service supports automatic rotation policies. You can view the rotation interval, last rotation time, and next rotation time in the rotation information.

**Step 5: Delete a secret**

Prerequisites: The secret is created.

Find the secret and click **Deletion settings** in the **Actions** column. You can select either **Force delete immediately** or **Schedule Deletion** as needed. The number of remaining days can be set to 7 to 30 days.

Before the scheduled deletion time, some operations are disabled, but you can cancel the scheduled deletion at any time. After the scheduled deletion time expires, the secret will be deleted, and can be restored only by using the secret restoration feature.

The following operations are disabled before the scheduled deletion time:


* Back up the secret

* Rotate the secret

* Schedule deletion of the secret

* Store a value of the secret

* Update the rotation policy of the secret

* Update the secret
