---
title: Configure verification settings for attribute updates
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.1.0/docs/guides/users/attributes/user-attribute-change-verification.md
---

# Configure verification settings for attribute updates

This guide explains how to configure notification and verification settings when a user changes specific attributes like their email address or mobile number. These settings ensure users are properly notified when attributes are updated or are requested to verify critical attribute updates.

Follow the steps below to configure attribute change verification settings:

1. On the WSO2 Identity Server Console, go to **User Attributes & Stores** > **Attributes**.

2. Under **Manage Attributes**, click on  **Attribute Update Settings** .

3. Configure the following properties:

    ![User attributes change verification settings](../../../../../assets/_versions/7.1.0/img/guides/users/change-verification-settings.png)

    
    <table>
        <tr>
            <td>Enable User Email Verification on Update</td>
            <td>When enabled, triggers an email verification process whenever a user updates their email address.</td>
        </tr>
        <tr>
            <td>Email verification on update link expiry time</td>
            <td>Defines the validity period (in minutes) of the email verification link. Default is set to 1440 minutes.</td>
        </tr>
        <tr>
            <td>Enable user email notification on update</td>
            <td>When enabled, triggers a notification email to the existing email address whenever the user attempts to update their email address.</td>
        </tr>
        <tr>
            <td>Enable user mobile number verification on update</td>
            <td>When enabled, triggers an SMS One-Time Password (OTP) verification process when the user updates their mobile number.</td>
        </tr>
        <tr>
            <td>Enable mobile number verification by Privileged Users</td>
            <td>When enabled, allows privileged users (such as administrators) to initiate mobile number verification on behalf of other users.</td>
        </tr>
    </table>
    

4. Click **Update** to save the changes.
