---
title: Enable Login for a SAML Web Application
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.1.0/docs/guides/login/webapp-saml.md
---

# Enable Login for a SAML Web Application

This page guides you through enabling login for a [SAML](../../references/concepts/authentication/intro-saml.md) web application.

### Prerequisites

- Download [Apache Tomcat 8.x](https://tomcat.apache.org/download-80.cgi) and install it. Tomcat server installation location will later be referred to as `<TOMCAT_HOME>` in this guide.

- It is recommended that you use a hostname that is not `localhost` to avoid browser errors. Modify your machine's `/etc/hosts` entry to reflect this.

    :::info

    Note that `wso2is.local` is used in this documentation as an example, but you must modify this when configuring the authenticators or connectors with this sample application.

    :::




- Download the [SAML pickup dispatch application](https://github.com/wso2/samples-is/releases/download/v4.5.2/saml2-web-app-pickup-dispatch.com.war) from the latest release assets.

---

### Deploy the sample web app

To deploy the sample web app on a web container:

1. Copy the downloaded `.war` file of the SAML application into the `webapps` directory of the Tomcat folder.

2. Start the Tomcat server.

---

### Register a service provider

1. On the Management Console, go to **Main** > **Identity** > **Service Providers** and click **Add**.

3. Enter `saml2-web-app-pickup-dispatch` as the **Service Provider Name**, and click **Register**.

4. Expand the **Inbound Authentication Configuration > SAML2 Web SSO Configuration** section and, click **Configure**.

5. Enter the following values in the fields mentioned.

    | Field name | Value |
    |-----------|-------|
    | **Issuer** | `saml2-web-app-pickup-dispatch.com`  |
    | **Assertion Consumer URL**    | `http://localhost.com:8080/saml2-web-app-pickup-dispatch.com/home.jsp`    |

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

    For more information on the advanced configurations, see [Advanced SAML Configurations](../../../guides/login/saml-app-config-advanced).

    :::

7. Click **Register** to add the service provider and save the configurations.  


## Try it out

Now, let's log in to the application.

1. Start the Tomcat server and access the following URL on your browser: `http://localhost:8080/saml2-web-app-pickup-dispatch.com`.

2. Click **Login** and enter your user credentials.

3. Provide the required consent. You will be redirected to the Pickup Dispatch application home page.

You have successfully configured authentication for a SAML application.

:::info[Related topics]

- [Concept: SAML](../../references/concepts/authentication/intro-saml.md)
- [Quick Start: SAML Authentication](../../get-started/sample-use-cases/single-sign-on.md#try-sso-with-saml-20)
- [Guide: Advanced SAML Configurations](saml-app-config-advanced.md)
- [Guide: SAML Front-Channel Logout](saml-front-channel-logout.md)
- [Guide: SAML Back-Channel Logout](saml-back-channel-logout.md)

:::
