---
title: Delete your user account
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.1.0/docs/guides/your-is/delete-your-user-account.md
---

# Delete your user account

If you have a requirement to delete your own user account from WSO2 Identity Server, see the guidelines and instructions given below.

## Owners

If you are the owner of one or multiple WSO2 Identity Server organizations, you will have user accounts (of type **Owner**) in each organization. Currently, you are not allowed to remove your owner accounts or to transfer your ownership of organizations to other users.

To delete your owner account(s), you need to [remove the organizations that you own](/identity/7.1.0/guides//#delete-root-organizations).

## Administrators

If you want to remove your administrator account from an organization, you need to send a request to another 
administrator in the organization. See the instruction on [deleting administrators](../users/manage-administrators.md#delete-an-administrator).

:::note

Note that removing your administrator account from one organization only removes your association with that organization. Your administrator account will continue to persist in other organizations that you are associated with.

:::
