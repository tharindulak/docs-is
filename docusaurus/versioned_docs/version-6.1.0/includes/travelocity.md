---
title: Travelocity
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.1.0/docs/includes/travelocity.md
---

### Prerequisites

- Download [Apache Tomcat 8.x](https://tomcat.apache.org/download-80.cgi) and install it. Tomcat server installation location will later be referred to as `<TOMCAT_HOME>` in this guide.

- It is recommended that you use a hostname that is not `localhost` to avoid browser errors. Modify your machine's `/etc/hosts` entry to reflect this.

    :::info

    Note that `wso2is.local` is used in this documentation as an example, but you must modify this when configuring the authenticators or connectors with this sample application.

    :::




- Download the [Travelocity application](https://github.com/wso2/samples-is/releases/download/v4.5.2/travelocity.com.war) from the latest release assets.

---

### Register a service provider

1. On the Management Console, go to **Main** > **Identity** > **Service Providers** and click **Add**.

3. Enter `travelocity.com` as the **Service Provider Name**, and click **Register**.

4. Expand the **Inbound Authentication Configuration > SAML2 Web SSO Configuration** section and, click **Configure**.

5. Enter the following values in the fields mentioned.

    | Field name | Value |
    |-----------|-------|
    | **Issuer** | `travelocity.com`  |
    | **Assertion Consumer URL**    | `http://wso2is.local:8080/travelocity.com/home.jsp`    |

    :::info

    Click **Yes** on the dialog that appears after you add the **Assertion Consumer URL**. This dialog appears when you add an `http` URL.

    :::

6. Enable the following by selecting the corresponding checkboxes:
    - **Enable Response Signing**
    - **Enable Signature Validation in Authentication Requests and Logout Requests**
    - **Enable Single Logout**
    - **Enable Attribute Profile**
        - **Include Attributes in the Response Always**  

    :::tip

    For more information on the advanced configurations, see [Advanced SAML Configurations](../../../../guides/login/saml-app-config-advanced).

    :::

7. Click **Register** to add the service provider and save the configurations.  

---
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



---

### Deploy the sample web app

To deploy the sample web app on a web container:

1. Copy the downloaded `.war` file of the SAML application into the `webapps` directory of the Tomcat folder.

2. Open a terminal and add the following entry to the `/etc/hosts` file of your machine to configure the hostname.

    ```bash
    127.0.0.1   wso2is.local
    127.0.0.1   localhost.com
    ```

    !!!info "Why is this step needed?"
		Some browsers do not allow you to create cookies for a naked hostname, such as `localhost`. Cookies are required when working with SSO . Therefore, to ensure that the SSO capabilities work as expected in this tutorial, you need to configure the `etc/host` file as explained in this step.

		The `etc/host` file is a read-only file. Therefore, you won't be able to edit it by opening the file via a text editor. Instead, edit the file using the terminal commands. For example, use the following command if you are working on a macOS/Linux environment.

		```java
		sudo nano /etc/hosts
		```

3. Open the `travelocity.properties` file in the `<TOMCAT_HOME>/webapps/travelocity.com/WEB-INF/classes ` directory and configure the following property with the hostname that you configured above.

    ```text
    #The URL of the SAML 2.0 Assertion Consumer
    SAML2.AssertionConsumerURL=http://<HOSTNAME>:8080/travelocity.com/home.jsp
    ```

4. Restart the Tomcat server.

To check the sample application, navigate to `http://<TOMCAT_HOST>:<TOMCAT_PORT>/travelocity.com/index.jsp` on your browser.

:::tip

If you wish to change properties like the `issuer ID`, `consumerURL`, and `IdP URL`, you can edit the **travelocity.properties** file in the `travelocity.com/WEB-INF/classes` directory.
Also if the service provider is configured in a tenant you can use `QueryParams` property to send the tenant domain. For example,`QueryParams=tenantDomain=wso2.com`.

This sample uses the following default values.

| Properties | Description  |
|------------|--------------|
| `SAML2.SPEntityId=travelocity.com`    | A unique identifier for this SAML 2.0 Service Provider application. |
| `SAML2.AssertionConsumerURL=http://wso2is.local:8080/travelocity.com/home.jsp`   | The URL of the SAML 2.0 Assertion Consumer.   |
| `SAML2.IdPURL=https://localhost:9443/samlsso` | The URL of the SAML 2.0 Identity Provider.    |
| `SAML2.IsPassiveAuthn=true`   | Set this to send SAML2 passive authentication requests.   |

For the changes to be effective, restart the Apache Tomcat server after updating the `travelocity.properties` file.

:::
