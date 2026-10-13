---
title: Implement OIDC front-channel logout
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.3.0/docs/guides/authentication/oidc/add-front-channel-logout.md
---

# Implement OIDC front-channel logout

Front-channel logout lets the authorization server notify client applications to end a user's session through the user's browser via iframes.

Use front-channel logout when client applications cannot accept server-to-server (back-channel) requests but can receive browser-delivered logout notifications.

For protocol details see the OpenID specification: [OpenID Connect Front-Channel Logout 1.0](https://openid.net/specs/openid-connect-frontchannel-1_0.html).

## How it works

![oidc-front-channel-logout-scenario](../../../../assets/img/guides/oidc-logout/oidc-frontchannel-logout-scenario.png)

The front-channel logout flow works as follows:

1. The client application initiates a user logout.
2. WSO2 Identity Server terminates the user's session.
3. WSO2 Identity Server identifies all the client applications associated with the user's session.
4. WSO2 Identity Server responds with an HTML page that embeds an iframe for each application that has a front-channel logout URI configured.
5. Upon receiving the logout request, each client application validates the requests and proceeds to invalidate the corresponding user session.

The logout request includes `iss` (issuer) and `sid` (session ID) query parameters.

<Tabs>
<TabItem value="tab-0" label="Logout request format">


```url
http://myapp.com?iss=https://localhost:9443/oauth2/token&sid={sid_value}
```

</TabItem>
<TabItem value="tab-1" label="Example request">


```url
http://myapp.com?iss=https://localhost:9443/oauth2/token&sid=15043ffc-****-****-****-9b107f7da38c
```

</TabItem>
</Tabs>

## Configure front-channel logout URL

If your application supports OIDC front-channel logout, you can configure the logout URL of the application in the Console. That endpoint can listen to OIDC front-channel logout requests from WSO2 Identity Server, and terminate the application's sessions.

To get started, you need to have an application registered in WSO2 Identity Server. If you don't already have one, [register a web app with OIDC](../../applications/register-oidc-web-app.md).

Follow the steps below to register the front-channel endpoint of your application with WSO2 Identity Server.

:::note[Before you begin]


[Register your OIDC application](../../applications/index.md) in WSO2 Identity Server.

:::

1. On the WSO2 Identity Server Console, go to **Applications** and select your OIDC application.

2. Go to the **Protocol** tab, and under **Logout URLs**, enter the **Front channel logout URL**.

       ![oidc-logout](../../../../assets/img/guides/oidc-logout/oidc-frontchannel-logout-configuration.png)

3. Click **Update** to save your configurations.

:::note


**Cross-site cookie considerations**

Front-channel logout uses GET requests delivered via iframes to notify client domains. While GET requests in iframes have good browser support, modern browsers restrict third-party cookies and cross-site tracking, which can cause logout to fail.

*Recommendations:*

- Prefer [back-channel logout](add-back-channel-logout.md) for reliable server-to-server session termination, as it does not depend on browser cookie policies.
- Consider hosting applications on subdomains of a shared parent domain (for example, `app1.example.com` and `app2.example.com`) so cookies can use `Domain=.example.com` and become first-party.

:::
