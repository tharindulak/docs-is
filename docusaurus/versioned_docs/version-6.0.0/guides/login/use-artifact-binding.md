---
title: Use SAML 2.0 Artifact Binding
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.0.0/docs/guides/login/use-artifact-binding.md
---

# Use SAML 2.0 Artifact Binding

This page guides you through enabling [SAML2 artifact binding](../../references/concepts/authentication/saml2-artifact-binding.md) with WSO2 Identity Server. 

Generally, SAML authentication requests and assertion data is sent through the browser using POST or Http Redirect binding. If you do not want to expose the entire message to the browser, you can use artifact binding instead. 

## Register a service provider

1.  Log in to the Management Console (`https://<IS_HOST>:<PORT>/carbon`) using admin/admin credentials. 

2.  Navigate to **Main** > **Identity** > **Service Providers** and click **Add**.

3.  Enter `saml2-web-app-pickup-dispatch` in the **Service Provider Name** text box,
    and click **Register**.

4.  In the **Inbound Authentication Configuration** section, click
    **Configure** under the **SAML2 Web SSO Configuration** section.

    1.  Now set the configuration as follows:

        1.  **Issuer** : `saml2-web-app-pickup-dispatch.com`

        2.  **Assertion Consumer URL** :  ` http://localhost.com:8080/saml2-web-app-pickup-dispatch.com/home.jsp `                       
        
        Click **Yes**, in the message that appears.

    2.  Select the following check-boxes:
        1.  **Enable Response Signing**

        2.  **Enable Single Logout**

        3.  **Enable Attribute Profile**

        4.  **Include Attributes in the Response Always**  
        
        5.  **Enable Signature Validation in Authentication Requests and Logout Requests**
    
5.  Click **Register** to save the changes.

:::tip

 To configure more advanced configurations, see [Advanced SAML Configurations](saml-app-config-advanced.md). 

:::

---


## Configure artifact expiration time

According to the [SAML 2.0 Binding
Specification](http://www.oasis-open.org/committees/download.php/35387/sstc-saml-bindings-errata-2.0-wd-05-diff.pdf), issued SAML Artifacts should have an expiration time. WSO2 Identity Server does not resolve the artifacts that have passed this time limit.

You can configure this restriction by adding the following property to the `<IS_HOME>/repository/conf/deployment.toml` file.

```java
[saml.artifact] 
validity= 4
```

:::tip

The default time limit is 4 minutes. In a practical scenario, this time limit should be lesser than the SAML response validity
period.

:::
    
----

## Resolve artifacts with WSO2 IS

According to the SAML Specification, issued SAML artifacts should be resolved, or exchanged to an actual SAML response, via a back-channel call to the issuer. 

WSO2 Identity Server supports SOAP Binding to resolve SAML artifacts according to Section 3.6 of the [SAML 2.0 Binding
Specification](http://www.oasis-open.org/committees/download.php/35387/sstc-saml-bindings-errata-2.0-wd-05-diff.pdf).

:::info

WSO2 IS Artifact Resolution Endpoint: `https://<IS_HOST>:<IS_PORT>/samlartresolve`

:::

The application should send an `<ArtifactResolve>` message wrapped in a SOAP envelope to the WSO2 Identity Server artifact resolution endpoint. The following example shows a SAML artifact resolve request.

```java
POST /samlartresolve HTTP/1.1
Host: wso2is.com
Content-Type: text/xml
Content-Length: nnn
SOAPAction: http://www.oasis-open.org/committees/security
<SOAP-ENV:Envelope
    xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/">
    <SOAP-ENV:Body>
        <samlp:ArtifactResolve
            xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"
            xmlns="urn:oasis:names:tc:SAML:2.0:assertion"
            ID="_6c3a4f8b9c2d" Version="2.0"
            IssueInstant="2004-01-21T19:00:49Z">
            <Issuer>https://ServiceProvider.com/SAML</Issuer>
            <Artifact>
                AAQAADWNEw5VT47wcO4zX/iEzMmFQvGknDfws2ZtqSGdkNSbsW1cmVR0bzU=
            </Artifact>
        </samlp:ArtifactResolve>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

If signature validation for artifact resolve is enabled, the application has to sign this request with its private key. WSO2 IS validates the request and if it is valid, an `<ArtifactResponse>` message is sent with the actual SAML response set as the message element. The code block below shows an example of an `<ArtifactResponse>` message.

```java
HTTP/1.1 200 OK
Date: 21 Jan 2004 07:00:49 GMT
Content-Type: text/xml
Content-Length: nnnn

<SOAP-ENV:Envelope
    xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/">
    <SOAP-ENV:Body>
        <samlp:ArtifactResponse
            xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"
            xmlns="urn:oasis:names:tc:SAML:2.0:assertion"
            ID="_FQvGknDfws2Z" Version="2.0"
            InResponseTo="_6c3a4f8b9c2d"
            IssueInstant="2004-01-21T19:00:49Z">
            <Issuer>https://wso2is.com</Issuer>
            <samlp:Status>
                <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
            </samlp:Status>
            <samlp:Response ID="d2b7c388cec36fa7c39c28fd298644a8"
                IssueInstant="2004-01-21T19:00:49Z"
                Version="2.0">
                ...
            </samlp:Response>
        </samlp:ArtifactResponse>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```


----


## Try it

### Set up the sample

- Download Apache Tomcat 8.x from
[here](https://tomcat.apache.org/download-80.cgi) and install. Tomcat
server installation location will be referred as `<TOMCAT_HOME>` later
in this guide.      

- It is recommended that you use a hostname that is not
`          localhost         ` to avoid browser errors. Modify the
`          /etc/hosts         ` entry in your machine to reflect this.
Note that `          wso2is.local         ` is used in
this documentation as an example, but you must modify this when
configuring the authenticators or connectors with this sample
application.

-   [Download](https://github.com/wso2/samples-is/releases/download/v4.5.2/saml2-web-app-pickup-dispatch.com.war) the `saml2-web-app-pickup-dispatch.com.war` file from the latest release assets.

### Configure CORS

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



### Deploy the sample

Deploy this sample web app on a web container.

1.  Copy the `saml2-web-app-pickup-dispatch.com.war` file into the `<TOMCAT_HOME>/apache-tomcat-<version>/webapps` folder. 

2.  Start the Tomcat server.

### Try artifact binding

1.  Access the application application URL: [http://wso2is.local:8080/saml2-web-app-pickup-dispatch.com](http://wso2is.local:8080/saml2-web-app-pickup-dispatch.com).

2.  You will be redirected to the login page of WSO2 IS. Log in using your WSO2 IS credentials (admin/admin). Provide the required consent.
You will be redirected to the Pickup Dispatch application home page.

3.  You can use a SAML tracer add-on with your browser to view the SAML2 response artifact for the SSO authentication request. The code block  below shows an example response.

    ```java
    HTTP/1.1 302 Object Moved
    Date: 21 Jan 2004 07:00:49 GMT
    Location: https://application.com/ACS/URL?
    SAMLart=AAQAADWNEw5VT47wcO4zX%2FiEzMmFQvGknDfws2ZtqSGdkNSbsW1cmVR0bzU%3D&RelayState=0043bfc1bc45110dae17004005b13a2b
    Content-Type: text/html; charset=iso-8859-1
    ```

You have successfully set up SAML artifact binding. See the sections below for more information on resolving SAML 2.0 artifacts and configuring an artifact expiration time.

-----

:::info[Related topics]

- [Concept: SAML2 Artifact Binding](../../references/concepts/authentication/saml2-artifact-binding.md)
- [Guide: Enable Login for a SAML Application](webapp-saml.md)

:::
