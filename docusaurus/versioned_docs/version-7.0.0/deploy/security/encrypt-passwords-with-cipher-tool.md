---
title: Encrypt Passwords with the Cipher Tool
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.0.0/docs/deploy/security/encrypt-passwords-with-cipher-tool.md
---

# Encrypt Passwords with the Cipher Tool

The instructions on this page explain how plain text passwords in configuration files can be encrypted using the secure vault implementation that is built into the WSO2 Identity Server.  

:::info[Before you begin]

If you are using Windows, you need to have [**Ant**](http://ant.apache.org/) installed in order to use the Cipher Tool.

:::

## Encrypt passwords



To encrypt passwords on the WSO2 Identity Server:

1. Add the following `[secrets]` configurations to the bottom of the `deployment.toml` file in the `<IS_HOME>/repository/conf/` directory. Give an alias for the password type followed by the actual password. The following example lists the most common passwords in configuration files.

    ```toml
    [secrets]
    admin_password = "[password_1]"
    keystore_password = "[password_2]"
    key_password = "[password_3]"
    truststrore_password = "[password_4]"
    log4j2_password = "[password_5]"
    ```

2. Open a terminal, navigate to the `<IS_HOME>/bin/` directory, and execute the following command to enable the cipher tool using the `-Dconfigure` flag.

    - On Linux: `./ciphertool.sh -Dconfigure`
    - On Windows: `ciphertool.bat -Dconfigure`

3. Open the `deployment.toml` file again and see that the alias passwords are encrypted.

    ```toml
    [secrets]
    admin_password = "xxxxxxx"
    keystore_password = "xxxxxxx"
    key_password = "xxxxxxx"
    truststrore_password = "xxxxxxx"
    log4j2_password = "xxxxxxx"
    ```



## Use encrypted passwords

:::note

When you start the server after configuring encrypted passwords, the server requires the keystore and private key passwords to decrypt the secrets. See [Resolve Encrypted Passwords](resolve-encrypted-passwords.md) for the available options to provide these passwords at server startup.

:::

Once you have [encrypted passwords](#encrypt-passwords), you can use them in the relevant configuration files as follows:

### In deployment.toml

You can include encrypted passwords in the `deployment.toml` file found in the `<IS_HOME>/repository/conf` directory by using the `$secret{alias}` format as shown below:

:::note

You may pass passwords as environment variables and system properties instead of directly setting the values. See [Set Passwords using Environment Variables/System Properties](set-passwords-using-environment-variables-or-system-properties.md) for instructions.

:::

```toml
[super_admin]
username="admin"
password="$secret{admin_password}"

[keystore.tls]
password = "$secret{keystore_password}" 
alias = "alias" 
key_password = "$secret{key_password}"  

[truststore]                  
password = "$secret{keystore_password}" 
```

### In log4j2.properties

You may include encrypted passwords in the `log4j2.properties` file found in the `<IS_HOME>/repository/conf` directory. For example, you may set `log4j.appender.LOGEVENT.password` as shown below:

```
log4j.appender.LOGEVENT.password=$secret{log4j2_password}
```

## Change encrypted passwords

You may follow the steps below to change passwords that are already encrypted.

1. Shut down the WSO2 Identity Server.

2. On a command prompt, navigate to the `<IS_HOME>/bin/` directory where the cipher tool scripts reside.



3. Run the cipher tool by executing the command corresponding to your operating system:

    * Linux: `./ciphertool.sh -Dchange`
    * Windows: `ciphertool.bat -Dchange`



4. You will be prompted for the primary keystore password. Enter the password. For the default keystore, it is `wso2carbon`.

5. A numbered list of all encrypted password aliases will be displayed. Enter the number corresponding to the alias of the password you want to change.

6. The system will then prompt you (twice) to enter the new password. Enter your new password.



:::info[Related topics]

- [Deploy: Resolve Encrypted Passwords](resolve-encrypted-passwords.md)
- [Deploy: Customize Secure Vault](customize-secure-vault.md)

:::
