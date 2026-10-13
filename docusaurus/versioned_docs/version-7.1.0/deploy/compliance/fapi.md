---
title: Financial-grade API (FAPI)
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.1.0/docs/deploy/compliance/fapi.md
---

# Financial-grade API (FAPI)

The Financial-grade API (FAPI) specifications, developed by the OpenID Foundation, define strict security requirements for OAuth 2.0 and OpenID Connect flows in financial and high-risk environments. FAPI compliance ensures that applications securely handle sensitive data, prevent token theft, mitigate replay attacks, and comply with industry standards for financial APIs.

WSO2 Identity Server implements [FAPI 1.0 – Advanced](https://openid.net/specs/openid-financial-api-part-2-1_0.html) and [FAPI 2.0](https://openid.net/specs/fapi-security-profile-2_0-final.html) profiles to help organizations achieve secure, standards-compliant API access.

To create a FAPI compliant application, refer to the guide on [registering a FAPI-compliant application](../../guides/applications/register-a-fapi-compliant-app.md).

## FAPI 1.0 – Advanced compliance features

WSO2 Identity Server fully supports the FAPI 1.0 Advanced Security Profile:

- **Mandatory Signed Request Objects**: Requests can be passed by value (request) or by reference (request_uri) for enhanced security.

- **JWT Secured Authorization Response Mode (JARM)**: Authorization responses are returned as signed JWTs to ensure authenticity.

- **Client Authentication**: Supports confidential clients using mutual TLS and Private Key JWT.

- **Sender-Constrained Access Tokens**: Access tokens are bound to clients with Mutual TLS (MTLS).

- **Secure Token Handling**: Access and refresh tokens are issued and validated according to FAPI 1.0 Advanced security requirements.

These features protect financial API interactions against interception, forgery, and replay attacks.


## FAPI 2.0 compliance features

WSO2 Identity Server supports FAPI 2.0 security profiles, including Read and Read/Write flows, with the following capabilities:

- **Pushed Authorization Requests (PAR)**: Clients must push authorization requests to the `/par` endpoint, enhancing security by using back-channel communication.

- **Proof Key for Code Exchange (PKCE)**: PKCE with the `S256` code challenge method is mandatory for authorization code flows.

- **Authorization code** - Restrict response type to authorization code.

- **Client Authentication**:  Supports confidential clients using mutual TLS and Private Key JWT.

- **Sender-Constrained Access Tokens**: Access tokens are bound to clients via Mutual TLS (MTLS).

- **Secure Token Handling**: Access and refresh tokens are issued and validated according to FAPI 2.0 Advanced security requirements.


WSO2 Identity Server undergoes continuous security reviews and updates. Compliance with the latest FAPI specifications is verified with every release. Cryptographic algorithms and frameworks are updated to meet industry standards. New security features and compliance enhancements are integrated without disrupting existing deployments.

Organizations deploying WSO2 Identity Server can confidently achieve FAPI 1.0 Advanced and FAPI 2.0 compliance, protecting financial data, reducing operational risk, and simplifying regulatory adherence.
