---
title: Change the Default Datasource for Agent Identities
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.2.0/docs/deploy/configure/databases/carbon-database/change-datasource-agent-identity.md
---

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

The elements in the above configuration are described below:

<table><tbody><tr className={"even"}><td><strong>{"maxActive"}</strong></td><td>{"This is the maximum number of active connections that can be allocated at the same time from this pool. Enter any negative value to denote an unlimited number of active connections."}</td></tr><tr className={"odd"}><td><strong>{"maxWait"}</strong></td><td>{"This is the maximum number of milliseconds that the pool will wait (when there are no available connections) for a connection to be returned before throwing an exception. You can enter zero or a negative value to wait indefinitely."}</td></tr><tr className={"even"}><td><strong>{"minIdle"}</strong></td><td>{"The minimum number of active connections that can remain idle in the pool without extra ones being created. Enter zero to create none."}</td></tr><tr className={"odd"}><td><p><strong>{"testOnBorrow"}</strong></p></td><td>{"This indicates whether objects will be validated before being borrowed from the pool. If the object fails to be validated, it will be dropped from the pool and another attempt will be made to borrow another."}</td></tr><tr className={"even"}><td><p><strong>{"defaultAutoCommit"}</strong></p></td><td>{"Indicates whether to commit database changes automatically or not"}</td></tr><tr className={"odd"}><td><strong>{"validationInterval"}</strong></td><td>{"This is the indication to avoid excess validation and only run validation after the specified frequency (time in milliseconds). If a connection is due for validation, but has been validated previously within this interval, it will not be validated again."}</td></tr><tr className={"even"}><td><strong>{"defaultAutoCommit"}</strong></td><td><div className={"content-wrapper"}><p>{"This property is "}<strong>{"not"}</strong>{" applicable to the carbon database in WSO2 Identity Server because auto committing is usually handled at the code level, i.e., the default auto commit configuration specified for the RDBMS driver will be effective instead of this property element. Typically, auto committing is enabled for RDBMS drivers by default."}</p><p>{"When auto committing is enabled, each SQL statement will be committed to the database as an individual transaction, as opposed to committing multiple statements as a single transaction."}</p></div></td></tr></tbody></table>

:::info

For more information on other parameters that can be defined in
the `<IS_HOME>/repository/conf/deployment.toml` file, see [Tomcat JDBC Connection Pool](http://tomcat.apache.org/tomcat-9.0-doc/jdbc-pool.html#Tomcat_JDBC_Enhanced_Attributes).

:::

<details>
<summary>Support for case-sensitive usernames</summary>


Usernames in WSO2 Identity Server are case-insensitive by default. If you wish to enable case-sensitive usernames, configure the following properties.

To enable the case-sensitivity for the primary user store, open the `deployment.toml` file found in the `<IS_HOME>/repository/conf/` directory and add the following configurations to the primary user store.

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
The database indexes are created using LOWER() functions to support case-insensitive usernames for the related tables. Therefore, remove the LOWER() functions from the related index creation queries in the scripts at `<IS_HOME>/dbscripts/`.

Eg:

```sql
CREATE UNIQUE INDEX INDEX_UM_USERNAME_UM_TENANT_ID ON UM_USER(LOWER(UM_USER_NAME), UM_TENANT_ID);
```

</details>


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
