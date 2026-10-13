---
title: Add Microsoft login
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.1.0/docs/guides/authentication/social-login/add-microsoft-login.md
---

# Add Microsoft login

You can add Microsoft login to your applications using WSO2 Identity Server and enable users to log in with their Microsoft accounts.

Follow this guide for instructions.


## Register WSO2 Identity Server on Microsoft

You need to register WSO2 Identity Server as an OAuth2.0 application on Microsoft Entra ID.

:::note

For detailed instructions, you can follow the [Microsoft documentation](https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-register-app).

:::

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) using an account with administrator permission.

    :::note

    You must use an account in the same Microsoft 365 subscription (tenant) with which you intend to register the app.

    :::

2. Go to **Identity** > **Applications** > **App registrations** and select **New registration**.

3. Click **Add** and select **App registration** from the list.

4. Provide the required information for app registration.

    ![Register an application on the Microsoft Entra admin center](../../../../../assets/_versions/7.1.0/img/guides/idp/microsoft-idp/register-an-application.png)

    <table>
        <tr>
            <th>Parameter</th>
            <th>Description</th>
        </tr>
        <tr>
            <td>Name</td>
            <td>Enter a meaningful name for your application.</td>
        </tr>
        <tr>
            <td>Supported Account Type</td>
            <td>Select the supported account type. <br /><b>Value: </b><code>Accounts in any organizational directory (Any Microsoft Entra ID tenant - Multitenant) and personal Microsoft accounts (e.g., Skype, Xbox)</code></td>
        </tr>
        <tr>
            <td>Redirect URI</td>
            <td>Select <b>Web</b> as the platform and provide the URL to redirect after the login is completed.<br /><b>Value:</b> <code>https://localhost:9443/commonauth</code></td>
        </tr>
    </table>

5. Click **Register** to create the application.

    :::note

    Take note of the client ID after the application is created.

    :::

Now, let's generate a client secret for the application.

1. Go to **Certificates & secrets** on the left navigation and click **+ New client secret**.
2. Enter a description for the client secret and select the expiry time.
3. Click **Add** to add the client secret.

    :::note[Important]

    Take note of the generated **Value**. Microsoft Entra will allow copying this value only once. This value is the newly generated client secret for your Microsoft connection in WSO2 Identity Server.

    :::


## Register the Microsoft IdP

Now, let's register the Microsoft IdP in WSO2 Identity Server.

1. On the WSO2 Identity Server Console, go to **Connections**.
2. Click **New Connections** and select **Microsoft**.
3. Enter the following details of the Microsoft identity provider and click **Finish**:

    ![Add Microsoft IDP in WSO2 Identity Server](../../../../../assets/_versions/7.1.0/img/guides/idp/microsoft-idp/add-microsoft-idp.png)

    <table>
      <tr>
        <th>Parameter</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Name</td>
        <td>A unique name for this Microsoft identity provider.</td>
      </tr>
      <tr>
          <td>Client ID</td>
          <td>The client ID obtained from Microsoft.</td>
      </tr>
      <tr>
          <td>Client secret</td>
          <td>The client secret obtained from Microsoft.</td>
      </tr>
    </table>  

4. Go to the **Settings** tab and see the list of **scopes** to which Microsoft has granted permissions.

- **email**: Allows to view the user's email address.
- **openid**: Allows authentication using OpenID Connect and to obtain the ID token.
- **profile**: Allows to view the user's basic profile data.

:::note

WSO2 Identity Server needs these scopes to get user information. WSO2 Identity Server checks the attribute configurations of the application and sends the relevant attributes received from Microsoft to the app. You can read the [Microsoft documentation](https://learn.microsoft.com/en-us/entra/identity-platform/scopes-oidc#openid-connect-scopes) to learn more.

:::


## Enable Microsoft login

:::note[Before you begin]

You need to [register an application with WSO2 Identity Server](../../applications/index.md). You can register your own application or use one of the [sample applications](../../../get-started/try-samples/index.md) provided.

:::

To enable Microsoft login:

1. On the WSO2 Identity Server Console, go to **Applications**.
2. Select your application, go to the **Login Flow** tab and add Microsoft login from your preferred editor:

    
    1. Click **Add Sign In Option** to add a new authenticator to the first step.

    2. Select the Microsoft connection.

    3. Click **Confirm** to add login with Microsoft to the sign-in flow.

        ![Configuring Microsoft login in WSO2 Identity Server using the Visual Editor](../../../../../assets/img/guides/idp/microsoft-idp/add-microsoft-login-with-visual-editor.png)
    

    :::note[Recommendations]



    :::
    It is recommended to add your social and enterprise connections to the first authentication step as they are used for identifying the user.

3. Click **Update** to save your changes.

## Try it out

Follow the steps given below.

1. Access the application URL.
2. Click **Login** to open the WSO2 Identity Server login page.
3. On the WSO2 Identity Server login page, **Sign in with Microsoft**.

    ![Login with Microsoft](../../../../../assets/_versions/7.1.0/img/guides/idp/microsoft-idp/sign-in-with-microsoft.png)

4. Log in to Microsoft with an existing user account.

:::note

When a user successfully logs in with Microsoft for the first time, a **user** account is created in the WSO2 Identity Server Console with the Microsoft username. Microsoft will manage this new user account.

:::

## Configure connection

To learn more about other configurations available for the connection, refer to the [add federated login](../federated-login/index.md) documentation.
