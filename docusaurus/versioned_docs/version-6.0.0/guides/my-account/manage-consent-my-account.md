---
title: Manage Consent from My Account
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.0.0/docs/guides/my-account/manage-consent-my-account.md
---

# Manage Consent from My Account

WSO2 IS provides a comprehensive consent management solution that can be used to manage consents related to Customer Identity and Access Management (CIAM), and also to manage consents that belong to third party applications. For more information, see [Consent Management](../../references/concepts/consent-management.md).
**My Account** allows users to revoke or edit the consent given to applications registered in WSO2 IS. In order to edit or revoke application consents, refer to the instructions given below.

## Revoke consent

1. Access **My Account** (`https://<IS_HOST>:<PORT>/myaccount`).
2. Click the **Security** tab on the side panel.
3. Under the **Manage consent** section, click on the **Revoke** button aligning with the application for which consent needs to be revoked. 

## Edit consent

1. Access **My Account** (`https://<IS_HOST>:<PORT>/myaccount`).
2. Click the **Security** tab on the side panel.
3. Under the **Manage consent** section, click on the edit icon aligning with the application for which the consent needs to be edited. 
4. Click and disable the toggle button aligning with any claim to revoke your consent.
5. Click **update**.
