---
title: Your WSO2 Identity Platform
deployment_options:
  - WSO2 Cloud
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/asgardeo/docs/guides/your-identity-platform/index.md
---

# Your WSO2 Identity Platform

When you [create an account](../../get-started/create-identity-platform-account.md) in WSO2 Identity Platform, you define your first organization (root), which functions as the root organization or tenant in your WSO2 Identity Platform subscription. From thereon, you (the account owner) or other delegated administrators can create multiple root organizations via the WSO2 Identity Platform Console and switch between them.

Listed below are the main characteristics of an organization (root).

- An organization (root) contains applications, external identity providers, and user identities belonging to a single domain.
- Users or applications created in one organization (root) cannot access the resources of another organization (root) unless they are onboarded to that organization (root).
- The administrator who creates the organization (root) is the owner of the organization (root).

If you are an owner of an organization (root) or an administrator, you can manage your WSO2 Identity Platform accounts [using the My Account portal](identity-platform-self-service.md).

The owner is a user who creates an organization (root) in WSO2 Identity Platform. This grants the owner all the administrative rights by default. An administrator is a user who is invited in to the organization (root) and assigned administrative privileges.
