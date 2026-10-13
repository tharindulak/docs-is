---
title: Maintain Logins and Passwords
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.0.0/docs/deploy/security/maintain-logins-and-passwords.md
---

# Maintain Logins and Passwords

## Change the super admin password

To change the default admin password, log in to the WSO2 Identity Server management console (`https://<IS_HOST>:<PORT>/carbon`)
with admin/admin credentials and use the **Change my password** option.

---

## Recover a password

Use the  `         <IS_HOME>/bin/chpasswd.sh        ` script.

---

## Log in with an email address

You can configure WSO2 Identity Server to authenticate users using an email address instead of a username. Refer [Enable Using Email Address as the Username](../../guides/identity-lifecycles/enable-email-as-username.md) for further information.
