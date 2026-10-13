---
title: Account management
deployment_options:
  - WSO2 Cloud
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/asgardeo/docs/guides/user-accounts/index.md
---

# Account management

This section explains how owners can create multiple organizations in the WSO2 Identity Platform Console, switch between them, manage user attributes, perform account recovery, provide users with self-service capabilities, and mitigate risks via configuring security measures for user accounts.

- Organization owners can manage the resources within their organizations.

    See [Manage multiple organizations](../organization-management/manage-organizations.md) for instructions.

- User attributes represent a user's information within an organization. These default attributes can either be mapped to OpenID Connect claims or SCIM 2 attributes.

    See [Manage user attributes](../users/attributes/index.md) for instructions.

- In WSO2 Identity Platform, accounts can be recovered by administrators or by the users themselves. Users can recover their forgotten passwords using the self-service passwords recovery option.

    See [Configure password recovery](/identity/guides/user-accounts/password-recovery/) for instructions.

- Users can self-register to an organization in WSO2 Identity Platform via an application's login page.

    See [Configure self-registration](configure-self-registration.md) for instructions.

- When you onboard several users onto your organization, it is of utmost importance to secure their accounts from unauthorized logins or other unfavorable misuses. Some popularly effective methods include locking the account on consecutive failed login attempts and using reCAPTCHA to detect bots.

  See the following sections for instructions on configuring these security measures:

  - [Configure login-attempts security](account-security/login-attempts-security.md)
  - [Configure bot detection](account-security/bot-detection.md)
