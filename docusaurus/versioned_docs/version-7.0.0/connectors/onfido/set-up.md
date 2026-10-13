---
title: Set up
mkdocs_template: connector
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.0.0/docs/connectors/onfido/set-up.md
---

# Set up

The following guide explains how you can install and set up Onfido in WSO2 Identity Server.

## Prerequisites

- You need to have an Onfido account. To create one, [contact](https://onfido.com/signup/) the Onfido team.

- Ensure comparison checks are enabled in your Onfido account. For more details, refer to the [Onfido comparison checks documentation](https://documentation.onfido.com/api/latest/#data_comparison).

## Step 1: Install the Onfido connector

Installing Onfido in WSO2 Identity Server involves two main steps, installing the connector file and installing the web application and resources that handle identity verification requests and responses from Onfido.

### Step 1.1: Install the connector file

1. From the WSO2 Identity Server [Connector Store](https://store.wso2.com/connector/identity-verification-onfido), download `org.wso2.carbon.identity.verification.onfido.connector-<version>.jar`.

2. Copy the `jar` file into the `<IS_HOME>/repository/components/dropins` directory of your WSO2 Identity Server installation.

### Step 1.2: Install the web application and resources

1. Download the `artifacts.zip` file from the WSO2 Identity Server [Connector Store](https://store.wso2.com/connector/identity-verification-onfido).

2. Extract the downloaded zip file.

3. From the extracted folder, copy the `idv#onfido.war` file and paste it into the `<IS_HOME>/repository/deployment/server/webapps` directory.

4. In the same extracted folder, copy the `onfido` directory and paste it into the `<IS_HOME>/repository/resources/identity/extensions/identity-verification-providers` directory.

### Step 1.3: Configure access control for Onfido

1. Configure the access control for Onfido by adding the following configuration the `<IS_HOME>/repository/conf/deployment.toml` file.

    ```toml
    [[resource.access_control]]
    context = "(.*)/idv/onfido/v1/(.*)/verify"
    secure = "false"
    http_method = "POST"

    [tenant_context]
    enable_tenant_qualified_urls = "true"
    enable_tenanted_sessions = "true"
    rewrite.custom_webapps = ["/idv/onfido/"]
    ```

2. Restart WSO2 Identity Server to apply changes.

## Step 2: Integrate your Onfido account with WSO2 Identity Server

Now that you have installed the Onfido connector, follow the steps below to integrate your Onfido account with WSO2 Identity Server.

### Step 2.1: Connect your Onfido account with WSO2 Identity Server

1. On the WSO2 Identity Server Console, go to **Connections** and click **New Connections**.

2. In the list of templates, find the **Onfido** card and click **Create** to add it.

3. Enter a name for the Onfido connector and the necessary configurations:

    - **API Token**: The API token generated via the Onfido dashboard.
    - **Workflow ID**: The unique identifier for the Workflow created using Workflow Studio. For more information refer to the [Onfido Workflow Studio](https://documentation.identity.entrust.com/getting-started/onfido-studio-product/).
    - **Base URL**: The regional base URL for Onfido API calls.
  
4. Click **Create** to create the Onfido connector.

5. On the created connection, note the URL displayed under the **Setup Guide**.

### Step 2.2: Generate and register an Onfido webhook

1. Log in to your Onfido dashboard and navigate to the Webhook configuration section.

2. Generate a Webhook token by providing the URL you noted earlier and selecting only the `workflow_run.completed` event. Onfido will use this webhook to send verification results to WSO2 Identity Server.

3. On the WSO2 Identity Server Console, return to the created connection and navigate to its **Settings** tab.

4. Enter the obtained token in the Webhook Token field, then click **Update** to finish the setup.

### Step 2.3: Map the Onfido attributes with that of WSO2 Identity Server

1. Open the created **Onfido** connection and go to its Attributes tab.

2. Update the mandatory first name and last name attribute mappings to match your Onfido configuration.

3. To add additional attributes,

    1. Click **Add Attribute Mapping**.
    2. Enter the external attribute and select the corresponding local user attribute.

4. Click **Update** to save the changes.

You have now successfully installed the Onfido connector and integrated your Onfido account with WSO2 Identity Server.
