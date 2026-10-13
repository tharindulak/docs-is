---
title: Configure backup codes
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.1.0/docs/guides/user-self-service/manage-backup-codes.md
---

# Configure backup codes

Backup codes help users log in to applications when they have lost access to the configured multi factor authentication methods.

## Enable backup codes

To enable backup codes:

1. On the My Account portal, go to **Security** > **Additional Authentication** > **Recovery Options**.

2. Click `+` to add backup codes.
    You will see a popup window with ten backup codes. Each backup code can be used only once.

    ![QR backup codes](../../../../assets/img/guides/mfa/backup-codes/backup-codes-via-myaccount.png)

3. Click **Download Codes** or **Copy Codes** and save the backup codes in a secure location, as the codes will only be shown once.

4. Click **Close** once you have securely stored the backup codes.

:::note

The backup codes will not be valid for your currently active sessions. Therefore it is recommended to terminate your active sessions.

:::

## Regenerate backup codes

In case you have lost the backup codes or have used them all, follow the steps below to generate a new set of backup codes.

1. On the My Account portal, go to **Security** > **Additional Authentication** > **Recovery Options**.

2. Click on the refresh icon to regenerate the backup codes.

    ![Regenerate backup codes](../../../../assets/img/guides/mfa/backup-codes/regenerate-backup-codes.png)

3. On the confirmation window, click **Regenerate** to confirm your action.
    You will see a popup window with ten backup codes. Each backup code can be used only once.

    ![QR backup codes](../../../../assets/img/guides/mfa/backup-codes/backup-codes-via-myaccount.png)

4. Click **Download Codes** or **Copy Codes** and save the copied or downloaded backup codes securely, as the codes will only be shown once.

5. Click **Close** once you have securely stored the backup codes.

## Remove backup codes
To remove the backup codes:

1. On the My Account portal, go to **Security** > **Additional Authentication** > **Recovery Options**.

2. Click on the trash icon to remove the existing backup codes.

    ![Remove backup codes](../../../../assets/img/guides/mfa/backup-codes/remove-backup-codes.png)

3. On the confirmation window, click **Remove** to confirm your action.
