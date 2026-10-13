---
title: Enroll a Push Notification Device
deployment_options:
  - WSO2 Cloud
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/asgardeo/docs/guides/user-self-service/register-push-notification-device.md
---

# Enroll a Push Notification Device

Application users can use the My Account portal to register their device to receive push notifications. This guide explains how to register a push notification device using the My Account portal.

:::note

A user can only maintain one push notification device at a time.

:::


1. In the user's My Account portal, go to **Security** > **Additional Authentication**.

    ![Enroll passkey via MyAccount](../../../assets/img/guides/passwordless/push/register-push-device-via-myaccount.png)

2. Click the **+** icon next to **Push Authenticator** to add a new device.

3. Scan the QR code with your mobile device using your Push Authenticator app to register the device.

    ![Scan QR for push device registration](../../../assets/img/guides/passwordless/push/scan-qr-for-push-device-enroll.png)

4. Once the device is registered through the app is successful, click **Verify** to check if the device is registered successfully in WSO2 Identity Platform.

5. If device registration is successful in WSO2 Identity Platform, the registered device will be displayed in the **Push Authenticator** section.

    ![Push device registered successfully](../../../assets/img/guides/passwordless/push/push-device-registered-view.png)
