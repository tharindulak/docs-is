---
title: Resending Account Recovery Confirmation Emails
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.1.0/docs/guides/identity-lifecycles/resend-account-recovery-mail.md
mdx:
  format: md
---

# Resending Account Recovery Confirmation Emails

This section explains how to resend the account recovery confirmation mail in the following account recovery scenarios:

- User creation through ask password option
- Notification-based password recovery
- Admin-initiated password reset through an email link
- Admin-initiated password reset via OTP
- Self-registration

Follow the steps below to configure WSO2 Identity Server to resend account recovery confirmation emails:

:::tip

Sign in to the WSO2 Identity Server Management Console.

:::

1. On the Main menu, click **Manage > Email Template > Add**.



2. Click **Add Email Template**.



3. To create an email template for account registration through password request:

    1. Enter resendAskPassword  as the Template Type Display Name and click Add.

        

        A success message about the email template creation and the Add a New Email Template screen appears.  

        

    2. Enter the following values:

        1. **Email Template Type**: resendAskPassword
        2. **Email Template Locale**: English (United States)
        3. **Email Content Type**: text/html
        4. **Email Template Subject**: WSO2 - Resend Create Password for New Account
        5. **Email Body**:  

            <details>
            <summary>Click to View</summary>

            ```html
            <table align="center" cellPadding="0" cellspacing="0" border="0" width="100%"bgcolor="#f0f0f0">
            <tr>
            <td>
                <table cellPadding="0" cellspacing="0" border="0" width="100%" bgcolor="#ffffff">
                <tr>
                    <td colSpan="2" align="center">
                        <a href="http://wso2.com/" target="_blank"><img src="http://cdn.wso2.com/wso2/newsletter/images/nl-2017/wso2-logo-transparent.png" border="0" /></a>
                    </td>
                </tr>
                <tr>
                    <td colSpan="2" align="center">
                        <h1>
                            Resend Password Reset
                        </h1>
                    </td>
                </tr>
                <tr>
                    <td valign="top">
                        <p>
                            Hi \{\{user.claim.givenname\}\},
                        </p>
                        <p>
                            We received a request to reset the password for the <b>\{\{user-name\}\}</b> account that is associated with this email address.<br />
                            If you made this request, please click the button below to securely reset your password.
                        </p>
                    </td>
                </tr>
                <tr>
                    <td>
                        <table align="left" cellPadding="0" cellspacing="0" border="0">
                            <tr>
                                <td>
                                    <a href="\{\{carbon.product-url\}\}/accountrecoveryendpoint/confirmrecovery.do?confirmation=\{\{confirmation-code\}\}&amp;userstoredomain=\{\{userstore-domain\}\}&amp;username=\{\{url:user-name\}\}&amp;tenantdomain=\{\{tenant-domain\}\}&amp;callback=\{\{callback\}\}"
                                    target="_blank">Reset Password</a>
                                </td>
                            </tr>
                        </table>
                    </td>
                </tr>
                <tr>
                    <td valign="top">
                        <p>
                            If clicking the button doesn't seem to work, you can copy and paste the following link into your browser. <br />
                            <a target="_blank"
                            href="\{\{carbon.product-url\}\}/accountrecoveryendpoint/confirmrecovery.do?confirmation=\{\{confirmation-code\}\}&amp;userstoredomain=\{\{userstore-domain\}\}&amp;username=\{\{url:user-name\}\}&amp;tenantdomain=\{\{tenant-domain\}\}&amp;callback=\{\{callback\}\}">
                                \{\{carbon.product-url\}\}/accountrecoveryendpoint/confirmrecovery.do?confirmation=\{\{confirmation-code\}\}&amp;userstoredomain=\{\{userstore-domain\}\}&amp;username=\{\{url:user-name\}\}&amp;tenantdomain=\{\{tenant-domain\}\}&amp;callback=\{\{callback\}\}</a>
                        </p>
                        <br />
                        <p>
                            If you did not request to have your \{\{user-name\}\} password reset, disregard this email and no changes to your account will be made.
                        </p>
                    </td>
                </tr>
                <tr>
                    <td valign="top">
                        <p>
                            Thanks,<br />WSO2 Identity Server Team
                        </p>
                    </td>
                </tr>
                <tr>
                    <td colSpan="2" align="center" bgcolor="#f0f0f0">
                        <p>
                            &copy; 2018
                            <a href="http://wso2.com/" target="_blank">WSO2</a>
                            <br />
                            787 Castro Street, Mountain View, CA 94041.
                        </p>
                    </td>
                </tr>
                </table>
            </td>
            </tr>
            </table>```

            </details>
        6. **Email Footer** :  --

4. To create an email template for **notification-based password recovery**, enter the following values:

    1. **Email Template Type**: resendPasswordReset
    2. **Email Template Locale**: English (United States)
    3. **Email Content Type**: text/html
    4. **Email Template Subject**: WSO2 - Resend Password Reset
    5. **Email Body**:  

        <details>
        <summary>Click to View</summary>

        ```html
        <table align="center" cellPadding="0" cellspacing="0" border="0" width="100%"bgcolor="#f0f0f0">
        <tr>
        <td>
            <table cellPadding="0" cellspacing="0" border="0" width="100%" bgcolor="#ffffff">
            <tr>
                <td colSpan="2" align="center">
                    <a href="http://wso2.com/" target="_blank"><img src="http://cdn.wso2.com/wso2/newsletter/images/nl-2017/wso2-logo-transparent.png" border="0" /></a>
                </td>
            </tr>
            <tr>
                <td colSpan="2" align="center">
                    <h1>
                        Resend Password Reset
                    </h1>
                </td>
            </tr>
            <tr>
                <td valign="top">
                    <p>
                        Hi \{\{user.claim.givenname\}\},
                    </p>
                    <p>
                        We received a request to reset the password for the <b>\{\{user-name\}\}</b> account that is associated with this email address.<br />
                        If you made this request, please click the button below to securely reset your password.
                    </p>
                </td>
            </tr>
            <tr>
                <td>
                    <table align="left" cellPadding="0" cellspacing="0" border="0">
                        <tr>
                            <td>
                                <a href="\{\{carbon.product-url\}\}/accountrecoveryendpoint/confirmrecovery.do?confirmation=\{\{confirmation-code\}\}&amp;userstoredomain=\{\{userstore-domain\}\}&amp;username=\{\{url:user-name\}\}&amp;tenantdomain=\{\{tenant-domain\}\}&amp;callback=\{\{callback\}\}"
                                target="_blank">Reset Password</a>
                            </td>
                        </tr>
                    </table>
                </td>
            </tr>
            <tr>
                <td valign="top">
                    <p>
                        If clicking the button doesn't seem to work, you can copy and paste the following link into your browser. <br />
                        <a target="_blank"
                        href="\{\{carbon.product-url\}\}/accountrecoveryendpoint/confirmrecovery.do?confirmation=\{\{confirmation-code\}\}&amp;userstoredomain=\{\{userstore-domain\}\}&amp;username=\{\{url:user-name\}\}&amp;tenantdomain=\{\{tenant-domain\}\}&amp;callback=\{\{callback\}\}">
                            \{\{carbon.product-url\}\}/accountrecoveryendpoint/confirmrecovery.do?confirmation=\{\{confirmation-code\}\}&amp;userstoredomain=\{\{userstore-domain\}\}&amp;username=\{\{url:user-name\}\}&amp;tenantdomain=\{\{tenant-domain\}\}&amp;callback=\{\{callback\}\}</a>
                    </p>
                    <br />
                    <p>
                        If you did not request to have your \{\{user-name\}\} password reset, disregard this email and no changes to your account will be made.
                    </p>
                </td>
            </tr>
            <tr>
                <td valign="top">
                    <p>
                        Thanks,<br />WSO2 Identity Server Team
                    </p>
                </td>
            </tr>
            <tr>
                <td colSpan="2" align="center" bgcolor="#f0f0f0">
                    <p>
                        &copy; 2018
                        <a href="http://wso2.com/" target="_blank">WSO2</a>
                        <br />
                        787 Castro Street, Mountain View, CA 94041.
                    </p>
                </td>
            </tr>
            </table>
        </td>
        </tr>
        </table>```

        </details>

    6. **Email Footer** :  --

5. To create an email template for an **admin-initiated password reset through an email link**, enter the following values:

    1. **Email Template Type**: resendAdminForcedPasswordReset
    2. **Email Template Locale**: English (United States)
    3. **Email Content Type**: text/html
    4. **Email Template Subject**: WSO2 - Resend Admin Forced Password Reset
    5. **Email Body**:  

        <details>
        <summary>Click to View</summary>

        ```html
        <table align="center" cellPadding="0" cellspacing="0" border="0" width="100%"bgcolor="#f0f0f0">
        <tr>
        <td>
            <table cellPadding="0" cellspacing="0" border="0" width="100%" bgcolor="#ffffff">
            <tr>
                <td colSpan="2" align="center">
                    <a href="http://wso2.com/" target="_blank"><img src="http://cdn.wso2.com/wso2/newsletter/images/nl-2017/wso2-logo-transparent.png" border="0" /></a>
                </td>
            </tr>
            <tr>
                <td colSpan="2" align="center">
                    <h1>
                        Resend Admin Forced Password Reset
                    </h1>
                </td>
            </tr>
            <tr>
                <td valign="top">
                    <p>
                        Hi \{\{user.claim.givenname\}\},
                    </p>
                    <p>
                        Please click the button below to reset your password for the account <b>\{\{user-name\}\}</b>.
                    </p>
                </td>
            </tr>
            <tr>
                <td>
                    <table align="left" cellPadding="0" cellspacing="0" border="0">
                        <tr>
                            <td>
                                <a href="\{\{carbon.product-url\}\}/accountrecoveryendpoint/confirmrecovery.do?confirmation=\{\{confirmation-code\}\}&amp;userstoredomain=\{\{userstore-domain\}\}&amp;username=\{\{url:user-name\}\}&amp;tenantdomain=\{\{tenant-domain\}\}"
                                target="_blank">Reset Password</a>
                            </td>
                        </tr>
                    </table>
                </td>
            </tr>
            <tr>
                <td valign="top">
                    <p>
                        If clicking the button doesn't seem to work, you can copy and paste the following link into your browser. <br />
                        <a target="_blank"
                        href="\{\{carbon.product-url\}\}/accountrecoveryendpoint/confirmrecovery.do?confirmation=\{\{confirmation-code\}\}&amp;userstoredomain=\{\{userstore-domain\}\}&amp;username=\{\{url:user-name\}\}&amp;tenantdomain=\{\{tenant-domain\}\}">
                            \{\{carbon.product-url\}\}/accountrecoveryendpoint/confirmrecovery.do?confirmation=\{\{confirmation-code\}\}&amp;userstoredomain=\{\{userstore-domain\}\}&amp;username=\{\{url:user-name\}\}&amp;tenantdomain=\{\{tenant-domain\}\}
                        </a>
                    </p>
                </td>
            </tr>
            <tr>
                <td valign="top">
                    <p>
                        Thanks,<br />WSO2 Identity Server Team
                    </p>
                </td>
            </tr>
            <tr>
                <td colSpan="2" align="center" bgcolor="#f0f0f0">
                    <p>
                        &copy; 2018
                        <a href="http://wso2.com/" target="_blank">WSO2</a>
                        <br />
                        787 Castro Street, Mountain View, CA 94041.
                    </p>
                </td>
            </tr>
            </table>
        </td>
        </tr>
        </table>```

        </details>
    6. **Email Footer** :  --

6. To create an email template for an **admin-initiated password reset through an OTP**, enter the following values:

    1. **Email Template Type**: resendAdminForcedPasswordResetWithOTP
    2. **Email Template Locale**: English (United States)
    3. **Email Content Type**: text/html
    4. **Email Template Subject**: WSO2 - Resend Admin Forced Password Reset
    5. **Email Body**:  

        <details>
        <summary>Click to View</summary>

        ```html
        <table align="center" cellPadding="0" cellspacing="0" border="0" width="100%"bgcolor="#f0f0f0">
        <tr>
        <td>
            <table cellPadding="0" cellspacing="0" border="0" width="100%" bgcolor="#ffffff">
            <tr>
                <td colSpan="2" align="center">
                    <a href="http://wso2.com/" target="_blank"><img src="http://cdn.wso2.com/wso2/newsletter/images/nl-2017/wso2-logo-transparent.png" border="0" /></a>
                </td>
            </tr>
            <tr>
                <td colSpan="2" align="center">
                    <h1>
                        Resend Admin Forced Password Reset
                    </h1>
                </td>
            </tr>
            <tr>
                <td valign="top">
                    <p>
                        Hi \{\{user.claim.givenname\}\},
                    </p>
                    <p>
                        We received a request to reset the password for the <b>\{\{user-name\}\}</b> account that is associated with this email address.<br />
                        Please use below OTP as the password at next login and then reset your password.<br />
                        OTP : <b>\{\{confirmation-code\}\}</b>
                    </p>
                </td>
            </tr>
            <tr>
                <td valign="top">
                    <p>
                        Thanks,<br />WSO2 Identity Server Team
                    </p>
                </td>
            </tr>
            <tr>
                <td colSpan="2" align="center" bgcolor="#f0f0f0">
                    <p>
                        &copy; 2018
                        <a href="http://wso2.com/" target="_blank">WSO2</a>
                        <br />
                        787 Castro Street, Mountain View, CA 94041.
                    </p>
                </td>
            </tr>
            </table>
        </td>
        </tr>
        </table>```

        </details>
    6. **Email Footer** :  --

:::tip

For information on the REST API for resending confirmation code, see [Resend-Code Using REST API](../../apis/use-the-self-sign-up-rest-apis.md).

:::
