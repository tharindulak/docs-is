---
title: Tokens
deployment_options:
  - WSO2 Cloud
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/asgardeo/docs/references/tokens/index.md
---

# Tokens

When a user or application completes an OAuth 2.0 or OpenID Connect flow with WSO2 Identity Platform, the server issues tokens. Each token type has a distinct role and a specific intended consumer.

| Token | Consumed by | Purpose |
| ----- | ----------- | ------- |
| Access token | Resource server (API) | Authorize the client to access a protected resource |
| Refresh token | Authorization server token endpoint | Get new access tokens without re-authentication |
| ID token | Client application | Verify the identity of the authenticated user |

:::note

- [Configure OIDC settings](../app-settings/oidc-settings-for-app.md) to set token types, expiry times, and other per-application token behavior.
- Learn how [token binding](../token-binding/index.md) securely links access tokens to the client that requested them.

:::

## Access tokens

An access token is a short-lived credential that a client presents to a resource server to prove authorization to act on behalf of a user or application.

Learn more about [access tokens](access-tokens.md) including supported token types, validation behavior, and token lifetime. To configure access token settings for your application, see [OIDC settings for apps](../app-settings/oidc-settings-for-app.md#access-token).

## Refresh tokens

A refresh token is a longer-lived credential. Clients exchange it for a new access token after the current one expires, without requiring re-authentication.

Learn more about [refresh tokens](refresh-tokens.md) including rotation behavior and graceful rotation runtime rules. To configure refresh token settings for your application, see [OIDC settings for apps](../app-settings/oidc-settings-for-app.md#refresh-token).

## ID tokens

An ID token is a signed JWT issued by WSO2 Identity Platform as part of an OpenID Connect authentication flow. The client application uses it to verify who authenticated, how, and when — ID tokens must not be sent to resource servers as authorization credentials.

Learn more about [ID tokens](id-tokens.md) including their claims and encryption mechanics. To configure ID token settings for your application, see [OIDC settings for apps](../app-settings/oidc-settings-for-app.md#id-token).
