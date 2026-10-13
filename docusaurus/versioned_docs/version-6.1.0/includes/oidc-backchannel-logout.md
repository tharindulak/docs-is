---
title: Oidc backchannel logout
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.1.0/docs/includes/oidc-backchannel-logout.md
---

## Configure back-channel single logout


1. Navigate to **Main** > **Identity** > **Service Providers** > **List**.

2. Click **Edit** to edit the OIDC service provider you created.

3. Expand **Inbound Authentication Configuration** > **OAuth/OpenID Connect Configuration**. 

4. Click **Edit**.



5. Select **Enable OIDC Backchannel Logout** and enter the Logout URL.

    :::info

    The **Logout URL** is the service provider's back-channel logout endpoint URL to which the logout token is sent to.

    :::

6. Click **Update** to save the changes.
