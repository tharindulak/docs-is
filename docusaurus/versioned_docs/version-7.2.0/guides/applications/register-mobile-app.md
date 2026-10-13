---
title: Register a mobile app
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.2.0/docs/guides/applications/register-mobile-app.md
---

# Register a mobile app

To add login to your mobile application with WSO2 Identity Server, you need to first register your app in WSO2 Identity Server.

Your app will be registered as an OpenID Connect mobile app and a client ID will be issued. Note that client secrets are not issued for mobile apps since they are public clients. However, the [PKCE (Proof Key for Code Exchange)](../../references/app-settings/oidc-settings-for-app.md#proof-key-for-code-exchange-pkce) extension is enabled by default as a security measure.

## Register the app

To register the app:

1. On the WSO2 Identity Server Console, go to **Applications**.

2. Click **New Application** and select **Mobile Application**.

    ![Select an app type](../../../../assets/img/guides/applications/select-app-type.png)

3. Enter the following details:

    ![Create a new Mobile](../../../../assets/_versions/7.2.0/img/guides/applications/create-new-mobile-app.png)

    <table>
        <tr>
            <th>Parameter</th>
            <th>Description</th>
        </tr>
        <tr>
            <td>Name</td>
            <td>A unique name to identify your application.</td>
        </tr>
        <tr>
            <td>Authorized redirect URLs</td>
            <td>The URL to which the authorization code is sent to upon user authentication and where the user is redirected to upon logout. If wildcard support is necessary, ensure it is limited to well-defined patterns and implemented securely to meet your specific requirements.</td>
        </tr>
        <tr>
            <td>Allow sharing with organizations</td>
            <td>Enable this to share the new application with all or any selected B2B organizations that belong to your primary organization.</td>
        </tr>
    </table>

4. Click **Register** to complete the registration.

    <details>
    <summary>Sharing with selected organizations</summary>

    If you have enabled **Allow sharing with organizations** while registering the application, you will see a popup window with the following options.

    ![Share the application with organizations](../../../../assets/img/guides/applications/share-application.png)

    <table>
        <tr>
            <th>Option</th>
            <th>Description</th>
        </tr>
        <tr>
            <td>Share with all organizations</td>
            <td>If selected, the application will be shared with all existing organizations and any new organizations you may create in the future.</td>
        </tr>
        <tr>
            <td>Share with only selected organizations</td>
            <td>If selected, you can select the organizations you wish to share the application with.</td>
        </tr>
    </table>

    </details>

5. [Enable the application](index.md#enabledisable-an-application) when it is ready for use.

## Get the client ID

When you register your mobile application, a client ID is generated. Your mobile application will identify itself to WSO2 Identity Server with this client ID.

You can get this client ID from the **Protocol** tab of the application as shown below.

![Get client ID of Mobile](../../../../assets/_versions/7.2.0/img/guides/applications/spa-client-id.png)

## What's next?

- [Add login to your mobile app](../authentication/add-login-to-mobile-app.md)
