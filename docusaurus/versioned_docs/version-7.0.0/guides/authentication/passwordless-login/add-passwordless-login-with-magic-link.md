---
title: Add Magic Link login
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.0.0/docs/guides/authentication/passwordless-login/add-passwordless-login-with-magic-link.md
---

# Add Magic Link login

Magic link is a form of passwordless authentication. It allows users to log in by clicking a link sent to their email instead of entering a password.

## Prerequisites

- To get started, you need to [register an application with WSO2 Identity Server](../../applications/index.md). You can register your own application or use one of the [sample applications](../../../get-started/try-samples/index.md) provided.

- You need to have a user account in WSO2 Identity Server. If you don't already have one, [create a user account](../../users/manage-users.md#onboard-a-user) in WSO2 Identity Server.



- You need to [configure the email sending module](../../../../deploy/configure/email-sending-module) for the WSO2 Identity Server to send the Magic link to the users.

## Enable Magic link login for an app

Follow the steps given below to add **Magic link** login to the login flow of your application.

1. On the WSO2 Identity Server Console, go to **Applications**.

2. Select the application to which you wish to add magic link login.

3. Go to the **Login Flow** tab of the application and add magic link login as follows:

    
    1. Go to **Predefined Flows** > **Basic Flows** > **Add Passwordless login**.

    2. Select **Magic Link**.

    3. Click **Confirm** to add passwordless login with magic link to the sign-in flow.

        ![Configuring magic link login in WSO2 Identity Server using the Visual Editor](../../../../../assets/_versions/7.0.0/img/guides/passwordless/magic-link/add-magic-link-login.png)
    

4. Click **Update** to save your changes.

## Try it out

Follow the steps given below.

1. Access the application URL.
2. Click **Login** to open the WSO2 Identity Server login page.
3. On the WSO2 Identity Server login page, enter your username and press **Continue**.

    ![Sign In magic link in WSO2 Identity Server](../../../../../assets/_versions/7.0.0/img/guides/passwordless/magic-link/magic-link-login-page.png)

    You will be redirected to the below page.

    ![Magic link login notification page](../../../../../assets/_versions/7.0.0/img/guides/passwordless/magic-link/magic-link-login-notification-page.png)

4. Check your inbox for the magic link email. The email reads as follows.

    ![Magic link email](../../../../../assets/_versions/7.0.0/img/guides/passwordless/magic-link/magic-link-email.png)

5. Open the magic link by clicking the **Sign In** button.

    :::note

    Magic links support cross-browser functionality, allowing you to open the link and log in from any browser of your choice even if it is different from the one you used to initiate the login process.
    If you want to remove the cross-browser functionality, you can do so by adding the following configuration in the `deployment.toml` file found in the &lt;IS_HOME>/repository/conf/ directory.

    ```toml
       [session.nonce.cookie]
       default_whitelist_authenticators=[] 
    ```
    This configuration ensures that the magic link can only be opened using the same browser from which the login was initiated.

    :::
