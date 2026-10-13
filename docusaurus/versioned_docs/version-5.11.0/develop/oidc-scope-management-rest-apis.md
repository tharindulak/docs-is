---
title: OpenID Connect Scope Management Rest API Definition - v1
mkdocs_template: swagger
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/5.11.0/docs/develop/oidc-scope-management-rest-apis.md
---

# OpenID Connect Scope Management Rest API Definition - v1

The OIDC scope API in WSO2 Identity Server(IS) can be used to manage OIDC scopes and map claims.
Since OIDC scope is a sub category of OAuth2 scopes, these end points cannot have the same scope names in WSO2 IS. 
For more information about the OAuth2 scope endpoint,  
see [OAuth2 Scope Management REST APIs](../../develop/oauth2-scope-management-rest-apis.md).

<details>
<summary>Click For Instructions</summary>

Follow the steps given below to try out the REST APIs with your local instance of WSO2 IS.
To try some APIs, a tenant needs to be created with the domain name as 'wso2.com'. 
See [here](../administer/adding-new-tenant.md) for more details on this.

1.  Expand the relevant API operation and click **Try It Out**.  
2.  Fill in the relevant sample values for the input parameters and click **Execute**. 
    You will receive a sample curl command with the sample values you filled in. 
3. Add a `-k` header to the curl command and run the curl command on the terminal with a running instance of WSO2 IS. 

</details>
    
<div id="swagger-ui"></div>




[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/fb712a9e2a2f92c54d8f)
