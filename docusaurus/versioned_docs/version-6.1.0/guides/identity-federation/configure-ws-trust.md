---
title: Configuring WS-Trust Security Token Service
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.1.0/docs/guides/identity-federation/configure-ws-trust.md
---

# Configuring WS-Trust Security Token Service

WSO2 Identity Server uses the security token service (STS) as the [WS-Trust](../../references/concepts/authentication/intro-ws-trust.md) implementation.

The STS is capable of issuing SAML 1.1 and 2.0 security tokens and has a SOAP/XML API for token issuance.

## Download the STS connector
WS-Trust authentication is no longer supported by default from IS 5.11.0 upwards and has been introduced as a connector. In order to use WS-Trust authentication, first, you should download the connector from the WSO2 Connector Store.

To download and install the WS-Trust connector:

1. Download the [WS-Trust Authenticator](https://store.wso2.com/connector) from the WSO2 Connector Store.
2. Copy and paste the downloaded `.zip` file to the home directory of your WSO2 Identity Server and extract the `.zip` file.
3. Open a terminal, navigate to the home of the extracted directory and execute the following commands.
    ```bash
    chmod u+r+x setup_sts.sh
    ./setup_sts.sh 
    ```
The connector is successfully installed. Now you can delete the extracted directory.

## Secure the Security Token Service

According to the trust-brokering model defined in the WS-Trust specification, the users should authenticate themselves to the STS before obtaining a token. STS may use this authentication information when constructing the security token.

For example, STS may populate the required claims based on the username provided by the user. Therefore, the STS service needs to be secured.

To secure the Security Token Service:

1. On the Management Console, go to **Identity Providers \> Resident**.

2. Enter the required values as given below.

    <table>
    <thead>
    <tr className="header">
    <th>Field</th>
    <th>Description</th>
    <th>Sample Value</th>
    </tr>
    </thead>
    <tbody>
    <tr className="odd">
    <td><strong>Home Realm Identifier</strong></td>
    <td>This is the domain name of the identity provider. If you do not enter a value here, the user will be prompted to specify a domain, when an authentication request comes to WSO2 Identity Server. You can enter multiple identifiers as a comma-separated list.</td>
    <td><code>localhost</code></td>
    </tr>
    <tr className="even">
    <td><strong>Idle Session Time Out</strong></td>
    <td>This is the duration in minutes for which an SSO session can be idle. If WSO2 Identity Server receives no SSO authentication requests for the given duration, a session time-out occurs. The default value is <code>15</code> .</td>
    <td><code>15</code></td>
    </tr>
    <tr className="odd">
    <td><strong>Remember Me Period</strong></td>
    <td><div className="content-wrapper">
    <p>This is the duration in weeks for which WSO2 Identity Server should remember an SSO session given that the <strong>Remember Me</strong> option is selected in the WSO2 Identity Server login screen.</p>
    <p>The default value is <code>2</code> weeks.</p>
    </div></td>
    <td><code>2</code></td>
    </tr>
    </tbody>
    </table>

3. Expand **Inbound Authentication Configuration** > **Security Token Service Configuration** and click **Apply Security Policy**.
    
    ![apply security policy](../../../../assets/img/guides/ws-trust-apply-policy.png)

4. Select **Yes** from the **Enable Security?** list and select a pre-configured security scenario according to your requirements.
We will be using `UsernameToken` under the **Basic Scenarios** section for this tutorial.

    :::note

    You can find further details about security policy scenarios from the **view scenario** option.

    ![enable-security](../../../../assets/img/guides/ws-trust-view-scenario.png)

    :::

5. Click **Next** and provide the required details as follows:

    :::info

    The next steps may vary according to the security scenario you have chosen under point (5) above. Given below are the steps for the **UsernameToken** scenario.

    :::

    1. Select **ALL-USER-STORE-DOMAINS** as the domain.
    2. Select the role you created to grant permission to access a secured service. In this example, the `admin` role is used.
        ![select-domain](../../../../assets/img/guides/ws-trust-select-domain.png)

        :::note

        The **Select Domain** list provides the available domains. The listed **User Groups** can vary depending on the domain selected.

        :::

6. Click **Finish**.
7. Click **Ok** on the confirmation dialog window that appears.
8. Click **Update** to save and complete the process.

Now STS is configured and secured with a username and password. Only users with the Admin role can consume the service.

The next step is to add a service provider to consume the STS.

## Configure the service provider

The steps in this section should be followed if you are using **Holder-of-Key** as the [subject confirmation method](../../references/concepts/authentication/intro-ws-trust.md#subject-confirmation).



:::tip[Before you begin]

You must first [register a service provider](../applications/register-sp.md).

:::

1. On the Management Console, go to **Service Providers** > **List** and select your service provider.
2. Expand **Inbound Authentication Configuration** > **WS-Trust Security Token Service Configuration** and click **Configure**.
3. Enter the required details as given below.
    <table>
        <thead>
            <tr className="header">
                <th>Field</th>
                <th>Description</th>
                <th>Sample Value</th>
            </tr>
        </thead>
        <tbody>
            <tr className="odd">
                <td><strong>Endpoint Address</strong></td>
                <td>
                    <div className="content-wrapper">
                    <div>
                        Enter the trusted relying party's <strong>endpoint address</strong>, which is the endpoint address of the Security Token Service.
                        <p>The endpoint must be used as the service URL to which the token gets delivered by the STS client. Then select the public certificate imported. Tokens issued are encrypted using the public certificate of the trusted relying party. Therefore, the consumer who obtains this token to invoke the RP service will not be able to see the token.</p>
                        <div className="admonition note">
                            <p className="admonition-title">Note</p>
                            Make sure to upload the certificate of the relying party to the trust store. For instructions, see [adding CA-signed certificates to keystores](../../deploy/security/create-new-keystores.md#add-ca-signed-certificates-to-keystores).
                        </div>
                        <br />
                    </div>
                    </div>
                </td>
                <td><code>https://localhost:9444/services/echo</code></td>
            </tr>
            <tr className="even">
                <td><strong>Certificate Alias</strong></td>
                <td>This is the alias of the certificate.</td>
                <td><code>wso2carbon</code></td>
            </tr>
        </tbody>
    </table>

    ![add-new-trusted-service](../../../../assets/img/guides/ws-trust-sts-config.png)

4. Click **Update** to save your changes.

## Run a sample STS Client

The following sample demonstrates the steps to run a Security Token Service (STS) client. The STS issues a security token to authenticate a user for your client application using WS-Trust protocols.

:::note[Before you begin]

You need to [configure WS-Trust](configure-ws-trust.md) for WSO2 Identity Server.

:::

To run the STS client:

1. Clone the [Identity Server samples](https://github.com/wso2/samples-is) repository.

2. In the cloned directory, navigate to the `SAMPLES-IS/sts/sts-client` directory to build the STS client.  

    :::info

    The sts-client sample sends the username and password defined in the `SAMPLES-IS/sts/sts-client/src/main/resources/client.properties` file. WSO2 Identity Server authenticates if the user is in the system, and if the user is in the system, a token is sent to the requesting party, which is the sts-client application in this case.

    The default username and password defined are that of the default super administrator, and you can change it accordingly.

    ```java
    ut.username=admin
    ut.password=admin
    ```

    :::

3. Build the client using `mvn install`.

4. Once the client is built successfully, run the `sts-client.sh` file in Unix or the `sts-client.bat` file in Windows.

You can see that the SAML token issued from the STS is being printed by the client.

:::note

The `connection refused` error occurs when the STS client attempts to send the received SAML token to a service that is not running in this case.

:::
