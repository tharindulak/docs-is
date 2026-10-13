---
title: Configure a custom connector
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.3.0/docs/guides/authentication/configure-custom-connector.md
---

import Recommendation from '../../_partials/guides/fragments/add-login/recommendation.mdx';
import AddGroups from '../../_partials/guides/fragments/manage-connection/add-groups.mdx';
import DeleteConnection from '../../_partials/guides/fragments/manage-connection/delete-connection.mdx';

# Configure a custom connector

You can add login to your applications using a custom connector in WSO2 Identity Server and enable users to log in with the configured connector. This custom connector can be any identity provider such as Facebook, Twitter, Google, Yahoo or a [custom federated authenticator](../../references/extend/federation/write-a-custom-federated-authenticator.md).

Follow this guide for instructions.

## Register the custom connector

1. On the WSO2 Identity Server Console, go to **Connections**.
2. Click **Create Connection** and select **Custom Connector**.
3. Enter a unique name and a description and click **Finish**.
4. Go to **Settings** tab and click **New Authenticator**.
5. Select the authenticator you want to add and click **Next**.

    :::note

    You can configure predefined authenticators as well as the custom federated authenticators. See [Write a custom federated authenticator](../../references/extend/federation/write-a-custom-federated-authenticator.md) for more information.

    :::

6. Enter the requested details depending on the selected authenticator and click **Finish**.

:::tip

You can add multiple authenticators to the custom connector and select one authenticator as the default.

:::

## Enable login using the custom connector

:::note[Before you begin]

You need to [register an application with WSO2 Identity Server](../applications/index.md). You can register your own application or use one of the [sample applications](../../get-started/try-samples/index.md) provided.

:::

1. On the WSO2 Identity Server console, go to **Applications**.

2. Select your application, go to the **Login Flow** tab and add the custom connector from your preferred editor:

    
    1. Click **Add Sign In Option** to add a new authenticator to the first step.

    2. Select the custom connection.

    3. Click **Confirm** to add login with the custom connection to the sign-in flow.

        ![Configuring login with a custom connector in WSO2 Identity Server using the Visual Editor](../../../assets/img/guides/idp/custom-connector/add-custom-federation-with-visual-editor.png)
    

    <Recommendation />

3. Click **Update** to save your changes.

## Try it out

1. Access the application URL.

2. Click **Login** to open the WSO2 Identity Server login page.

3. On the WSO2 Identity Server login page, select the sign in option configured.

    ![Login with custom connector](../../../assets/img/guides/idp/custom-connector/sign-in-with-custom-connector.png)

4. Log in using an existing account in the authenticator selected (e.g. Google, Facebook, custom federated authenticator etc.)

5. The user is now redirected to the application and logged in.

## Map groups with WSO2 Identity Server

<AddGroups />

## Delete a connection

<DeleteConnection />
