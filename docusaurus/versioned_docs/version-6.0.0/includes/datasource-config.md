---
title: Datasource config
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.0.0/docs/includes/datasource-config.md
---

A datasource is used to establish the connection to a database. By
default, `WSO2_IDENTITY_DB` and `WSO2_SHARED_DB` datasources are used to connect
to the default H2 database. 

- `WSO2_SHARED_DB` - The datasource which stores registry and user management
                     data.
- `WSO2_IDENTITY_DB` - The datasource specific to the identity server which stores
                       identity related data.
