---
title: SMS templates
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.1.0/docs/references/sms-templates.md
---

# SMS templates

WSO2 Identity Server organizations use several SMS templates to send SMS notifications to users.

:::note


- You can customize all available SMS templates to match your organization's preferences using the [Notification Template Management API](../apis/notification-templates.md).
- You can also use the Console to change some of the most frequently used SMS templates in WSO2 Identity Server. Learn how to [customize SMS content from the Console](../guides/branding/customize-sms-templates.md#customize-sms-content).

:::


## SMS templates in WSO2 Identity Server

The following is a list of all SMS templates available in WSO2 Identity Server.

<table><thead><tr><th>{"Template ID"}</th><th>{"Description"}</th></tr></thead><tbody><tr><td>{"SMSOTP"}</td><td>{"These SMS messages are sent when a user attempts to sign in to an account using SMS OTP. The OTP can be displayed using the {{confirmation-code}} literal."}</td></tr><tr><td>{"passwordReset"}</td><td>{"These SMS messages are sent when a user attempts to recover the password using SMS OTP. The OTP can be displayed using the {{confirmation-code}} literal."}</td></tr><tr><td>{"accountconfirmation"}</td><td>{"These SMS messages are sent when a user creates an account in WSO2 Identity Server, when administrators have enabled account confirmation via SMS. The OTP can be displayed using the {{confirmation-code}} literal."}</td></tr><tr><td>{"verifyMobileOnUpdate"}</td><td>{"This SMS message is sent when a user changes the mobile number associated with the account, when administrators have enabled mobile number verification. The OTP can be displayed using the {{confirmation-code}} literal."}</td></tr><tr><td>{"accountIdRecovery"}</td><td>{"This SMS message is sent when a user requests a username recovery. The username can be displayed using the {{user-name}} literal."}</td></tr></tbody></table>

## Literals in SMS templates

Literals are placeholders used to display dynamic information in SMS templates. The following are the template literals that are accessible for all SMS templates in WSO2 Identity Server.

### General literals

The following user-related literals are accessible for all SMS templates.

<table><thead><tr><th>{"Literal"}</th><th>{"Description"}</th></tr></thead><tbody><tr><td>{"{{user-name}}"}</td><td>{"Name of the user account."}</td></tr><tr></tr><tr><td>{"{{userstore-domain}}"}</td><td>{"Name of the user store."}</td></tr><tr></tr><tr><td>{"{{organization-name}}"}</td><td>{"Name of the organization. Insert this placeholder where you want to display the organization's name in a human-readable format."}</td></tr><tr><td>{"{{tenant-domain}}"}</td><td>{"Domain name specific to the organization. For root organizations, this is the human-readable domain name. For other organizations, it is the UUID."}</td></tr><tr><td>{"{{current-year}}"}</td><td>{"Current calendar year."}</td></tr></tbody></table>

:::note

Root organizations created before October 2022 will utilize `{{ tenant-domain }}` as the placeholder to represent the organization name. As this placeholder may not provide the organization name in a human-readable format, consider updating it to `{{ organization-name }}` as needed for clarity and ease of understanding.

:::
