---
title: Best practices to protect your organization
deployment_options:
  - WSO2 Cloud
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/asgardeo/docs/references/production-checklist/best-practices.md
---

# Best practices to protect your organization

We recommend the following best practices to protect your organization in the production environment:

- **Strong authentication for WSO2 Identity Platform administrators**

    It is recommended to enable strong authentication for administrators with access to your admin console. This can be done by users' preference only. Administrators can enable multi-factor authentication for their WSO2 Identity Platform account. [Learn more](../../guides/your-identity-platform/identity-platform-self-service.md#enroll-totp-for-wso2-identity-platform-users)

- **Enable account locking upon failed login attempts**

    Protect your organization from password brute-force attacks by locking the affected user accounts. [Learn more](../../guides/user-accounts/account-security/login-attempts-security.md#enable-login-attempts-security)

    :::note

    Make sure you have branded the account locking and account unlocked email templates according to your organization's theme.

    :::

- **Enable multi-factor authentication for business applications**

    MFA provides an additional layer of security to the resources of the organization. If one factor is compromised or broken, an attacker still has at least one more barrier to breach before successfully breaking into the resource. [Learn more](../../guides/authentication/mfa/index.md)

- **Prevent using undocumented features**

    You should not use undocumented features without confirming with the product team.
