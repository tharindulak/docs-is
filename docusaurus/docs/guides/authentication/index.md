---
title: Authentication
deployment_options:
  - WSO2 Cloud
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/asgardeo/docs/guides/authentication/index.md
---

import AddGroups from '../../_partials/guides/fragments/manage-connection/add-groups.mdx';

# Authentication

See the topics given below to manage authentication for your applications.

## Design the login flow

When you register an application, you can customize the login flow.

- Configure WSO2 Identity Platform login for [single-page applications with OIDC](add-login-to-single-page-app.md) or [web applications](add-login-to-web-app.md) with OIDC or SAML.

- Add [social login](social-login/index.md) options such as [Google](social-login/add-google-login.md), [Facebook](social-login/add-facebook-login.md), [Apple](social-login/add-apple-login.md), and [Microsoft](social-login/add-microsoft-login.md).

- Add other [enterprise identity providers](standard-based-login/index.md) as login options.

- Configure the number of factors (2FA or MFA) in the login flow to enforce [multi-factor authentication](mfa/index.md).

- Enforce [conditional authentication](conditional-auth/index.md) to dynamically change the login flow of a user based on the user's devices, networks, locations, or usage contexts.



- Add [SSO integrations](sso-integrations/index.md) using WSO2 Identity Platform to log in to applications such as [Google](sso-integrations/add-google-workspace-template.md), [Salesforce](sso-integrations/add-salesforce-template.md), [Microsoft](sso-integrations/add-microsoft-365-template.md), [Zoom](sso-integrations/add-zoom-template.md), and [Slack](sso-integrations/add-slack-template.md).



## Manage user attributes

Manage the user attributes you want to share with your application:

- [Enable user attributes for OpenID Connect apps](user-attributes/enable-attributes-for-oidc-app.md)
- [Enable user attributes for SAML apps](user-attributes/enable-attributes-for-saml-app.md)

## Manage connections

External Identity Providers (IdPs) can be registered as connections in WSO2 Identity Platform and be used to authenticate users who log in to your applications. These IdPs authenticate users and issue identification information using security tokens based on protocols like SAML 2.0, OpenID Connect, OAuth 2.0, and WS-Trust. This process of authenticating users with external IdPs is known as **Identity Federation**.

With identity federation, users can use an existing user account registered to a trusted IdP to login to your applications without having to create accounts for them in WSO2 Identity Platform.

:::note

If the IdP is configured to use [JIT user provisioning](jit-user-provisioning.md), when a user signs in with an external IdP, an account will automatically be created for the user in WSO2 Identity Platform.

:::

### Supported external IdPs

WSO2 Identity Platform supports a variety of external identity providers with various open-standard protocols (such as OAuth2.0, OpenID Connect, and SAML).

- [Social identity providers](social-login/index.md)
- [Enterprise identity providers](standard-based-login/index.md)

You can configure any number of external connections for your application via WSO2 Identity Platform.

<AddGroups />
