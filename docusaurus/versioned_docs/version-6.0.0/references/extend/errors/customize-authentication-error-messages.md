---
title: Customize Authentication Error Messages
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.0.0/docs/references/extend/errors/customize-authentication-error-messages.md
---

# Customize Authentication Error Messages

WSO2 Identity Server has standard error messages for different authentication errors that are encountered. See [Error Codes and
Descriptions](error-codes-and-descriptions.md) for more information on the standard error codes and descriptions of
those errors. There are three types of custom errors handled here:

-   Invalid credentials
-   Invalid user
-   Account lock

:::note

Account lock errors are returned only when account locking is enabled on the server. Refer [User Account Locking](../../../guides/identity-lifecycles/lock-account.md) document to enable account locking.

:::
    

Add the following properties to the `deployment.toml` file found in the `<IS_HOME>/repository/conf` folder to enable the authenticator to be able to customize error messages.

```toml
[authentication.authenticator.basic.parameters]
showAuthFailureReason = true
```

The following query parameters are sent to the web application from authentication endpoint.

-   errorCode
-   failedUsername
-   remainingAttempts

The error messages can be customized based on these query parameters in the jsp files as in  `authenticationendpoint/login.jsp`.
