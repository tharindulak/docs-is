---
title: Add MFA using app-native APIs
mkdocs_template: complete-guide
deployment_options:
  - WSO2 Cloud
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/asgardeo/docs/complete-guides/app-native/add-mfa.md
---

Multi-factor authentication (MFA) is a security mechanism that requires users to provide two or more forms of verification before granting access to an application. This adds an extra layer of security to your application and helps protect sensitive data from unauthorized access.

In this guide, we will look into enabling Email OTP as an MFA factor in your Next.js application. Email OTP is a simple and effective MFA method that sends a one-time passcode to the user's email address, which they must enter to complete the login process.



<Applies to="WSO2 Cloud">

You can configure SMTP settings in the WSO2 Identity Platform Console by navigating to the **Notification Channels** tab > **Email Provider** section. In WSO2 Identity Platform you can simply use default WSO2 Identity Platform SMTP settings available out of the box without configuring an  **Email Provider**.

</Applies>



<Applies to="Self-hosted">

You can configure SMTP settings in the WSO2 Identity Server Console by navigating adding the SMTP configurations in the deployment.toml file.

</Applies>



First, let's set up Email OTP as an MFA factor by following the steps given below.

- Navigate to the WSO2 Identity Platform Console and select your application under the **Applications** tab.
- Click on the **Login Flow** tab.
- Click on either the **+** button in the Visual Editor and select **Email OTP** from the pop-up prompt or click on **Username & Password -> Email OTP** button under the **Predefined Flows > Basic Login Flows > Add Multi-factor Login** section.

  ![Visual Editor](../../../assets/img/complete-guides/app-native/image12.png)
- Click on the **Update** button to save the changes.

You can now test the Email OTP MFA factor in your Next.js application. When a user logs in with their email and password, they will be redirected to the Email OTP page to enter the OTP code sent to their email address. Upon successful verification, the user will be redirected to the home page.

![Email OTP Page](../../../assets/img/complete-guides/app-native/image13.png)
