---
title: Add X login
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.3.0/docs/guides/authentication/social-login/add-x-login.md
---

import JitProvisioning from '../../../_partials/guides/fragments/manage-connection/jit-provisioning.mdx';
import Recommendation from '../../../_partials/guides/fragments/add-login/recommendation.mdx';
import ManageAttributes from '../../../_partials/guides/fragments/manage-connection/manage-attributes.mdx';

# Add X login

You can add X login to your applications using WSO2 Identity Server and enable users to log in with their X accounts.

## Register WSO2 Identity Server on X

1. Log in to the [X Developer Portal](https://developer.twitter.com/) using your X credentials.

2. Navigate to **Projects & Apps**, click **Add project** and provide details of your project.

3. Either during project creation, or by navigating to your created project in **Projects & Apps**, click **Add App**.

    1. Provide an **App name**.
       ![Set X app_name](../../../../assets/img/guides/idp/x-idp/x-app-name.png)

    2. Take note of the **API Key** and **API Key Secret** of the application.
       ![Set X app_name](../../../../assets/img/guides/idp/x-idp/x-key-token.png)

4. Click **App Settings** at the bottom of the page.

5. Click **Set up** under **User Authentication Settings** and do the following.

   1. Under **Type of App** select **Web App, Automated App or Bot**.

   2. Fill in the user authentication details with the following values.

      - Callback URI / Redirect URL - `/commonauth`
      - Website URL - `http://localhost.com:8080/pickup-dispatch/home.jsp`

   3. Click **Save**.

    :::note

    The **App Client ID** and **App client secret** presented at this moment is not required for this guide.

    :::

## Register the X IdP

Now, let's register the Microsoft IdP in WSO2 Identity Server.

1. On the WSO2 Identity Server Console, go to **Connections**.

2. Click **Create Connection** and select **Custom Connector**.

3. Provide a name and a description for the connector and click **Finish**.

      ![Create a custom connector](../../../../assets/img/guides/idp/x-idp/x-custom-connector.png)

4. On the created custom connector, go to the **Settings** tab.

5. Click **New Authenticator**, select **Twitter** and click **Next**.

6. Enter the following details and click **Finish**.

      ![Configure the X connector](../../../../assets/img/guides/idp/x-idp/x-configure-connector.png)

      {"<tr\">"}<table><tbody><tr><th>{"Parameter"}</th><th>{"Description"}</th></tr><tr><td>{"API Key"}</td><td>{"The "}<code>{"API key"}</code>{" generated when registering WSO2 Identity Server in X."}<br />{" e.g. "}<code>{"wuerRmdgwlqX0oE1WNDdsh17o"}</code></td></tr><tr><td>{"API Secret"}</td><td>{"The "}<code>{"API Key Secret"}</code>{" generated when registering WSO2 Identity Server in X. "}<br />{" e.g. "}<code>{"771tqnkpcbRyTBSCRQvVud1x8j1uQlCDpNZo3hRG0s4cEtsFky"}</code></td></tr><tr><td>{"Callback URL"}</td><td><p>{"The Callback URL you entered when registering WSO2 Identity Server in X. This is the URL to which the browser should be redirected after the authentication is successful."}</p>{" e.g. "}<code>{"/commonauth"}</code></td></tr></tbody></table>

<JitProvisioning />

## Enable X login

:::note[Before you begin]

You need to [register an application with WSO2 Identity Server](../../applications/index.md). You can register your own application or use one of the [sample applications](../../../get-started/try-samples/index.md) provided.

:::

1. On the WSO2 Identity Server Console, go to **Applications**.
2. Select your application, go to the **Login Flow** tab and add X login from your preferred editor:

    
    1. Click **Add Sign In Option** to add a new authenticator to the first step.

    2. Select the Twitter connection.

    3. Click **Confirm** to add login with X to the sign-in flow.

        ![Configuring X login in WSO2 Identity Server using the Visual Editor](../../../../assets/img/guides/idp/x-idp/add-x-login-with-visual-editor.png)
    

    <Recommendation />

3. Click **Update** to save your changes.

## Try it out

Follow the steps given below.

1. Access the application URL.

2. Click **Login** to open the WSO2 Identity Server login page.

3. On the WSO2 Identity Server login page, **Sign in with X**.

    ![Login with X](../../../../assets/img/guides/idp/x-idp/sign-in-with-x.png)

4. Log in to X with an existing user account.

:::note

When a user successfully logs in with X for the first time, a **user** account is created in the WSO2 Identity Server Console with the X username. This new user account will be managed by X.

:::

## Configure user attributes

<ManageAttributes />

## Configure connection

To learn more about other configurations available for the connection, refer to the [add federated login](../federated-login/index.md) documentation.
