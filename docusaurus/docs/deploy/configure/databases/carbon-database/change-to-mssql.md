---
title: Change to MS SQL
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.3.0/docs/deploy/configure/databases/carbon-database/change-to-mssql.md
---

import DatasourceConfig from '../../../../_partials/datasource-config.mdx';
import DbBasicConfig from '../../../../_partials/db-basic-config.mdx';
import DbAdvancedConfig from '../../../../_partials/db-advanced-config.mdx';
import DbConfigTable from '../../../../_partials/db-config-table.mdx';
import ConnectionPoolBehavior from '../../../../_partials/connection-pool-behavior.mdx';
import CommitPending from '../../../../_partials/commit-pending.mdx';
import RollbackPending from '../../../../_partials/rollback-pending.mdx';
import DriverLevelTimeouts from '../../../../_partials/driver-level-timeouts.mdx';

# Change to MS SQL

By default, WSO2 Identity Server uses the embedded H2 database as the database
for storing user management and registry data. Given below are the steps
you need to follow in order to use MS SQL for this purpose.

---

## Set up datasource configurations

<DatasourceConfig />

After setting up the MS SQL database, you can point the `WSO2_IDENTITY_DB` or
`WSO2_SHARED_DB` or both to that MS SQL database by following the instructions given below.

---

## Change the default datasource

### Minimum configurations for changing default datasource to MS SQL

You can configure the datasource by editing the default configurations in `<IS_HOME>/repository/conf/deployment.toml`.

Following are the basic configurations and their descriptions.

<DbBasicConfig />

A sample configuration is given below.

1. `WSO2_IDENTITY_DB`

    1. Configure the `<IS_HOME>/repository/conf/deployment.toml` file.

        ```toml
        [database.identity_db]
        type = "mssql"
        hostname = "localhost"
        name = "regdb"
        username = "regadmin"
        password = "regadmin"
        port = "1433"
        ```

    2. Execute database scripts.

        Navigate to `<IS_HOME>/dbscripts`. Execute the scripts in the following files against the database created.
        
        - `<IS_HOME>/dbscripts/identity/mssql.sql`
        - `<IS_HOME>/dbscripts/consent/mssql.sql`

2. `WSO2_SHARED_DB`

    1.  Configure the `<IS_HOME>/repository/conf/deployment.toml` file.

        ```toml
        [database.shared_db]
        type = "mssql"
        hostname = "localhost"
        name = "regdb"
        username = "regadmin"
        password = "regadmin"
        port = "1433"
        ```

    2.  Execute database scripts.

        Execute the scripts in the `<IS_HOME>/dbscripts/mssql.sql` file, against the database created.

    :::note

    As Microsoft SQL Server is inherently case-insensitive, it is recommended to deactivate the case-insensitive functionality of WSO2 Identity Server when integrating with the Microsoft SQL Server.
    Disabling this feature in WSO2 Identity Server eliminates unnecessary processing, thereby potentially enhancing overall system performance.

    To disable case-insensitivity for the primary user store, open the `deployment.toml` file found in the `<IS_HOME>/repository/conf/` directory and add the following configurations to the primary user store.

    ```toml
    [user_store.properties]
    CaseInsensitiveUsername = false
    UseCaseSensitiveUsernameForCacheKeys = false
    ```  

    For secondary user stores, add the following configurations to the `<userstore>.xml` file found in the `<IS_HOME>/repository/deployment/server/userstores` directory.

    ```xml
    <Property name="CaseInsensitiveUsername">false</Property>
    <Property name="UseCaseSensitiveUsernameForCacheKeys">false</Property>
    ```

    :::

    :::note

    To store user attributes as Unicode for the primary user store, open the `deployment.toml` file found in the `<IS_HOME>/repository/conf/` directory and add the following configuration under the primary user store.

    ```toml
    [user_store.properties]
    StoreUserAttributeValueAsUnicode = true
    ```

    For secondary user stores, this setting is enabled by default. However, if you need to explicitly configure it, add the following property to the `<userstore>.xml` file located in the `<IS_HOME>/repository/deployment/server/userstores` directory.

    ```xml
    <Property name="StoreUserAttributeValueAsUnicode">true</Property>
    ```

    :::
    
3.  Download the [MSSQL JDBC driver](https://mvnrepository.com/artifact/com.microsoft.sqlserver/mssql-jdbc) and copy the JAR (mssql-jdbc-x.x.x.jre11.jar) to the `<IS_HOME>/repository/components/lib` folder.

---

### Advanced database configurations

<DbAdvancedConfig />

<DbConfigTable />

---
  
## Configure the connection pool behavior on return 

<ConnectionPoolBehavior />

### Configure the connection pool to commit pending transactions on connection return
        
<CommitPending />

### Configure the connection pool to rollback pending transactions on connection return

<RollbackPending />

## Driver-Level Timeouts (Recommended for Production)

<DriverLevelTimeouts />

### Example: MSSQL database

```toml
[database.identity_db]
url = "jdbc:sqlserver://DB_HOST:1433;databaseName=WSO2_IDENTITY_DB;loginTimeout=10;socketTimeout=60000"
username = "..."
password = "..."
driver = "com.microsoft.sqlserver.jdbc.SQLServerDriver"
```

Learn more in [Microsoft JDBC driver properties](https://learn.microsoft.com/sql/connect/jdbc/setting-the-connection-properties).
