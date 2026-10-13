---
title: Configure Keystores
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.2.0/docs/deploy/security/keystores/configure-keystores.md
---

# Configure Keystores

This page explains how to configure keystores in the `deployment.toml` file. Before you begin, ensure you have already created the keystores you need.

:::info[Before you begin]


1. Review the [recommendations for setting up keystores](index.md#recommendations-for-setting-up-keystores) to understand which keystores you need (primary, internal, TLS).

2. If you have not already created keystores, see [Create New Keystores](create-new-keystores.md).

:::


## Configure default keystore and truststore

WSO2 Identity Server provides default keystore and truststore files:

- `wso2carbon.p12`: The default keystore that includes a private key and a self-signed certificate.
- `client-truststore.p12`: The default truststore containing Certificate Authority (CA) certificates and the self-signed certificate from wso2carbon.p12.

These files are originally located in the `<IS_HOME>/repository/resources/security` folder. The file settings can be configured by specifying them in the `deployment.toml` file found in the `<IS_HOME>/repository/conf` folder as follows.

<Tabs>
<TabItem value="tab-0" label="JKS">


For the primary keystore:
```toml
[keystore.primary]
file_name = "<keystore file name>.jks"
password = "<password>"
key_password = "<password>"
type = "JKS"
alias = "<alias of the public certificate>"
```

For the truststore:
```toml
[truststore]
file_name = "truststore file name>.jks"
password = "<password>"
type = "JKS"
```

</TabItem>
<TabItem value="tab-1" label="PKCS12">


For the primary keystore:
```toml
[keystore.primary]
file_name = "<keystore file name>.p12"
password = "<password>"
key_password = "<password>"
type = "PKCS12"
alias = "<alias of the public certificate>"
```

For the truststore:
```toml
[truststore]
file_name = "<truststore file name>.p12"
password = "<password>"
type = "PKCS12"
```

To generate keystores for newly created tenants in PKCS12 format:
```toml
[keystore.tenant]
type = "PKCS12"
```

</TabItem>
</Tabs>

## Use multiple keystores

In production environments, it is recommended to use distinct keystores for different purposes. See the [Recommendations for setting up keystores](index.md#recommendations-for-setting-up-keystores) in the overview to understand the primary, internal, and TLS keystores.

:::note

All keystores should be placed in `<IS_HOME>/repository/resources/security`.

:::

### Configure the internal keystore

:::warning

If [asymmetric encryption](../asymmetric-encryption/index.md) is used, adding a new keystore for internal data encryption for an existing deployment will make already encrypted data unusable. In such cases, an appropriate data migration effort is needed.

:::

:::note

Before configuring the internal keystore, you must first [create it](create-new-keystores.md#create-the-internal-keystore).

:::

To configure the internal keystore, add the following configuration block to the `deployment.toml` file found in the `<IS_HOME>/repository/conf` folder.

<Tabs>
<TabItem value="tab-0" label="JKS">


```toml
[keystore.internal]
file_name = "<internal-keystore-name>.jks"
password = "<internal-keystore-password>"
key_password = "<internal-keystore-password>"
type = "JKS"
alias = "<internal-key-alias>"
```

</TabItem>
<TabItem value="tab-1" label="PKCS12">


```toml
[keystore.internal]
file_name = "<internal-keystore-name>.p12"
password = "<internal-keystore-password>"
key_password = "<internal-keystore-password>"
type = "PKCS12"
alias = "<internal-key-alias>"
```

</TabItem>
</Tabs>

### Configure TLS keystore

To configure a custom TLS keystore for SSL/TLS connections, update the following configuration:

<Tabs>
<TabItem value="tab-0" label="JKS">


```toml
[keystore.tls]
file_name = "tls.jks"
type = "JKS"
password = "<tls-keystore-password>"
alias = "<tls-key-alias>"
key_password = "<tls-keystore-password>"
```

</TabItem>
<TabItem value="tab-1" label="PKCS12">


```toml
[keystore.tls]
file_name = "tls.p12"
type = "PKCS12"
password = "<tls-keystore-password>"
alias = "<tls-key-alias>"
key_password = "<tls-keystore-password>"
```

</TabItem>
</Tabs>
  
The internally used trust-store configurations given below can be changed to define a custom truststore for SSL validations.

```toml
[transport.https.sslHostConfig.properties]
truststoreFile="${carbon.home}/repository/resources/security/$ref{truststore.file_name}"
truststorePassword = "$ref{truststore.password}"
truststoreType = "$ref{truststore.type}"
```

### Complete production keystore configuration

The following is a complete `deployment.toml` example for a production setup with all three keystores configured separately:

<Tabs>
<TabItem value="tab-0" label="JKS">


```toml
# Primary keystore — used for token signing (OIDC, SAML)
[keystore.primary]
file_name = "primary.jks"
type = "JKS"
password = "<primary-keystore-password>"
alias = "<primary-key-alias>"
key_password = "<primary-keystore-password>"

# Internal keystore — used for encrypting internal data and config passwords (Cipher Tool)
[keystore.internal]
file_name = "internal.jks"
type = "JKS"
password = "<internal-keystore-password>"
alias = "<internal-key-alias>"
key_password = "<internal-keystore-password>"

# TLS keystore — used for HTTPS/SSL connections
[keystore.tls]
file_name = "tls.jks"
type = "JKS"
password = "<tls-keystore-password>"
alias = "<tls-key-alias>"
key_password = "<tls-keystore-password>"

# Truststore
[truststore]
file_name = "client-truststore.jks"
type = "JKS"
password = "<truststore-password>"
```

</TabItem>
<TabItem value="tab-1" label="PKCS12">


```toml
# Primary keystore — used for token signing (OIDC, SAML)
[keystore.primary]
file_name = "primary.p12"
type = "PKCS12"
password = "<primary-keystore-password>"
alias = "<primary-key-alias>"
key_password = "<primary-keystore-password>"

# Internal keystore — used for encrypting internal data and config passwords (Cipher Tool)
[keystore.internal]
file_name = "internal.p12"
type = "PKCS12"
password = "<internal-keystore-password>"
alias = "<internal-key-alias>"
key_password = "<internal-keystore-password>"

# TLS keystore — used for HTTPS/SSL connections
[keystore.tls]
file_name = "tls.p12"
type = "PKCS12"
password = "<tls-keystore-password>"
alias = "<tls-key-alias>"
key_password = "<tls-keystore-password>"

# Truststore
[truststore]
file_name = "client-truststore.p12"
type = "PKCS12"
password = "<truststore-password>"
```

</TabItem>
</Tabs>

:::tip

After configuring keystores, use the [Cipher Tool](../encrypt-passwords-with-cipher-tool.md) to encrypt the keystore passwords in `deployment.toml` so they are not stored in plain text.

:::

## Add new keys to an existing keystore

The following guides explain how you can add new keys to existing keystores.

1. Navigate to the [default keystore](#configure-default-keystore-and-truststore) or other existing keystore on a terminal.

2. Execute the following command.

    <Tabs>
    <TabItem value="tab-0" label="Format">


    ```bash
    keytool -genkey -alias <public_certificate_alias> -keyalg RSA -keysize 2048 -keystore <keystore_name> -storetype <keystore_type> -dname "CN=<<Common Name>>,OU=<<Organization Unit>>,O=<<Organization>>,L=<<Locality>>,S=<<StateofProvice Name>>,C=<<Country Name>>"-storepass <keystore_password> -keypass <private_key_password>
    ```

    </TabItem>
    <TabItem value="tab-1" label="Sample command (JKS)">


    ```bash
    keytool -genkey -alias newkey -keyalg RSA -keysize 2048 -keystore wso2carbon.jks -dname "CN=localhost, OU=IT,O=/identity/7.2.0,L=SL,S=WS,C=LK" -storepass wso2carbon -keypass wso2carbon
    ```

    </TabItem>
    <TabItem value="tab-2" label="Sample command (PKCS12)">


    ```bash
    keytool -genkey -alias newkey -keyalg RSA -keysize 2048 -keystore wso2carbon.p12 -storetype PKCS12 -dname "CN=localhost, OU=IT,O=/identity/7.2.0,L=SL,S=WS,C=LK" -storepass wso2carbon -keypass wso2carbon
    ```

    </TabItem>
    </Tabs>

    :::tip

    If you are planning to delete the newly added keys in the future, it is recommended to [maintain separate keystores](#use-multiple-keystores).

    :::

## View public keys via JWKS

To view super tenant public key sets via the JWKS endpoint, visit `https://<IS_HOST>:<PORT>/oauth2/jwks`.

:::note

**Example**
```json
// 20190612140905
// https://localhost:9443/oauth2/jwks
  
{
  "keys": [
    {
      "kty": "RSA",
      "e": "AQAB",
      "use": "sig",
      "kid": "MGZlMjg1MTEyZjE5ZGEyZTI2MWY4ODNlOGM5ZWQwZDIyNzk4MTJiZg",
      "alg": "RS256",
      "n": "swfFo3uUhsEE5SSJSUrzE4-U-PuYmQn-d71GOV59VcL1_cZRAPS89GE1_M3fmFP4xzB7X4p5vYW7lYYZvOUeZGC0BwR1YXz7uK9VRqXDQM1t_X8yUxtYf6u6hajD5fR3PzirlMzjW1ckojeGTgKS5G-HdixOs2OX2n_kQ5LVUHwIEJ2lryGkfd2Vfq7IBgAifQqYDLcrKqK3-iwF7-foii0lLFg8E_dRuOD5sa6Ec01WjogsA14fZRHzmNKiocjP_FOzmvfq7uHRYta6erTVHtsdOvJBVDy1ANvR0cxGdydfRnGwDYI05kgA5L27MnlN6NMroffDBtHmlCvvwToylw"
    },
    {
      "kty": "RSA",
      "e": "AQAB",
      "use": "sig",
      "kid": "NTAxZmMxNDMyZDg3MTU1ZGM0MzEzODJhZWI4NDNlZDU1OGFkNjFiMQ",
      "alg": "RS256",
      "n": "luZFdW1ynitztkWLC6xKegbRWxky-5P0p4ShYEOkHs30QI2VCuR6Qo4Bz5rTgLBrky03W1GAVrZxuvKRGj9V9-PmjdGtau4CTXu9pLLcqnruaczoSdvBYA3lS9a7zgFU0-s6kMl2EhB-rk7gXluEep7lIOenzfl2f6IoTKa2fVgVd3YKiSGsyL4tztS70vmmX121qm0sTJdKWP4HxXyqK9neolXI9fYyHOYILVNZ69z_73OOVhkh_mvTmWZLM7GM6sApmyLX6OXUp8z0pkY-vT_9-zRxxQs7GurC4_C1nK3rI_0ySUgGEafO1atNjYmlFN-M3tZX6nEcA6g94IavyQ"
    }
  ]
}
```

:::
