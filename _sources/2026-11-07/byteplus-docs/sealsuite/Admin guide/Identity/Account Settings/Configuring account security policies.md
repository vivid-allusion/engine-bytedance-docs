---
title: "Configuring account security policies"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-account-security-policies"
---

On the Account Setup page, you can adjust employee account security\-related policies, including password rules, employee self\-service settings, and anti\-brute force policy settings.

<span id="79a57f0e"></span>
# Setting up password rules

To enhance account security, enterprises mandate that platform passwords meet specific complexity requirements. Additionally, they implement strategies such as routinely changing passwords among employees and enforcing a rule where passwords cannot be repeated within a certain period to effectively safeguard account security. In the Password Rules module, you can configure the strength of employee account passwords, as well as the client\-side forget password and mandatory password change functions.


1. Log in to the SealSuite Admin Console.

2. In the left\-side navigation bar, select **Identity** \> **Account Setup**.

3. On the **Account Setup** page, click the **Account Security** tab.

4. In the **Account Security** tab, click **Edit** in the upper right corner of the Password Rules area.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/392b6f1251734a95a4f3bea11805458a~tplv-goo7wpa0wc-image.image) </span>

5. On the **Password Rule** edit page, configure the following fields, and click **Confirm**.

   
   |**Configuration Area** |**Configuration Item** |**Description** |
   |---|---|---|
   |Password strength |Password Requirements (Select a minimum of 2 password requirements) |Set the composition of employee passwords. By default, the password composition requirements are fully selected. You can select multiple options, but at least two must be chosen. |
   ||Minimum Password Length (at least 6 digits) |Set the minimum length requirement for employee passwords. The default minimum length for a password is 8 characters. |
   ||Password strength check |Once enabled, employees entering their passwords will have them evaluated and checked, with an alert issued for weak passwords. After activation, configuration is required:<br><br><br>* **Validation Method**: You can select multiple options, such as **SealSuite Internal Password Library** and **Custom Rules**.<br><br>   * **SealSuite Internal Password Library**: SealSuite's built\-in weak password database typically includes known, commonly used, machine\-generated, or easily guessable passwords like "password" and "qwerty." These can be used with custom rules to identify weak passwords.<br><br>   * **Custom Rules**: Custom rules allow the definition of weak passwords by incorporating brand names, frequently used words, personal information, and other common elements. This helps in compiling a list of weak passwords and instructs employees to adhere to more stringent password guidelines.<br><br>* **Action**: Options include **Log without enforcement** and **Enforce strong** **password**. |
   ||Test Password Strength |Enter the test password and click **Validate** on the right. |
   |Forget password | |Sets whether to display the forgot password feature on the client side.<br><br><br>* **Do not allow password reset**: In the process of logging in to the SealSuite account, the forgot password function will not be displayed.<br><br>* **Allow password reset**: In the process of logging in to the SealSuite account, the forgot password feature will be displayed, and you can reset your password by clicking it. You need to configure the authentication method when resetting your password.<br><br>   * **Primary Authentication Method**: Mandatory option with the default value of **Disabled**. You can choose **SealSuite Mobile OTP**, **SMS Verification Code**, or **Email Verification Code**.<br><br>   * **Alternative MFA**: Optional option with no default value set. You can choose **SealSuite Mobile OTP**, **SMS Verification Code**, or **Email Verification Code**. You must select a different authentication method than the primary authentication method.<br><br>* **Display prompt message**: In the process of logging in to the SealSuite account, the forgot password function will be displayed, and clicking it will show information. You need to configure the prompt text in both Chinese and English. For example, you can advise employees to contact the IT administrator to assist in changing passwords.<br><br>* **Redirect to password reset page**: In the process of logging in to the SealSuite account, the forgot password function will be displayed, and clicking it will redirect to a specified URL. You need to configure the redirect link. For example, setting up the company's IT service desk entry URL so that employees can easily request to change their password. |
   |Initial password settings | |Set whether to require employees to change their password the first time they log in to the client. Once enabled, employees must change their initial password according to the password rule requirements the first time they log into the SealSuite client. |
   |Advanced Password Policies | |Set whether to turn on periodic password changes. The default value is disabled. Once enabled, you need to configure the following settings:<br><br><br>* **Password Rotation Duration** (required): The default value is **90 days**. Options include **180 days**, **365 days**, or **Custom** days. The custom range is 30 to 730 days. If the selected period is exceeded, employees will be required to change their password upon login to SealSuite.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the following situations, the password cycle will be recalculated in hours:   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">First non\-password login: The current time after the user first logs in to SealSuite.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Initial account login: The current time when the user triggers initial password login.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Initial account login + Initial password settings: The current time when the user triggers a password change request.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Forgot password: The current time after the user retrieves the forgotten password.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Reset password: The current time after the user resets their password.   </div><br>   <br><br>* **Prevent passwords from repeating for** (optional): The default value is **365 days**. Options include **180 days**, **540 days**, \*\*\*\* or **disable** this option. Within the selected period, historical passwords cannot be repeated.<br><br>* **Notify users before password expires** (optional): The default value is disabled. Once enabled, SealSuite will notify employees through the specified notification method to change the password in advance.<br><br>   * **Password Expiry Reminder** (required): The default value is 7 days, meaning when the password has 7 days left to expire. At 11:00 daily, SealSuite will send a password expiry reminder to the employee until they change their password. The custom range is 1 to 15 days.<br><br>   * **Notification Methods** (required): Options include **SMS**, **Email**, and **Third\-party** **IM**. You can select multiple options.<br><br>      * **SMS**: Once selected, it can be enabled without configuration, and SealSuite will provide default notification content.<br><br>      * **Email**: Once selected, click **Configure**. After completing the configuration, it will be enabled. For detailed configuration instructions, please refer to [Manage Email configuration](https://docs.byteplus.com/docs/sealsuite/docs-overview-of-notifications#598a8170).<br><br>      * **Third\-party** **IM**: Select a specified robot or add a new one. For detailed configuration instructions, please refer to [Manage third-party IM](https://docs.byteplus.com/docs/sealsuite/docs-overview-of-notifications#7e2d6168).<br><br>* **Require users to verify their identity when changing** **password** (required): Click **Edit**, and select at least one **Primary MFA**. You can also add one **Alternative MFA**, and multiple options are supported for alternative MFA. |
   


<span id="d469cf04"></span>
# Setting up employee self\-service

This policy determines whether employees are allowed to modify their phone number or password on the SealSuite web portal or the SealSuite mobile client.


1. Log in to the SealSuite Admin Console.

2. In the left\-side navigation bar, select **Identity** \> **Account Setup**.

3. On the **Account Setup** page, click the **Account Security** tab.

4. In the **Account Security** tab, in the top\-right corner of the **Employee Self\-Service Settings** section, click **Edit**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1af4596ce10a469b80aed887f0c7a0a4~tplv-goo7wpa0wc-image.image) </span>

5. On the **Employee Self\-Service Settings** page, configure the following fields and click **Confirm**.

   * **Modify Mobile Phone Number**: Once enabled, it allows employees to modify their phone number on the SealSuite portal independently. You need to configure the authentication method.

      * **Primary Authentication Method**: This is a required field. Options include **SealSuite Mobile OTP**, **SMS Verification Code**, or **Email Verification Code**.

      * **Secondary Authentication Method**: This is a required field. Options include **SealSuite Mobile OTP**, **SMS Verification Code**, or **Email Verification Code**. You must select a different authentication method than the primary authentication method.

   * **Change Password**: Once enabled, employees can use the self\-service option to change their passwords on the SealSuite portal. You need to configure the authentication method.

      * **Primary Authentication Method**: This is a required field. Options include **SealSuite Mobile OTP**, **SMS Verification Code**, or **Email Verification Code**.

      * **Secondary Authentication Method**: This is a required field. Options include **SealSuite Mobile OTP**, **SMS Verification Code**, or **Email Verification Code**. You must select a different authentication method than the primary authentication method.


<span id="082df367"></span>
# Setting up anti\-brute force policy

This policy controls the security of employee accounts by imposing restrictions on account login after a preset number of incorrect attempts.


1. Log in to the SealSuite Admin Console.

2. In the left\-side navigation bar, select **Identity** \> **Account Setup**.

3. On the **Account Setup** page, click the **Account Security** tab.

4. In the top right corner of the **Account Security** tab's **Anti\-brute Force Policy Settings** area, click **Edit**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bff34c81fb514ed0a8155e301e985548~tplv-goo7wpa0wc-image.image) </span>

5. On the **Edit Anti\-brute Force Policy Settings** page, configure the following fields, and click **Confirm**.

   * **IP login error**: Once enabled, you must set the number of consecutive failed login attempts allowed from an IP address within a specified period before it is banned from making further login requests to a login employee's account. Additionally, the duration of the ban must be determined.

   * **Incorrect password**: Once enabled, you must set up how many consecutive incorrect password attempts are allowed for the same employee account within a specified period. After exceeding this limit, the account will be locked out and you will also need to set the duration of this lockout.
