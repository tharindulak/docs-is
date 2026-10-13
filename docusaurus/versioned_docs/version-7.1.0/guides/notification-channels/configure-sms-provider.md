---
title: Configure SMS provider
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.1.0/docs/guides/notification-channels/configure-sms-provider.md
---

# Configure SMS provider

Configurations related to SMS providers are located under the **Notification Channels** section.

## Supported Providers

WSO2 Identity Server supports Twilio, Vonage, or custom SMS providers by default. To learn how to configure each provider, please see the relevant section.

<details>
<summary>Configuring Twilio</summary>

To configure Twilio as your SMS provider, follow the steps below:

- Go to [Twilio](https://www.twilio.com/try-twilio) and create an account.
- After signing up for your account, navigate to the Phone Numbers page in your console. You’ll see the phone number that has been selected for you. Note the phone number’s capabilities, such as "Voice", "SMS", and "MMS".
- After signing up, navigate to the Phone Numbers page in your console and note the phone number’s capabilities.
- Get your first Twilio phone number and use that as the “Sender” in the settings. For more information, see this tutorial in the Twilio documentation.
- Copy the Account SID and Auth Token from the Twilio console dashboard.
- Go to **SMS Provider** section in the WSO2 Identity Server Console and click the **Twilio** tab and fill the required fields.

<table><tbody><tr><th>{"Name"}</th><th>{"Description"}</th><th>{"Example"}</th></tr><tr><td>{"Twilio Account SID"}</td><td>{"Account SID received in the previous step."}</td><td><code>{"YourAccountSID"}</code></td></tr><tr><td>{"Twilio Auth Token"}</td><td>{"Auth token received in the previous step."}</td><td><code>{"YourAuthToken"}</code></td></tr><tr><td>{"Sender"}</td><td>{"Phone number that you received when creating the Twilio account."}</td><td><code>{"+1234567890"}</code></td></tr></tbody></table>

</details>

<details>
<summary>Configuring Vonage</summary>

To configure Vonage as your SMS provider, follow the steps below:

- Login to [Vonage](https://dashboard.nexmo.com/sign-in) and create an account.
- Fill in the required fields and create the account.
- Login to the Vonage dashboard and copy the API Key and API Secret.
- Go to **SMS Provider** section in the WSO2 Identity Server Console and click the **Vonage** tab and fill the required fields.

<table><tbody><tr><th>{"Name"}</th><th>{"Description"}</th><th>{"Example"}</th></tr><tr><td>{"Vonage API Key"}</td><td>{"Use the API Key from the previous step."}</td><td><code>{"YourAPIKey"}</code></td></tr><tr><td>{"Vonage API Secret"}</td><td>{"Use the API Secret from the previous step."}</td><td><code>{"YourAPISecret"}</code></td></tr><tr><td>{"Sender"}</td><td>{"The number that the receiver will see when you send an SMS."}</td><td><code>{"+1234567890"}</code></td></tr></tbody></table>

</details>

<details>
<summary>Configuring a Custom Provider</summary>

If you are not using either Twilio or Vonage as the SMS provider, you can configure a custom SMS provider. Custom SMS provider configuration will pass the SMS data to the given URL as an HTTP request.

To configure a custom SMS provider, in the  **SMS Provider** section click the **Custom** tab and fill the required fields.

<table><tbody><tr><th>{"Name"}</th><th>{"Description"}</th><th>{"Example"}</th></tr><tr><td>{"SMS Provider URL"}</td><td>{"URL of the SMS gateway where the payload should be published."}</td><td><code>{"https://api.example.com/api/v1"}</code></td></tr><tr><td>{"Content Type"}</td><td>{"Content type of the payload. Possible values are "}<code>{"JSON"}</code>{" or "}<code>{"FORM"}</code>{" (Optional)."}</td><td><code>{"JSON"}</code></td></tr><tr><td>{"HTTP Method"}</td><td>{"HTTP method that should be used when publishing the payload to the provider URL. Possible values: "}<code>{"PUT"}</code>{", "}<code>{"POST"}</code>{" (Optional)."}</td><td><code>{"POST"}</code></td></tr><tr><td>{"Payload Template"}</td><td>{"How the payload template should be. "}<br />{"Placeholders: "}<br /><code>{"{{body}}"}</code>{" - Generated body of the SMS. (Example - This can be the OTP). "}<br /><code>{"{{mobile}}"}</code>{" - Number that this sms should be sent to."}</td><td>{"Example JSON payload template: "}<br /><code>{"{“content”: {{body}},“to”: {{mobile}}}"}</code><br /><br />{"("}<code>{"{{mobile}}"}</code>{" and "}<code>{"{{body}}"}</code>{" will be replaced with the corresponding values at the runtime.)"}</td></tr><tr><td>{"Headers"}</td><td>{"Custom static headers need to be passed. If multiple headers need to be passed, they should be comma separated. (Optional)"}</td><td><code>{"x-csrf: true, x-abc: some-value"}</code></td></tr></tbody></table>

</details>
