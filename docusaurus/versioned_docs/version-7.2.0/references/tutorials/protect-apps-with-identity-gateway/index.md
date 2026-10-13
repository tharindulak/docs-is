---
title: Use WSO2 Identity Server with identity gateways
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.2.0/docs/references/tutorials/protect-apps-with-identity-gateway/index.md
---

# Use WSO2 Identity Server with identity gateways

An identity gateway sits in front of your application and enforces authentication and authorization before requests reach your application.

Identity gateways protect your application by,

- intercepting incoming traffic.

- verifying the user’s identity (using protocols like OAuth2 or OpenID Connect).

- enforcing fine-grained access rules.

- forwarding the request to the application only if it meets the security requirements.

By connecting WSO2 Identity Server with identity gateways, you can centralize user management and apply consistent access control across your entire application ecosystem.

![Identity gateway architecture showing the flow between client, identity gateway, WSO2 Identity Server, and protected applications](../../../../../assets/_versions/7.2.0/img/tutorials/protect-apps-with-identity-gateway/identity_gateway_architecture.png)

This section explains how to connect WSO2 Identity Server with the following identity gateways.

- [OAuth2 Proxy](protect-apps-with-oauth2proxy.md)

- [Oathkeeper](protect-apps-with-oathkeeper.md)

- [Mod Auth OpenIDC](protect-apps-with-mod-auth-openidc.md)
