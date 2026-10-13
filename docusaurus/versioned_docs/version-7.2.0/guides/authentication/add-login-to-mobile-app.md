---
title: Add login to a mobile app
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.2.0/docs/guides/authentication/add-login-to-mobile-app.md
---

# Add login to a mobile app

Mobile applications, by design, cannot maintain any secrets. These kinds of applications are called public clients.

Based on the [OAuth 2.0 best practices for browser-based apps](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-browser-based-apps-08), WSO2 Identity Server recommends securing your mobile apps using the OpenID Connect Authorization Code Flow for public clients with the PKCE ([Proof Key for Code Exchange](https://datatracker.ietf.org/doc/html/rfc7636)) extension.

See the guides given below to add login to your mobile applications with WSO2 Identity Server.

## Manually add login to your mobile app

- [Implement authorization code flow with PKCE](oidc/implement-auth-code-with-pkce.md)
