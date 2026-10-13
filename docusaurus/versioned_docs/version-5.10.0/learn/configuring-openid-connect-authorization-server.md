---
title: Configuring OpenID Connect Authorization Server
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/5.10.0/docs/learn/configuring-openid-connect-authorization-server.md
---

# Configuring OpenID Connect Authorization Server

This topic guides you through configuring the OpenID Connect
Authorization Server by configuring the deployment.toml file found in the
`         <IS_HOME>/repository/conf/      ` directory.

```toml
[oauth.oidc.extensions]
id_token_builder= org.wso2.carbon.identity.openidconnect.DefaultIDTokenBuilder
claim_callback_handler= org.wso2.carbon.identity.openidconnect.SAMLAssertionClaimsCallback
user_info_claim_retriever= org.wso2.carbon.identity.oauth.endpoint.user.impl.UserInfoUserStoreClaimRetriever
user_info_access_token_validator= org.wso2.carbon.identity.oauth.endpoint.user.impl.UserInfoISAccessTokenValidator

[oauth.oidc]
user_info.response_type= "json"

[oauth.oidc.id_token]
issuer= ${carbon.protocol}://${carbon.host}:${carbon.management.port}/oauth2/token

[oauth.oidc.token_validation]
id_token_validity= 3600

[oauth]
consent_prompt= true

[authentication]
sign_auth_response_with_tenant_of= "user"
```

The following sub elements are the important configurations for
configuring the OpenID Connect Authorization Server.

<table><thead><tr className={"header"}><th>{"Element"}</th><th>{"Description"}</th></tr></thead><tbody><tr className={"odd"}><td><code>{" issuer "}</code></td><td>{"The value of "}<code>{" issuer "}</code>{" of the "}<code>{" IDToken "}</code>{" . This should be changed according to the deployment values."}</td></tr><tr className={"even"}><td><code>{" id_token_validity "}</code></td><td>{"The expiration value of the "}<code>{" IDToken "}</code>{" in seconds."}</td></tr><tr className={"odd"}><td><code>{" claim_callback_handler "}</code></td><td>{"This can be used to return extra custom claims with the "}<code>{" IDToken "}</code>{" . You can implement a claims call back handler to push the custom claims to the "}<code>{" IDToken "}</code>{" . This class needs to implement the interface "}<code>{" CustomClaimsCallbackHandler "}</code>{" . You can find the default implementation "}<a href={"https://svn.wso2.org/repos/wso2/carbon/platform/branches/turing/components/identity/org.wso2.carbon.identity.oauth/4.2.0/src/main/java/org/wso2/carbon/identity/openidconnect/SAMLAssertionClaimsCallback.java"}>{"here"}</a>{" as a reference."}</td></tr><tr className={"even"}><td><code>{" user_info_claim_retriever "}</code></td><td>{"Defines the class which builds the claims for the User Info Endpoint's response. This class needs to implement the interface "}<code>{" UserInfoClaimRetriever "}</code>{" . The default implementation can be found "}<a href={"https://svn.wso2.org/repos/wso2/carbon/platform/branches/turing/components/identity/org.wso2.carbon.identity.oauth.endpoint/4.2.0/src/main/java/org/wso2/carbon/identity/oauth/endpoint/user/impl/UserInfoUserStoreClaimRetriever.java"}>{"here"}</a>{" as a reference."}</td></tr><tr className={"odd"}><td><code>{" user_info.response_type= "}</code></td><td><div className={"content-wrapper"}><p>{"The value that is set to get JWT response from user info endpoint. Change the value as follows:"}</p><div className={"code panel pdl"}><div className={"codeContent panelContent pdl"}><div className={"sourceCode"} id={"cb1"} data-syntaxhighlighter-params={"brush: xml; gutter: false; theme: Confluence"} data-theme={"Confluence"}><pre className={"sourceCode xml"}><code className={"sourceCode xml"}><a className={"sourceLine"} id={"cb1-1"} title={"1"}><span className={"kw"}>{"user_info.response_type= \"json\""}</span></a></code></pre></div></div></div></div></td></tr></tbody></table>
