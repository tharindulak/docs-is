---
title: Generate tokens for organization applications
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.1.0/docs/guides/organization-management/generate-tokens-for-organization-apps.md
---

# Generate tokens for organization applications

After you authorize applications to API resources and assign users to the appropriate roles, you can generate tokens to access the protected resources. Organization applications support the following OAuth 2.0 grant types to generate tokens and issue scopes.



## Password grant

Use the following steps to use the user's credentials to get an access token.

<Tabs>
<TabItem value="tab-0" label="Request format">


```bash
curl --user <OAUTH_CLIENT_KEY>:<OAUTH_CLIENT_SECRET> -k 
-d "grant_type=password&username=<USERNAME>&password=<PASSWORD>" 
-H "Content-Type: application/x-www-form-urlencoded" 
/o/<ORG_ID>/oauth2/token
```

</TabItem>
<TabItem value="tab-1" label="Sample request">


```bash
curl --user 7wYeybBGCVfLxPmS0z66WNMffyMa:WYfwHUsbsEvwtqmDLuaxF_VCQJwa -k 
-d "grant_type=password&username=Charlie&password=jG9A5KrX" 
-H "Content-Type: application/x-www-form-urlencoded" 
/o/7e98b86f-63c7-41a1-8c56-c909a21a2615/oauth2/token
```

</TabItem>
<TabItem value="tab-2" label="Sample response">


```
{
    "access_token": "4778085e-5802-3090-aa70-ec877663f194",
    "refresh_token": "13bcbd1d-a4bb-33da-9274-d2c1a1f17d97",
    "token_type": "Bearer",
    "expires_in": 3600
}
```

</TabItem>
</Tabs>

:::note

If you need scopes in the response, add the `scope` parameter to the token request with the required scopes.

:::

## Client credentials grant

Use the following steps to use the client credentials to get an access token.

<Tabs>
<TabItem value="tab-0" label="Request format">


```bash
curl --user <OAUTH_CLIENT_KEY>:<OAUTH_CLIENT_SECRET> -k 
-d "grant_type=client_credentials" 
-H "Content-Type: application/x-www-form-urlencoded" 
/o/<ORG_ID>/oauth2/token
```

</TabItem>
<TabItem value="tab-1" label="Sample request">


```bash
curl --user fhErtAT2YF_M0Ek3AAYHLI8L25oa:JirxvtfoecnrS8vBjM7ygOtSIXuCS_uK_9WEC7d1zPEa -k 
-d "grant_type=client_credentials" 
-H "Content-Type: application/x-www-form-urlencoded" 
/o/12d1c4d2-2bb1-443b-aa4a-68f98a40d7c6/oauth2/token
```

</TabItem>
<TabItem value="tab-2" label="Sample response">


```
{
    "access_token": "bc978da1-6c56-3125-a999-a8d61c889672",
    "token_type": "Bearer",
    "expires_in": 3600
}
```

</TabItem>
</Tabs>



:::note

If you need scopes in the response, add the `scope` parameter to the token request with the required scopes.

:::

## Introspect tokens

You can use the token introspection endpoint to validate access tokens issued for organization applications. The following example demonstrates how to introspect an access token.

<Tabs>
<TabItem value="tab-0" label="Request format">


```bash
curl --user <OAUTH_CLIENT_KEY>:<OAUTH_CLIENT_SECRET> -k 
-d "token=<SUB_ORG_APP_TOKEN>" 
-H "Content-Type: application/x-www-form-urlencoded" 
/o/<ORG_ID>/oauth2/introspect
```

</TabItem>
<TabItem value="tab-1" label="Sample request">


```bash
curl --user fhErtAT2YF_M0Ek3AAYHLI8L25oa:JirxvtfoecnrS8vBjM7ygOtSIXuCS_uK_9WEC7d1zPEa -k 
-d "token=ef757efc-6ec3-3e12-83f6-cb2849d67f7b" 
-H "Content-Type: application/x-www-form-urlencoded" 
/o/12d1c4d2-2bb1-443b-aa4a-68f98a40d7c6/oauth2/introspect
```

</TabItem>
<TabItem value="tab-2" label="Sample response">


```
{
    "aut": "APPLICATION_USER",
    "aud": "fhErtAT2YF_M0Ek3AAYHLI8L25oa",
    "nbf": 1739253383,
    "org_id": "12d1c4d2-2bb1-443b-aa4a-68f98a40d7c6",
    "active": true,
    "token_type": "Bearer",
    "exp": 1739256983,
    "iat": 1739253383,
    "client_id": "fhErtAT2YF_M0Ek3AAYHLI8L25oa",
    "username": "Charlie@12d1c4d2-2bb1-443b-aa4a-68f98a40d7c6"
}
```

</TabItem>
</Tabs>

## Revoke tokens

The following example demonstrates how to revoke tokens issued for organization applications.

<Tabs>
<TabItem value="tab-0" label="Request format">


```bash
curl --user <OAUTH_CLIENT_KEY>:<OAUTH_CLIENT_SECRET> -k 
-d "token=<SUB_ORG_APP_TOKEN>&token_type_hint=<TOKEN_TYPE>" 
-H "Content-Type: application/x-www-form-urlencoded" 
/o/<ORG_ID>/oauth2/revoke
```

</TabItem>
<TabItem value="tab-1" label="Sample request">


```bash
curl --user fhErtAT2YF_M0Ek3AAYHLI8L25oa:JirxvtfoecnrS8vBjM7ygOtSIXuCS_uK_9WEC7d1zPEa -k 
-d "token=ef757efc-6ec3-3e12-83f6-cb2849d67f7b&token_type_hint=access_token" 
-H "Content-Type: application/x-www-form-urlencoded" 
/o/12d1c4d2-2bb1-443b-aa4a-68f98a40d7c6/oauth2/revoke
```

</TabItem>
<TabItem value="tab-2" label="Sample response">


```json
Empty JSON response with HTTP status code 200 OK
```

</TabItem>
</Tabs>
