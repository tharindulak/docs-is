---
title: Invoke the OAuth Introspection Endpoint
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/5.9.0/docs/learn/invoke-the-oauth-introspection-endpoint.md
---

# Invoke the OAuth Introspection Endpoint

The OAuth Introspection endpoint is as follows:

```
https://localhost:9443/oauth2/introspect
```
OAuth 2.0 Token Introspection defines a protocol that allows authorized
protected resources to query the authorization server to determine the
set of metadata for a given token that was presented to them by an OAuth
Client. This metadata includes whether the token is currently **active**
(or if it has **expired** or otherwise been **revoked** ), what rights
of access the token carries (usually conveyed through OAuth 2.0 scopes),
and the authorization context in which the token was granted (including
who authorized the token and which client it was issued to). Token
introspection allows a protected resource to query this information
regardless of whether it is carried in the token itself, allowing this
method to be used along with or independently of structured token
values.

The states and descriptions of authorization codes and access tokens are
as follows.

-   **Authorization codes:**

    1.  `             ACTIVE            ` - Valid and yet to be
        exchanged for an access token.
    2.  `             INACTIVE            ` - Invalid and already being
        exchanged for an access token.
    3.  `             EXPIRED            ` - Invalid as it got expired
        before being exchanged to an access token.

-   **Access tokens:**

    1.  `             ACTIVE            ` - Valid access token. Although
        the state is ACTIVE, the `             timestamp            `
        calculation may reveal it to be
        `             EXPIRED            `, but this happens only
        during the first access token request or token validation
        request after expiration.
    2.  `             INACTIVE            ` - Refreshed using
        `             refresh_token            ` grant type before
        expiration. Also, this state is used in cases when users and
        user stores are deleted, user passwords are updated, etc.
    3.  `             EXPIRED            ` - Invalid and expired access
        token. Refresh token can still be valid though.
    4.  `             REVOKED            ` - Revoked access token.
        Refresh token also gets revoked along with access token. Access
        token could have been in `             ACTIVE            ` or
        `             EXPIRED            ` state while revoking.

## Invoking the endpoint for the super tenant

Use the following cURL commands given in the following sections to
invoke the OAuth introspection endpoint for the super tenant users.

:::note


-   For requests that require
    `          CLIENT_ID:CLIENT_SECRET         `, use the client ID and
    client secret of the OAuth service provider. For more information on
    creating an OAuth service provider, see [Configuring Inbound
    Authentication for a Service
    Provider](../../learn/configuring-inbound-authentication-for-a-service-provider).
-   For requests that require `           USERNAME:PASSWORD          `,
    by default you can use credentials of any user with
    "/permission/admin/manage/identity/applicationmgt/view" permissions.
    To allow users with other permissions to send validation requests,
    the permissions can be added to the `<IS_HOME>/repository/conf/deployment.toml`         `
    file.

    ```toml
    [resource_access_control.introspect]
    permissions = ["/permission/admin/manage/identity/applicationmgt/view","/permission/admin/login"]
    ```

-   Token introspection across tenant domains is enabled by default. To disable cross tenant token validation,
    add the following configuration to the `<IS_HOME>/repository/conf/deployment.toml` file and restart the server.

    ```toml
    [oauth.introspect]
    allow_cross_tenant = false
    ```

:::

### Get a valid token

<table><tbody><tr className={"odd"}><td>{"Request"}</td><td><div className={"code panel pdl"}><div className={"codeHeader panelHeader pdl"}><strong>{"Request"}</strong></div><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb1"} data-syntaxhighlighter-params={"brush: bash; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode bash"}><code className={"sourceCode bash"}><a className={"sourceLine"} id={"cb1-1"} title={"1"}><span className={"ex"}>{"curl"}</span>{" -v -X POST --basic -u "}<span className={"op"}>{"<"}</span>{"CLIENT_ID"}<span className={"op"}>{">"}</span>{":"}<span className={"op"}>{"<"}</span>{"CLIENT_SECRET"}<span className={"op"}>{">"}</span>{" -H "}<span className={"st"}>{"'Content-Type: application/x-www-form-urlencoded;charset=UTF-8'"}</span>{" -k -d "}<span className={"st"}>{"'grant_type=client_credentials'"}</span>{" https://localhost:9443/oauth2/token"}</a></code></pre></div></div></div><div className={"code panel pdl"}><div className={"codeHeader panelHeader pdl"}><strong>{"Sample cURL"}</strong></div><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb2"} data-syntaxhighlighter-params={"brush: bash; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode bash"}><code className={"sourceCode bash"}><a className={"sourceLine"} id={"cb2-1"} title={"1"}><span className={"ex"}>{"curl"}</span>{" -v -X POST --basic -u rgfKVdnMQnJSSr_pKFTxj3apiwYa:BRebJ0aqfclQB9v7yZwhj0JfW0ga -H "}<span className={"st"}>{"'Content-Type: application/x-www-form-urlencoded;charset=UTF-8'"}</span>{" -k -d "}<span className={"st"}>{"'grant_type=client_credentials'"}</span>{" https://localhost:9443/oauth2/token"}</a></code></pre></div></div></div></td></tr><tr className={"even"}><td>{"Response"}</td><td><div className={"code panel pdl"}><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb3"} data-syntaxhighlighter-params={"brush: java; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode java"}><code className={"sourceCode java"}><a className={"sourceLine"} id={"cb3-1"} title={"1"}>{"{"}<span className={"st"}>{"\"token_type\""}</span>{":"}<span className={"st"}>{"\"Bearer\""}</span>{","}<span className={"st"}>{"\"expires_in\""}</span>{":"}<span className={"dv"}>{"3600"}</span>{","}<span className={"st"}>{"\"access_token\""}</span>{":"}<span className={"st"}>{"\"fbc4e794-23db-3394-b1e5-f2c3e511d01f\""}</span>{"}"}</a></code></pre></div></div></div></td></tr></tbody></table>

### Validate the token

<table><tbody><tr className={"odd"}><td>{"Request"}</td><td><div className={"code panel pdl"}><div className={"codeHeader panelHeader pdl"}><strong>{"Request"}</strong></div><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb1"} data-syntaxhighlighter-params={"brush: bash; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode bash"}><code className={"sourceCode bash"}><a className={"sourceLine"} id={"cb1-1"} title={"1"}><span className={"ex"}>{"curl"}</span>{" -k -u "}<span className={"op"}>{"<"}</span>{"USERNAME"}<span className={"op"}>{">"}</span>{":"}<span className={"op"}>{"<"}</span>{"PASSWORD"}<span className={"op"}>{">"}</span>{" -H "}<span className={"st"}>{"'Content-Type: application/x-www-form-urlencoded'"}</span>{" -X POST --data "}<span className={"st"}>{"'token=<ACCESS_TOKEN>'"}</span>{" https://localhost:9443/oauth2/introspect"}</a></code></pre></div></div></div><div className={"code panel pdl"}><div className={"codeHeader panelHeader pdl"}><strong>{"Sample cURL"}</strong></div><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb2"} data-syntaxhighlighter-params={"brush: bash; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode bash"}><code className={"sourceCode bash"}><a className={"sourceLine"} id={"cb2-1"} title={"1"}><span className={"ex"}>{"curl"}</span>{" -k -u admin:admin -H "}<span className={"st"}>{"'Content-Type: application/x-www-form-urlencoded'"}</span>{" -X POST --data "}<span className={"st"}>{"'token=fbc4e794-23db-3394-b1e5-f2c3e511d01f'"}</span>{" https://localhost:9443/oauth2/introspect"}</a></code></pre></div></div></div><p>{"You can pass the token type as an optional parameter in the request (e.g., "}<code>{"token_type_hint=access_token "}</code>{" or "}<code>{"token_type_hint=refresh_token"}</code>{")."}</p></td></tr><tr className={"even"}><td>{"Response"}</td><td><div className={"code panel pdl"}><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb3"} data-syntaxhighlighter-params={"brush: java; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode java"}><code className={"sourceCode java"}><a className={"sourceLine"} id={"cb3-1"} title={"1"}>{"{"}<span className={"st"}>{"\"exp\""}</span>{":"}<span className={"dv"}>{"1464161608"}</span>{","}<span className={"st"}>{"\"username\""}</span>{":"}<span className={"st"}>{"\"admin@carbon.super\""}</span>{","}<span className={"st"}>{"\"active\""}</span>{":"}<span className={"kw"}>{"true"}</span>{","}<span className={"st"}>{"\"token_type\""}</span>{":"}<span className={"st"}>{"\"Bearer\""}</span>{","}<span className={"st"}>{"\"client_id\""}</span>{":"}<span className={"st"}>{"\"rgfKVdnMQnJSSr_pKFTxj3apiwYa\""}</span>{","}<span className={"st"}>{"\"iat\""}</span>{":"}<span className={"dv"}>{"1464158008"}</span>{"}"}</a></code></pre></div></div></div></td></tr></tbody></table>

### Get a valid token with a scope

<table><tbody><tr className={"odd"}><td>{"Request"}</td><td><div className={"code panel pdl"}><div className={"codeHeader panelHeader pdl"}><strong>{"Request"}</strong></div><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb1"} data-syntaxhighlighter-params={"brush: bash; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode bash"}><code className={"sourceCode bash"}><a className={"sourceLine"} id={"cb1-1"} title={"1"}><span className={"ex"}>{"curl"}</span>{" -v -X POST --basic -u "}<span className={"op"}>{"<"}</span>{"CLIENT_ID"}<span className={"op"}>{">"}</span>{":"}<span className={"op"}>{"<"}</span>{"CLIENT_SECRET"}<span className={"op"}>{">"}</span>{" -H "}<span className={"st"}>{"'Content-Type: application/x-www-form-urlencoded;charset=UTF-8'"}</span>{" -k -d "}<span className={"st"}>{"'grant_type=client_credentials&scope=test1 test2'"}</span>{" https://localhost:9443/oauth2/token"}</a></code></pre></div></div></div><div className={"code panel pdl"}><div className={"codeHeader panelHeader pdl"}><strong>{"Sample cURL"}</strong></div><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb2"} data-syntaxhighlighter-params={"brush: bash; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode bash"}><code className={"sourceCode bash"}><a className={"sourceLine"} id={"cb2-1"} title={"1"}><span className={"ex"}>{"curl"}</span>{" -v -X POST --basic -u rgfKVdnMQnJSSr_pKFTxj3apiwYa:BRebJ0aqfclQB9v7yZwhj0JfW0ga -H "}<span className={"st"}>{"'Content-Type: application/x-www-form-urlencoded;charset=UTF-8'"}</span>{" -k -d "}<span className={"st"}>{"'grant_type=client_credentials&scope=test1 test2'"}</span>{" https://localhost:9443/oauth2/token"}</a></code></pre></div></div></div></td></tr><tr className={"even"}><td>{"Response"}</td><td><div className={"code panel pdl"}><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb3"} data-syntaxhighlighter-params={"brush: java; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode java"}><code className={"sourceCode java"}><a className={"sourceLine"} id={"cb3-1"} title={"1"}>{"{"}<span className={"st"}>{"\"access_token\""}</span>{":"}<span className={"st"}>{"\"34060588-dd4e-36a5-ad93-440cc77a1cfb\""}</span>{","}<span className={"st"}>{"\"scope\""}</span>{":"}<span className={"st"}>{"\"test1 test2\""}</span>{","}<span className={"st"}>{"\"token_type\""}</span>{":"}<span className={"st"}>{"\"Bearer\""}</span>{","}<span className={"st"}>{"\"expires_in\""}</span>{":"}<span className={"dv"}>{"3600"}</span>{"}"}</a></code></pre></div></div></div></td></tr></tbody></table>

### Validate the token

<table><tbody><tr className={"odd"}><td>{"Request"}</td><td><div className={"code panel pdl"}><div className={"codeHeader panelHeader pdl"}><strong>{"Request"}</strong></div><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb1"} data-syntaxhighlighter-params={"brush: bash; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode bash"}><code className={"sourceCode bash"}><a className={"sourceLine"} id={"cb1-1"} title={"1"}><span className={"ex"}>{"curl"}</span>{" -k -u "}<span className={"op"}>{"<"}</span>{"USERNAME"}<span className={"op"}>{">"}</span>{":"}<span className={"op"}>{"<"}</span>{"PASSWORD"}<span className={"op"}>{">"}</span>{" -H "}<span className={"st"}>{"'Content-Type: application/x-www-form-urlencoded'"}</span>{" -X POST --data "}<span className={"st"}>{"'token=<ACCESS_TOKEN>'"}</span>{" https://localhost:9443/oauth2/introspect"}</a></code></pre></div></div></div><div className={"code panel pdl"}><div className={"codeHeader panelHeader pdl"}><strong>{"Sample cURL"}</strong></div><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb2"} data-syntaxhighlighter-params={"brush: bash; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode bash"}><code className={"sourceCode bash"}><a className={"sourceLine"} id={"cb2-1"} title={"1"}><span className={"ex"}>{"curl"}</span>{" -k -u admin:admin -H "}<span className={"st"}>{"'Content-Type: application/x-www-form-urlencoded'"}</span>{" -X POST --data "}<span className={"st"}>{"'token=334060588-dd4e-36a5-ad93-440cc77a1cfb'"}</span>{" https://localhost:9443/oauth2/introspect"}</a></code></pre></div></div></div></td></tr><tr className={"even"}><td>{"Response"}</td><td><div className={"code panel pdl"}><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb3"} data-syntaxhighlighter-params={"brush: java; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode java"}><code className={"sourceCode java"}><a className={"sourceLine"} id={"cb3-1"} title={"1"}>{"{"}<span className={"st"}>{"\"exp\""}</span>{":"}<span className={"dv"}>{"1464161560"}</span>{","}<span className={"st"}>{"\"username\""}</span>{":"}<span className={"st"}>{"\"admin@carbon.super\""}</span>{","}<span className={"st"}>{"\"scope\""}</span>{":"}<span className={"st"}>{"\"test1 test2\""}</span>{","}<span className={"st"}>{"\"active\""}</span>{":"}<span className={"kw"}>{"true"}</span>{","}<span className={"st"}>{"\"token_type\""}</span>{":"}<span className={"st"}>{"\"Bearer\""}</span>{","}<span className={"st"}>{"\"client_id\""}</span>{":"}<span className={"st"}>{"\"rgfKVdnMQnJSSr_pKFTxj3apiwYa\""}</span>{","}<span className={"st"}>{"\"iat\""}</span>{":"}<span className={"dv"}>{"1464157960"}</span>{"}"}</a></code></pre></div></div></div></td></tr></tbody></table>

### Invalid token

If the token that you used is invalid, you get the following response:

```java
{'active':false}
```

### Empty token

If you leave the token parameter empty as shown below, you get the 
following response :

<table><tbody><tr className={"odd"}><td>{"Request"}</td><td><div className={"code panel pdl"}><div className={"codeHeader panelHeader pdl"}><strong>{"Request"}</strong></div><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb1"} data-syntaxhighlighter-params={"brush: bash; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode bash"}><code className={"sourceCode bash"}><a className={"sourceLine"} id={"cb1-1"} title={"1"}><span className={"ex"}>{"curl"}</span>{" -k -u "}<span className={"op"}>{"<"}</span>{"USERNAME"}<span className={"op"}>{">"}</span>{":"}<span className={"op"}>{"<"}</span>{"PASSWORD"}<span className={"op"}>{">"}</span>{" -H "}<span className={"st"}>{"'Content-Type: application/x-www-form-urlencoded'"}</span>{" -X POST --data "}<span className={"st"}>{"'token='"}</span>{" https://localhost:9443/oauth2/introspect"}</a></code></pre></div></div></div><div className={"code panel pdl"}><div className={"codeHeader panelHeader pdl"}><strong>{"Sample cURL"}</strong></div><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb2"} data-syntaxhighlighter-params={"brush: bash; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode bash"}><code className={"sourceCode bash"}><a className={"sourceLine"} id={"cb2-1"} title={"1"}>{" "}<span className={"ex"}>{"curl"}</span>{" -k -u admin:admin -H "}<span className={"st"}>{"'Content-Type: application/x-www-form-urlencoded'"}</span>{" -X POST --data "}<span className={"st"}>{"'token='"}</span>{" https://localhost:9443/oauth2/introspect"}</a></code></pre></div></div></div></td></tr><tr className={"even"}><td>{"Response"}</td><td><div className={"code panel pdl"}><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb3"} data-syntaxhighlighter-params={"brush: java; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode java"}><code className={"sourceCode java"}><a className={"sourceLine"} id={"cb3-1"} title={"1"}>{"{'error': 'Invalid input'}"}</a></code></pre></div></div></div></td></tr></tbody></table>


## Invoking the endpoint for tenants

Use the following cURL commands given in the following sections to
invoke the OAuth introspection endpoint for tenant users.

:::note


-   For requests that require
    `          CLIENT_ID:CLIENT_SECRET         `, use the client ID and
    client secret of the OAuth service provider. For more information on
    creating an OAuth service provider, see [Configuring Inbound
    Authentication for a Service
    Provider](../../learn/configuring-inbound-authentication-for-a-service-provider)
    .
-   For requests that require
    `           USERNAME@TENANT_DOMAIN:PASSWORD          `, by default
    you can use credentials of any user with
    "/permission/admin/manage/identity/applicationmgt/view" permissions.

:::
    

### Get a valid token

<table><tbody><tr className={"odd"}><td>{"Request"}</td><td><div className={"code panel pdl"}><div className={"codeHeader panelHeader pdl"}><strong>{"Request"}</strong></div><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb1"} data-syntaxhighlighter-params={"brush: bash; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode bash"}><code className={"sourceCode bash"}><a className={"sourceLine"} id={"cb1-1"} title={"1"}><span className={"ex"}>{"curl"}</span>{" -v -X POST --basic -u "}<span className={"op"}>{"<"}</span>{"CLIENT_ID"}<span className={"op"}>{">"}</span>{":"}<span className={"op"}>{"<"}</span>{"CLIENT_SECRET"}<span className={"op"}>{">"}</span>{" -H "}<span className={"st"}>{"'Content-Type: application/x-www-form-urlencoded;charset=UTF-8'"}</span>{" -k -d "}<span className={"st"}>{"'grant_type=client_credentials'"}</span>{" https://localhost:9443/oauth2/token"}</a></code></pre></div></div></div><div className={"code panel pdl"}><div className={"codeHeader panelHeader pdl"}><strong>{"Sample cURL"}</strong></div><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb2"} data-syntaxhighlighter-params={"brush: bash; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode bash"}><code className={"sourceCode bash"}><a className={"sourceLine"} id={"cb2-1"} title={"1"}><span className={"ex"}>{"curl"}</span>{" -v -X POST --basic -u rgfKVdnMQnJSSr_pKFTxj3apiwYa:BRebJ0aqfclQB9v7yZwhj0JfW0ga -H "}<span className={"st"}>{"'Content-Type: application/x-www-form-urlencoded;charset=UTF-8'"}</span>{" -k -d "}<span className={"st"}>{"'grant_type=client_credentials'"}</span>{" https://localhost:9443/oauth2/token"}</a></code></pre></div></div></div></td></tr><tr className={"even"}><td>{"Response"}</td><td><div className={"code panel pdl"}><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb3"} data-syntaxhighlighter-params={"brush: java; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode java"}><code className={"sourceCode java"}><a className={"sourceLine"} id={"cb3-1"} title={"1"}>{"{"}<span className={"st"}>{"\"token_type\""}</span>{":"}<span className={"st"}>{"\"Bearer\""}</span>{","}<span className={"st"}>{"\"expires_in\""}</span>{":"}<span className={"dv"}>{"3600"}</span>{","}<span className={"st"}>{"\"access_token\""}</span>{":"}<span className={"st"}>{"\"fbc4e794-23db-3394-b1e5-f2c3e511d01f\""}</span>{"}"}</a></code></pre></div></div></div></td></tr></tbody></table>

### Validate the token

<table><tbody><tr className={"odd"}><td>{"Request"}</td><td><p>{"You can use any of the request formats given below:"}</p><div className={"code panel pdl"}><div className={"codeHeader panelHeader pdl"}><strong>{"Request"}</strong></div><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb1"} data-syntaxhighlighter-params={"brush: bash; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode bash"}><code className={"sourceCode bash"}><a className={"sourceLine"} id={"cb1-1"} title={"1"}><span className={"ex"}>{"curl"}</span>{" -k -u "}<span className={"op"}>{"<"}</span>{"USERNAME"}<span className={"op"}>{">"}</span>{"@"}<span className={"op"}>{"<"}</span>{"TENAND_DOMAIN"}<span className={"op"}>{">"}</span>{":"}<span className={"op"}>{"<"}</span>{"PASSWORD"}<span className={"op"}>{">"}</span>{" -H "}<span className={"st"}>{"'Content-Type: application/x-www-form-urlencoded'"}</span>{" -X POST --data "}<span className={"st"}>{"'token=<ACCESS_TOKEN>'"}</span>{" https://localhost:9443/t/"}<span className={"op"}>{"<"}</span>{"TENANT_DOMAIN"}<span className={"op"}>{">"}</span>{"/oauth2/introspect"}</a></code></pre></div></div></div><p>{"Or"}</p><div className={"code panel pdl"}><div className={"codeHeader panelHeader pdl"}><strong>{"Request"}</strong></div><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb2"} data-syntaxhighlighter-params={"brush: java; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode java"}><code className={"sourceCode java"}><a className={"sourceLine"} id={"cb2-1"} title={"1"}>{"curl -v -k -H 'Authorization: Basic <"}<span className={"fu"}>{"BASE64ENCODED"}</span>{"(USERNAME"}<span className={"at"}>{"@TENAND_DOMAIN"}</span>{":PASSWORD)>' -H 'Content-"}<span className={"bu"}>{"Type"}</span>{": application/x-www-form-urlencoded' -X POST --data 'token=<ACCESS_TOKEN>' https:"}<span className={"co"}>{"//localhost:9443/t/<TENANT_DOMAIN>/oauth2/introspect"}</span></a></code></pre></div><p>{"You can pass the token type as an optional parameter in the request (e.g., "}<code>{"token_type_hint=access_token "}</code>{" or "}<code>{"token_type_hint=refresh_token"}</code>{")."}</p></div></div><div className={"code panel pdl"}><div className={"codeHeader panelHeader pdl"}><strong>{"Sample cURL"}</strong></div><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb3"} data-syntaxhighlighter-params={"brush: java; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode java"}><code className={"sourceCode java"}><a className={"sourceLine"} id={"cb3-1"} title={"1"}>{"curl -k -u admin"}<span className={"at"}>{"@foo"}</span>{"."}<span className={"fu"}>{"com"}</span>{":admin -H 'Content-"}<span className={"bu"}>{"Type"}</span>{": application/x-www-form-urlencoded' -X POST --data 'token=fbc4e794-23db-"}<span className={"dv"}>{"3394"}</span>{"-b1e5-f2c3e511d01f' https:"}<span className={"co"}>{"//localhost:9443/t/foo.com/oauth2/introspect"}</span></a></code></pre></div></div></div></td></tr><tr className={"even"}><td>{"Response"}</td><td><div className={"code panel pdl"}><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb4"} data-syntaxhighlighter-params={"brush: java; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode java"}><code className={"sourceCode java"}><a className={"sourceLine"} id={"cb4-1"} title={"1"}>{"{"}<span className={"st"}>{"\"active\""}</span>{":"}<span className={"kw"}>{"true"}</span>{","}<span className={"st"}>{"\"token_type\""}</span>{":"}<span className={"st"}>{"\"Bearer\""}</span>{","}<span className={"st"}>{"\"exp\""}</span>{":"}<span className={"dv"}>{"1517922556"}</span>{","}<span className={"st"}>{"\"iat\""}</span>{":"}<span className={"dv"}>{"1517918956"}</span>{","}<span className={"st"}>{"\"client_id\""}</span>{":"}<span className={"st"}>{"\"okaN2IXAsLx5SBH9Los1C6zX1RIa\""}</span>{","}<span className={"st"}>{"\"username\""}</span>{":"}<span className={"st"}>{"\"admin@foo.com”}"}</span></a></code></pre></div></div></div></td></tr></tbody></table>

### Get a valid token with a scope

<table><tbody><tr className={"odd"}><td>{"Request"}</td><td><div className={"code panel pdl"}><div className={"codeHeader panelHeader pdl"}><strong>{"Request"}</strong></div><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb1"} data-syntaxhighlighter-params={"brush: bash; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode bash"}><code className={"sourceCode bash"}><a className={"sourceLine"} id={"cb1-1"} title={"1"}><span className={"ex"}>{"curl"}</span>{" -v -X POST --basic -u "}<span className={"op"}>{"<"}</span>{"CLIENT_ID"}<span className={"op"}>{">"}</span>{":"}<span className={"op"}>{"<"}</span>{"CLIENT_SECRET"}<span className={"op"}>{">"}</span>{" -H "}<span className={"st"}>{"'Content-Type: application/x-www-form-urlencoded;charset=UTF-8'"}</span>{" -k -d "}<span className={"st"}>{"'grant_type=client_credentials&scope=test1 test2'"}</span>{" https://localhost:9443/oauth2/token"}</a></code></pre></div></div></div><div className={"code panel pdl"}><div className={"codeHeader panelHeader pdl"}><strong>{"Sample cURL"}</strong></div><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb2"} data-syntaxhighlighter-params={"brush: bash; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode bash"}><code className={"sourceCode bash"}><a className={"sourceLine"} id={"cb2-1"} title={"1"}><span className={"ex"}>{"curl"}</span>{" -v -X POST --basic -u rgfKVdnMQnJSSr_pKFTxj3apiwYa:BRebJ0aqfclQB9v7yZwhj0JfW0ga -H "}<span className={"st"}>{"'Content-Type: application/x-www-form-urlencoded;charset=UTF-8'"}</span>{" -k -d "}<span className={"st"}>{"'grant_type=client_credentials&scope=test1 test2'"}</span>{" https://localhost:9443/oauth2/token"}</a></code></pre></div></div></div></td></tr><tr className={"even"}><td>{"Response"}</td><td><div className={"code panel pdl"}><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb3"} data-syntaxhighlighter-params={"brush: java; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode java"}><code className={"sourceCode java"}><a className={"sourceLine"} id={"cb3-1"} title={"1"}>{"{"}<span className={"st"}>{"\"access_token\""}</span>{":"}<span className={"st"}>{"\"34060588-dd4e-36a5-ad93-440cc77a1cfb\""}</span>{","}<span className={"st"}>{"\"scope\""}</span>{":"}<span className={"st"}>{"\"test1\""}</span>{","}<span className={"st"}>{"\"token_type\""}</span>{":"}<span className={"st"}>{"\"Bearer\""}</span>{","}<span className={"st"}>{"\"expires_in\""}</span>{":"}<span className={"dv"}>{"3600"}</span>{"}"}</a></code></pre></div></div></div></td></tr></tbody></table>

### Validate the token

<table><tbody><tr className={"odd"}><td>{"Request"}</td><td><p>{"You can use any of the request formats given below:"}</p><div className={"code panel pdl"}><div className={"codeHeader panelHeader pdl"}><strong>{"Request"}</strong></div><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb1"} data-syntaxhighlighter-params={"brush: bash; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode bash"}><code className={"sourceCode bash"}><a className={"sourceLine"} id={"cb1-1"} title={"1"}><span className={"ex"}>{"curl"}</span>{" -k -u "}<span className={"op"}>{"<"}</span>{"USERNAME"}<span className={"op"}>{">"}</span>{"@"}<span className={"op"}>{"<"}</span>{"TENANT_DOMAIN"}<span className={"op"}>{">"}</span>{":"}<span className={"op"}>{"<"}</span>{"PASSWORD"}<span className={"op"}>{">"}</span>{" -H "}<span className={"st"}>{"'Content-Type: application/x-www-form-urlencoded'"}</span>{" -X POST --data "}<span className={"st"}>{"'token=<ACCESS_TOKEN>'"}</span>{" https://localhost:9443/t/"}<span className={"op"}>{"<"}</span>{"TENANT_DOMAIN"}<span className={"op"}>{">"}</span>{"/oauth2/introspect"}</a></code></pre></div></div></div><p>{"Or"}</p><div className={"code panel pdl"}><div className={"codeHeader panelHeader pdl"}><strong>{"Request"}</strong></div><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb2"} data-syntaxhighlighter-params={"brush: java; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode java"}><code className={"sourceCode java"}><a className={"sourceLine"} id={"cb2-1"} title={"1"}>{"curl -v -k -H 'Authorization: Basic <"}<span className={"fu"}>{"BASE64ENCODED"}</span>{"(USERNAME"}<span className={"at"}>{"@TENANT_DOMAIN"}</span>{":PASSWORD)>' -H 'Content-"}<span className={"bu"}>{"Type"}</span>{": application/x-www-form-urlencoded' -X POST --data 'token=<ACCESS_TOKEN>' https:"}<span className={"co"}>{"//localhost:9443/t/<TENANT_DOMAIN>/oauth2/introspect"}</span></a></code></pre></div></div></div><div className={"code panel pdl"}><div className={"codeHeader panelHeader pdl"}><strong>{"Sample cURL"}</strong></div><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb3"} data-syntaxhighlighter-params={"brush: bash; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode bash"}><code className={"sourceCode bash"}><a className={"sourceLine"} id={"cb3-1"} title={"1"}><span className={"ex"}>{"curl"}</span>{" -k -u admin@foo.com:admin -H "}<span className={"st"}>{"'Content-Type: application/x-www-form-urlencoded'"}</span>{" -X POST --data "}<span className={"st"}>{"'token=334060588-dd4e-36a5-ad93-440cc77a1cfb'"}</span>{" https://localhost:9443/t/foo.com/oauth2/introspect"}</a></code></pre></div></div></div></td></tr><tr className={"even"}><td>{"Response"}</td><td><div className={"code panel pdl"}><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb4"} data-syntaxhighlighter-params={"brush: java; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode java"}><code className={"sourceCode java"}><a className={"sourceLine"} id={"cb4-1"} title={"1"}>{"{"}<span className={"st"}>{"\"scope\""}</span>{":"}<span className={"st"}>{"\"1 test\""}</span>{","}<span className={"st"}>{"\"active\""}</span>{":"}<span className={"kw"}>{"true"}</span>{","}<span className={"st"}>{"\"token_type\""}</span>{":"}<span className={"st"}>{"\"Bearer\""}</span>{","}<span className={"st"}>{"\"exp\""}</span>{":"}<span className={"dv"}>{"1517922663"}</span>{","}<span className={"st"}>{"\"iat\""}</span>{":"}<span className={"dv"}>{"1517919063"}</span>{","}<span className={"st"}>{"\"client_id\""}</span>{":"}<span className={"st"}>{"\"okaN2IXAsLx5SBH9Los1C6zX1RIa\""}</span>{","}<span className={"st"}>{"\"username\""}</span>{":"}<span className={"st"}>{"\"admin@foo.com\""}</span>{"}"}</a></code></pre></div></div></div></td></tr></tbody></table>

### Invalid token

If the token that you used is invalid, you get the following response:

  

**Response**

```java
{'active':false}
```

### Empty token

If you leave the token parameter empty as shown below, you get the
following response:

<table><tbody><tr className={"odd"}><td>{"Request"}</td><td><p>{"Example:"}</p><div className={"code panel pdl"}><div className={"codeHeader panelHeader pdl"}><strong>{"Request"}</strong></div><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb1"} data-syntaxhighlighter-params={"brush: bash; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode bash"}><code className={"sourceCode bash"}><a className={"sourceLine"} id={"cb1-1"} title={"1"}><span className={"ex"}>{"curl"}</span>{" -k -u "}<span className={"op"}>{"<"}</span>{"USERNAME"}<span className={"op"}>{">"}</span>{"@"}<span className={"op"}>{"<"}</span>{"TENANT_DOMAIN"}<span className={"op"}>{">"}</span>{":"}<span className={"op"}>{"<"}</span>{"PASSWORD"}<span className={"op"}>{">"}</span>{" -H "}<span className={"st"}>{"'Content-Type: application/x-www-form-urlencoded'"}</span>{" -X POST --data "}<span className={"st"}>{"'token='"}</span>{" https://localhost:9443/t/"}<span className={"op"}>{"<"}</span>{"TENANT_DOMAIN"}<span className={"op"}>{">"}</span>{"/oauth2/introspect"}</a></code></pre></div></div></div><div className={"code panel pdl"}><div className={"codeHeader panelHeader pdl"}><strong>{"Sample cURL"}</strong></div><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb2"} data-syntaxhighlighter-params={"brush: bash; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode bash"}><code className={"sourceCode bash"}><a className={"sourceLine"} id={"cb2-1"} title={"1"}>{" "}<span className={"ex"}>{"curl"}</span>{" -k -u admin:admin -H "}<span className={"st"}>{"'Content-Type: application/x-www-form-urlencoded'"}</span>{" -X POST --data "}<span className={"st"}>{"'token='"}</span>{" https://localhost:9443/oauth2/introspect"}</a></code></pre></div></div></div></td></tr><tr className={"even"}><td>{"Response"}</td><td><div className={"code panel pdl"}><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb3"} data-syntaxhighlighter-params={"brush: java; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode java"}><code className={"sourceCode java"}><a className={"sourceLine"} id={"cb3-1"} title={"1"}>{"{'error': 'Invalid input'}"}</a></code></pre></div></div></div></td></tr></tbody></table>

:::tip

Above samples only explains validating a token obtained for
Client credentials grant using the **introspect endpoint**. Similarly, you may [invoke introspection endpoint](#validate-the-token) with a token
obtained from any other grant type as well.

:::
