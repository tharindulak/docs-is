---
title: Configure OIDC Flows
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.2.0/docs/guides/authentication/oidc/index.md
---

# Configure OIDC Flows

Learn how to discover the OIDC endpoints in your WSO2 Identity Server organization and then use them to implement OIDC flows in your applications.

## Discover the OIDC endpoints

This section covers how you can configure OIDC-based login for your single page application by discovering the required OIDC endpoints and configuring them in the WSO2 Identity Server Console.

[Discover OIDC endpoints](discover-oidc-configs.md) has detailed instructions on this.


## Implement authorization code grant in apps

The guides listed below will help you understand the OIDC login flow using the authorization code flow.

- [Implement authorization code flow](implement-auth-code.md)

- [Implement authorization code flow with PKCE](implement-auth-code-with-pkce.md)

- [Implement private key JWT client authentication for OIDC](private-key-jwt-client-auth.md)

## Implement login using Pushed Authorization Requests

WSO2 Identity Server provides the '/par' endpoint which returns a reference to the authorization payload called the request_uri. This authorization payload is sent by the back-channel during a PAR initiated login.

- [Implement login using Pushed Authorization Requests](implement-login-with-par.md) has detailed instructions on this.

## JWT Secured Authorization Response Mode (JARM) for OAuth 2.0

With JWT Secured Authorization Response Mode, clients can request authorization response parameters in JWT format instead of plain text.

- [JWT Secured Authorization Response Mode (JARM) for OAuth 2.0](jarm.md) has detailed instructions on this.

## Encrypt ID tokens

WSO2 Identity Server supports ID token encryption to enhance security in production environments.

[Encrypt ID tokens](oidc-token-encryption.md) has detailed instructions on how to configure ID token encryption for your applications.

## Decrypt encrypted ID tokens

If you have enabled ID token encryption, you can decrypt the encrypted ID tokens to view the JSON values.

[Decrypt encrypted ID tokens](oidc-token-decryption.md) has detailed instructions on how to decrypt ID tokens using a Java program.

## Validate ID tokens

This section explains how the signature and the claims are verifieed in the ID token that is sent by WSO2 Identity Server to an application.

[Validate ID tokens](validate-id-tokens.md) has detailed instructions on this.

## Request user information

When WSO2 Identity Server sends the ID token to an application, there is user information encoded within it. This can be obtained using the userinfo endpoint.

[Request user information](request-user-info.md) has detailed instructions on this.

## Token validation by resource servers

WSO2 Identity Server provides the '/oauth2/introspect' endpoint to perform token validation. Using this, the resource server can verify the access token before authorizing the access.

[Token validation by resource servers](token-validation-resource-server.md) has detailed instructions on this.

## Revoke access tokens

The token revocation endpoint can revoke any access granted to both confidential clients such as web apps and public clients such as the SPAs or mobile apps.

[Revoke access tokens](revoke-tokens.md) has detailed instructions on this.

## Add logout to application

The logout endpoint is used to terminate the user session at WSO2 Identity Server and to log the user out.

[Add logout to application](add-logout.md) has detailed instructions on this.
