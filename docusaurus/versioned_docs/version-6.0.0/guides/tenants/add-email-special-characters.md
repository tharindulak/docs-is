---
title: Configure Emails with Special Characters
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.0.0/docs/guides/tenants/add-email-special-characters.md
---

# Configure Emails with Special Characters

Follow the steps below to accommodate email addresses with special character in WSO2 Identity Server.  

1.	Sign in to WSO2 Identity Server Management Console at `https://<IS_HOST>:<PORT>/carbon` as an administrator. 

2.	On the **Main** menu of the Management Console, click **Identity > Claims > List**.

	<img src="/identity/assets/img/guides/claims-list-menu-item.png" alt="Claims List menu-item" width="200" />   

3.	Click  **http://wso2.org/claims**.

	<img src="/identity/assets/img/guides/claim-list-wso2.png" alt="WSO2 Claim" width="600" />   	

4.	Under **Email**, click **Edit**.

	<img src="/identity/assets/img/guides/email-claim-edit.png" alt="Claim Edit option" width="600" /> 

5.	Enter the required special characters (`!#$%&'*+-=?^_`) in the **Regular Expression** text box.

	<img src="/identity/assets/img/guides/wso2-claim-edit-screen.png" alt="WSO2 Claim Edit screen" width="700" /> 


	:::note[Using # and $]



	:::

		-	To add **`#`** to the email regex pattern: 
			```
			^([a-zA-Z0-9_.-#])+\@(([a-zA-Z0-9#-])+.)+([a-zA-Z0-9#]{2,4})+$`
			```			

		-	To add **`$`** to the email regex pattern:
			```
			^([a-zA-Z0-9_.-\])+\@(([a-zA-Z0-9\\-])+.)+([a-zA-Z0-9\]{2,4})+
			```

	:::warning[Escaping $]



	:::

		When using the `$` character, make sure to use the appropriate escape characters, such as `\`, e.g., `abc\$def@somemail.com`
