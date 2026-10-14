---
title: Change to MySQL
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.3.0/docs/deploy/configure/databases/carbon-database/change-to-mysql.md
---

import DatasourceConfig from '../../../../_partials/datasource-config.mdx';
import DbBasicConfig from '../../../../_partials/db-basic-config.mdx';
import DbAdvancedConfig from '../../../../_partials/db-advanced-config.mdx';
import DbConfigTable from '../../../../_partials/db-config-table.mdx';
import ConnectionPoolBehavior from '../../../../_partials/connection-pool-behavior.mdx';
import CommitPending from '../../../../_partials/commit-pending.mdx';
import RollbackPending from '../../../../_partials/rollback-pending.mdx';
import DriverLevelTimeouts from '../../../../_partials/driver-level-timeouts.mdx';

# Change to MySQL

By default, WSO2 Identity Server uses the embedded H2 database as the database
for storing user management and registry data. Given below are the steps
you need to follow in order to use MySQL for this purpose. 

---

## Datasource configurations

<DatasourceConfig />
                       
After setting up the MySQL database. You can point the `WSO2_IDENTITY_DB` or 
`WSO2_SHARED_DB` or both to that MySQL database by following the instructions given below.

---

## Change the default datasource

### Minimum configurations for changing default datasource to MySQL
 
You can configure the datasource by editing the default configurations in `<IS_HOME>/repository/conf/deployment.toml`. 

Following are the basic configurations and their descriptions. 

<DbBasicConfig />
 
A sample configuration is given below.

1. `WSO2_IDENTITY_DB` 

    1. Configure the`deployment.toml` file.

        ```toml
        [database.identity_db]
        type = "mysql"
        hostname = "localhost"
        name = "regdb"
        username = "regadmin"
        password = "regadmin"
        port = "3306"
        ```
    
    1. Execute database scripts.
    
        Navigate to `<IS_HOME>/dbscripts`. Execute the scripts in the following files, against the database created.
        
        - `<IS_HOME>/dbscripts/identity/mysql.sql`
        - `<IS_HOME>/dbscripts/consent/mysql.sql`
        
2. `WSO2_SHARED_DB`
    
    1.  Configure the `deployment.toml` file. 

        ```toml
        [database.shared_db]
        type = "mysql"
        hostname = "localhost"
        name = "regdb"
        username = "regadmin"
        password = "regadmin"
        port = "3306"
        ```
        
    2.  Execute database scripts.
    
        Execute the scripts in the `<IS_HOME>/dbscripts/mysql.sql` file against the database created.
                         
    :::note

    Instead of defining `hostname`, `port`, and `name` separately, you can define the `url`
    of the database in the following format.
                
    ```toml
    type = "mysql"
    url = "jdbc:mysql://localhost:3306/regdb"
    username = "regadmin"
    password = "regadmin"
    ```

    :::

    :::note

    As MySQL DB is inherently case-insensitive, it is recommended to deactivate the case-insensitive functionality of WSO2 Identity Server when integrating with MySQL DB.
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
    
    3.  Download the [MySQL JDBC driver](https://mvnrepository.com/artifact/com.mysql/mysql-connector-j) and copy the JAR (mysql-connector-j-x.x.x.jar) to the `<IS_HOME>/repository/components/lib` folder.
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

### Example: MySQL database

```toml
[database.identity_db]
url = "jdbc:mysql://DB_HOST:3306/WSO2_IDENTITY_DB?connectTimeout=10000&amp;socketTimeout=60000&amp;tcpKeepAlive=true"
username = "..."
password = "..."
driver = "com.mysql.cj.jdbc.Driver"
```

Learn more in [MySQL Connector/J properties](https://docs.oracle.com/cd/E19509-01/820-3497/agqju/index.html).
