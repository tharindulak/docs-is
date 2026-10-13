---
title: Outbound provisioning
deployment_options:
  - WSO2 Cloud
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/asgardeo/docs/guides/users/outbound-provisioning/outbound-provisioning-overview.md
---

# Outbound provisioning

Outbound provisioning automatically provisions user accounts from WSO2 Identity Platform to external systems. When enabled, user lifecycle events such as creation, updates, and deletion are synchronized in real-time with connected applications.

## Provisioning levels

WSO2 Identity Platform lets you configure outbound provisioning at the following levels:


- [Organization-level](setup-outbound-provisioning.md): Organization-level outbound provisioning acts as the default provisioner for all applications. You can override this by configuring an **application-level** outbound provisioner. With organization-level outbound provisioning, users are automatically provisioned to external systems when:
    - a user is provisioned in WSO2 Identity Platform over an API.
    - an administrator onboards a user from the WSO2 Identity Platform Console.
    - a user self-signs up from a WSO2 Identity Platform login page.
    - a user is JIT provisioned in WSO2 Identity Platform.

- [Application-level](setup-outbound-provisioning.md): Application-level outbound provisioning is specific to an individual application. If an application does not have its own outbound provisioner configured, it defaults to the organization-level outbound provisioner. When application-level provisioning is enabled, users are automatically provisioned to the external system when:
    - a user is created using a token retrieved by the application.
    - a user is JIT provisioned through the application.



## Group-based provisioning

In addition to provisioning levels, you can refine your provisioning criteria by managing which users are provisioned based on their assigned groups. Group-based provisioning can be applied alongside both organization-level and application-level provisioning to further filter which users are provisioned based on group membership.

Learn more about [group-based provisioning](group-based-provisioning.md).


## Outbound connectors



<Applies to="WSO2 Cloud">

WSO2 Identity Platform supports provisioning users via [SCIM2](outbound-connectors/scim2.md).

</Applies>



<Applies to="Self-hosted">

WSO2 Identity Server supports provisioning users via the following outbound connectors:

- [Google](outbound-connectors/google.md)
- [Salesforce](outbound-connectors/salesforce.md)
- [SCIM2](outbound-connectors/scim2.md)

</Applies>



## Provisioning attributes

When a provisioning request uses a token issued to an authorized application (other than the Console application), WSO2 Identity Platform applies attribute filtering. Only the attributes requested by that application are provisioned to the external system.
