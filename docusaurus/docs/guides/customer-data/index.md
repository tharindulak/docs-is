---
title: Customer data
deployment_options:
  - WSO2 Cloud
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/asgardeo/docs/guides/customer-data/index.md
---

# Customer data

The Customer Data Service (CDS) collects and unifies data about your end users across every interaction with your applications. It gives each user a single profile that represents who they are and what they have done across your applications.

:::note

You need to enable the Customer Data Service for your organization before you start. See [Enable Customer Data Service](enable-customer-data-service.md).

:::

## What you can do with it

- **Capture anonymous activity:** Capture what a visitor favorites, submits, or browses, before they ever create an account or sign in.
- **Keep the data when they sign up:** CDS merges the anonymous profile into the user's permanent one at sign in, so activity from before the account existed gets carried over.
- **Unify a person across devices and applications:** Bring user data together into a single profile, linked by the `user_id` after sign-in or by a matching identifier, such as an email address, before sign-in.
- **Control what a profile holds and how it merges:** Define profile attributes, data types, and merge rules, including whether values accumulate over time or are replaced by the most recent value.

## Where to start

| Read | What it covers |
|---|---|
| [Enable Customer Data Service](enable-customer-data-service.md) | Turn the feature on from the **Customer Data** page. |
| [Profiles](concepts/profiles.md) | The shape of a profile and how anonymous and permanent profiles relate. |
| [Profile attributes](concepts/profile-attributes.md) | Attribute types, mutability, and merge strategies. |
| [Unification rules](concepts/unification-rules.md) | When two records get merged into one. |
| [Use cases](use-cases/index.md) | Common integration patterns for unifying activity across sessions, devices, and applications. |
