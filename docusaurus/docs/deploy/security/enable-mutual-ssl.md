---
title: Enable mutual SSL
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.3.0/docs/deploy/security/enable-mutual-ssl.md
---

# Enable mutual SSL

Mutual SSL is a security mechanism where both the client and server authenticate each other using digital certificates. Unlike traditional SSL, which only verifies the server’s identity, mutual SSL requires both parties to present certificates issued by a trusted Certificate Authority (CA). This ensures a highly secure connection and often eliminates the need for username/password authentication, as the client is authenticated based on its certificate.

## How it works

Let's take a look at how mutual SSL works with clients and WSO2 Identity Server. The relevant digital certificates are stored in the following `keystores`.

-   WSO2 Identity Server server certificates are stored in,

    `<IS_HOME>/repository/resources/security/wso2carbon.p12`


-   The trusted client certificates are stored in,
    `<IS_HOME>/repository/resources/security/clienttruststore.p12`

:::note


Learn more about WSO2 Identity Server's [keystores and truststores](keystores/index.md).

:::

These certificates are signed and issued by a certificate authority that allows both the client and server to communicate freely. Now let's look at how it works:


![Certificate exchange flow](../../../assets/img/deploy/security/mutual-ssl.png) 

1.  The client attempts to access a protected resource and the SSL/TSL
    handshake process begins.
2.  The server presents its certificate,`Server.crt`, according to the above example.
3.  The client takes this certificate and requests the CA for authenticity and validity of the certificate.
4.  If the certificate is valid, the client will provide its certificate, `Client.crt`, to the server.
5.  The Server takes this certificate and requests the CA for authenticity and validity of the certificate.
6.  If the certificate is valid, the server grants the client access to the resource.

## Enable Mutual SSL in WSO2 Identity Server

To enable mutual SSL,

1.  Open the `<IS_HOME>/repository/conf/tomcat/catalina-server.xml` file and find the  `certificateVerification` attribute within the `SSLHostConfig` tag under the `https` connector. Make sure the value of it is set to `want`

    ```java
    certificateVerification="want"
    ```

    :::tip[Why?]


    This configuration is set to `want` in order to make certificate authentication disabled for some scenarios (such as for mobile apps), essentially making two-way SSL authentication optional. You can set the value to `require` to make it mandatory.

    :::

    
    Alternatively, you can add the following configuration to the `<IS_HOME>/repository/conf/deployment.toml` file.
    
    ```toml
    [transport.https.sslHostConfig.properties]
    certificateVerification = "want"
    ```

2.  Open the `<IS_HOME>/repository/conf/deployment.toml` file and add the following configuration to enable the mutual SSL authenticator.

    ```toml
    [admin_console.authenticator.mutual_ssl_authenticator]
    enable = true
    
    [admin_console.authenticator.mutual_ssl_authenticator.config]
    WhiteList = ""
    ```

3.  For mutual SSL authentication to succeed, import the public certificate of WSO2 Identity Server to the client's truststore and import the public certificate of the client to WSO2 Identity Server's truststore. Consider the following example scenario.

    :::note


    If both the client and WSO2 Identity Server use WSO2 Identity Server's keystore and truststore for authentication, WSO2 Identity Server's certificate must also be present in the truststore. This ensures that the client can verify and trust WSO2 Identity Server during the authentication process. To do this, execute the following commands from the `<IS_HOME>/repository/resources/security` directory.

    1. Extract the public certificate of WSO2 Identity Server using the following command.

       ```shell
       keytool -export -alias wso2carbon -file carbon_public2.crt -keystore wso2carbon. -storetype PKCS12 -storepass wso2carbon
       ```

    2. Import the public certificate to the truststore using the following command.

       ```shell
       keytool -import -trustcacerts -alias carbon -file carbon_public2.crt -keystore  client-truststore. -storetype PKCS12 -storepass wso2carbon
       ```

    :::
