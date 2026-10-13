---
title: Register a Machine-to-Machine (M2M) application
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.1.0/docs/guides/applications/register-machine-to-machine-app.md
---

# Register a Machine-to-Machine (M2M) application

To integrate your machine-to-machine (M2M) application with WSO2 Identity Server, you need to first register your application from the WSO2 Identity Server Console. 
Then you can authorize your M2M applications to access management APIs of WSO2 Identity Server or your business APIs.
A client ID and client secret are issued to the application upon registration.

Follow the instructions given below.

## Register the app

To register the app:

1. On the WSO2 Identity Server Console, click **Applications**.

    ![Select app type](../../../../assets/img/guides/applications/select-app-type.png)

2. Click **New Application** and select **M2M Application**.

3. In the **Name** field, enter a unique name to identify your application.

4. Click **Register** to complete the registration.

5. [Enable the application](index.md#enabledisable-an-application) when it is ready for use.

## Authorize the API resources for the app

You can authorize your M2M applications to access APIs and their scopes(permissions) from **API Authorization** tab of the application, as shown below.

![Authorize API](../../../../assets/_versions/7.1.0/img/guides/applications/authorize-api-to-m2m.png)

Learn more about [API authorization](/identity/7.1.0/guides/api-authorization/).

## Get the client ID and secret

When you register your M2M application, a client ID and client secret are generated. Your M2M application will identify itself to WSO2 Identity Server with these credentials.

You can get this client ID and client secret from the **Protocol** tab of the application, as shown below.

![Get client ID and secret of M2M app](../../../../assets/_versions/7.1.0/img/guides/applications/client-id-secret-m2m.png)

## What's Next?

- [Obtain an M2M token using client credential grant](../../references/grant-types.md#client-credentials-grant)
