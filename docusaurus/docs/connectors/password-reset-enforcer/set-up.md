---
title: Set up
mkdocs_template: connector
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.3.0/docs/connectors/password-reset-enforcer/set-up.md
---

# Set up

The following guide explains how you can install and set up Password Reset Enforcer in WSO2 Identity Server.

## Prerequisites

- A running WSO2 Identity Server instance.
- Access to the WSO2 Identity Server installation directory (referred to as `IS_HOME`).

## Step 1: Install the Password Reset Enforcer connector

1. From the WSO2 Identity Server [Connector Store](https://store.wso2.com/connector/identity-outbound-auth-passwordPolicy), download the Password Reset Enforcer and its artifacts.

2. Copy the `jar` file into the `<IS_HOME>/repository/components/dropins` directory of your WSO2 Identity Server installation.



## Step 2: Configure password expiry event handling

Add the following configuration to the `IS_HOME/repository/conf/deployment.toml` file.

```toml
[[event_handler]]
name = "passwordExpiry"
subscriptions = [
  "POST_UPDATE_CREDENTIAL",
  "POST_UPDATE_CREDENTIAL_BY_ADMIN",
  "POST_ADD_USER"
]

[event_handler.properties]
passwordExpiryInDays = "30"
enableDataPublishing = false
priorReminderTimeInDays = "0"
```

## Step 3: Enable the authenticator

To make the authenticator available in application step configurations, add the following configuration to the `<IS_HOME>/repository/conf/deployment.toml` file.

```toml
[authentication.authenticator.password-reset-enforcer]
name = "password-reset-enforcer"
enable = true
```


## Step 4: Enable the enforcement scope configuration

To make the **Enforce password expiry for** setting available in the Console, add the following configuration to the `<IS_HOME>/repository/conf/deployment.toml` file.

```toml
[console.ui]
is_password_reset_enforcement_scope_enabled = true
```


## Step 5: Restart WSO2 Identity Server

Restart WSO2 Identity Server to apply the configuration and deploy the artifacts.
