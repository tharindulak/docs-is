---
title: Add Facebook login
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.2.0/docs/guides/authentication/social-login/add-facebook-login.md
---

# Add Facebook login

You can add Facebook login to your applications using WSO2 Identity Server and enable users to log in with their Facebook accounts.

Follow this guide for instructions.

## Register WSO2 Identity Server on Facebook
You need to register WSO2 Identity Server as an app on Facebook.

:::note

You can follow the [Facebook Documentation](https://developers.facebook.com/docs/development/create-an-app) for detailed instructions.

:::

To register an app on Facebook:

1. Go to the [My Apps](https://developers.facebook.com/apps) page in **Meta for developers**.

2. Click **Create App**.

    ![Facebook developer portal](../../../../../assets/img/guides/idp/facebook-idp/facebook-developer-portal.jpg)

3. Select the use case as **Authenticate and request data from users with Facebook Login** and click **Next**.

    ![Create Facebook consumer app](../../../../../assets/img/guides/idp/facebook-idp/facebook-app-type.jpg)

4. Select the login type out of the options and click **Next**.

    ![Choose login type](../../../../../assets/img/guides/idp/facebook-idp/facebook-choose-login-type.png)

5. Provide **Display Name** and click **Create App** to create an application.

    ![Provide information to Facebook app](../../../../../assets/img/guides/idp/facebook-idp/facebook-app-info.jpg)

6. While in the created application, select **Use cases** from the left navigation.

7. Under **Use cases** > **Authentication and account creation**, click **Customize**.

8. Under **Facebook Login** > **Quickstart**, click **Go to quickstart**.

9. Select **Web** as the platform for this app and provide the following **Site URL** and click **Save**.

    ```bash
    https://localhost:9443
    ```

10. Return to the **Use cases** > **Customize** section and under **Facebook login** > **Settings**, click **Go to settings**.

11. Add the following as the **Valid OAuth Redirect URIs** and click **Save changes**.

    ```bash
    https://localhost:9443/commonauth
    ```

12. Enable **Client OAuth Login** and **Web OAuth Login** (these are enabled by default) and save the changes.

    ![Add Facebook settings](../../../../../assets/_versions/7.2.0/img/guides/idp/facebook-idp/facebook-app-settings.jpg)

13. On the left navigation panel, go to **App settings** > **Basic** and take note of the **App ID** and **App Secret**.

    ![Get AppID and Secret from Facebook](../../../../../assets/_versions/7.2.0/img/guides/idp/facebook-idp/app-id-secret-from-facebook.png)

## Register the Facebook IdP

Now, let's register the Facebook IdP in WSO2 Identity Server.

1. On the WSO2 Identity Server Console, go to **Connections**.
2. Click **Create Connection** and select **Facebook**.
3. Enter the following details of the Facebook identity provider and click **Finish**:

    ![Add Facebook IDP in WSO2 Identity Server](../../../../../assets/_versions/7.2.0/img/guides/idp/facebook-idp/add-facebook-idp.png)

    <table>
        <tr>
            <th>Parameter</th>
            <th>Description</th>
        </tr>
        <tr>
            <td>Name</td>
            <td>A unique name for this Facebook identity provider.</td>
        </tr>
        <tr>
            <td>App ID</td>
            <td>App ID obtained from Facebook.</td>
        </tr>
        <tr>
            <td>App Secret</td>
            <td>The app secret obtained from Facebook.</td>
        </tr>
    </table>



5. Go to the **Settings** tab and see the list of permissions granted by Facebook to WSO2 Identity Server.

    - **email**: Grants read access to a user's primary email address.
    - **public_profile**: Grants read access to a user's default public profile details.  

    :::note


    WSO2 Identity Server needs these permissions to get user information. WSO2 Identity Server checks the attribute configurations of the application and sends the relevant attributes received from Facebook to the app. You can read the [Facebook documentation](https://developers.facebook.com/docs/permissions/reference) to learn more.

    :::

## Enable Facebook login

:::note[Before you begin]

You need to [register an application with WSO2 Identity Server](../../applications/index.md). You can register your own application or use one of the [sample applications](../../../get-started/try-samples/index.md) provided.

:::

1. On the WSO2 Identity Server Console, go to **Applications**.
2. Select your application, go to the **Login Flow** tab and add Facebook login as follows:

    
    1. Click **Add Sign In Option** to add a new authenticator to the first step.

    2. Select the Facebook connection.

    3. Click **Confirm** to add login with Facebook to the sign-in flow.

        ![Configuring Facebook login in WSO2 Identity Server using the Visual Editor](../../../../../assets/img/guides/idp/facebook-idp/add-facebook-login-with-visual-editor.png)
    

    :::note[Recommendations]



    :::
    It is recommended to add your social and enterprise connections to the first authentication step as they are used for identifying the user.

3. Click **Update** to save your changes.

## Try it out

Follow the steps given below.

1. Access the application URL.

2. Click **Login** to open the WSO2 Identity Server login page.

3. On the WSO2 Identity Server login page, click **Sign in with Facebook**.

    ![Login with Facebook](../../../../../assets/_versions/7.2.0/img/guides/idp/facebook-idp/sign-in-with-facebook.png)

4. Log in to Facebook with an existing user account.

5. The user is now redirected to the application and logged in.

:::note

When a user successfully logs in with Facebook for the first time, a **user** account is created in the WSO2 Identity Server Console with the Facebook username. This new user account will be managed by Facebook.

:::

## Configure connection

To learn more about other configurations available for the connection, refer to the [add federated login](../federated-login/index.md) documentation.
