---
title: Recover your password
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.3.0/docs/guides/your-is/recover-password.md
---

# Recover your password

If you are the owner or an administrator of an WSO2 Identity Server organization, the following guide explains how you can recover a forgotten password.

To recover your password:

1. Go to the sign-in page of the [My Account Portal](is-self-service.md#access-my-account-portal).

    ![Recover your password](../../../assets/img/guides/organization/self-service/customer/recover-your-password.png)

2. Click **Forgot password?**.


3. Follow one of the following methods that are configured for your organization.

    <Tabs>
    <TabItem value="tab-0" label="Email link">


    Enter your username and click **Send Reset Link**. An email notification will be sent to your email address.
    ![Forgot your password](../../../assets/img/guides/organization/self-service/customer/password-recovery-option-email-only.png)

    </TabItem>
    <TabItem value="tab-1" label="Email OTP">


    Enter your username and click **Send Email OTP**. An OTP code will be sent to your registered email address.
    ![Forgot your password](../../../assets/img/guides/organization/self-service/customer/password-recovery-option-email-otp.png)

    </TabItem>
    <TabItem value="tab-2" label="SMS OTP">


    Enter your username and click **Send SMS OTP**. An OTP code will be sent to your registered mobile number.
    ![Forgot your password](../../../assets/img/guides/organization/self-service/customer/password-recovery-option-sms-only.png)

    </TabItem>
    </Tabs>

    :::note


    - Setting an email address is required for email link and email OTP recovery methods, while setting a mobile number is required for SMS OTP recovery.

    - If you have configured both options for password recovery, select your preferred method and click **Proceed**.

    :::




4. Confirm password reset request.

    <Tabs>
    <TabItem value="tab-0" label="Email link">


    Open the email you received and click **Reset Password**.
    ![Reset password email](../../../assets/img/guides/organization/self-service/customer/reset-password-email.png)

    </TabItem>
    <TabItem value="tab-1" label="Email OTP">


    Enter the OTP code sent to your email and click **Continue**.
    ![Reset password email OTP](../../../assets/img/guides/organization/self-service/customer/reset-password-email-otp.png)

    </TabItem>
    <TabItem value="tab-2" label="SMS OTP">


    Enter the OTP code sent to your mobile and click **Continue**.
    ![Reset password SMS OTP](../../../assets/img/guides/organization/self-service/customer/reset-password-sms-otp.png)

    </TabItem>
    </Tabs>




5. Enter new password and **Proceed**.
