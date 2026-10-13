---
title: Setup webhooks
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.2.0/docs/guides/webhooks/setup-webhooks.md
---

# Setup webhooks

This guide provides a step-by-step approach to setting up webhooks in WSO2 Identity Server to integrate external systems.

## Prerequisites

Ensure that you have:

- Access to the WSO2 Identity Server console.
- Ability to implement a web service or endpoint accessible to WSO2 Identity Server.

## Create the external service

Your external web service should do the following to receive event notifications:

1. Implement the service according to the [webhook event payload contract](../../references/webhooks/api-contract.md), which defines the structure of every event payload WSO2 Identity Server delivers to your endpoint.


1. Expose an endpoint that accepts HTTP POST requests with JSON payloads.

    WSO2 Identity Server sends POST requests to deliver the actual event notifications. These requests contain the event payload in JSON format.  

1. Deploy this endpoint on a server accessible to WSO2 Identity Server.

## Configure a webhook in WSO2 Identity Server

Follow the steps below to configure a webhook.

1. On the WSO2 Identity Server Console, go to **Webhooks**.

2. Click **Add Webhook** and provide the following:
    - **Name**: A descriptive name for the webhook.
    - **Endpoint**: The URL of your web service, where WSO2 Identity Server will send event notifications.
    - **Secret**: A unique string for HMAC signature  (<code>x-wso2-event-signature</code>)  header to verify event security.
    - **Events to subscribe**: Select event types for notifications (for example choosing Logins notifies of successful and failed login attempts).

3. Click **Create** to create the webhook.

4. Webhooks are inactive by default. Toggle the switch to activate it during or after creation.


6. After creation, you can:
    - Deactivate or reactivate the webhook.
    - Delete the webhook.


## Receive webhook events

WSO2 Identity Server sends an HTTP POST request to your webhook endpoint when a subscribed event is triggered. This request contains a JSON message with event details. Your service can then use this information as needed.

### Event payload structure

Webhook event payloads adhere to the [Security Event Token (SET) specification (RFC 8417)](https://www.rfc-editor.org/rfc/rfc8417.html). This ensures a standardized and secure format for event information. Each payload includes:

- <code>iss</code> **(Issuer)**: Identifies the WSO2 Identity Server instance that issued the event.  
- <code>iat</code> **(Issued At)**: Timestamp showing when WSO2 Identity Server issues the event.  
- <code>rci</code> **(Request Correlation ID)**: A unique identifier that correlates the event with the original request that triggered it.
- <code>jti</code> **(JWT ID)**: A unique identifier for the event.
- <code>events</code>: This object holds the actual event data. Its internal structure changes depending on the specific event types you've subscribed to. For instance, subscribing to **Logins** will deliver both successful and failed login events, with distinct data structures for each.

**Example event payload for login success event**:



```http
POST /your-webhook-endpoint
Content-Type: application/json
x-wso2-event-signature: sha256=abcdef12345... (HMAC signature)

{
  "iss": "https://localhost:9443/t/myorg.com",
  "jti": "051f0c37-b689-44d4-b7d2-29b980ece273",
  "iat": 1751705149662,
  "rci": "05268edb-9a87-4656-87c0-0fb674dd03b1",
  "events": {
    "https://schemas.identity.wso2.org/events/login/event-type/loginSuccess": {
      "user": {
        "id": "d4002616-f00c-49d5-b9b7-63b063819049",
        "claims": [
          {
            "uri": "http://wso2.org/claims/username",
            "value": "peter@aol.com"
          }
        ],
        "organization": {
          "id": "6f8d17ae-1ad5-441b-b9e0-c7731e739e94",
          "name": "myorg",
          "orgHandle": "myorg.com",
          "depth": 0
        },
        "ref": "https://localhost:9443/t/myorg.com/scim2/Users/d4002616-f00c-49d5-b9b7-63b063819049"
      },
      "tenant": {
        "id": "12402",
        "name": "myorg.com"
      },
      "organization": {
        "id": "6f8d17ae-1ad5-441b-b9e0-c7731e739e94",
        "name": "myorg",
        "orgHandle": "myorg.com",
        "depth": 0
      },
      "userStore": {
        "id": "UFJJTUFSWQ==",
        "name": "PRIMARY"
      },
      "application": {
        "id": "40d982e5-23be-4ee1-8540-9cb696d8c321",
        "name": "MyApp"
      },
      "authenticationMethods": [
        "BasicAuthenticator"
      ]
    }
  }
}
```



### Event signature using hash-based message authentication code

To ensure the authenticity and integrity of events, WSO2 Identity Server includes an  <code>x-wso2-event-signature</code>  header with each webhook payload. This header contains an hash-based message authentication code (HMAC) signature computed using the **Secret** you provided when configuring the webhook.

**Verifying the signature:**

Verify the signature to confirm that WSO2 Identity Server sent the event and that no one tampered with the payload.

1. **Retrieve the secret:** Use the same secret string you configured in WSO2 Identity Server for the webhook.  
2. **Compute HMAC:** Generate an HMAC-SHA256 hash of the raw request body using your secret as the key.  
3. **Compare Signatures:** Compare the computed HMAC with the value in the  <code>x-wso2-event-signature</code>  header. If they match, the event is authentic.

## Test your webhook

After you configure and activate your webhook, test it by triggering the specific flow for the event type you subscribed to. This step confirms that your webhook endpoint correctly receives notifications in real-world scenarios.

Here's how to test different event types:

- **Login events**: Initiate a login request with a user from your organization (for example through a configured application).  
- **Registration events**: Attempt to onboard a new user into your organization.
- **Token events**: Issue or revoke an access token for a user or an application.
- **Session events**: Create, extend, or terminate a user session within the system.
- **Credential events**: Update the password of an existing user.  
- **User account management events**: Perform actions such as updating a user's profile or changing their account status (for example enabling or disabling a user).


Observe the requests received by your webhook endpoint to confirm that it successfully receives and processes the event notifications as expected.

## Troubleshoot issues

If your webhook isn't functioning as expected, consider the following common issues and their solutions:



1. **Event signature (HMAC) mismatch**

      - **Problem**: Your endpoint receives events, but the <code>x-wso2-event-signature</code> verification fails.  
      - **Cause**: You may use an incorrect secret key for HMAC computation, or you may calculate the HMAC incorrectly in your endpoint.  
      - **Solution**:  
          - Make sure that the **Secret** configured in WSO2 Identity Server for your webhook exactly matches the secret key used in your endpoint's signature verification logic.
          - Ensure you are computing the HMAC on the raw, unmodified request body received by your endpoint, not a parsed or formatted version. Encoding issues (for example UTF-8) can also cause     mismatches.
          - Confirm you are using HMAC-SHA256, as specified by WSO2 Identity Server.



## Security best practices

To maintain the security and integrity of your webhook integration, follow these best practices:

- **Secure endpoint address**:

    Always use HTTPS for your webhook endpoint address. HTTPS encrypts event data in transit and protects it from eavesdropping. WSO2 Identity Server lets you configure an HTTP endpoint for local testing only. Use HTTPS for all production environments.

- **Protect your secret**:

    The webhook secret verifies event authenticity. Never expose it publicly (for example, in client-side code or public repositories). Store it securely in environment variables or a dedicated secrets management service.

- **Verify signatures**:

    Always validate the  <code>x-wso2-event-signature</code>  header for every incoming webhook event. This step protects you from spoofed or tampered events. Discard any events with invalid signatures.

- **Idempotency**:

    Design your webhook endpoint to be idempotent. Processing the same event multiple times (due to retries) should have the same effect as processing it once. This approach prevents unintended side effects.

## Implementing webhooks for forward compatibility

When developing your webhook endpoint, it's important to design it to be robust and adaptable to future changes in WSO2 Identity Server's event structure. WSO2 Identity Server may introduce new event types, new event URIs, or additional properties to existing events.

Follow these guidelines to ensure your webhook implementation remains resilient and compatible with future enhancements:

1. Validate event URI of the exact event you want to consume  
   Always validate the specific event URI within the <code>events</code> object of the payload.
   For instance, if the event of interest is a login successful event, always explicitly check for <code>https://schemas.identity.wso2.org/events/login/event-type/loginSuccess</code> to process a successful login.
   This practice allows your endpoint to gracefully ignore new, unrecognized event URIs if WSO2 Identity Server adds them to the event type in the future.

2. Anticipate new event indicators  
   WSO2 Identity Server may trigger new events for the same event type, but associate them with different flows or resources.

    - **Flow indicators** (<code>initiatorType</code>, <code>action</code>):

     Pay attention to properties like <code>initiatorType</code> and <code>action</code> in the payload. These properties act as flow indicators. If your processing logic depends on the flow rather than just the high-level event type, ensure it handles new combinations or values for these properties. This approach lets your logic adapt when WSO2 Identity Server triggers events for new flows.

    - **Resource indicators** (<code>credentialType</code>):

     Events might also apply to different resources under the same event type. For example, *credential updated events* currently happen for password updates, indicated by the <code>credentialType</code> property in the payload. In the future, the same event could happen for passkeys, TOTP, or other credential types, introducing new values for <code>credentialType</code>. Design your logic to safely ignore or specifically handle new values for such properties if you only want particular resource updates (for example, only password updates).

3. Ensure graceful unknown property handling  
   Avoid strict schema validation that would cause your webhook to fail if WSO2 Identity Server adds new, optional properties to an existing event payload. Your parser should be able to ignore unrecognized properties, ensuring forward compatibility.

By following these practices, your webhook will be more adaptable to future enhancements in WSO2 Identity Server's event delivery, requiring fewer updates on your side to maintain functionality.
