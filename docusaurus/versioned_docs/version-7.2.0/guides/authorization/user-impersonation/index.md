---
title: User Impersonation
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.2.0/docs/guides/authorization/user-impersonation/index.md
---

# User Impersonation

User impersonation enables an authorized user to act on behalf of another user. This feature proves useful for administrators or support personnel who need to perform tasks without requiring the credentials of the end user.

:::note[Limitations]

  Impersonated tokens won't include any user claim values set during adaptive authentication.

:::

You can start user impersonation in two ways:

   1. [Via Console](via-console.md)

   2. [Via business application (advanced)](via-business-application.md)

If the impersonator is a shared user (a user whose profile is managed by a parent organization), see [Impersonation for shared users](/identity/7.2.0/guides/organization-management/shared-user-impersonation).
