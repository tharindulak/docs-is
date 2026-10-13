---
title: Outbound provisioning
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.2.0/docs/guides/users/outbound-provisioning/index.md
---

# Outbound provisioning

Outbound provisioning automatically provisions user accounts from WSO2 Identity Server to external systems. When enabled, user lifecycle events such as creation, updates, and deletion are synchronized in real-time with connected applications.

## Provisioning levels

WSO2 Identity Server lets you configure outbound provisioning at the following levels:


- [Organization-level](setup-outbound-provisioning.md): Users are automatically provisioned to the external system when:
    - a user is provisioned in WSO2 Identity Server over an API.
    - an administrator onboards a user from the WSO2 Identity Server Console.
    - a user self-signs up from a WSO2 Identity Server login page.
    - a user is JIT provisioned in WSO2 Identity Server.



## Role-based provisioning

In addition to provisioning levels, you can refine your provisioning criteria by managing which users are provisioned based on their assigned roles.

Learn more about [role-based provisioning](role-based-provisioning.md).


## Outbound connectors


WSO2 Identity Server supports provisioning users via the following outbound connectors:

- [Google](outbound-connectors/google.md)
- [Salesforce](outbound-connectors/salesforce.md)
- [SCIM2](outbound-connectors/scim2.md)


## Provisioning attributes

When a provisioning request uses a token issued to an authorized application (other than the Console application), WSO2 Identity Server applies attribute filtering. Only the attributes requested by that application are provisioned to the external system.
