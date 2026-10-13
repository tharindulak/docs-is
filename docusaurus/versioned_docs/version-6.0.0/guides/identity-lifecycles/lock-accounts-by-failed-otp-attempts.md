---
title: Lock accounts by failed OTP attempts
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.0.0/docs/guides/identity-lifecycles/lock-accounts-by-failed-otp-attempts.md
---

# Lock accounts by failed OTP attempts

WSO2 Identity Server can be configured to lock a user account when the number of consecutive failed OTP attempts is exceeded.

If you want to configure different settings for another tenant, log out
and follow the same steps to configure these properties for the other
tenants.

:::note

-   A user account locked by failed login attempts can be unlocked 
by setting the <strong>Account Unlock Time</strong> period.
-   If the lock time is set to 0, the account has to be unlocked by an admin
user. For more information about this, see [Lock and Unlock User Accounts](lock-account.md).
-   If a user is assigned the **Internal/system** role, the user can

:::
		bypass account locking even if the user exceeds the specified number
		of **Maximum failed login attempts**.

## Configure the WSO2 IS server

Add the following configurations into `<IS_HOME>/repository/conf/deployment.toml` file to enable account locking for each type of OTP attempts and restart the server.

- For Email OTP:

    ```
    [authentication.authenticator.email_otp.parameters]
    EnableAccountLockingForFailedAttempts = true
    ```

- For SMS OTP:

    ```
    [authentication.authenticator.sms_otp.parameters]
    EnableAccountLockingForFailedAttempts = true
    ```

    :::note

    Since `BackupCode = true` in the default configuration, configure the backup code claim. 
    Alternatively, you can disable the backup codes for SMS OTP by setting the property to **false**.

    ```
    [authentication.authenticator.sms_otp.parameters]
    BackupCode = false
    ```

    :::
        
- For TOTP:

    ```
    [authentication.authenticator.totp.parameters]
    EnableAccountLockingForFailedAttempts = true
    ```

## Enable claims

1. Navigate to **Main** > **Identity** > **Claims** > **Add** > **Add Local Claim**.
2. Click **http://wso2.org/claims**.
3. Once the user account gets locked, the **Account Locked** attribute will be updated to **true**.
To check this via the user profile:
    1. Click **Edit** under the **Account Locked** claim.
    2. Select **Supported by Default** and click **Update**.
    3. Navigate to the relevant user's user profile and you will see that the attribute has been updated.
  
4. **Failed Email OTP Attempts**, **Failed SMS Attempts**, and **Failed TOTP Attempts** attribute values will be incremented for the wrong attempt of Email OTP, SMS OTP, and TOTP attempt respectively. To check this via the user profile.
    - For Email OTP:
        1. Click **Edit** under the **Failed Email OTP Attempts** claim.
        2. Select **Supported by Default** and click **Update**.
        3. Navigate to the relevant user's user profile and you will see that the attribute has been updated.

    - For SMS OTP:
        1. Click **Edit** under the **Failed SMS Attempts** claim.
        2. Select **Supported by Default** and click **Update**.
        3. Navigate to the relevant user's user profile and you will see that the attribute has been updated.

    - For TOTP:
        1. Click **Edit** under the **Failed TOTP Attempts** claim.
        2. Select **Supported by Default** and click **Update**.
        3. Navigate to the relevant user's user profile and you will see that the attribute has been updated.

## Enable account locking


1. 	Ensure that the identity listener with the
   `              priority=50             ` is set to **false** and
   the identity listener with the `              priority=95             ` is set to
   **true**  by adding the following configuration to the
   `              <IS_HOME>/repository/conf/deployment.toml             ` file.  

	:::note



	:::
		If you haven't changed these configurations previously, you can skip this step since these are the default values. 

		```xml
		[event.default_listener.identity_mgt]
		priority= "50"
		enable = false
		[event.default_listener.governance_identity_mgt]
		priority= "95"
		enable = true
		```

2.  <a name="lockingaspecificuseraccount"></a>Start the Identity Server and log into the management console (`https://<IS_HOST>:<PORT>/carbon`) using
   your tenant credentials.
      
3.  Click **Main** > **Identity** > **Identity Providers** > **Resident**.
4.  Expand the **Login Attempts Security** tab.
5.  Expand the **Account Lock** tab and select the **Lock user accounts** checkbox. Click **Update** to save changes.  
	
	
         
         
6.  To enable account locking for other tenants, log out and repeat the
   steps given above from [step 2](#lockingaspecificuseraccount)
   onwards.

The following table describes the configuration properties and
descriptions you need to configure:

<table><thead><tr className={"header"}><th><p>{"Configuration"}</p></th><th><p>{"Description"}</p></th></tr></thead><tbody><tr className={"odd"}><td><p>{"Maximum Failed Login Attempts"}</p></td><td><div className={"content-wrapper"}><p>{"This indicates the number of consecutive attempts that a user can try to log in without the account getting locked. If the value you specify is 2, the account gets locked if the login attempt fails twice."}</p><div className={"admonition tip"}><p className={"admonition-title"}>{"Tip"}</p>{" Add the following configuration to the "}<code>{" <IS_HOME>/repository/conf/deployment.toml "}</code>{" file to configure the "}<strong>{"Maximum Failed Login Attempts"}</strong>{" property by default for all the tenants at tenant creation. "}<div className={"code panel pdl"}><div className={"codeContent panelContent pdl"}><pre className={"html/xml"} data-syntaxhighlighter-params={"brush: html/xml; gutter: false; theme: Confluence"} data-theme={"Confluence"}><code>{"[identity_mgt.account_locking]"}<br />{"allowed_failed_attempts=5"}</code></pre></div></div></div></div></td></tr><tr className={"even"}><td><p>{"Lock Timeout Increment Factor"}</p></td><td><div className={"content-wrapper"}><p>{"This indicates how much the account unlock timeout is incremented by after each failed login attempt. For example, according to the values configured in the above screen, when a user exceeds the specified limit of 4 "}<strong>{"Maximum Failed Login Attempts"}</strong>{", the account is locked for 10 minutes. This account unlock timeout is calculated as follows."}</p><p>{"Account unlock timeout = Configured "}<strong>{"Account Unlock Time"}</strong>{" * ("}<strong>{"Lock Timeout Increment Factor"}</strong>{" ^ failed login attempt cycles)"}</p><p>{"i.e.,10 minutes = 5 * ( 2 ^ 1 )"}</p><div className={"admonition tip"}><p className={"admonition-title"}>{"Tip"}</p>{" Add the following configuration to the "}<code>{" <IS_HOME>/repository/conf/deployment.toml "}</code>{" file to configure the "}<strong>{"Lock Timeout Increment Factor"}</strong>{" property by default for all the tenants at tenant creation. "}<div className={"code panel pdl"}><div className={"codeContent panelContent pdl"}><pre className={"html/xml"} data-syntaxhighlighter-params={"brush: html/xml; gutter: false; theme: Confluence"} data-theme={"Confluence"}><code>{"[identity_mgt.account_locking]"}<br />{"auto_unlock_time_increment_ratio=2"}</code></pre></div></div></div></div><p>{"If the user attempts to log in with invalid credentials again after the wait time has elapsed and the account is unlocked, the number of login attempt cycles is now 2 and the wait time is 20 minutes."}</p></td></tr><tr className={"odd"}><td><p>{"Account Unlock Time"}</p></td><td><div className={"content-wrapper"}><p>{"The time specified here is in minutes. According to the values in the screenshot above, the account is locked for 5 minutes after the user's second failed attempt and authentication can be attempted once this time has passed."}</p><div className={"admonition tip"}><p className={"admonition-title"}>{"Tip"}</p>{" Add the following configuration to the "}<code>{" <IS_HOME>/repository/conf/deployment.toml "}</code>{" file to configure the "}<strong>{"Account Unlock Time"}</strong>{" property by default for all the tenants at tenant creation. "}<div className={"code panel pdl"}><div className={"codeContent panelContent pdl"}><pre className={"html/xml"} data-syntaxhighlighter-params={"brush: html/xml; gutter: false; theme: Confluence"} data-theme={"Confluence"}><code>{"[identity_mgt.account_locking]"}<br />{"auto_unlock_after=5"}</code></pre></div></div></div></div></td></tr><tr className={"even"}><td><p>{"Account Lock Enabled"}</p></td><td><div className={"content-wrapper"}><p>{"This enables locking the account when authentication fails."}</p><div className={"admonition tip"}><p className={"admonition-title"}>{"Tip"}</p>{" Add the following configuration to the "}<code>{" <IS_HOME>/repository/conf/deployment.toml "}</code>{" file to "}<strong>{"Enable"}</strong>{" Account lock on failed login by default for all the tenants at tenant creation. "}<div className={"code panel pdl"}><div className={"codeContent panelContent pdl"}><pre className={"html/xml"} data-syntaxhighlighter-params={"brush: html/xml; gutter: false; theme: Confluence"} data-theme={"Confluence"}><code>{"[identity_mgt.account_locking]"}<br />{"enable_account_locking=true"}</code></pre></div></div></div></div></td></tr></tbody></table>

## Configure the email sender

[Enable the email sending configurations](../../deploy/configure-email-sending.md) of the WSO2 Identity Server.

:::info[Related topics]

-   [Guides: Customize Automated Emails](../tenants/customize-automated-mails.md)
-   [Guides: Lock and Unlock User Accounts](lock-account.md)


:::
