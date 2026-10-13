---
title: Connection pool behavior
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.0.0/docs/includes/connection-pool-behavior.md
---

By default, when a database connection is returned to the pool, the product rolls back the pending transactions if `defaultAutoCommit=true`. 

However, if required, you can disable the latter mentioned default behavior by disabling the JDBC-Pool JDBC interceptor, `ConnectionRollbackOnReturnInterceptor`, and setting the connection pool behavior on return via the datasource configurations.
