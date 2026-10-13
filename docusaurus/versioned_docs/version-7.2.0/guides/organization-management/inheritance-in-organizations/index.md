---
title: Customize organization settings
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.2.0/docs/guides/organization-management/inheritance-in-organizations/index.md
---

# Customize organization settings

Parent organizations sit higher in the hierarchy and often define common behaviors for their child organizations. At the same time, child organizations need to maintain their own unique identity and configurations.

WSO2 Identity Server allows child organizations to **inherit** and **override** configurations from their parent organizations. This model simplifies administration by letting parent organizations set baseline configurations. It also gives child organizations the flexibility to customize their settings.

The following guides explain how inheritance works for each of these features:



- **[Configurations for login & registration](login-registration-inheritance.md)**: Learn how child organizations can inherit or override configurations related to login and registration.

- **[User attributes](attribute-inheritance.md)**: Learn how to manage user attribute configurations in organizations.
- **[OIDC scopes](oidc-scope-inheritance.md)**: Learn how organizations inherit OpenID Connect (OIDC) scopes.
- **[Flows](flow-inheritance.md)**: Learn how organizations inherit Flows.



- **[UI branding](ui-branding-inheritance.md)**: Discover how organizations can inherit or define their own look and feel.
- **[Email and SMS template](email-sms-templates-inheritance.md)**: Learn how customizations to Email and SMS templates propagate in an organization hierarchy.
