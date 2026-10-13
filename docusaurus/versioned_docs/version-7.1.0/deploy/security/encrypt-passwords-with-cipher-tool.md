---
title: Encrypt Passwords with the Cipher Tool
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.1.0/docs/deploy/security/encrypt-passwords-with-cipher-tool.md
---

# Encrypt Passwords with the Cipher Tool

The instructions on this page explain how plain text passwords in configuration files can be encrypted using the secure vault implementation that is built into the WSO2 Identity Server.  

:::info[Before you begin]

If you are using Windows, you need to have [**Ant**](http://ant.apache.org/) installed in order to use the Cipher Tool.

:::

## Encrypt passwords



While you are able to encrypt passwords using symmetric or asymmetric encryption, it is recommended to use symmetric encryption due to its greater resilience towards emerging post-quantum threats. 
Asymmetric encryption methods like RSA are not recommended due to their vulnerability to quantum computing capabilities.

:::warning

[Configure the internal keystore](keystores/configure-keystores.md#configure-the-internal-keystore) to encrypt passwords. If the internal keystore is not specified, the primary keystore will be used instead.

:::

Follow the steps below to encrypt passwords:

1. Add the following `[secrets]` configurations to the bottom of the `deployment.toml` file in the `<IS_HOME>/repository/conf/` directory. Provide an alias for the password type followed by the actual password enclosed within square brackets `[]` as shown below.

    ```toml
    [secrets]
    admin_password = "[password_1]"
    keystore_password = "[password_2]"
    key_password = "[password_3]"
    truststrore_password = "[password_4]"
    log4j2_password = "[password_5]"
    ```

2.  Open a terminal, navigate to the `<IS_HOME>/bin/` directory, and execute the following command based on the encryption method and your operating system:

    <Tabs>
    <TabItem value="tab-0" label="Symmetric encryption">


    :::note[Prerequisite]


    To support symmetric encryption, you should have a symmetric secret in an internal keystore of type PKCS12. Follow the instructions for [creating the internal keystore](keystores/create-new-keystores.md#create-the-internal-keystore) with a symmetric AES key.

    :::

    - **For Linux**: `./ciphertool.sh -Dconfigure -Dsymmetric`

    - **For Windows**: `ciphertool.bat -Dconfigure -Dsymmetric`

    </TabItem>
    <TabItem value="tab-1" label="Asymmetric encryption">


    :::warning


    Asymmetric encryption methods like RSA are not recommended due to their vulnerability to post-quantum threats.

    :::

    - **For Linux**: `./ciphertool.sh -Dconfigure`

    - **For Windows**: `ciphertool.bat -Dconfigure`

    </TabItem>
    </Tabs>

3. Open the `deployment.toml` again and see that the passwords are encrypted.

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



3. Run the cipher tool by executing the command corresponding to your encryption method and operating system:

    <Tabs>
    <TabItem value="tab-0" label="Symmetric encryption">


    - **For Linux**: `./ciphertool.sh -Dchange -Dsymmetric`

    - **For Windows**: `ciphertool.bat -Dchange -Dsymmetric`

    </TabItem>
    <TabItem value="tab-1" label="Asymmetric encryption">


    - **For Linux**: `./ciphertool.sh -Dchange`

    - **For Windows**: `ciphertool.bat -Dchange`

    </TabItem>
    </Tabs>



4. You will be prompted for the primary keystore password. Enter the password. For the default keystore, it is `wso2carbon`.

5. A numbered list of all encrypted password aliases will be displayed. Enter the number corresponding to the alias of the password you want to change.

6. The system will then prompt you (twice) to enter the new password. Enter your new password.


## Rotating Encryption Secrets

:::note

To support symmetric encryption, you must specify a PKCS12 type keystore as the internal keystore.

:::

You can rotate encryption keys by switching between symmetric and asymmetric encryption or by changing the encryption keys within the same encryption mode. Follow the steps below.

1. Use the corresponding command to add the new key to an existing keystore with a new alias.

    <Tabs>
    <TabItem value="tab-0" label="Symmetric encryption">


    ```bash
    keytool -genseckey -alias new_alias -keyalg AES -keysize 256 -keystore internal.p12 -storetype PKCS12 -storepass password -keypass password
    ```

    </TabItem>
    <TabItem value="tab-1" label="Asymmetric encryption (JKS)">


    ```bash
    keytool -genkeypair -alias new_alias -keyalg RSA -keystore wso2carbon.jks -storepass password -keypass password
    ```

    </TabItem>
    <TabItem value="tab-2" label="Asymmetric encryption (PKCS12)">


    ```bash
    keytool -genkeypair -alias new_alias -keyalg RSA -keystore wso2carbon.p12 -storetype PKCS12 -storepass password -keypass password
    ```

    </TabItem>
    </Tabs>

2. Update the `deployment.toml` file found in the `<IS_HOME>/repository/conf` directory to reflect the new key or secret alias:

    <Tabs>
    <TabItem value="tab-0" label="JKS">


    ```toml
    [keystore.internal]
    file_name = "internal.jks"
    type = "JKS"
    alias = "new_alias"
    password = "$secret{keystore_password}"
    key_password = "$secret{keystore_password}"
    ```

    </TabItem>
    <TabItem value="tab-1" label="PKCS12">


    ```toml
    [keystore.internal]
    file_name = "internal.p12"
    type = "PKCS12"
    alias = "new_alias"
    password = "$secret{keystore_password}"
    key_password = "$secret{keystore_password}"
    ```

    </TabItem>
    </Tabs>

3. Navigate to the `<IS_HOME>/bin/` directory on the command prompt, where the cipher tool scripts reside.

4. Execute the cipher tool script to re-encrypt the passwords with the new key or secret. Use the `-Drotate` option and specify the old alias.

    <Tabs>
    <TabItem value="tab-0" label="Symmetric encryption">


    - For Linux: `./ciphertool.sh -Drotate -Dold.alias=wso2carbon -Dsymmetric`

    - For Windows: `ciphertool.bat -Drotate -Dold.alias=wso2carbon -Dsymmetric`

    </TabItem>
    <TabItem value="tab-1" label="Asymmetric encryption">


    - On Linux: `./ciphertool.sh -Drotate -Dold.alias=wso2carbon`

    - On Windows: `ciphertool.bat -Drotate -Dold.alias=wso2carbon`

    </TabItem>
    </Tabs>

5. Go back to the `deployment.toml` file and see that the passwords are re-encrypted with the new encryption key.



:::info[Related topics]

- [Deploy: Resolve Encrypted Passwords](resolve-encrypted-passwords.md)
- [Deploy: Customize Secure Vault](customize-secure-vault.md)

:::
