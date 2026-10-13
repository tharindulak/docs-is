---
title: Access the My Account portal
deployment_options:
  - WSO2 Cloud
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/asgardeo/docs/guides/user-self-service/overview.md
---

# Access the My Account portal

Users and administrators in your organization can manage their accounts and information by accessing the **My Account portal**, a self-service portal offered by WSO2 Identity Platform.

Users can access the My Account portal using the following link - 

<Applies to="Self-hosted">

<code>https:&#47;/\{host_name\}:\{port\}/myaccount</code>

For example, if using the default settings, the link to your My Account portal is,

<code>https://localhost:9443/myaccount</code>

</Applies>



:::note


If you have set up organizations in WSO2 Identity Platform and [shared the My Account portal with organization users](../organization-management/share-applications.md#share-the-my-account-portal), they can access the organization-specific My Account Portal using the following link:

```bash
<MY_ACCOUNT_ORG_LINK>
```

:::
You can access the following features from the **My Account portal**.

- [Update profile information](update-profile-info.md)
- [Change password](change-password.md)
- [View and revoke consents given to applications](manage-consents.md)
- [Enroll TOTP](enable-totp.md)
- [Manage backup codes](manage-backup-codes.md)
- [Manage linked social accounts](manage-linked-accounts.md)
- [Export profile information](export-profile-information.md)
- [View and revoke login sessions](manage-login-sessions.md)
- [Manage password recovery](user-password-recovery.md)
- [Discover and maintain applications](discover-applications.md)
- [Register passkeys](register-passkey.md)
- [View and update the approvals](manage-approvals.md)
