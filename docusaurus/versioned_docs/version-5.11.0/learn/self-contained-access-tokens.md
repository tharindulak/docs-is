---
title: Self-contained Access Tokens
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/5.11.0/docs/learn/self-contained-access-tokens.md
---

# Self-contained Access Tokens

Access tokens are credentials used to access protected resources.
Typically, an access token is a string representing an authorization
issued to the client. The string is usually opaque to the client.

The [OAuth 2.0](https://tools.ietf.org/html/rfc6749) specification does
not mandate any particular implementation for access tokens but it
[mentions](https://tools.ietf.org/html/rfc6749#section-1.4) two possible
strategies.

1.  The access token is an identifier that is hard to guess. For
    example, a randomly generated string of sufficient length, that the
    server handling the protected resource can use to lookup the
    associated authorization information.
2.  The access token self-contains the authorization information in a
    manner that can be verified. For example, by encoding authorization
    information along with a signature into the token.

So by default, a UUID is issued as an access token in WSO2 Identity
Server, which is of the first type above. But, it also can be configured
to issue a self-contained access token, which is of the second type
above.

### Why do we need self-contained access tokens?

When short string identifiers are used as access tokens, a network
request to the Authorization server is required to retrieve the
authorization information associated with each access token. But with
self-contained access tokens there is no need for a network call to
retrieve the authorization information, as it’s self-contained. Thus,
access token processing may be significantly quicker and more efficient.
However, when it comes to token revocation self-contained access tokens
lag, whereas access tokens with string identifiers can be revoked with
almost immediate effect. The common practice is to have a short
expiration time with self-contained access tokens, but that may result
in more refresh token requests at the Authorization server.

### Configuring WSO2 Identity Server to issue self-contained access tokens

WSO2 Identity Server needs to be configured to issue above explained
self-contained JWT access tokens as below.

1.  Add the following configuration property to the `deployment.toml` file in the `<IS_HOME>/repository/conf` folder.
    ```toml
    [oauth.token_generation]
    access_token_type= "self_contained"
    ```

2.  Restart the server.
3.  Configure an [OAuth service
    provider](../../learn/adding-and-configuring-a-service-provider).
4.  Initiate an access token request to the WSO2 Identity Server, over a
    known [grant type](../../learn/oauth-2.0-grant-types). For example, the
    following cURL command illustrates the syntax of an access token
    request that can be initiated over the [Resource Owner Password
    Credential](../../learn/resource-owner-password-credentials-grant) grant type.

    <table><tbody><tr className={"odd"}><td>{"cURL command"}</td><td><div className={"content-wrapper"}><div className={"code panel pdl"}><div className={"codeHeader panelHeader pdl"}><strong>{"Request"}</strong></div><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb1"} data-syntaxhighlighter-params={"brush: powershell; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode powershell"}><code className={"sourceCode powershell"}><a className={"sourceLine"} id={"cb1-1"} title={"1"}><span className={"fu"}>{"curl"}</span>{" -u <CLIENT_ID>:<CLIENT_SECRET> -k -d "}<span className={"st"}>{"\"grant_type=password&username=<USERNAME>&password=<PASSWORD>\""}</span>{" -H "}<span className={"st"}>{"\"Content-Type:application/x-www-form-urlencoded\""}</span>{" https://<IS_HOST>:<IS_HTTPS_PORT>/oauth2/token"}</a></code></pre></div></div></div><ul><li>{"Navigate to your service provider, expand Inbound Authenitcaion Configurations and expand OAuth/OpenID Connect Configuration. "}<ul><li>{"Copy the OAuth Client Key as the value for "}<code>{" <CLIENT_ID> "}</code>{" ."}</li><li>{"Copy the OAuth Client Secret as the value for "}<code>{" <CLIENT_SECRET> "}</code>{" ."}</li></ul></li><li>{"Enter the username and password of the user you want to get the token as the value for "}<code>{" <USERNAME> "}</code>{" and "}<code>{" <PASSWORD> "}</code>{" respectively."}</li><li>{"By default, "}<code>{" <IS_HOST> "}</code>{" is "}<code>{" localhost. "}</code>{" However, if you are using a public IP, the respective IP address or domain needs to be specified."}</li><li>{"By default, "}<code>{" <IS_HTTPS_PORT> "}</code>{" has been set to 9443. However, if the port offset has been incremented by "}<code>{" n "}</code>{", the default port value needs to be incremented by "}<code>{" n "}</code>{" ."}</li></ul><p>{"Example:"}</p><div className={"code panel pdl"}><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb2"} data-syntaxhighlighter-params={"brush: java; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode java"}><code className={"sourceCode java"}><a className={"sourceLine"} id={"cb2-1"} title={"1"}>{"curl -u liXJsel4bJ76arbg3DXC3rU4w60a:wQEYq83njU29ZFbpQWdZsUlXcnga -k -d "}<span className={"st"}>{"\"grant_type=password&username=testuser2&password=testuser2 -H \""}</span>{"Content-"}<span className={"bu"}>{"Type"}</span>{":application/x-www-form-urlencoded"}<span className={"st"}>{"\" https://localhost:9443/oauth2/token"}</span></a></code></pre></div></div></div></div></td></tr><tr className={"even"}><td>{"Response"}</td><td><div className={"content-wrapper"}><p>{"In response, the self-contained JWT access token will be returned as shown below."}</p><div className={"code panel pdl"}><div className={"codeHeader panelHeader pdl"}><strong>{"Response"}</strong></div><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb3"} data-syntaxhighlighter-params={"brush: java; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode java"}><code className={"sourceCode java"}><a className={"sourceLine"} id={"cb3-1"} title={"1"}>{"{  "}</a>{"\n    "}<a className={"sourceLine"} id={"cb3-2"} title={"2"}><span className={"st"}>{"\"access_token\""}</span>{":"}<span className={"st"}>{"\"eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJhZG1pbiIsImF1ZCI6WyJkZDlVM1FGd05GMlBRZnZsSHpUY1NTdU5DMndhIl0sImF6cCI6ImRkOVUzUUZ3TkYyUFFmdmxIelRjU1N1TkMyd2EiLCJpc3"}</span></a>{"\n    "}<a className={"sourceLine"} id={"cb3-3"} title={"3"}>{"MiOiJodHRwczpcL1wvbG9jYWxob3N0Ojk0NDNcL29hdXRoMlwvdG9rZW4iLCJleHAiOjE1MTA4MjQ5MzUsImlhdCI6MTUxMDgyMTMzNSwianRpIjoiNDA1YjRkNGUtODUwMS00ZTFhLWExMzgtZWQ4NDU1Y2QxZDQ3I"}</a>{"\n    "}<a className={"sourceLine"} id={"cb3-4"} title={"4"}>{"n0."}<span className={"fu"}>{"FCk3Wo8DnFEHb02JCd9BWAHQ48BBt3n2YLQV6TpLMpFvTRNCZJAA"}</span>{"-aEH4LrE7oVejvGd7YWGDy2Vzb7x-Bpg7yMYxozUerCkMy_F4Iw_xctgEJ3WF_TTJFhISGNoWlFXspM5d9EQvMvk0JxAovhE0HfXv5GCosGy"}</a>{"\n    "}<a className={"sourceLine"} id={"cb3-5"} title={"5"}>{"-0oT7ShQrwZLBIwE9d0ceUcmly42dvDZSsqHDIzPjrFzvpXwbZqq_sRFnh6MHlmmug7t1UCs85caoLhfSweaT0z7ED8P2Tsg_HgmnaaeDapszG6LckeBglqYwbRHy6X6LAcJfAkkwAlqrU0Vu4azsuE8BsLPKMYzu9Ze"}</a>{"\n    "}<a className={"sourceLine"} id={"cb3-6"} title={"6"}>{"CoHdLHYdtz-I0yKQ"}<span className={"st"}>{"\","}</span></a>{"\n    "}<a className={"sourceLine"} id={"cb3-7"} title={"7"}>{"   "}<span className={"st"}>{"\"refresh_token\""}</span>{":"}<span className={"st"}>{"\"5974cdcc-865e-3144-82c5-4f147ddcb519\""}</span>{","}</a>{"\n    "}<a className={"sourceLine"} id={"cb3-8"} title={"8"}>{"   "}<span className={"st"}>{"\"token_type\""}</span>{":"}<span className={"st"}>{"\"Bearer\""}</span>{","}</a>{"\n    "}<a className={"sourceLine"} id={"cb3-9"} title={"9"}>{"   "}<span className={"st"}>{"\"expires_in\""}</span>{":"}<span className={"dv"}>{"589"}</span></a>{"\n    "}<a className={"sourceLine"} id={"cb3-10"} title={"10"}>{"}"}</a></code></pre></div></div></div><p>{"The access token you receive is a signed "}<a href={"https://tools.ietf.org/html/rfc7519"}>{"JSON Web Token (JWT)"}</a>{" . Use a JWT decoder to decode the access token and you are able to see the payload of the token that includes the following JWT claims:"}</p><div className={"table-wrap"}><table><thead><tr className={"header"}><th>{"Claim Name"}</th><th>{"Type"}</th><th>{"Claim Value"}</th></tr></thead><tbody><tr className={"odd"}><td>{"iss"}</td><td>{"string"}</td><td>{"The issuer of the JWT. The ' "}<em>{"Identity Provider Entity Id"}</em>{" ' value of the OAuth2/OpenID Connect Inbound Authentication configuration of the "}<a href={"../../learn/adding-and-configuring-an-identity-provider"}>{"Resident Identity Provider"}</a>{" is returned here."}</td></tr><tr className={"even"}><td>{"aud"}</td><td>{"string array"}</td><td>{"The token audience list. The client identifier of the OAuth clients that the JWT is intended for, is sent herewith."}</td></tr><tr className={"odd"}><td>{"azp"}</td><td>{"string"}</td><td>{"The autorized party for which the token is issued to. The client identifier of the OAuth client that the token is issued for, is sent herewith."}</td></tr><tr className={"even"}><td>{"iat"}</td><td>{"integer"}</td><td>{"The token issue time."}</td></tr><tr className={"odd"}><td>{"exp"}</td><td>{"integer"}</td><td>{"The token expiration time."}</td></tr><tr className={"even"}><td>{"jti"}</td><td>{"string"}</td><td>{"Unique identifier for the JWT token."}</td></tr></tbody></table></div><div><p>{"In addition, a user claims can be obtained by an authorized user over this JWT as per "}<a href={"http://openid.net/specs/openid-connect-core-1_0.html#Claims"}>{"OpenID Connect claim"}</a>{" configurations, by "}<a href={"../../learn/configuring-claims-for-a-service-provider"}>{"configuring requested user claims"}</a>{" in the OAuth service provider. After configuring the service provider you can run the cURL command given below by providing the required details."}</p><div className={"code panel pdl"}><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb4"} data-syntaxhighlighter-params={"brush: java; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode java"}><code className={"sourceCode java"}><a className={"sourceLine"} id={"cb4-1"} title={"1"}>{"curl -u <CLIENT_ID>:<CLIENT_SECRET> -k -d "}<span className={"st"}>{"\"grant_type=password&username=<USERNAME>&password=<PASSWORD>&scope=openid\""}</span>{" -H "}<span className={"st"}>{"\"Content-Type:application/x-www-form-urlencoded\""}</span>{" https:"}<span className={"co"}>{"//<IS_HOST>:<IS_HTTPS_PORT>/oauth2/token"}</span></a></code></pre></div></div></div></div></div></td></tr></tbody></table>
