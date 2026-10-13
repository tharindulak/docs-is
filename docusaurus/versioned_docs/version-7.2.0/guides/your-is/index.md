---
title: Your WSO2 Identity Server
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.2.0/docs/guides/your-is/index.md
---

# Your WSO2 Identity Server

When you start the WSO2 Identity Server, an organization get created by default. It functions as the **organization (root)** in your WSO2 Identity Server.

Listed below are the main characteristics of an organization (root).

- An organization (root) contains applications, external identity providers, and user identities belonging to a single domain.

- The admin user configured under realm configuration in `<IS_HOME>/repository/conf/user-mgt.xml` is the owner of the organization (root).

If you are an owner of an organization (root) or an administrator, you can manage your WSO2 Identity Server accounts [using the My Account portal](is-self-service.md).

The owner is a user who creates an organization (root) in WSO2 Identity Server. This grants the owner all the administrative rights by default. An administrator is a user who is invited in to the organization (root) and assigned administrative privileges.
