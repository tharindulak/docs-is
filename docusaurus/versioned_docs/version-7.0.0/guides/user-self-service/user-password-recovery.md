---
title: Password recovery for users
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.0.0/docs/guides/user-self-service/user-password-recovery.md
---

# Password recovery for users

Users may recover a forgotten password from an application sign-in page by following the steps below.

:::note[Before you begin]


Administrators should [enable password recovery](/identity/7.0.0/guides/flows/password-recovery/) for users of the organization.

:::

## Recover a forgotten password

:::warning

Users that onboard from a read-only remote user store are not able to recover their passwords through the My Account portal.

:::

To reset the password, the user should follow these steps.

1. Go to a login page via a business application or the [My Account portal](/identity/7.0.0/guides/user-self-service/customer-self-service-portal/).

    ![Recover your password](../../../../assets/_versions/7.0.0/img/guides/organization/self-service/customer/recover-your-password.png)

2. Click **Forgot password?**


3. Enter your username and click **Send Reset Link**. An email notification will be sent to your email address.
        ![Forgot your password](../../../../assets/_versions/7.0.0/img/guides/organization/self-service/customer/password-recovery-option-email-only.png)

4. Open the email you received and click **Reset Password**.
        ![Reset password email](../../../../assets/_versions/7.0.0/img/guides/organization/self-service/customer/reset-password-email.png)



5. Enter new password and click **Proceed**.

:::note

If the user is already signed in to the My Account portal, the password can be reset from there. Learn how to [change password from the My Account portal](change-password.md).

:::

## Check password recovery email
Users can also check the email address and mobile number to which their password recovery information is sent.

1. In the My Account portal, navigate to **Security** > **Account Recovery**.

    ![Account recovery in WSO2 Identity Server MyAccount](../../../../assets/_versions/7.0.0/img/guides/users/account-recovery.png)

2. Click the eye icon of the relevant row, to check the recovery email address or the recovery mobile.

3. Click **Done**.
