---
title: Single Sign-On
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.1.0/docs/references/concepts/single-sign-on.md
---

# Single Sign-On

## What is SSO?

Single sign-on (SSO) occurs when a user enters their credentials to log in to an application and is then simultaneously logged in to other connected applications without having to enter their credentials again. This also eliminates the need to have and remember different credentials for different applications. 

For instance, logging in to your Gmail account logs you in to other Google services such as Youtube as well. Notice that it only requires you to enter your credentials once. 

**Single Logout** occurs when a user logs out of an application and is then simultaneously logged out of other connected applications without having to explicitly log out of them one by one. For instance, if you log out of Gmail, you are automatically logged out of Youtube and other Google apps as well. 

----

## How it works

Within a single sign-on system, there are two main entities; the applications and the identity provider. Applications and identity providers store browser cookies and share session information with each other in order to facilitate SSO. The vital part of an SSO mechanism is the pre-defined trust relationship between the applications and the identity providers, which enables this sharing of session data. 

The identity provider is responsible for authenticating the user and issuing an assertion or access token, which contains authentication data, authorization data, and attributes related to the user. The connected application trusts the assertion or access token issued by the identity provider and uses it to authenticate the user to the application. 

<img name='sso-diagram' src='/identity/assets/img/concepts/sso-diagram.png' className='img-zoomable' alt="SSO flow" />

Authentication requests and information are passed using standard, secure protocols, such as [SAML](authentication/intro-saml.md) or [OpenID Connect](authentication/intro-oidc.md). 


----

## Benefits of SSO

SSO authentication is a necessity in most systems today. Some of the benefits of using SSO are:

- Users need only a single set of credentials (username/password) to access multiple services. Therefore, they do not have to face the issue of remembering multiple sets of credentials (username/password pairs).

- Users are authenticated only once at the identity provider and then they are automatically logged in to all services within that "trust-domain". This process is more convenient to users since they do not have to provide their username/password at every application.

- Applications can avoid the overhead of managing user identities, which is more convenient for them.

- User identities are managed at a central point. This is more secure, less complex, and easily manageable.

---


## SSO and Federation

You can use SSO on its own or use SSO and Federation coupled together. Identity Federation involves configuring a third-party identity provider as the federated authenticator to log in to an application. When federation is coupled with SSO, the user can log in to one application using the credentials of the federated authenticator, and simultaneously be authenticated to other connected applications without having to provide credentials again.

For instance, you can set up Google as a federated authenticator and then set up SSO between App1 and App2.  This will allow users to log in to App1 using their Google credentials. Once the user is logged in, when the user attempts to access App2, they will not be prompted for credentials again and will be logged in automatically. 

:::info

 For more information on Identity Federation on its own (without SSO), see [Identity Federation](../../guides/identity-federation/identity-federation-overview.md).

:::


:::info[Related topics]

- [Concept: Authentication](../../guides/authentication-overview.md)
- [Concept: SAML](authentication/intro-saml.md)
- [Concept: OpenID Connect](authentication/intro-oidc.md)
- [Guide: Single Sign-On](../../guides/login/enable-single-sign-on.md)
- [Quick Start: SSO for OpenID Connect apps](../../get-started/sample-use-cases/single-sign-on.md#try-sso-with-oidc)
- [Quick Start: SSO for SAML apps](../../get-started/sample-use-cases/single-sign-on.md#try-sso-with-saml-20)


:::
