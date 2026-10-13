---
title: Get Started with the Management Console
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.0.0/docs/deploy/get-started/get-started-with-the-management-console.md
---

# Get Started with the Management Console

The WSO2 Identity Server Management Console is a web-based user
interface. It allows users to interact with a running identity server
instance, without having to intervene with any underlying
configuration files. The controls in the Management Console are usually
self-explanatory. This page provides an overview of the user interface of the 
management console. 

:::info

You can access the management console of the WSO2 Identity
server at `https://<server-host>:<server-port>/carbon`. When the server
is [running](run-the-product.md) in your local setup:
        
```
https://localhost:9443/carbon
```

The default credentials for an administrative user is as follows. It is a
must that you change this administrator credentials in the `<IS_HOME>/repository/conf/deployment.toml` file.

```java
username = admin
password = admin
```

:::

The following screen depicts the home screen of the management console.

![Management Console Home Screen](../../../../assets/img/deploy/server_home_management_console.png)

The main menu items of the console appear in the left hand side of the 
home screen. Each of these menus carry a list of sub menus. These menus and subsections will 
navigate you via different configurations and features. The usable features for each
sub section will appear in the middle of the screen. 

The Management Console provides a list of tools and
features that you can use. These are divided among the following menu items.

-   Main menu
-   Monitor menu
-   Configure menu
-   Tools menu

:::note

The menus and sub menus of the management console may vary depending on the 
product version and any additional feature you have installed to provision the
server.

:::

---

## Main menu

The main menu in the Management Console includes the main list of
features that the WSO2 Identity Server provides. The main menu is
divided into different sections.

---

### Identity section

![identity-section-mgt-console](../../../../assets/img/deploy/identity-section-mgt-console.png)

:::info[Related topics]

Refer to the following topics for instructions to use sub menu items.
-   [Guide: Manage User Operations](../../guides/identity-lifecycles/manage-user-overview.md) 
    for configuring users and roles. 
-   [Guide: Manage User Roles](../../guides/identity-lifecycles/manage-roles-overview.md)
-   [Deploy: Configure the Realm](../configure-the-realm.md) for configuring user stores.
-   [Guide: Manage User Attributes](../../guides/identity-lifecycles/manage-user-attributes.md) for configuring claims.

:::

---

### Entitlement section

![entitlement-section-mgt-console](../../../../assets/img/deploy/entitlement-section-mgt-console.png)



---

### Manage section

![manage-section-mgt-console](../../../../assets/img/deploy/manage-section-mgt-console.png)

:::info[Related topics]

Refer to the following topics for instructions to use sub menu items.

-   [Guide: Manage Challenge Questions](../../guides/password-mgt/challenge-question.md)
    for information on configuring challenge questions. Also see [Account Recovery](../../guides/my-account/recover-user-account.md) for
    information on challenge questions.
-   [Guide: Email Sender Configurations](../configure-email-sending.md) for configuring email
    sender. Also see [Customizing Automated Emails](../../guides/tenants/customize-automated-mails.md)
    for information on how to customize these templates.
-   [Deploy: Create New Keystores in the WSO2 Administration Guide](../security/create-new-keystores.md) for configuring keystores.


:::
---

## Monitor menu

The monitor menu includes a list of features focused on providing logs
and statistics related to the Identity Server. For more
information on these features and their usage, see the topics on
[monitoring the Identity Server](../monitor/monitor-the-identity-server.md).


![monitor-section-mgt-console](../../../../assets/img/deploy/monitor-section-mgt-console.png)

---

## Configure menu

The configure menu is mainly a list of administration features which can
help you customize and configure the Identity Server to suit your
specific requirements.

![configure-section-mgt-console](../../../../assets/img/deploy/configure-section-mgt-console.png)

:::info[Related topics]

Refer to the following topics for instructions to use sub menu items.

-   See [Creating and Managing Tenants](../../guides/tenants/tenant-mgt.md)
    for information on multitenancy.



:::
    

:::note

`Server Roles` are used with Carbon Apps. From WSO2 Identity Server 5.9.0, this feature is not available.

:::

---

## Tools menu

The tools menu includes SAML and XACML tools.


![tools-section-mgt-console](../../../../assets/img/deploy/tools-section-mgt-console.png)
