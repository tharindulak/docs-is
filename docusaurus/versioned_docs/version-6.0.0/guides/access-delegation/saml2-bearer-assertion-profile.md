---
title: Set Up SAML2 Bearer Assertion Profile
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.0.0/docs/guides/access-delegation/saml2-bearer-assertion-profile.md
---

# Set Up SAML2 Bearer Assertion Profile

This page guides you through using the [SAML2 Bearer grant](../../references/concepts/authorization/saml2-bearer-assertion-profile.md) to exchange a SAML2 assertion for a valid OAuth access token.

## Create a service provider

To register your application as a service provider in the WSO2 Identity Server:

1. Log in to the WSO2 Identity Server Management Console using administrator credentials.

2. Go to **Main** > **Identity** > **Service Providers** > **Add**.
     
    

3. Enter a **Service Provider Name**. Optionally, enter a **Description**.
    
    

4. Click **Register**.

----

## Basic OAuth/OpenID Connect configuration

Make the following changes to the created service provider.

1. Expand **Inbound Authentication Configuration** > **OAuth/OpenID Connect Configuration** and click **Configure**.

2. Enter the **Callback Url**. 

    :::note

    The **Callback Url** is the exact location in the service provider's application to which an access token will be sent. This URL should be the URL of the page that the user is redirected to after successful authentication.

    :::

3. Click **Add**. Note the **OAuth Client Key** and **OAuth Client Secret** that appear. 


:::note

-   Make sure the **SAML2** grant is enabled under **Allowed Grant Types** when configuring OAuth/OpenID Connect.

-   You can provide any valid URL as the **Callback Url**. This URL value is not used for any other operations during this sample.

:::

:::tip

To configure more advanced configurations, see [OAuth/OpenID Connect Configurations](../../../../guides/login/oauth-app-config-advanced). 

:::



----

## SAML2 Web SSO configuration

1. In the **Inbound Authentication Configuration** section of the previously created service provider, click **Configure** under the **SAML2 Web SSO Configuration** section.

    1.  Now set the configurations as follows:

        1.  **Issuer**: `travelocity.com`

        2.  **Assertion Consumer URL**: `http://wso2is.local:8080/travelocity.com/home.jsp`  
            Click Yes, in the message that appears.

    2.  Select the following check-boxes:
    
        1.  **Enable Response Signing**

        2.  **Enable Single Logout**

        3.  **Enable Attribute Profile**

        4.  **Include Attributes in the Response Always**  
        
        5.  **Enable Signature Validation in Authentication Requests and Logout Requests**
        
    3. Select the the following check-boxes and enter the following values:
           1. **Enable Audience Restriction**
            - **Audience**: `https://localhost:9443/oauth2/token`
           2. **Enable Recipient Validation**
            - **Recipient**: `https://localhost:9443/oauth2/token`

           ![enable-audience-restriction](../../../../assets/img/samples/enable-audience-restriction.png) 
    
    :::tip

    For more information on other advanced configurations refer, [Advanced SAML Configurations](../login/saml-app-config-advanced.md)

    :::

5.  Click **Register** to save the changes.

-----

## Exchange SAML assertion for an OAuth access token

1. Use the following curl command to exchange the SAML assertion for an OAuth access token.

    :::note

    **Request Format**
    ```curl
    curl -k -d "grant_type=urn:ietf:params:oauth:grant-type:saml2-bearer&assertion=<base64-URL_encoded_assertion>&scope=<scope>" -H "Authorization: Basic <base64_encoded_clientid:clientsecret>" -H "Content-Type: application/x-www-form-urlencoded" https://<host>:<port>/oauth2/token
    ```
    ---
    **Sample Request**
    ```curl
    curl -k -d "grant_type=urn:ietf:params:oauth:grant-type:saml2-bearer&assertion=PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZczpUcmFuc2Zvcm1zPgo8ZHM6VHJhbnNmb3JtIEFsZ29yaXRobT0iaHR0cDovL3d3zOlRyYW5zZm9ybXMaW&scope=PRODUCTION" -H "Authorization: Basic TGZkcWt3eVNGVVNZVjNtUkNNaE5vNmw1cWZJYTpOb0JQZjZkZGhxS2pXdEpNWHVibU04bndqNW9h" -H "Content-Type: application/x-www-form-urlencoded" https://localhost:9443/oauth2/token
    ```

    :::
    
2. Use the introspection endpoint of WSO2 Identity Server to get the token information.

    :::note

    **Request Format**
    ```curl
    curl -k -u <username>:<password> -H 'Content-Type: application/x-www-form-urlencoded' -X POST --data 'token=<access token>' https://<IS_HOST>:<IS_PORT>/oauth2/introspect
    ```
    ---
    **Sample Request**
    ```curl
    curl -k -u admin:admin -H 'Content-Type: application/x-www-form-urlencoded' -X POST --data 'token=f3116b04-924f-3f1a-b323-4f0988b94f9f' https://localhost:9443/oauth2/introspect
    ```

    :::

## Try it

### Set up the sample application

### Prerequisites

- Download [Apache Tomcat 8.x](https://tomcat.apache.org/download-80.cgi) and install it. Tomcat server installation location will later be referred to as `<TOMCAT_HOME>` in this guide.

- It is recommended that you use a hostname that is not `localhost` to avoid browser errors. Modify your machine's `/etc/hosts` entry to reflect this.

    :::info

    Note that `wso2is.local` is used in this documentation as an example, but you must modify this when configuring the authenticators or connectors with this sample application.

    :::



-   Download the `travelocity.com.war` file from the latest release assets.

### Deploy the sample

Deploy this sample web app on a web container.

1.  Copy the `travelocity.com.war`file into the `webapps` folder. For
    example, ` <TOMCAT_HOME>/apache-tomcat-<version>/webapps`
    
2.  Open a terminal window and add the following entry to the
    `/etc/hosts` file of your machine to configure
    the hostname.

    ```bash
    127.0.0.1   wso2is.local
    ```

    !!!info "Why is this step needed?"
		Some browsers do not allow you to create cookies for a naked
		hostname, such as `localhost`. Cookies are
		required when working with SSO . Therefore, to ensure that the SSO
		capabilities work as expected in this tutorial, you need to
		configure the `etc/host` file as explained in
		this step.

		The `etc/host` file is a read-only file.
		Therefore, you won't be able to edit it by opening the file via a
		text editor. Instead, edit the file using the terminal commands.  
		For example, use the following command if you are working on a
		macOS/Linux environment.

		```java
		sudo nano /etc/hosts
		```
		
3.  Open the `travelocity.properties` file found in the `
    &lt;TOMCAT_HOME>/webapps/travelocity.com/WEB-INF/classes ` directory
    and configure the following property with the hostname ( `
    wso2is.local ` ) that you configured above.

    ```text
    #The URL of the SAML 2.0 Assertion Consumer
    SAML2.AssertionConsumerURL=http://wso2is.local:8080/travelocity.com/home.jsp
    ```
    
4.  Restart the Tomcat server.

To check the sample application, navigate to
`http://<TOMCAT_HOST>:<TOMCAT_PORT>/travelocity.com/index.jsp`
on your browser.

For example,
`http://wso2is.local:8080/travelocity.com/index.jsp`

:::tip


If you wish to change properties like the issuer ID, consumer
URL, and IdP URL, you can edit the **travelocity.properties** file found
in the `         travelocity.com/WEB-INF/classes        ` directory.
Also if the service provider is configured in a tenant you can use
"QueryParams" property to send the tenant domain.For example,
"QueryParams=tenantDomain=wso2.com".

This sample uses the following default values.

| Properties                                                                                                                                                                          | Description                                                        |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------|
| `             SAML2.SPEntityId=travelocity.com                         `                                                                                                            | A unique identifier for this SAML 2.0 Service Provider application |
| `              SAML2.AssertionConsumerURL=                                             http://wso2is.local:8080/travelocity.com/home.jsp                                          ` | The URL of the SAML 2.0 Assertion Consumer                         |
| `              SAML2.IdPURL=                                             https://localhost:9443/samlsso                                          `                                  | The URL of the SAML 2.0 Identity Provider                          |
| `             SAML2.IsPassiveAuthn=true                         `                                                                                                                   | Set this to send SAML2 passive authentication requests             |

If you edit the `travelocity.properties` file, restart the
Apache Tomcat server for the changes to take effect.

:::

### CORS configuration

SAML2 POST Binding requires CORS configurations to be set up.

Before configuring the service provider, add the following configurations to the `deployment.toml` file found in `<IS_HOME>/repository/conf/`. Adding this configuration allows `HTTP POST` requests.


    ```toml
    [cors]
    allow_generic_http_requests = true
    allow_any_origin = false
    allowed_origins = [
        "http://localhost:8080"
    ]
    allow_subdomains = false
    supported_methods = [
        "GET",
        "POST",
        "HEAD",
        "OPTIONS"
    ]
    support_any_header = true
    supported_headers = []
    exposed_headers = []
    supports_credentials = true
    max_age = 3600
    tag_requests = false
    ```



### Enable SAML2 grant in the sample

1. Open the `travelocity.properties` file found in the `<TOMCAT_HOME>/webapps/travelocity.com/WEB-INF/classes` folder.

2. Edit the following configurations.

    Enter the client ID and client secret you received when registering the OAuth/OpenID Connect application.

    ```java
    EnableOAuth2SAML2Grant=true
    OAuth2.ClientId= (enter the client ID received at the application registration)
    OAuth2.ClientSecret= (enter the client secret received at the application registration)
    ```

    
2. Restart the Tomcat server to apply the changes.

### Log in with SAML

1. Start the Tomcat server and access the following URL on your browser: `http://wso2is.local:8080/travelocity.com`

2. Click **Click here to login with SAML from Identity Server (Post binding or Redirect Binding)**. 

    You are redirected to WSO2 Identity Server for authentication. 

3.  Enter the username and password and click **Continue**.  

    ![login-page](../../../../assets/img/samples/sign-in-sample.png) 

4.  Click **Request OAuth2 Access Token** to receive the access token.  

    ![request-oauth2-access-token](../../../../assets/img/samples/request-oauth2-access-token.png)  

    You will receive an access token as shown below.

    ![oauth2-token-details](../../../../assets/img/samples/oauth2-token-details.png) 

6.  Use the introspection endpoint of WSO2 Identity Server to get the token information.

    **Request**

    :::note

    **Request Format**
    ```java
    curl -k -u <username>:<password> -H 'Content-Type: application/x-www-form-urlencoded' -X POST --data 'token=<access token>' https://<IS_HOST>:<IS_PORT>/oauth2/introspect
    ```
    ---
    **Sample Request**
    ```java
    curl -k -u admin:admin -H 'Content-Type: application/x-www-form-urlencoded' -X POST --data 'token=f3116b04-924f-3f1a-b323-4f0988b94f9f' https://localhost:9443/oauth2/introspect
    ```

    :::

    **Response**

    ```java
    {
        "active":true,
        "token_type":"Bearer",
        "exp":1508927700,
        "iat":1508924100,
        "client_id":"EiqKsYfVH6dffF0b6LmrFBJW95Aa"
        "username":"admin@carbon.super"
    }
    ```

7.  Since the Travelocity application has now exchanged the SAML assertion for a valid OAuth access token, you can use the received access token to access a protected resource in WSO2 Identity Server. 

    Use the [SCIM User Endpoint](../../apis/scim2-rest-apis.md) which is secured with OAuth to retrieve users. 

    **Request**

    :::note

    **Request Format**
    ```java
    curl -v -k --header "Authorization: Bearer <access token>" https://<IS_HOST>:<IS_PORT>/wso2/scim/Users
    ```
    ---
    **Sample Request**
    ```java
    curl -v -k --header "Authorization: Bearer 865c60a5-969b-36b4-95e2-721a1fb5c867" https://localhost:9443/wso2/scim/Users
    ```

    :::
    
    **Response**

    ```java
    {
        "totalResults":1,
        "schemas":["urn:scim:schemas:core:1.0"],
        "Resources":[{
            "meta":{
                "created":"2017-11-15T11:23:25",
                "location":"https://localhost:9443/wso2/scim/Users/admin"
                "lastModified":"2017-11-15T11:23:25"
            },
            "id":"0fb2af3f-03f2-4d6b-8340-957012df23f4",
            "userName":"admin"
        }]
    }
    ```
----

:::info[Related topics]

-   [Concept: SAML2 Bearer Assertion Profile for OAuth 2.0](../../references/concepts/authorization/saml2-bearer-assertion-profile.md)

:::
