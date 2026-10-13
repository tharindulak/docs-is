---
title: Configure auth properties
mkdocs_template: complete-guide
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.1.0/docs/complete-guides/dotnet/configure-authentication-properties.md
---

The information that was noted in step 3 can now be utilized in the created .NET application.

For the purpose of this guide, these properties will be added to the `/Properties/launchSettings.json` file. You can, however, use any other configuration source according to your preference. The following are the properties that you need to configure.

- Authorization Endpoint
- Token Endpoint
- JWKS URI
- Logout Endpoint
- Authority
- Client ID
- Client Secret
- Metadata address

An example configuration is shown below (placeholders have to be replaced with the actual values). Make sure to add the configuration properties to the profile that is utilized for running the application. In this case, we will be using only the `https` profile. The complete `/Properties/launchSettings.json` file we will be utilizing is shown below.

```json title="launchSettings.json" {12-19}
{
  "$schema": "https://json.schemastore.org/launchsettings.json",
  "profiles": {
    "https": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "inspectUri": "{wsProtocol}://{url.hostname}:{url.port}/_framework/debug/ws-proxy?browser={browserInspectUri}",
      "applicationUrl": "https://localhost:5001;http://localhost:5000",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development",
        "AUTHORIZATION_ENDPOINT": "https://localhost:9443/oauth2/authorize",
        "TOKEN_ENDPOINT": "https://localhost:9443/oauth2/token",
        "JWKS_URI": "https://localhost:9443/oauth2/jwks",
        "LOGOUT_URI": "https://localhost:9443/oidc/logout",
        "AUTHORITY": "https://localhost:9443",
        "CLIENT_ID": "<client_id>",
        "CLIENT_SECRET": "<client_secret>",
        "METADATA_ADDRESS": "https://localhost:9443/oauth2/token/.well-known/openid-configuration"
      }
    },
  }
}
```

## Add authentication package

As the next step we have to add `Microsoft.AspNetCore.Authentication.OpenIdConnect` package to our application. This package allows your .NET app to authenticate users using an OIDC identity providers such as WSO2 Identity Platform and WSO2 Identity Server and also manage authentication tokens.

When adding `Microsoft.AspNetCore.Authentication.OpenIdConnect` package, make sure to pick the right version as per your .Net SDK installation.

<Tabs>
<TabItem value="tab-0" label=".Net 8 SDK ">


```bash
dotnet add package Microsoft.AspNetCore.Authentication.OpenIdConnect --version 8.0.0
```

</TabItem>
<TabItem value="tab-1" label=".Net 9 SDK">


```bash
dotnet add package Microsoft.AspNetCore.Authentication.OpenIdConnect --version 9.0.0
```

</TabItem>
</Tabs>

Now that we have configured the authentication properties, we can proceed to implement the authentication logic in the .NET application.
