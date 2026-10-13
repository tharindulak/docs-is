---
title: Add Passkey login
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.2.0/docs/guides/authentication/passwordless-login/add-passwordless-login-with-passkey.md
---

# Add Passkey login

Based on FIDO concepts, **Passkeys** are a replacement for traditional passwords that allows users to log in to applications without a password using the following methods.
    <ul>
    <li><b>Roaming authenticators</b> - platform-independant FIDO2-supported hardware security keys such as YubiKey.</li>
    <li><b>Platform authenticators</b> - built-in biometrics bound to a single device such as fingerprint scanners or facial recognition features.</li>
    </ul>

Passkeys are phishing resistant and they provide an enhanced user experience as users are not required to manage and remember multiple passwords.

:::note[What is FIDO2?]

The FIDO Alliance, whose mission is to reduce the world's reliance on passwords, introduced its latest specifications, collectively called FIDO2. FIDO2 specifications are the World Wide Web Consortium's (W3C) Web Authentication specification (WebAuthn) and FIDO alliance's corresponding Client to Authenticator Protocol (CTAP). Learn more about [FIDO2](https://fidoalliance.org/fido2/).

:::

There are two types of passkeys based on how they are synchronized.

- **Single-Device Passkeys**

    These passkeys are bound to a single device and are not meant to be shared across multiple devices. Single-device passkeys are useful if you want to reduce the impact of an attack if the credentials are compromised.

- **Multi-Device Passkeys**

    These passkeys enable synchronization across multiple devices allowing users to log into an application from any device, even when their credentials are stored on another.

    Major vendors have already introduced their passkey implementations.

    - Apple users will find their passkeys synced across all devices that are signed into the same Apple ID and iCloud Keychain. Refer to the [Apple documentation](https://developer.apple.com/passkeys/) for more information.

    - Android users will have their passkeys synced across all devices linked to their Google account.  Refer to the [Google documentation](https://developers.google.com/identity/passkeys) for more information.

    If the devices do not sync through the cloud, a user can generate a QR code in the other device and scan it using the device that stores the passkeys to successfully log into the application.

    Refer to the [passkeys documentation](https://passkeys.dev/device-support/) to stay up-to-date with the device support for FIDO2 passkeys.

:::info

- WSO2 Identity Server uses the WebAuthn API to enable FIDO-based authentication for browsers that no longer support the u2f extension.
- The following browser versions support the WebAuthn API by default:
    - Chrome 67 and above
    - Firefox 60 and above
    - Edge 17723 and above
- Passkey login with platform authenticators will NOT work on the Firefox browser in macOS Catalina, Big Sur, and Monterey due to browser limitations.
- Passkey login with roaming authenticators will NOT work on the Firefox browser as the browser doesn't support CTAP2 (Client to Authenticator Protocol 2) with PIN.

:::

The following guide explains how you can enable log in with passkeys in your application.

## Prerequisites

- To get started, you need to [register an application with WSO2 Identity Server](../../applications/index.md). You can register your own application or use one of the [sample applications](../../../get-started/try-samples/index.md) provided.

- You need to have a user account in WSO2 Identity Server. If you don't already have one, [create a user account](../../users/manage-users.md#onboard-a-user) in WSO2 Identity Server.

## Enable passkey login

Follow the steps given below to enable login with passkeys for your application.

1. On the WSO2 Identity Server Console, go to **Applications**.

2. Select the application to which you wish to add passkey login.

3. Go to the **Login Flow** tab of the application and add passkey login as follows:

    
    1. Go to **Predefined Flows** > **Basic Flows** > **Add Passwordless login**.

    2. Select **Passkey**.

    3. Click **Confirm** to add passwordless login with passkey to the sign-in flow.

        ![Configuring Passkey login in WSO2 Identity Server using the Visual Editor](../../../../../assets/_versions/7.2.0/img/guides/passwordless/passkey/add-passkey-login.png)
    

4. Click **Update** to save your changes.


## Enable users to register passkeys during login

Enabling users to enroll their passkeys on the fly offers a blend of convenience and security. To do so:

1. On the WSO2 Identity Server Console, go to **Connections**.

2. Select the `Passkey` connection and go to its **Settings** tab.

3. Select the **Allow passkey progressive enrollment** checkbox.

    ![Enable passkey progressive enrollment in WSO2 Identity Server](../../../../../assets/img/guides/passwordless/passkey/enable-passkey-progressive-enrollment.png)

4. Click **Update** to save your changes.

5. [Add the passkey progressive enrollment adaptive script](../conditional-auth/passkey-progressive-enrollment-based-template.md) to the login flow of the application.

:::note

- If progressive enrollment is disabled, users need to pre-register their passkeys from the MyAccount portal. Learn how to do so in [Register passkeys](../../user-self-service/register-passkey.md).

- Passkey progressive enrollment can only be configured at the organizational level and cannot be modified at the application level.

:::

## Configure usernameless passkey login

Usernameless authentication enhances user experience by eliminating the need for users to enter a username during login with passkeys. This is the default behavior in WSO2 Identity Server. Follow the steps given below to configure passkey usernameless authentication for your application.

1. On the WSO2 Identity Server Console, go to **Connections**.

2. Select the **Passkey** connection.

3. Go to the **Settings** tab of the connection.

4. Select the **Allow passkey usernameless authentication** checkbox to enable usernameless authentication.

    :::note

    If this option is disabled, users are prompted to enter the username during login with passkeys.

    :::

    ![Enable passkey usernameless authentication in WSO2 Identity Server](../../../../../assets/img/guides/passwordless/passkey/enable-passkey-usernameless-authentication.png)

5. Click **Update** to save your changes.

:::note

Passkey usernameless authentication can only be configured at the organizational level and cannot be modified at the application level.

:::

## Try it out

The following guides let you try out a scenario where, passkey progressive enrollment is **enabled** and passkey usernameless authentication is **disabled**.

### Enroll a passkey

Follow the steps below to enroll a passkey on the fly during login.

1. Access the application URL.

2. Click **Login** to access the WSO2 Identity Server login page.

3. Select **Sign In With Passkey**.

    ![Sign In with passkey login in WSO2 Identity Server](../../../../../assets/_versions/7.2.0/img/guides/passwordless/passkey/sign-in-with-passkey.png)

4. To enroll a new passkey, enter your username and select **Create a passkey**.

    ![Create a passkey in WSO2 Identity Server](../../../../../assets/_versions/7.2.0/img/guides/passwordless/passkey/create-passkey.png)

5. Enter the corresponding password for the user and click **Sign In**.

    ![Basic authenticator in WSO2 Identity Server](../../../../../assets/_versions/7.2.0/img/guides/passwordless/passkey/basic-authenticator.png)

6. Follow the instructions given by your browser or device to enroll the passkey.

    ![Create a passkey browser prompt in WSO2 Identity Server](../../../../../assets/img/guides/passwordless/passkey/create-passkey-browser-prompt.png)

7. Provide a name to uniquely identify your passkey.

    ![Rename passkey in WSO2 Identity Server](../../../../../assets/_versions/7.2.0/img/guides/passwordless/passkey/rename-passkey.png)

8. Click **Submit** to complete the enrollment. You'll be authenticated in the application.


### Sign in with passkey

Follow the steps below to use an enrolled passkey to sign in to an application.

1. Navigate to the login page of the application.

1. Click  **Login** to access the WSO2 Identity Server login page.

3. Select **Sign In With Passkey**.

4. Enter your username and select **Continue**.

5. Follow the browser/device instructions to log in with a passkey.

    ![Sign In with passkey browser prompt WSO2 Identity Server](../../../../../assets/img/guides/passwordless/passkey/sign-in-with-passkey-browser-prompt.png)

:::note

During passkey progressive enrollment, if a user wishes to use a federated authenticator, they should have their external accounts already provisioned within WSO2 Identity Server. If, for example, a user logs in with Google using an account not provisioned in WSO2 Identity Server, passkey enrolment results in an error and the login flow fails.

:::



## Restrict passkey generation and prompting to subdomains

By default, WSO2 Identity Server generates and prompts passkeys for the top-level domain. For example, if the application is running on `app.example.com`,
the passkey will be generated for `example.com` and prompts the user to use the passkey for all applications running on `example.com` and its subdomains.

If required, you can restrict passkey generation and prompting to subdomains instead.

For example, you can configure the system so that passkeys are generated and used only for `app.example.com`.
In this case, users will be prompted to use their passkeys only when accessing applications hosted on `app.example.com`.
To enable this restriction, add the following configuration to the `<IS_HOME>/repository/conf/deployment.toml` file.

  ```toml
    [fido.webauthn.relying_party]
    use_full_effective_domain = true
  ```


:::note

This configuration is available starting from update level 7.2.0.13.

:::


:::warning

Enabling this configuration restricts passkeys to the exact subdomain where they were registered,
preventing cross-subdomain usage within the same parent domain. For example,
a passkey registered on `app.example.com` cannot be used to authenticate to applications on other subdomains such as `admin.example.com` or `login.example.com`.
If the application's subdomain changes (e.g., from `app.example.com` to `newapp.example.com`) or a different subdomain is introduced,
previously registered passkeys become invalid and users must register new passkeys for the new subdomain.

:::





## Configure FIDO user response timeout

During FIDO2 device registration, WSO2 Identity Server sends a timeout hint to the browser indicating how long it should wait for the user to interact with their FIDO2 authenticator. By default, this is set to **300000 milliseconds (5 minutes)**.

:::note

This timeout is enforced by the browser, not by WSO2 Identity Server, and only applies to **device registration**. It does not affect the authentication flow. Some browsers may override this value based on their own policies.

:::

To change this timeout, add the following configuration to the `<IS_HOME>/repository/conf/deployment.toml` file.

  ```toml
    [fido]
    user_response_timeout = "<timeout_in_milliseconds>"
  ```

For example, to set the timeout to 2 minutes:

  ```toml
    [fido]
    user_response_timeout = "120000"
  ```



## Use passkeys with app-native authentication

:::tip[What is app-native authentication?]


App-native authentication is an API-based mechanism that provides users with a seamless login experience right within the application. This eliminates the need to redirect users to an external web browser for authentication. Follow the guide to learn more about [app-native authentication](../app-native-authentication/index.md).

:::

Passkeys support app-native authentication. This is especially useful for mobile applications to provide a seamless, passwordless login experience. Since users enter their passkeys directly within the application, iOS and Android platforms enforce mandatory validation processes to verify an application's association with the identity provider's domain. These validations ensure the authenticity of the authentication requests and help protect against credential theft by malicious actors.





The validation services of [iOS](https://developer.apple.com/documentation/xcode/supporting-associated-domains) and [Android](https://developer.android.com/identity/sign-in/credential-manager#add-support-dal) require specific application details to be hosted at the following publicly accessible URLs:

- For Android - `<your_domain>/.well-known/assetlinks.json`
- For iOS - `<your_domain>/.well-known/apple-app-site-association`

To facilitate this, WSO2 Identity Server provides you with the option to publish details at the following local endpoints. 

- For Android - `<base_url>/.well-known/trusted-apps/android`

- For iOS - `<base_url>/.well-known/trusted-apps/ios`

Follow the guide below to implement this. Once implemented, ensure that these local endpoints map to the relevant publicly accessible URLs of your domain.

1. On the WSO2 Identity Server Console, go to **Applications** and select your application.

2. In its **Advanced** tab, under **Trusted App Settings**, select **Add as a FIDO trusted app**.

3. Under **Platform Settings**, enter the following platform-specific details.
    
    - For an Android app:

        - Provide the package name of the application which takes the reverse domain format (e.g. com.example.myapp)

        - Provide key hashes, which are SHA256 fingerprints of the app's signing certificate.
    
    - For an iOS app:

        - Provide the app ID of your application which consists of the team ID and the bundle ID separated by a period (.). (e.g. A1B2C3D4E5.com.domainname.applicationname)

4. Click **Update** to save the changes.
