---
title: Use cases
deployment_options:
  - WSO2 Cloud
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/asgardeo/docs/guides/customer-data/use-cases/index.md
---

<h1>Customer data service use cases</h1>

These guides show common patterns for integrating with the Customer Data Service from your application. They capture visitor activity even before an account is created, and unify it into a single profile that follows the user across sessions, devices, and applications.

---

## Before you begin

- [Enable Customer Data Service](../enable-customer-data-service.md) for your organization.
- A [machine-to-machine (M2M) application](../../applications/register-machine-to-machine-app.md) is registered for your backend to call the Customer Data Service APIs, granted the `internal_cds_profile_create`, `internal_cds_profile_update`, and `internal_cds_profile_view` scopes and configured to issue tokens with the `iam-cds` audience.
- The [profile attributes](../guides/manage-profile-attributes.md) that your activity maps to are defined, each with the merge strategy it should use.
- The [unification rules](../guides/manage-unification-rules.md) that decide when two profiles are the same person are defined.

---

## Use cases

| Read | Use this when |
|---|---|
| [Unify anonymous and registered profiles](self-registration.md) | A visitor interacts anonymously, then signs up, and their activity is consolidated into the new profile. |
| [Accumulate data across multiple devices](cross-device.md) | A user interacts anonymously across multiple devices and then signs in, and their activity is consolidated into a single profile. |
| [Stitch user profiles across websites](lead-stitching.md) | A visitor interacts anonymously across multiple applications or domains, and their activity is consolidated into a single profile based on a shared identifier. |
