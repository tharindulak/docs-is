---
title: Change the Default Datasource for Agent Identities
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.3.0/docs/deploy/configure/databases/carbon-database/change-datasource-agent-identity.md
---

import DbConfigTable from '../../../../_partials/db-config-table.mdx';

# Change the Default Datasource for Agent Identities

WSO2 Identity Server ships with an embedded H2 database for storing data. These default databases are located in the `<IS_HOME>/repository/database` directory.

Agent identity data is stored in the agent database (AGENT). You can use any database type that is supported by WSO2 Identity Server.

:::note

For more information about databases, see 
[Work with Databases](../index.md) and [Set Up Separate Databases for Clustering](../../../set-up-separate-databases-for-clustering.md).

:::

Following are the sample configuration for each database type.

<details>
<summary>PostgreSQL</summary>


1.  Configure the `<IS_HOME>/repository/conf/deployment.toml` file.
    
    ```
    [datasource.AgentIdentity]
    id = "AgentIdentity"
    url = "jdbc:postgresql://localhost:5432/AgentDB"
    username = "regadmin"
    password = "regadmin"
    driver = "org.postgresql.Driver"
    jmx_enable=false
    ```
    
2.  Execute the database scripts. 

    Execute the scripts in the `<IS_HOME>/dbscripts/identity/agent/postgresql.sql` file against 
    the created database.    

</details>
          
<details>
<summary>MySQL</summary>


1.  Configure the `<IS_HOME>/repository/conf/deployment.toml` file.
    
    ```
    [datasource.AgentIdentity]
    id = "AgentIdentity"
    url = "jdbc:mysql://localhost:3306/AgentDB?useSSL=false"
    username = "root"
    password = "root"
    driver = "com.mysql.jdbc.Driver"
    jmx_enable=false
    ```
    
2.  Execute the database scripts. 

    Execute the scripts in the `<IS_HOME>/dbscripts/identity/agent/mysql.sql` file against 
    the created database.    

</details>
            
<details>
<summary>DB2</summary>

1.  Configure the `<IS_HOME>/repository/conf/deployment.toml` file.
    ```
    [datasource.AgentIdentity]
    id = "AgentIdentity"
    url = "jdbc:db2://192.168.108.31:50000/AgentDB"
    username = "db2inst1"
    password = "db2inst1"
    driver = "com.ibm.db2.jcc.DB2Driver"
    jmx_enable=false
    ```
    
2.  Execute the database scripts. 

    Execute the scripts in the `<IS_HOME>/dbscripts/identity/agent/db2.sql` file against 
    the created database.    

</details>


<details>
<summary>MSSQL</summary>

1.  Configure the `<IS_HOME>/repository/conf/deployment.toml` file.
    ```
    [datasource.AgentIdentity]
    id = "AgentIdentity"
    url = "jdbc:sqlserver://localhost:1433;databaseName=AgentDB;SendStringParametersAsUnicode=false"
    username = "sa"
    password = "pass#word2"
    driver = "com.microsoft.sqlserver.jdbc.SQLServerDriver"
    jmx_enable=false
    ```
    
2.  Execute the database scripts. 

    Execute the scripts in the `<IS_HOME>/dbscripts/identity/agent/mssql.sql` file against 
    the created database.

</details>

<details>
<summary>Oracle</summary>

1.  Configure the `<IS_HOME>/repository/conf/deployment.toml` file.
    ```
    [datasource.AgentIdentity]
    id = "AgentIdentity"
    url = "jdbc:oracle:thin:@localhost:1521/AGENTDB"
    username = "IS590Test"
    password = "ora12c"
    driver = "oracle.jdbc.OracleDriver"
    jmx_enable=false
    ```
    
2.  Execute the database scripts. 

    Execute the scripts in the `<IS_HOME>/dbscripts/identity/agent/oracle.sql` file against 
    the created database.    

</details>

---

## Advanced database configurations

Apart from above basic configurations, WSO2 Identity Server supports advanced database 
configurations. Add the following configurations to the `&lt;IS_HOME>/repository/conf/
deployment.toml` file under the corresponding `[[datasource]]` tag.

<Tabs>
<TabItem value="tab-0" label="PostgreSQL">

```json
pool_options.maxActive = "80"
pool_options.maxWait = "60000"
pool_options.minIdle = "5"
pool_options.testOnBorrow = true
pool_options.validationQuery="SELECT 1; COMMIT"
pool_options.validationInterval="30000"
pool_options.defaultAutoCommit=false
```

</TabItem>
<TabItem value="tab-1" label="MySQL">

```json
pool_options.maxActive = "80"
pool_options.maxWait = "60000"
pool_options.minIdle = "5"
pool_options.testOnBorrow = true
pool_options.validationQuery="SELECT 1"
pool_options.validationInterval="30000"
pool_options.defaultAutoCommit=false
```

</TabItem>
<TabItem value="tab-2" label="DB2">

```json
pool_options.maxActive = "80"
pool_options.maxWait = "360000"
pool_options.minIdle = "5"
pool_options.testOnBorrow = true
pool_options.validationQuery="SELECT 1"
pool_options.validationInterval="30000"
pool_options.defaultAutoCommit=false
```

</TabItem>
<TabItem value="tab-3" label="MSSQL">

```json
pool_options.maxActive = "80"
pool_options.maxWait = "60000"
pool_options.minIdle = "5"
pool_options.testOnBorrow = true
pool_options.validationQuery="SELECT 1"
pool_options.validationInterval="30000"
pool_options.defaultAutoCommit=false
```

</TabItem>
<TabItem value="tab-4" label="Oracle">

```json
pool_options.maxActive = "80"
pool_options.maxWait = "60000"
pool_options.minIdle = "5"
pool_options.testOnBorrow = true
pool_options.validationQuery="SELECT 1 FROM DUAL"
pool_options.validationInterval="30000"
pool_options.defaultAutoCommit=false
```

</TabItem>
</Tabs>

<DbConfigTable />

:::note[Sample Config]

If you have correctly configured, the `deployment.toml` file should have an entry 
similar to the following config. 

The following sample configuration is for a separate **PostgreSQL** consent 
management database.

```
[datasource.AgentIdentity]
id = "AgentIdentity"
url = "jdbc:postgresql://localhost:5432/AgentDB"
username = "regadmin"
password = "regadmin"
driver = "org.postgresql.Driver"
jmx_enable=false
pool_options.maxActive = "80"
pool_options.maxWait = "60000"
pool_options.minIdle = "5"
pool_options.testOnBorrow = true
pool_options.validationQuery="SELECT 1"
pool_options.validationInterval="30000"
pool_options.defaultAutoCommit=false
``` 

:::
