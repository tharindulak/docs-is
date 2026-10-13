---
title: Impersonation for shared users
deployment_options:
  - WSO2 Cloud
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/asgardeo/docs/guides/organization-management/shared-user-impersonation.md
---

# Impersonation for shared users

Shared users are users whose profiles are managed by a parent organization but [shared with child organizations](share-user-profiles.md). This guide explains how to allow shared users to impersonate other users within those child organizations.

To allow shared users to perform impersonation, the login flow of the relevant application must be updated to include the **Shared User Identifier** authenticator as its first step. This lets WSO2 Identity Platform resolve the shared user's resident profile before proceeding with the remaining authentication steps. Learn more about [allowing shared users to log in to organizations](shared-user-direct-login.md).

## Prerequisites

- The impersonator's user profile must be [shared with the organization](share-user-profiles.md) where impersonation will take place.

- The target organization must have user impersonation already configured. If not, follow the steps in one of the guides below before proceeding:
  - [User impersonation via Console](../authorization/user-impersonation/via-console.md)
  - [User impersonation via business application](../authorization/user-impersonation/via-business-application.md)

## Impersonate via the console

To enable shared user impersonation via the Console, update the Console application's login flow in the target organization. Add the **Shared User Identifier** authenticator as its first step.

### Update the console login flow

1. Sign in to the WSO2 Identity Platform Console of the **target organization**.

2. Go to **Console Settings** and go to the **Login Flow** tab.

3. Add the **Shared User Identifier** as the first step of the login flow.

    <Tabs>
    <TabItem value="tab-0" label="Classic Editor">


    1. In the first step, click **Add Authentication** and select **Shared User Identifier**.

        :::note

        Remove the **Username & Password** authenticator from the first step. The **Shared User Identifier** must be the only authenticator in the first step.

        :::

    2. Add a second authentication step by clicking the **+** icon and add your preferred authenticators (such as **Username & Password** or a passwordless option) to this step.

    </TabItem>
    <TabItem value="tab-1" label="Visual Editor">


    1. Switch to the **Visual Editor** tab.

    2. In the first step, click **+ Add Sign In Option** and select **Shared User Identifier**.

        :::note

        Remove the **Username & Password** authenticator from the first step. The **Shared User Identifier** must be the only authenticator in the first step.

        :::

    3. Add a second authentication step by clicking the **+** icon and add your preferred authenticators to this step.

    </TabItem>
    </Tabs>

4. Click **Update** to save your changes.

Once configured, when a shared user logs in to the Console they will be prompted for their identifier in the first step. WSO2 Identity Platform resolves the resident profile and then engages the authenticators in the second step to complete login.

The shared user can then follow the [standard Console impersonation steps](../authorization/user-impersonation/via-console.md##impersonate-users-in-an-organization) to impersonate users within the organization.

## Impersonate via a business application

For a shared user to impersonate another user through a business application, add the **Shared User Identifier** authenticator as the first step of that application's login flow.

### Update the application login flow

1. Sign in to the WSO2 Identity Platform Console of the **target organization**.

2. Go to **Applications** and select the application that the shared user will use for impersonation.

3. Go to the application's **Login Flow** tab.

4. Add the **Shared User Identifier** as the first step of the login flow.

    <Tabs>
    <TabItem value="tab-0" label="Classic Editor">


    1. In the first step, click **Add Authentication** and select **Shared User Identifier**.

        :::note

        Remove the **Username & Password** authenticator from the first step. The **Shared User Identifier** must be the only authenticator in the first step.

        :::

    2. Add a second authentication step by clicking the **+** icon and add your preferred authenticators (such as **Username & Password** or a passwordless option) to this step.

    </TabItem>
    <TabItem value="tab-1" label="Visual Editor">


    1. Switch to the **Visual Editor** tab.

    2. In the first step, click **+ Add Sign In Option** and select **Shared User Identifier**.

        :::note

        Remove the **Username & Password** authenticator from the first step. The **Shared User Identifier** must be the only authenticator in the first step.

        :::

    3. Add a second authentication step by clicking the **+** icon and add your preferred authenticators to this step.

    </TabItem>
    </Tabs>

5. Click **Update** to save your changes.

Once configured, shared users can follow the [standard business application impersonation steps](../authorization/user-impersonation/via-business-application.md#step-3-get-tokens-for-user-impersonation) to get a subject token and exchange it for an impersonated access token.
