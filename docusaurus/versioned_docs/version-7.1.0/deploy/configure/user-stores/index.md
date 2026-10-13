---
title: Introduction to Realms
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.1.0/docs/deploy/configure/user-stores/index.md
---

# Introduction to Realms

The user management functionality is provided by default in WSO2 Identity Server and is configured in the
`deployment.toml` file found in the
`<IS_HOME>/repository/conf/` directory. 

The complete functionality and contents of the user management module are called a **user realm**. The realm includes the user management
classes, configurations, and user stores that store information. Configuring the user management functionality in WSO2 Identity Server involves setting up the relevant user stores and updating the relevant configuration files.

The following diagram illustrates the required configurations and repositories.

![configuring the realm](../../../../../assets/img/setup/configure/configuring-the-realm.png)

## User Stores

User stores are used to store all the users, roles, and permissions within our realm. WSO2 Identity Server (WSO2 IS) supports JDBC, LDAP, and Active Directory user stores by default with the capability of configuring custom user stores. 

There are two types of user stores.
 
- Primary user store (Mandatory)
- Secondary user stores (Optional) 

All the supported user stores can be categorized under these two types. There are different user store adapters called *user store managers*, which are used to connect with these user store types. 

The different types of user stores and how they can be configured to store the users and roles are explained in the [Manage user stores](../../../guides/users/user-stores/index.md) section.
