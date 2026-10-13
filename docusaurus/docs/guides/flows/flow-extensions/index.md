---
title: Flow extensions
deployment_options:
  - WSO2 Cloud
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/asgardeo/docs/guides/flows/flow-extensions/index.md
---

# Flow extensions

A **flow extension** lets you call your own external service from within a flow. This allows you to inject custom business logic, such as validation, enrichment, or risk evaluation, into a user journey without building it into the flow itself.

## Supported flows

You can add a flow extension to any of the following flows.

| Flow | Flow type in the request |
| ---- | ------------------------ |
| [Self Registration](../self-registration.md) | `REGISTRATION` |
| [Password Recovery](../password-recovery.md) | `PASSWORD_RECOVERY` |
| [Invited User Registration](../invited-user-registration.md) | `INVITED_USER_REGISTRATION` |

You can reuse one extension across more than one flow. Every request tells your endpoint which flow invoked it, so a single service can branch on the flow type instead of you registering a separate extension per flow.

## How it works

A flow extension follows a simple request-response cycle:

1. A user reaches the step in the flow where the extension is placed.
2. WSO2 Identity Platform sends a request to your endpoint, **exposing** the attributes you have marked as readable (for example, the user's email address and the application ID).
3. Your service runs its logic and responds with the attributes you have marked as writable.
4. WSO2 Identity Platform writes the returned values back into the flow as user attributes (claims) and continues to the next step.

Because the logic runs entirely in your own service, you control the data sources and business rules without embedding them into the flow itself.

## What an extension can read and write

An extension only ever sees and changes what you allow. You declare this per attribute in the extension's access configuration, using two independent access levels.

- **Read:** Retrieves the attribute's current value and includes it in the request that WSO2 Identity Platform sends to your endpoint.
- **Write:** Allows your endpoint to return a value for that attribute, which WSO2 Identity Platform then applies to the flow.

WSO2 Identity Platform enforces these declarations on both legs of the call. The request carries only the attributes you marked as **Read**, and an `allowedOperations` whitelist that names exactly the attributes you marked as **Write**. Anything your endpoint returns outside that whitelist is discarded.

Two things narrow this further. WSO2 Identity Platform owns a small number of attributes that no extension may write, and a few attributes are available only in some flows. So an extension reused across flows can legitimately receive a smaller payload in one flow than in another. For the full picture, see [attribute access levels](../flow-extension-configuration.md#attribute-access-levels).

You can also encrypt individual field values exchanged with your endpoint, so sensitive data such as credentials never travels in plain text. To learn more, see [configure field encryption](../flow-extension-configuration.md#step-4-configure-field-encryption).

## What's next

- [Flow extension configuration](../flow-extension-configuration.md) - Register your external service as a flow extension, map the attributes it reads and writes, and add it to a flow.
- [Implement an external service for flow extension](../flow-extension-external-service.md) - Build the endpoint that WSO2 Identity Platform calls, including the request and response contract it must follow.
