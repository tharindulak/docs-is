---
title: Add GitHub login
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.0.0/docs/guides/authentication/social-login/add-github-login.md
---

# Add GitHub login

You can add GitHub login to your applications using WSO2 Identity Server and enable users to log in with their GitHub accounts.

Follow this guide for instructions.

## Register WSO2 Identity Server on GitHub

You need to register WSO2 Identity Server as an OAuth app on GitHub.

:::note

You can follow the [GitHub documentation](https://docs.github.com/en/developers/apps/building-oauth-apps/creating-an-oauth-app) for detailed instructions.

:::

1. Log in to [GitHub](https://github.com/), click your profile icon, and click **Settings**.
2. On the left panel of the **Settings** page, click **Developer settings**.
3. Under **OAuth apps**, click **Register a new application**.

    ![Register oauth2 app in GitHub](../../../../../assets/img/guides/idp/github-idp/github-register-app.jpg)

4. Give the application a name and the following URLs:
    
    - **Homepage URL**
        ```bash
        https://localhost:9443
        ```
    
    - **Authorization callback URL**
        ```bash
        https://localhost:9443/commonauth
        ```

    ![Enter GitHub app details](../../../../../assets/img/guides/idp/github-idp/github-app-info.png)

5. Click **Register application**.
6. Generate a new client secret and take note of the **Client ID** and **Client secret**.

## Register the GitHub IdP

Now, let's register the GitHub IdP in WSO2 Identity Server.

1. On the WSO2 Identity Server Console, go to **Connections**.
2. Click **New Connections** and select **GitHub**.
3. Enter the following details and click **Finish**:

    ![Add GitHub IDP in WSO2 Identity Server](../../../../../assets/_versions/7.0.0/img/guides/idp/github-idp/add-github-idp.png)

    <table>
      <tr>
        <th>Parameter</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Name</td>
        <td>A unique name for this GitHub identity provider.</td>
      </tr>
      <tr>
          <td>Client ID</td>
          <td>The client ID obtained from GitHub.</td>
      </tr>
      <tr>
          <td>Client secret</td>
          <td>The client secret obtained from GitHub.</td>
      </tr>
    </table>

4. Go to the **Settings** tab and see the list of **scopes** to which GitHub has granted permissions.

    - **email**: Grants read access to a user's primary email address.
    - **public_profile**: Grants read access to a user's default public profile details.  

    :::note


    WSO2 Identity Server needs these scopes to get user information. WSO2 Identity Server checks the attribute configurations of the application and sends the relevant attributes received from GitHub to the app. You can read the [GitHub Documentation](https://docs.github.com/en/developers/apps/building-oauth-apps/scopes-for-oauth-apps) to learn more.

    :::

## Enable GitHub login

:::note[Before you begin]

You need to [register an application with WSO2 Identity Server](../../applications/index.md). You can register your own application or use one of the [sample applications](../../../get-started/try-samples/index.md) provided.

:::

1. On the WSO2 Identity Server Console, go to **Applications**.
2. Select your application, go to the **Login Flow** tab and add GitHub login from your preferred editor:

    

    1. Click **Add Sign In Option** to add a new authenticator to the first step.

    2. Select the GitHub connection.

    3. Click **Confirm** to add login with GitHub to the sign-in flow.

        ![Configuring GitHub login in WSO2 Identity Server using the Visual Editor](../../../../../assets/img/guides/idp/github-idp/add-github-login-with-visual-editor.png)
    

    :::note[Recommendations]



    :::
    It is recommended to add your social and enterprise connections to the first authentication step as they are used for identifying the user.

3. Click **Update** to save your changes.

## Try it out

Follow the steps given below.

1. Access the application URL.

2. Click **Login** to open the WSO2 Identity Server login page.

3. On the WSO2 Identity Server login page, **Sign in with GitHub**.

    ![Login with GitHub](../../../../../assets/_versions/7.0.0/img/guides/idp/github-idp/sign-in-with-github.png)

4. Log in to GitHub with an existing user account.

:::note

When a user successfully logs in with GitHub for the first time, a **user** account is created in the WSO2 Identity Server Console with the GitHub username. This new user account will be managed by GitHub.

:::

## Configure connection

To learn more about other configurations available for the connection, refer to the [add federated login](../federated-login/index.md) documentation.
