---
title: Change to Remote H2
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.3.0/docs/deploy/configure/databases/carbon-database/change-to-remote-h2.md
---

import DatasourceConfig from '../../../../_partials/datasource-config.mdx';
import DbAdvancedConfig from '../../../../_partials/db-advanced-config.mdx';
import DbConfigTable from '../../../../_partials/db-config-table.mdx';
import ConnectionPoolBehavior from '../../../../_partials/connection-pool-behavior.mdx';
import CommitPending from '../../../../_partials/commit-pending.mdx';
import RollbackPending from '../../../../_partials/rollback-pending.mdx';
import DriverLevelTimeouts from '../../../../_partials/driver-level-timeouts.mdx';

# Change to Remote H2

By default, WSO2 Identity Server uses the embedded H2 database as the database
for storing user management and registry data.
The following sections describe how to replace the default H2 databases
with Remote H2:

:::warning[H2 is not recommended in production]

The embedded H2 database is NOT recommended in enterprise testing and
production environments. It has lower performance, clustering
limitations, and can cause file corruption failures. Please use an
industry-standard RDBMS such as Oracle, PostgreSQL, MySQL, or MS SQL
instead.

You can use the embedded H2 database in development environments and as
the local registry in a registry mount.

:::

---   

## Datasource configurations

<DatasourceConfig />
                       
After setting up the H2 database, You can point the `WSO2_IDENTITY_DB` or 
`WSO2_SHARED_DB`, or both to that H2 database by following the instructions given below.

---

## Change the default datasource

### Minimum configurations for changing default datasource to H2
 
You can configure the datasource by editing the default configurations in `<IS_HOME>/repository/conf/deployment.toml`. 

Following are the basic configurations and their descriptions. 

<table><thead><tr className={"header"}><th>{"Element"}</th><th>{"Description"}</th></tr></thead><tbody><tr className={"even"}><td><strong>{"username"}</strong>{" and "}<strong>{"password"}</strong></td><td>{"The name and password of the database user."}</td></tr><tr className={"even"}><td><strong>{"driver"}</strong></td><td>{"The jdbc driver of the database."}</td></tr><tr className={"even"}><td><strong>{"url"}</strong></td><td>{"The url of the database."}</td></tr></tbody></table>
 
A sample configuration is given below.

1. `WSO2_IDENTITY_DB` 

    1. Configure the `deployment.toml` file.

        ```toml
        [database.identity_db]
        url = "jdbc:h2:tcp://localhost/~/registryDB;create=true"
        username = "regadmin"
        password = "regadmin"
        driver = "org.h2.Driver"
        [database.identity_db.pool_options]
        maxActive = "80"
        maxWait = "60000"
        minIdle = "5"
        testOnBorrow = true
        validationQuery="SELECT 1"
        validationInterval="30000"
        defaultAutoCommit=false
        ```
    
    1. Execute database scripts.
    
        Navigate to `<IS_HOME>/dbscripts`. Execute the scripts in the following files against the database created.
        
        - `<IS_HOME>/dbscripts/identity/h2.sql`
        - `<IS_HOME>/dbscripts/consent/h2.sql`
        
2. `WSO2_SHARED_DB`
    
    1. Configure the `deployment.toml` file.

        ```toml
        [database.shared_db]
        url = "jdbc:h2:tcp://localhost/~/registryDB;create=true"
        username = "regadmin"
        password = "regadmin"
        driver = "org.h2.Driver"
        [database.identity_db.pool_options]
        maxActive = "80"
        maxWait = "60000"
        minIdle = "5"
        testOnBorrow = true
        validationQuery="SELECT 1"
        validationInterval="30000"
        defaultAutoCommit=false
        ```
        
    1.  Execute the database scripts.
    
        Execute the scripts in the `<IS_HOME>/dbscripts/h2.sql` file against the database created.
    
3.  Download the H2 JDBC driver for the version you are using. Extract the downloaded file if necessary, and copy all required JAR files from the driver package to the `<IS_HOME>/repository/components/lib` folder.

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

### Example: Remote H2 database

```toml
[database.identity_db]
url = "jdbc:h2:tcp://localhost/~/WSO2_IDENTITY_DB;QUERY_TIMEOUT=60000"
username = "..."
password = "..."
driver = "org.h2.Driver"
```

Learn more in [H2 connection settings](http://www.h2database.com/html/features.html#connection_settings).
