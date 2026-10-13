---
title: Maintain Logins and Passwords
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.0.0/docs/deploy/security/maintain-logins-and-passwords.md
---

# Maintain Logins and Passwords

Changing default credentials before deploying the server in a production environment is crucial. Using default login information poses a significant security risk by making the system vulnerable to unauthorized access. This section provides guidance on enhancing the security of the WSO2 Identity Server console by updating login details.

## Change the super admin password

To change the default admin password, log in to the WSO2 Identity Server MyAccount portal with admin credentials and [change the password](../../guides/user-self-service/change-password.md)

## Recover a password

If you forget your password, you can recover it using the [password recovery](../../guides/your-is/recover-password.md) option available on the WSO2 Identity Server.

## Log in with an email address

You can configure the WSO2 Identity Server to authenticate users using an email address instead of a username. Refer to [Enable Using Email Address as the Username](../../guides/users/attributes/enable-email-as-username.md) for further information.
