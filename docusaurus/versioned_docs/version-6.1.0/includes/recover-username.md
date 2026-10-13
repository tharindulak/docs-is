---
title: Recover username
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.1.0/docs/includes/recover-username.md
---

Follow the steps below to configure WSO2 Identity Server to enable username recovery.

1.	Open the `deployment.toml` file in the `<IS_HOME>/repository/conf` directory.

	1.	Check whether the following listener configs are in place.

		```
		[event.default_listener.identity_mgt]
		priority= "50"
		enable = false
		[event.default_listener.governance_identity_mgt]
		priority= "95"
		enable = true
		```

1. Navigate to the `<IS_HOME>/repository/conf/deployment.toml` file and uncomment the `[output_adapter.email]` configuration block.

    ```toml
    [output_adapter.email]
    from_address= "wso2iam@outlook.com"
    username= "wso2iam@outlook.com"
    password= "xxxx"
    hostname= "smtp.office365.com"
    port= 587
    ```

    :::info

    - If you use a Gmail account as the email OTP sender, you must create an [App Password](https://support.google.com/accounts/answer/185833?visit_id=637943607149528455-3801902236&p=InvalidSecondFactor&rd=1). After you get an **App Password** from Google, update the `password`.
    - If your password contains special characters (example: `<`, `>`, `&`), you will run into errors when running the server. To avoid errors, update the `password` parameter as follows:
    ```toml
    password= "<![CDATA[xxxx]]>"
    ```

    :::

2. Update the sample values with your email adapter configurations.

    :::info

    Refer [configure email sending module](../../../deploy/configure-email-sending) for the complete list of email adapter configurations.

    :::

3. Save the configurations and restart the server.


3.	On the **Main** > **Identity** menu of the Management Console, click **Identity Providers** > **Resident**.

	<img src="../../../../assets/img/fragments/resident-menu-item.png" alt="Resident menu-item" width="200" />  

4.	Under the **Account Management** section, click **Account Recovery**.	

5.	Select the following check boxes:
	-	**Username Recovery**
	-	**Manage notifications sending internally**

	<img src="../../../../assets/img/fragments/user-name-recovery-options.png" alt="User Name Recover options" width="600" />  	

6.	Click **Update**.
