---
title: Maintaining Logins and Passwords
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/5.11.0/docs/setup/maintaining-logins-and-passwords.md
---

# Maintaining Logins and Passwords

### Changing the super admin password

To change the default admin password, log in to the management console
with admin/admin credentials and use the **Change my password** option.

### Recovering a password

Use `         <IS_HOME>/bin/chpasswd.sh        ` script.

### Login with an email address

You can configure WSO2 Identity Server to authenticate users using an email address instead of a username. Refer [Using Email Address as the Username](../../learn/using-email-address-as-the-username) section for configurations steps.
