---
title: Log in to Google Workspace using WSO2 Identity Platform
deployment_options:
  - WSO2 Cloud
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/asgardeo/docs/guides/authentication/sso-integrations/add-google-workspace-template.md
---

# Log in to Google Workspace using WSO2 Identity Platform

:::note[Legacy SSO Profile]

Google has marked their old SSO profile as legacy and now supports a new profile. We recommend using the new profile for better compatibility. If you still need to set up the legacy profile, refer to [Google's legacy guide](https://support.google.com/a/answer/12032922?hl=en&ref_topic=7579248&sjid=3736947215943977003-AP#legacy_profile&zippy=%2Cconfigure-the-legacy-sso-profile) and use our [Standard-Based SAML template](../../applications/register-saml-web-app.md).

:::

This page guides you through integrating WSO2 Identity Platform for Single Sign-On (SSO) with Google.

:::note[Before you begin]

You need to have a Google domain. Further, ensure you have a Google Workspace account and your account supports SSO by referring to the [Google documentation](https://support.google.com/a/answer/182076?sjid=13406338490513240799-AP).


<Applies to="Self-hosted">

If you're testing the integration locally, make sure to [configure a hostname](../../../deploy/change-the-hostname.md).

</Applies>

:::

    

## Create the Google Workspace application

Follow the steps given below to register the Google Workspace application in WSO2 Identity Platform.

1. On the WSO2 Identity Platform Console, go to **Applications**.

2. Click **New Application** and under **SSO Integrations**, select **Google Workspace**.

    ![Select app type in the WSO2 Identity Platform](../../../../assets/img/guides/authentication/sso-integrations/common/add-app.png)

3. Provide the Entity ID and a Name for the application.

    :::info[Entity ID]

    A unique URL dynamically generated for your Google SAML SSO profile. To find it, follow [Google's guide](https://support.google.com/a/answer/12032922?hl=en&ref_topic=7579248&sjid=3736947215943977003-AP#create_profile) on creating a SAML SSO profile. Once completed, copy the `Entity ID` from the `SP Details` section of the specific SAML SSO profile.

    **Note:** While setting up the SAML SSO profile in Google, simply provide a name first. The IdP details can be added later.

    :::

    ![Select google workspace app in the WSO2 Identity Platform](../../../../assets/img/guides/authentication/sso-integrations/google-workspace-sso/add-google-app.png)

4. Click **Create** to complete the registration.

5. Download WSO2 Identity Platform's certificate from the `Guide` tab of the created application.

-----

## Configure Google

Follow the steps below to configure Google for SSO authentication with WSO2 Identity Platform.

1. Access your Google domain's [admin console](https://admin.google.com).

2. Follow Google’s instructions to [configure the SSO profile for your organization](https://support.google.com/a/answer/12032922?hl=en&ref_topic=7579248&sjid=3736947215943977003-AP#org_profile). Use the details below:

    - IDP entity ID:
      `<ISSUER_NAME>`

    - Sign-in page URL:
      `<PRODUCT_URL_FORMAT>/samlsso`

    - Sign-out page URL:
      `<PRODUCT_URL_FORMAT>/samlsso`
   
    - Password URL:
      `<MY_ACCOUNT_HOST_PATH>/myaccount/security`

3. Upload WSO2 Identity Platform's certificate you downloaded earlier.

    ![sso-fill-google.png](../../../../assets/img/guides/authentication/sso-integrations/google-workspace-sso/sso-fill-google.png)
-----

## Try it out

Now that you have integrated WSO2 Identity Platform with Google Workspace, follow the steps below to test it.

:::note

Google restricts administrators from being redirected to external identity providers. Therefore, use a non-administrator account to try it out.

:::

1. Create a new account in WSO2 Identity Platform for a user that already exists in Google Workspace under the same email address.

2. Navigate to [Google](http://accounts.google.com) and enter the email address of the user you created. You will be navigated to WSO2 Identity Platform's login page.

3. Enter the username and password for the user to login. Once authenticated, you will be navigated to the relevant domain's G-Suite.

:::note

If you only wish to access Gmail, navigate to [mail.google.com](http://mail.google.com), and repeat the process.

:::
