---
title: Manage roles
deployment_options:
  - WSO2 Cloud
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/asgardeo/docs/guides/users/manage-roles.md
---

# Manage roles

A role is simply a collection of permissions. As roles facilitate adding, removing and updating permissions collectively, it is a convenient way of managing permissions rather than doing it individually for each user. You can assign users and groups to one or many roles. When a group is assigned to a role, all group members inherit the permissions of the role.

In WSO2 Identity Platform, roles play a crucial role in controlling access to APIs and applications. Based on the audience, you can define the following two types of roles.

- **Application level** - Roles tailored to a specific application. Used to control access to [API resources authorized for the application](../authorization/api-authorization/api-authorization.md#authorize-the-api-resources-for-an-app).

- **Organization level** - Roles that are available throughout the organization and used to control access to API resources of an organization. Suited for organizations having multiple applications sharing the same login, registration and authorization requirements (such as applications with both a web and a mobile component).

    :::note

    - API resources of an organization consist of [management APIs](../../apis/index.md), [organization APIs](../../apis/index.md) and [registered APIs](../authorization/api-authorization/api-authorization.md#register-an-api-resource).

    - Applications can be set to work with application roles or organization roles. Learn how to [select the role audience for an application](../authorization/api-authorization/api-authorization.md#set-the-role-audience-for-apps).

    :::

## Create a role

To create a role and assign permissions to it:

1. On the WSO2 Identity Platform Console, go to **User Management** > **Roles**.

2. Click **New Role** and provide a name that is unique to the specified audience.

3. Select the role audience. Choose,

     - **Application** if the role is meant for a single application and select the relevant application from the dropdown.

     - **Organization** if the role is intended for multiple applications.

    :::warning

    Once a role is created, you cannot modify the selected audience.

    :::

    ![create new role](../../../assets/img/guides/roles/create-role.png)

4. Click **Next**.

5. Select one or more API resources from the dropdown.

    - If the audience is **Application**, select from the [API resources authorized for the application](../authorization/api-authorization/api-authorization.md#authorize-apps-to-consume-api-resources).

    - If the audience is **Organization**, select from your organization's API resources.

    ![Assign permission on role creation](../../../assets/img/guides/roles/assign-permissions-to-role-on-creation.png)

7. Under each API resource, select the check box to grant all permissions or use the dropdown to grant limited permissions.

6. Click **Finish**.

## Assign users to a role

To assign users to a role:

1. On the WSO2 Identity Platform Console, go to **User Management > Roles**.

2. Select the role to which you wish to assign users.

3. Navigate to its **Users** tab.

    ![Assign users to role](../../../assets/img/guides/roles/assign-users-to-role.png)

4. Click **Assign User** and select users to add to the role.

5. Click **Update**.

## Assign groups to a role

To assign groups to a role:

1. On the WSO2 Identity Platform Console, go to **User Management > Roles**.

2. Select the role to which you wish to assign user groups.

3. Navigate to its **Groups** tab.

    ![Assign user groups to role](../../../assets/img/guides/roles/assign-usergroups-to-role.png)

4. Select the groups you wish to add from the dropdown under **Local Groups**.

5. Click **Update**.

## Assign external groups to a role

You can assign groups of an external Identity Provider (IdP) to an application role by following the steps below.

:::note[Prerequisites]


- Enable application users to login with an external IdP. Learn more in [Add standard-based login](../authentication/standard-based-login/index.md)
- [Configure groups for the IdP](../authentication/index.md#add-groups-to-connections).

:::

To assign external groups to an application role:

1. On the WSO2 Identity Platform Console, go to **User Management > Roles**.

2. Select the role to which you wish to assign IdP groups.

3. Navigate to its **Groups** tab.

    ![Assign IdP groups to role](../../../assets/img/guides/roles/assign-idpgroups-to-role.png)

4. Select the relevant IdP under **External Groups** and select the groups from the dropdown.

5. Click **Update**.

## Edit permissions of a role

To edit permissions of a role:

1. On the WSO2 Identity Platform Console, go to **User Management > Roles**.

2. Select the role for which you wish to edit permissions.

3. Navigate to its **Permissions** tab and make the following changes as necessary.

    - **Add a new API**:
        - Select the API resource from the dropdown.

        - For the selected API resource, select the checkbox to grant all permissions or use the dropdown to select limited permissions.

    - **Remove an API**:
        - click the cross icon next to the API name.

    - **Add new permissions to a selected API**:
        - select permissions from the dropdown of the selected API.

    - **Remove permissions from a selected API**:
        - click the **X** icon next to the permission listed under the API.

    ![Update permissions of a role](../../../assets/img/guides/roles/update-permissions-of-role.png)

5. Click **Update**.

## Remove users from a role

To remove users from a role:

1. On the WSO2 Identity Platform Console, go to **User Management > Roles**.

2. Select the role from which you wish to remove users.

3. Navigate to its **Users** tab.

4. Move the relevant users to **Removing users** by clicking the **X** icon next to their usernames.

    ![Remove users from role](../../../assets/img/guides/roles/remove-users-from-role.png)

5. Click **Update**.

## Remove groups from a role

To remove local/external user groups from a role:

1. On the WSO2 Identity Platform Console, go to **User Management > Roles**.

2. Select the role from which you wish to remove user groups.

3. Navigate to its **Groups** tab.

4. Move the relevant groups to **Removing groups** by clicking the **X** icon next to their names.

    ![Remove user groups from role](../../../assets/img/guides/roles/remove-usergroups-from-role.png)

5. They will be added to **Removing groups** section.
6. Click **Update**.

## Delete a role

To delete a role:

1. On the WSO2 Identity Platform Console, go to **User Management > Roles**.

2. Click the trash icon next to the role you wish to delete.

    :::note

    Deleting an application role also removes the association it has with the respective application.

    :::

3. Select the checkbox and confirm your action.

## What's next?

Learn how you may use roles to implement [Role-based Access Control (RBAC)](/identity/guides/api-authorization/).
