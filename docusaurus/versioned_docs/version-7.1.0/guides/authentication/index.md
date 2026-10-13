---
title: Authentication
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.1.0/docs/guides/authentication/index.md
---

# Authentication

See the topics given below to manage authentication for your applications.

## Design the login flow

When you register an application, you can customize the login flow.

- Configure WSO2 Identity Server login for [single-page applications with OIDC](add-login-to-single-page-app.md) or [web applications](add-login-to-web-app.md) with OIDC or SAML.

- Add [social login](social-login/index.md) options such as [Google](social-login/add-google-login.md), [Facebook](social-login/add-facebook-login.md), [Apple](social-login/add-apple-login.md), and [Microsoft](social-login/add-microsoft-login.md).

- Add other [enterprise identity providers](standard-based-login/index.md) as login options.

- Configure the number of factors (2FA or MFA) in the login flow to enforce [multi-factor authentication](mfa/index.md).

- Enforce [conditional authentication](conditional-auth/index.md) to dynamically change the login flow of a user based on the user's devices, networks, locations, or usage contexts.



- Add [SSO integrations](sso-integrations/index.md) using WSO2 Identity Server to log in to applications such as [Google](sso-integrations/add-google-workspace-template.md), [Salesforce](sso-integrations/add-salesforce-template.md), [Microsoft](sso-integrations/add-microsoft-365-template.md), [Zoom](sso-integrations/add-zoom-template.md), and [Slack](sso-integrations/add-slack-template.md).



## Manage user attributes

Manage the user attributes you want to share with your application:

- [Enable user attributes for OpenID Connect apps](user-attributes/enable-attributes-for-oidc-app.md)
- [Enable user attributes for SAML apps](user-attributes/enable-attributes-for-saml-app.md)

## Manage connections

External Identity Providers (IdPs) can be registered as connections in WSO2 Identity Server and be used to authenticate users who log in to your applications. These IdPs authenticate users and issue identification information using security tokens based on protocols like SAML 2.0, OpenID Connect, OAuth 2.0, and WS-Trust. This process of authenticating users with external IdPs is known as **Identity Federation**.

With identity federation, users can use an existing user account registered to a trusted IdP to login to your applications without having to create accounts for them in WSO2 Identity Server.

:::note

If the IdP is configured to use [JIT user provisioning](jit-user-provisioning.md), when a user signs in with an external IdP, an account will automatically be created for the user in WSO2 Identity Server.

:::

### Supported external IdPs

WSO2 Identity Server supports a variety of external identity providers with various open-standard protocols (such as OAuth2.0, OpenID Connect, and SAML).

- [Social identity providers](social-login/index.md)
- [Enterprise identity providers](standard-based-login/index.md)

You can configure any number of external connections for your application via WSO2 Identity Server.

### Map local attributes to external attributes

Follow the steps below to map attributes of WSO2 Identity Server with that of a connection.

1. On the WSO2 Identity Server Console, go to **Connections**.

2. Select your connection and go to its **Attributes** tab.

3. Click **Add Attribute Mapping** to add a new attribute mapping.

    ![Add attribute mappings](../../../../assets/img/guides/idp/group-mapping/add-attribute-mappings.png)

4. Enter the  **External IdP Attribute** of the connection and map it to the **Groups** attribute of WSO2 Identity Server.

    ![Add new group attribute mapping](../../../../assets/img/guides/idp/group-mapping/add-new-group-attribute-mapping.png)

5. Click **Add Attribute Mapping** and then click **Save**.

    ![Stage new group attribute mapping](../../../../assets/img/guides/idp/group-mapping/stage-new-group-attribute-mapping.png)

6. Click **Update** to save the changes.

    ![Submit attribute mappings](../../../../assets/img/guides/idp/group-mapping/submit-attribute-mappings.png)



### Add required attributes for provisioning

When provisioning users from an external identity provider (IdP), you may want to include specific attributes in the user’s profile. Follow the steps below to define the required attributes and assign default values.

1. On the WSO2 Identity Server Console, go to **Connections**.
2. Select your connection and go to its **Attributes** tab.
3. Under **Provisioning Attributes Selection**, click **Add Attribute**.
4. Move the attributes that you want to include in the provisioned user's profile and click **Save**.

    ![Add required attributes for provisioning](../../../../assets/img/guides/idp/add-required-attributes-for-provisioning.png)

5. Add a default value to the attribute. If the federated user lacks data for it, the system adds the default to the provisioned user’s profile.

    ![Add default value for required attributes](../../../../assets/img/guides/idp/add-default-value-for-required-attributes.png)

    :::note


    To add default values to the provisioned user’s profile when the federated user has no value, configure the following in the `<IS_HOME>/repository/conf/deployment.toml` file.

    ```toml
    [authentication.endpoint]
    enable_merging_custom_claim_mappings_with_default = true
    ```

    :::



### Add groups to connections

Follow the steps below to add the groups from your connection to WSO2 Identity Server:

1. On the WSO2 Identity Server Console, go to **Connections**.
2. Select your connection and go to its **Groups** tab.
3. Click **New Group** and enter the group name. Be sure to enter the exact group name that will be returned from the connection.

    ![Add group](../../../../assets/img/guides/idp/add-federated-group.png)

4. Click **Finish** to add the group information.
