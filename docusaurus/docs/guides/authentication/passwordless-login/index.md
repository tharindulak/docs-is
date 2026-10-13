---
title: Add passwordless login
mkdocs_template: no-right-sidebar
deployment_options:
  - WSO2 Cloud
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/asgardeo/docs/guides/authentication/passwordless-login/index.md
---

# Add passwordless login

Passwordless login represents a modern authentication approach that enhances security and user convenience by eliminating traditional password requirements. This section introduces various passwordless methods such as Magic Links, Passkeys, HYPR, and Email OTP, offering a secure and user-friendly alternative for accessing SPAs and web applications.

## Magic link login

Magic link lets users log in by clicking a link sent to their email instead of entering a password.

[Add Magic Link login](add-passwordless-login-with-magic-link.md) has detailed instructions on this.

## Passkey login

Passkey lets users use hardware security keys or biometrics to log in.

[Add login with Passkey](add-passwordless-login-with-passkey.md) has detailed instructions on this.



<Applies to="WSO2 Cloud">

## HYPR login

HYPR is a FIDO-certified platform that lets users use biometrics to log in.

[Add login with HYPR](../../../guides/authentication/passwordless-login/add-passwordless-login-with-hypr.md) has detailed instructions on this.

</Applies>



## Email OTP login

Email OTP allows users to log in by providing a one-time passcode sent to their email instead of entering a password.

[Add Email OTP login](add-passwordless-login-with-email-otp.md) has detailed instructions on this.

## SMS OTP login

SMS OTP allows users to log in by providing a one-time passcode sent to their mobile phone instead of entering a password.

[Add SMS OTP login](add-passwordless-login-with-sms-otp.md) has detailed instructions on this.

## Push Notification login

Push Notification allows users to log in by approving an authentication request sent to their mobile device through push notifications.

[Add Push Notification login](add-passwordless-login-with-push-notification.md) has detailed instructions on this.
