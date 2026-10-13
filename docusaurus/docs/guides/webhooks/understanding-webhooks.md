---
title: Understanding webhooks
deployment_options:
  - WSO2 Cloud
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/asgardeo/docs/guides/webhooks/understanding-webhooks.md
---

# Understanding webhooks

Webhooks enable your applications to receive instant notifications from WSO2 Identity Platform, allowing you to respond immediately to important identity-related events. Common use cases for WSO2 Identity Platform webhooks include:

- Automatically provision users or send welcome notifications upon successful user registration.
- Update external user directories or CRM systems whenever a user profile changes.
- Notify external services or security teams immediately upon password changes or resets.
- Integrate with SIEM systems to instantly detect and respond to suspicious login attempts or failed authentications.

Using webhooks, you can seamlessly integrate external systems with WSO2 Identity Platform's identity flows. When an event happens, WSO2 Identity Platform immediately sends HTTP callbacks to your configured webhook endpoints.



<Applies to="WSO2 Cloud">

WSO2 Identity Platform webhooks use the [WebSubHub](https://websubhub.com/) protocol for secure and reliable event delivery.

</Applies>



## How webhooks work

When an identity-related event (for example user registration, login success, profile update) occurs within WSO2 Identity Platform, it automatically generates a notification event. WSO2 Identity Platform sends this event as an HTTP request to your configured webhook URL. The request contains detailed information encoded in a structured JSON payload.

## Webhook event types

WSO2 Identity Platform supports webhooks for identity-related events categorized as follows:

- **Login events**
      - Login success
      - Login failure
- **Registration events**
      - Registration success
      - Registration failure
- **Token events**
      - Access token issued
      - Access token revoked
- **Session events**
      - Session established
      - Session presented
      - Session revoked
- **Credential events**
      - Credential updates
- **User Account Management events**
      - User profile updates
      - User account status changes (lock/unlock, enable/disable, delete)

- **Role management events**
      - Role created
      - Role metadata updated
      - Role deleted
      - Role users updated
      - Role groups updated
      - Role IdP groups updated
      - Role permissions updated
- **Consent events**
      - Consent added
      - Consent revoked
- **Consent purpose events**
      - Purpose version added


Each webhook event payload includes structured details compliant with the [Security Event Token (SET) specification (RFC 8417)](https://datatracker.ietf.org/doc/html/rfc8417), containing issuer information, timestamp, unique identifiers, user and organization context, and event-specific metadata.
