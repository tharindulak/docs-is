---
title: OAuth 2.0 Scope Management Rest API Definition - v1
mkdocs_template: swagger
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/5.10.0/docs/develop/oauth2-scope-management-rest-apis.md
---

# OAuth 2.0 Scope Management Rest API Definition - v1

The OAuth2 scope API in WSO2 Identity Server (IS) can be used to manage oauth2 scopes and scope bindings such as 
roles and permissions. Since OIDC scope is a sub category of OAuth2 scopes, these end points cannot have the same 
scope names in WSO2 IS. For information about the OIDC scope endpoint,  
see [OIDC Scope Management REST APIs](../../develop/oidc-scope-management-rest-apis)

<details>
<summary>Click For Instructions</summary>

Follow the steps given below to try out the REST APIs with your local instance of WSO2 IS.
To try some APIs, a tenant needs to be created with the domain name as 'wso2.com'. 
See [here](../administer/adding-new-tenant.md) for more details on this.


[here](../administer/adding-new-tenant.md).

1.  Expand the relevant API operation and click **Try It Out** button.  
2.  Fill in relevant sample values for the input parameters and click **Execute**. 
    You will receive a sample curl command with the sample values you filled in. 
3. Add a `-k` header to the curl command and run the curl command on the terminal with a running instance of WSO2 IS. 

</details>
    
<div id="swagger-ui"></div>




[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/80f948e159dd8e0a8a6a)
