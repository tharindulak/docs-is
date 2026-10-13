---
title: Refresh tokens
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.1.0/docs/references/tokens/refresh-tokens.md
---

# Refresh tokens

A refresh token is a long-lived credential issued alongside an access token — typically valid for days or weeks. Clients use refresh tokens to get new access tokens after the current one expires, without requiring the user to log in again.

Refresh tokens are only issued when the `Refresh Token` grant type is enabled for your application. They are sent only to the WSO2 Identity Server token endpoint and must never be forwarded to resource servers.

:::warning

A valid refresh token can get new access tokens at any time. Store refresh tokens securely — treat them with the same care as passwords or other long-lived credentials.

Never send refresh tokens as URL query parameters in GET requests. Tokens in URLs can leak through server logs, browser history, and the `Referer` header. Always send them as form parameters in the body of the `POST` request to the token endpoint.

:::

## Refresh token rotation

By default, whenever the refresh token is exchanged for a new access token, WSO2 Identity Server issues the same refresh token back, as long as it has not expired.

When **Renew refresh token** is enabled, WSO2 Identity Server invalidates the current refresh token and issues a new one on each exchange. This limits exposure if a token is stolen — the old token becomes invalid immediately on use.

To configure rotation settings for your application, see [OIDC settings for apps](../app-settings/oidc-settings-for-app.md#refresh-token).



## Token lifetime

Refresh tokens have a configurable validity period. When **Renew refresh token** is enabled, the expiry behavior of the renewed token depends on the **Extend expiry time of renewed refresh token** setting.

- When enabled (default), the renewed refresh token is issued with a fresh validity period starting from the time of renewal.
- When disabled, the renewed refresh token carries the remaining validity period of the original refresh token.

Once a refresh token expires, the client must restart the authorization flow to get new tokens.

## Revocation

A refresh token can be revoked before it expires. Common triggers include a user signing out, a password change, or an explicit revocation request by the application.

When a refresh token is revoked, it can no longer be used to get new access tokens, and any associated access tokens are also invalidated. Applications should handle a revocation response by redirecting the user to re-authenticate.

:::note

To configure refresh token expiry and rotation settings for your application, see [OIDC settings for apps](../app-settings/oidc-settings-for-app.md#refresh-token).

:::
