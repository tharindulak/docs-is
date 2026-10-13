---
title: Role-based Permissions
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.0.0/docs/guides/identity-lifecycles/role-based-permissions.md
---

# Role-based Permissions

Permission can be granted to a role at two levels:

- **Super tenant level:** A role with super tenant permissions is used for managing all the tenants in the system and also for managing the key features in the system which are applicable to all the tenants.

- **Tenant level:** A role with tenant-level permissions is only applicable to individual tenant spaces.

You need to first have roles created in your tenant with the required permissions. You can then assign the role to users.

Users with the `admin` role are granted all permissions by default. Let's see how to configure a user with `admin` permissions.

## Configure admin permissions for a user

:::note[Prerequisites]

You need to [create a new user](admin-creation-workflow.md) on the management console.

:::

To configure admin permissions for a user:

1. On the Management Console, go to **Users and Roles > List > Users**.
2. Click **Assign Roles** to assign all administrative permissions for the created user.
    ![Assign roles to Alex](../../../../assets/img/guides/assign-roles.png)
3. Select **admin** and click **Update**.
    ![Assign login permissions to Alex](../../../../assets/img/guides/assign-login-permissions.png)

The user will be granted login permissions for the management console along with other admin permissions. See the complete list of [access permissions](#access-permissions) given below.

## Access permissions

The permissions navigator that you use to enable permissions for a role is divided into two categories (**Super Admin** permissions and **Admin** permissions), as shown below. However, note that there may be other categories of permissions enabled for a WSO2 product depending on the type of features that are installed in the product.

![](../../../../assets/img/fragments/role-permissions.png)

You can access the permissions navigator for a particular role by clicking **Permissions** as shown below.  

![](../../../../assets/img/fragments/permission-navigator.png)

By default, every WSO2 Identity Server comes with the default [user](../../references/concepts/user-management/users.md) and [role](../../references/concepts/user-management/roles-and-permissions.md).

- The **Admin** role has all the permissions in the system enabled by default. Therefore, this is a super tenant with all permissions enabled.

    :::tip

    You can change the default role name '**admin**' of the Administrative role as described [here](edit-delete-roles.md)

    :::

You can create new users and roles and configure permissions for the roles using the management console. However, note that you cannot modify the permissions of the **Admin** role. The possibility of managing users, roles, and permissions is granted by the **User Management** permission.

## Permissions

The descriptions of permissions in the **Permissions** navigator are as follows:

- The **Login** permission defined under **Admin** permissions allows users to log in to the product's management console. Therefore, this is the primary permission required for using the management console.

- The following table describes the permissions at the **Super Tenant** level. These are also referred to as **Super Admin** permissions.

    <table><colgroup><col /><col /></colgroup><thead><tr className={"header"}><th>{"Permission"}</th><th>{"Description of UI menus enabled"}</th></tr></thead><tbody><tr className={"odd"}><td><strong>{"Configuration"}</strong>{" permissions:"}<br />{" "}<img src={"/identity/assets/img/fragments/super-admin-config.png"} /></td><td>{"The "}<strong>{"Super Admin/Configuration"}</strong>{" permissions are used to grant permission to the key functions in a product server, which is common to all the tenants. In each WSO2 product, several configuration permissions will be available depending on the features installed in the product."}<br />{" "}<br />{" "}<strong>{"- Feature Management"}</strong>{" permission ensures that a user can control the features installed in the product using the management console. That is, the "}<strong>{"Features"}</strong>{" option will be enabled under the "}<strong>{"Configure"}</strong>{" menu."}<br />{" "}<strong>{"- Logging"}</strong>{" permission enables the possibility to configure server logging from the management console. That is, the "}<strong>{"Logging"}</strong>{" option will be enabled under the "}<strong>{"Configure"}</strong>{" menu."}</td></tr><tr className={"even"}><td><strong>{"Management"}</strong>{" permissions:"}<br />{" "}<img src={"/identity/assets/img/fragments/management-permissions.png"} /></td><td><p>{"The "}<strong>{"Super Admin/Manage"}</strong>{" permissions are used for adding new tenants and monitoring them."}</p><p><strong>{"- Modify/Tenants"}</strong>{" permission enables the "}<strong>{"Add New Tenant"}</strong>{" option in the "}<strong>{"Configure"}</strong>{" menu of the management console, which allows users to add new tenants."}<br />{" "}<strong>{"- Monitor/Tenants"}</strong>{" permission enables the "}<strong>{"View Tenants"}</strong>{" option in the "}<strong>{"Configure"}</strong>{" menu of the management console."}</p></td></tr><tr className={"odd"}><td><strong>{"Server Admin"}</strong>{" permissions:"}<br />{" "}<img src={"/identity/assets/img/fragments/server-admin-permissions.png"} /></td><td>{"Selecting the "}<strong>{"Server Admin"}</strong>{" permission enables the "}<strong>{"Shutdown/Restart"}</strong>{" option in the "}<strong>{"Main"}</strong>{" menu of the management console."}</td></tr></tbody></table>

- The following table describes the permissions at the **Tenant** level. These are also referred to as **Admin** permissions.

    :::info

    Note that when you select a node in the **Permissions** navigator, all the subordinate permissions that are listed under the selected node are also automatically enabled.

    :::

    :::note

    Also, not all permissions in the permission tree are listed here. You can get the information related to them throughout the documentation wherever applicable.

    :::


    <table><colgroup><col /><col /></colgroup><thead><tr className={"header"}><th>{"Permission level"}</th><th>{"Description of UI menus enabled"}</th></tr></thead><tbody><tr className={"odd"}><td>{"Admin"}</td><td><p>{"When the "}<strong>{"Admin"}</strong>{" permission node is selected, the following menus are enabled in the management console:"}</p><p><strong>{"- User Store Management:"}</strong>{" This permission allows users to add new user stores and manage them with the management console. Note that only secondary user stores can be added using this option. See the topic on "}<a href={"/identity/6.0.0/deploy/configure-user-stores/"}>{"user store management"}</a>{" for more details."}<br />{" "}<strong>{"- Identity Providers:"}</strong></p><p>{"- All permissions listed under "}<strong>{"Admin"}</strong>{" in the permissions navigator are selected automatically."}</p></td></tr><tr className={"even"}><td>{"Admin/Configure"}</td><td>{"When the "}<strong>{"Admin/Configure"}</strong>{" permission node is selected, the following menus are enabled in the management console:"}<br />{" "}<strong><br />{" - Main"}</strong>{" menu "}<strong>{"/PAP:"}</strong>{" - Main menu "}<strong>{"/PDP:"}</strong>{" - Tools menu "}<strong>{"/Tryit (XACML):"}</strong>{" - All permissions listed under "}<strong>{"Configure"}</strong>{" in the permissions navigator are selected automatically."}</td></tr><tr className={"odd"}><td>{"Admin/Configure/Security"}</td><td>{"When the "}<strong>{"Admin/Configure/Security"}</strong>{" permission node is selected, the following menus are enabled in the "}<strong>{"Configure"}</strong>{" menu of the management console:"}<br />{" "}<br />{" "}<strong>{"- Claim Management:"}</strong>{" See the topic on "}<a href={"/identity/6.0.0/guides/dialects/configure-claims/"}>{"claim management"}</a>{" for details on how to use this option."}<br />{" "}<strong>{"- Keystores:"}</strong>{" See the topic on "}<a href={"/identity/6.0.0/deploy/security/create-new-keystores/"}>{"keystores"}</a>{" for details on how to use this option. "}<strong><br /></strong>{" "}<strong>{"- Email Templates:"}</strong>{" See the topics on "}<a href={"/identity/6.0.0/guides/tenants/customize-automated-mails/"}>{"email templates"}</a>{" for details on how to use this option."}<br />{" "}<br />{" - This permission will also enable the "}<strong>{"Roles"}</strong>{" option under "}<strong>{"Configure/Users and Roles"}</strong>{" . See the topics on "}<a href={"/identity/6.0.0/guides/identity-lifecycles/manage-user-overview/"}></a>{"configuring Users, and "}<a href={"/identity/6.0.0/guides/identity-lifecycles/manage-roles-overview/"}>{"roles"}</a>{" for more information."}<br />{" "}<br />{" - Additionally, all permissions listed under "}<strong>{"Security"}</strong>{" in the permissions navigator are selected automatically."}</td></tr><tr className={"even"}><td>{"Admin/Configure/Security/Identity Management/User Management"}</td><td>{"This permission allows adding users from the management console. That is, the "}<strong>{"Users"}</strong>{" option will be enabled under "}<strong>{"Configure/Users and Roles"}</strong>{" ."}</td></tr><tr className={"odd"}><td>{"Admin/Configure/Security/Identity Management/Password Management"}</td><td>{"This permission enables the "}<strong>{"Change Password"}</strong>{" option for the users listed in the "}<strong>{"User Management/Users and Roles/Users"}</strong>{" screen, which allows the logged-in user to change the passwords"}</td></tr><tr className={"even"}><td>{"Admin/Configure/Security/Identity Management/Profile Management"}</td><td>{"This permission enables the "}<strong>{"User Profile"}</strong>{" option for the users listed in the "}<strong>{"User Management/Users and Roles/Users"}</strong>{" screen, which allows the logged-inuser to update user profiles."}</td></tr><tr className={"odd"}><td>{"Admin/Manage"}</td><td>{"When the "}<strong>{"Admin/Manage"}</strong>{" permission is selected, the following menus will be enabled in the management console:"}<br />{" "}<br />{" "}<strong>{"- Main"}</strong>{" menu "}<strong>{"/Service Providers:"}</strong>{" "}<strong>{"- Tools"}</strong>{" menu "}<strong>{"/SAML:"}</strong>{" "}<br />{" - Additionally, all permissions listed under "}<strong>{"Admin/Manage"}</strong>{" in the permissions navigator will be enabled automatically. "}<strong></strong></td></tr><tr className={"even"}><td>{"Admin/Manage/Resources/Browse"}</td><td>{"This permission enables the "}<strong>{"Browse"}</strong>{" option under the "}<strong>{"Registry"}</strong>{" menu in the main navigator. This option allows users to browse the resources stored in the registry using the "}<strong>{"Registry"}</strong>{" tree navigator. "}<strong><br /></strong></td></tr><tr className={"odd"}><td>{"Admin/Manage/Search"}</td><td>{"This permission enables the "}<strong>{"Search"}</strong>{" option under the "}<strong>{"Registry"}</strong>{" sub-menu in the "}<strong>{"Main"}</strong>{" menu. This option allows users to search for specific resources stored in the registry by filling in the search criteria. "}<strong><br /></strong></td></tr><tr className={"even"}><td>{"Admin/Monitor"}</td><td>{"When the "}<strong>{"Admin/Monitor"}</strong>{" permission node is selected, the following menus are enabled in the management console:"}<br />{" "}<br />{" "}<strong>{"- Monitor"}</strong>{" menu "}<strong>{"/System Statistics:"}</strong>{" See the topic on "}<a href={"/identity/6.0.0/deploy/monitor/system-statistics/"}>{"system statistics"}</a>{" for information on how to use this option."}<br />{" "}<br />{" - Additionally, all permissions listed under "}<strong>{"Admin/Monitor"}</strong>{" in the permissions navigator will be enabled automatically."}</td></tr><tr className={"odd"}><td>{"Admin/Monitor/Logs"}</td><td>{"When the "}<strong>{"Admin/Monitor/Logs"}</strong>{" permission node is selected, the following menus are enabled in the management console:"}<br />{" "}<br />{" "}<strong>{"- Monitor"}</strong>{" menu "}<strong>{"/Application Logs"}</strong><br />{" "}<strong>{"- Monitor"}</strong>{" menu "}<strong>{"/System Logs"}</strong><br />{" "}<br />{" See the topic on "}<a href={"/identity/6.0.0/deploy/monitor/monitor-logs/"}>{"system logs"}</a>{" for information on how to use these options."}</td></tr></tbody></table>



:::info[Related topics]

- [Concept: Roles and Permissions](../../references/concepts/user-management/roles-and-permissions.md)
- [Guide: Edit/Delete Roles](edit-delete-roles.md)

:::
