---
title: Add login to an SPA
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.1.0/docs/guides/authentication/add-login-to-single-page-app.md
---

# Add login to an SPA

Single-page apps (SPAs) by design run with the source code exposed in the browser, which means that they cannot maintain any secrets. These kinds of applications are called public clients.

Based on the [OAuth 2.0 best practices for browser-based apps](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-browser-based-apps-08), WSO2 Identity Server recommends securing your SPAs using the OpenID Connect Authorization Code Flow for public clients with the PKCE ([Proof Key for Code Exchange](https://datatracker.ietf.org/doc/html/rfc7636)) extension.

See the guides given below to add login to your SPAs with WSO2 Identity Server.

## Try out samples

- [React SPA Sample](../../get-started/try-samples/qsg-spa-react.md)
- [JavaScript SPA Sample](../../get-started/try-samples/qsg-spa-javascript.md)

## Use an SDK to add login to your SPA

- [React SDK](../../get-started/try-your-own-app/react.md)
- [Javascript SDK](../../get-started/try-your-own-app/javascript.md)

## Manually add login to your SPA

- [Implement authorization code flow with PKCE](oidc/implement-auth-code-with-pkce.md)
