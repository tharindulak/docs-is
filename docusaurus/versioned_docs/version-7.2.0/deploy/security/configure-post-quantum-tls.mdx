---
title: Configure post-quantum TLS
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.2.0/docs/deploy/security/configure-post-quantum-tls.md
---

# Configure post-quantum TLS

As quantum computing becomes a reality, traditional public key algorithms like RSA and ECC grow increasingly vulnerable. WSO2 Identity Server mitigates this issue by supporting **Post-Quantum Cryptography (PQC)** through hybrid key exchange algorithms, specifically the X25519MLKEM768 ([RFC10024](https://datatracker.ietf.org/doc/rfc10024/)) hybrid key agreement algorithm.

## What are hybrid key exchange algorithms?

A hybrid key agreement algorithm combines a classical algorithm with a post-quantum algorithm to establish a shared secret. This approach keeps communication secure even if one algorithm is compromised, helping systems transition seamlessly to post-quantum cryptography.

## Why post-quantum TLS?

- **Future-proof security**: Safeguards TLS communication against future quantum-based attacks.

- **Hybrid compatibility**: Ensures compatibility with current systems while introducing quantum-resistant security.

## Supported communication channels

WSO2 Identity Server supports post-quantum security for both:

- Inbound connections: Between clients (like browsers or apps) and the server.
- Outbound connections: Between the server and other external services.

## Enabling post-quantum TLS

1. Shut down the WSO2 Identity Server instance if running.

2. Add the following configuration to the `<IS_HOME>/repository/conf/deployment.toml` file:

    ```toml
    [transport.https.client]
    provider_name = "BC"

    [transport.https.sslHostConfig.properties]
    protocols="TLSv1.2+TLSv1.3"
    ```

3. Restart the Server.

:::note

Some outbound TLS connections may omit the Server Name Indication (SNI) extension when the Bouncy Castle (BC) provider is enabled, causing certain servers to reject the handshake.

To resolve this, add the following system property at server startup:

<Tabs>
<TabItem value="tab-0" label="Linux/Mac OS">

```bash
sh wso2server.sh -Dorg.bouncycastle.jsse.client.assumeOriginalHostName=true
```

</TabItem>
<TabItem value="tab-1" label="Windows">

```bash
wso2server.bat -Dorg.bouncycastle.jsse.client.assumeOriginalHostName=true
```

</TabItem>
</Tabs>

Note that this may expose connections to **man-in-the-middle (MITM) attacks** if the name service is not trustworthy.

:::
