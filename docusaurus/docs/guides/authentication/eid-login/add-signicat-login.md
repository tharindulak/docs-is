---
title: Add Signicat login
deployment_options:
  - WSO2 Cloud
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/asgardeo/docs/guides/authentication/eid-login/add-signicat-login.md
---

import Recommendation from '../../../_partials/guides/fragments/add-login/recommendation.mdx';

# Add Signicat login

[Signicat’s](https://www.signicat.com/) eID Hub simplifies digital identity verification and authentication by connecting your platform to more than 30 electronic identities (eIDs) from across Europe, all through one streamlined integration.

By integrating Signicat, you can authenticate users and prove their identity easily using trusted eIDs, whether for onboarding, access control, or compliance needs.

You can add Signicat login to your applications using WSO2 Identity Platform and enable users to log in with their eIDs.

Follow this guide for instructions.

## Prerequisites
- A Signicat account. If you don't have one, you can [sign up for free](https://developer.signicat.com/docs/).

## Register WSO2 Identity Platform on Signicat

You need to register WSO2 Identity Platform as an OIDC app on Signicat.

:::note

You can follow the [Signicat documentation](https://developer.signicat.com/docs/) for detailed instructions.

:::

1. Log in to [Signicat Dashboard](https://dashboard.signicat.com), and click .
2. On the left panel, Click **Products** and select **eID Hub**.
3. Under **eID Hub**, click **OIDC Clients**.

    ![Register OIDC app in Signicat](../../../../assets/img/guides/idp/signicat-idp/signicat-register-app.png)

4. Give the application a name and the following URLs:

    - **Authorization callback URL**
        ```bash
        <PRODUCT_URL_FORMAT>/commonauth
        ```

    ![Enter Signicat app details](../../../../assets/img/guides/idp/signicat-idp/signicat-app-info.png)

5. Click **Create**.
6. Click **Add Secret** and Generate a new client secret.
7. Take note of the **Client ID** and **Client secret**.
8. To add required eIDs, Click **eIDs** in the left panel (under **eID Hub**), and click **Add new**.
   ![Add new eID](../../../../assets/img/guides/idp/signicat-idp/signicat-add-eid.png)

9. Select the eIDs you want to add and click **Add**.

## Register the Signicat Connection

Now, let's register the Signicat IdP in WSO2 Identity Platform.

1. On the WSO2 Identity Platform Console, go to **Connections**.
2. Click **New Connections** and select **Signicat**.
3. Enter the following details and click **Finish**:

    ![Add Signicat Connection in WSO2 Identity Platform](../../../../assets/img/guides/idp/signicat-idp/add-signicat-idp.png)

    <table><tbody><tr><th>{"Parameter"}</th><th>{"Description"}</th></tr><tr><td>{"Name"}</td><td>{"A unique name for this Signicat identity provider."}</td></tr><tr><td>{"Client ID"}</td><td>{"The client ID obtained from Signicat."}</td></tr><tr><td>{"Client secret"}</td><td>{"The client secret obtained from Signicat."}</td></tr><tr><td>{"Authorised redirect URL"}</td><td>{"Provide the Authorised redirect URL of your Signicat organization. For example https://{your_signicat_domain}/auth/open/connect/authorize.."}</td></tr><tr><td>{"Token Endpoint URL"}</td><td>{"Provide the Token endpoint URL of your Signicat organization. For example https://{your_signicat_domain}/auth/open/connect/token."}</td></tr></tbody></table>

## Enable Signicat login

:::note[Before you begin]

You need to [register an application with WSO2 Identity Platform](../../applications/index.md). You can register your own application or use one of the [sample applications](../../../get-started/try-samples/index.md) provided.

:::

1. On the WSO2 Identity Platform Console, go to **Applications**.
2. Select your application, go to the **Login Flow** tab and add Signicat login from your preferred editor:

    

    <Applies to="WSO2 Cloud">

    <Tabs>
    <TabItem value="tab-0" label="Classic Editor">

    To add Signicat login using the Classic Editor: 

     1. If you haven't already defined a sign-in flow, click **Start with Default configuration** to get started.
     2. Click **Add Authentication** on the step, select your Signicat identity provider, and click **Add**.
        ![Add Signicat login in WSO2 Identity Platform](../../../../assets/img/guides/idp/signicat-idp/add-signicat-federation-with-basic.png)

    </TabItem>
    <TabItem value="tab-1" label="Visual Editor">

    To add Signicat login using the Visual Editor: 

    1. Switch to the **Visual Editor** tab, by default the `Username & Password` login flow will be added onto the Visual Editor's workspace.
    2. Click on `+ Add Sign In Option` to add a new authenticator to the same step and select your Signicat connection.
      ![Add Signicat login in WSO2 Identity Platform](../../../../assets/img/guides/idp/signicat-idp/add-signicat-federation-with-visual-editor.png)

    </TabItem>
    </Tabs>

    ---

    </Applies>

    

    <Applies to="Self-hosted">

    1. Click **Add Sign In Option** to add a new authenticator to the first step.

    2. Select the Signicat connection.

    3. Click **Confirm** to add login with Signicat to the sign-in flow.

         ![Configuring Signicat in WSO2 Identity Server using the Visual Editor](../../../../assets/img/guides/idp/signicat-idp/add-signicat-login-with-visual-editor.png)

    </Applies>

    

    <Recommendation />


3. Click **Update** to save your changes.


## Try it out

Follow the steps given below.

1. Access the application URL.

2. Click **Login** to open the WSO2 Identity Platform login page.

3. On the WSO2 Identity Platform login page, **Sign in with Signicat**.

    ![Login with Signicat](../../../../assets/img/guides/idp/signicat-idp/sign-in-with-signicat.png)

4. Log in to the eIDs configured in Signicat.

## Configure connection

To learn more about other configurations available for the connection, refer to the [add federated login](../federated-login/index.md) documentation.
