---
title: Connect sms provider
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.1.0/docs/includes/connect-sms-provider.md
---

&lt;!--
1. Download the certificate of the SMS provider.

    :::note

    If you wish to have NEXMO as your SMS provider:

    1. Go to the SMS provider's website, [https://www.nexmo.com](https://www.nexmo.com/).
    2. Click on the security padlock next to the URL, and export the certificate.

    :::

2. Navigate to the `<IS_HOME>/repository/resources/security` directory and import the downloaded certificate into the WSO2 IS client keystore.

    ```java
    keytool -importcert -file <CERTIFICATE_FILE_PATH> -keystore client-truststore.jks -alias "Nexmo" 
    ```

3. You are prompted to enter the keystore password. The default `client-truststore.jks` password is `wso2carbon`.
-->
