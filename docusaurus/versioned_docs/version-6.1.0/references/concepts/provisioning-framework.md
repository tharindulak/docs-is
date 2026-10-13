---
title: Identity Provisioning Framework
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.1.0/docs/references/concepts/provisioning-framework.md
---

# Identity Provisioning Framework 

The identity provisioning framework is the main component that handles user/role provisioning in WSO2 Identity Server (WSO2 IS). The WSO2 Identity Provisioning framework can be separated into three main components:

- **Inbound provisioning**: used by the external applications to provision users to WSO2 Identity Server 
- **Outbound provisioning**: responsible for provisioning users from WSO2 Identity Server to external applications
- **Userstore management**: used to persist users within the system

<img name='sso-diagram' src='/identity/assets/img/concepts/provisioning-framework.png' className='img-zoomable' />

---

## Inbound provisioning

Inbound provisioning focuses on how to provision users to WSO2 IS.  

The userstore manager receives provisioning requests from the provisioning framework. These provisioning requests are handled and the relevant userstore is updated. The request can affect multiple userstores if the configuration is such. Once this request has been handled, an update is sent back to the provisioning framework.

---

## Outbound provisioning

Outbound provisioning focuses on provisioning users to external systems. This can be initiated by any of the following.

- An inbound provisioning request (initiated by a service provider or the resident service provider)
- JIT provisioning (initiated by a service provider)
- Adding a user via the WSO2 IS portal
- Assigning a user to a provisioning role 

WSO2 Identity Server supports outbound provisioning with the following connectors. 

- SCIM
- SPML

- Google Apps provisioning API
- Salesforce provisioning API

To set up outbound provisioning, one or more outbound provisioning connectors need to configured for a given identity provider, and the identity provider should be associated with an application. All the provisioning requests must be initiated by an application registered in WSO2 IS and will be provisioned to all the identity providers configured in the outbound provisioning configuration of the corresponding application. 

The provisioning request comes into the outbound provisioning component from the provisioning framework. This request will then go to the relevant connector.

:::info[Related topics]

- [Concept: Provisioning](identity-provisioning-intro.md)
- [Guide: Inbound Provisioning](../../guides/identity-lifecycles/inbound-provisioning.md)
- [Guide: Outbound Provisioning](../../guides/identity-lifecycles/outbound-provisioning.md)

:::
