---
title: Changing the Default Datasource for Consent Management
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/5.11.0/docs/setup/changing-datasource-consent-management.md
---

# Changing the Default Datasource for Consent Management

WSO2 Identity Server is shipped with an embedded H2 database for storing data. 
These default databases are located in the `<IS_HOME>/repository/database` directory 
of the product pack.

By default Consent Management data is stored in the identity database (IDENTITY_DB) with 
Identity and UMA data. However, you can separate consent specific data into a separate 
data-source to any database type that is supported by WSO2 Identity Server.

:::note

For more information about databases, see 
[Working with Databases](../../setup/working-with-databases) and 
[Setting Up Separate Databases for Clustering](../../setup/setting-up-separate-databases-for-clustering).

:::

Following are the sample configuration for each database type.

<details>
<summary>PostgreSQL</summary>

1. deployment.toml Configurations.
    ```
    [[datasource]]
    id="WSO2CONSENT_DB"
    url = "jdbc:postgresql://localhost:5432/gregdb"
    username = "regadmin"
    password = "regadmin"
    driver = "org.postgresql.Driver"
    jmx_enable=false
    ```

2. Executing database scripts. 

    Navigate to `<IS_HOME>/dbscripts`. Execute the scripts in the following file, against 
    the created database.    
        
      - `<IS_HOME>/dbscripts/consent/postgresql.sql`

</details>
          
<details>
<summary>MySQL</summary>

1. deployment.toml Configurations.
    ```
    [[datasource]]
    id="WSO2CONSENT_DB"
    url = "jdbc:mysql://localhost:3306/IAMtest?useSSL=false"
    username = "root"
    password = "root"
    driver = "com.mysql.jdbc.Driver"
    jmx_enable=false
    ```

2. Executing database scripts. 

    Navigate to `<IS_HOME>/dbscripts`. Execute the scripts in the following file, against 
    the created database.    
        
      - `<IS_HOME>/dbscripts/consent/mysql.sql`

</details>

<details>
<summary>DB2</summary>

1. deployment.toml Configurations.
    ```
    [[datasource]]
    id="WSO2CONSENT_DB"
    url = "jdbc:db2://192.168.108.31:50000/test"
    username = "db2inst1"
    password = "db2inst1"
    driver = "com.ibm.db2.jcc.DB2Driver"
    jmx_enable=false
    ```

2. Executing database scripts. 

    Navigate to `<IS_HOME>/dbscripts`. Execute the scripts in the following file, against 
    the created database.    
        
      - `<IS_HOME>/dbscripts/consent/db2.sql`

</details>

<details>
<summary>MSSQL</summary>

1. deployment.toml Configurations.
    ```
    [[datasource]]
    id="WSO2CONSENT_DB"
    url = "jdbc:sqlserver://localhost:1433;databaseName=test;SendStringParametersAsUnicode=false"
    username = "sa"
    password = "pass#word2"
    driver = "com.microsoft.sqlserver.jdbc.SQLServerDriver"
    jmx_enable=false
    ```

2. Executing database scripts. 

    Navigate to `<IS_HOME>/dbscripts`. Execute the scripts in the following file, against 
    the created database.    
        
      - `<IS_HOME>/dbscripts/consent/mssql.sql`

</details>

<details>
<summary>Oracle</summary>

1. deployment.toml Configurations.
    ```
    [[datasource]]
    id="WSO2CONSENT_DB"
    url = "jdbc:oracle:thin:@localhost:1521/ORCLPDB"
    username = "IS590Test"
    password = "ora12c"
    driver = "oracle.jdbc.OracleDriver"
    jmx_enable=false
    ```

2. Executing database scripts. 

    Navigate to `<IS_HOME>/dbscripts`. Execute the scripts in the following file, against 
    the created database.    
        
      - `<IS_HOME>/dbscripts/consent/oracle.sql`

</details>


**Advanced Database Configurations**

Apart from above basic configurations, WSO2 Identity Server supports advanced database 
configurations. Add the following configurations to the `&lt;IS_HOME>/repository/conf/
deployment.toml` file under the corresponding `[[datasource]]` tag.

```tab
    pool_options.maxActive = "80"
    pool_options.maxWait = "60000"
    pool_options.minIdle = "5"
    pool_options.testOnBorrow = true
    pool_options.validationQuery="SELECT 1; COMMIT"
    pool_options.validationInterval="30000"
    pool_options.defaultAutoCommit=false
```

```tab
    pool_options.maxActive = "80"
    pool_options.maxWait = "60000"
    pool_options.minIdle = "5"
    pool_options.testOnBorrow = true
    pool_options.validationQuery="SELECT 1"
    pool_options.validationInterval="30000"
    pool_options.defaultAutoCommit=false
```

```tab
    pool_options.maxActive = "80"
    pool_options.maxWait = "360000"
    pool_options.minIdle = "5"
    pool_options.testOnBorrow = true
    pool_options.validationQuery="SELECT 1"
    pool_options.validationInterval="30000"
    pool_options.defaultAutoCommit=false
```

```tab
    pool_options.maxActive = "80"
    pool_options.maxWait = "60000"
    pool_options.minIdle = "5"
    pool_options.testOnBorrow = true
    pool_options.validationQuery="SELECT 1"
    pool_options.validationInterval="30000"
    pool_options.defaultAutoCommit=false
```

```tab
    pool_options.maxActive = "80"
    pool_options.maxWait = "60000"
    pool_options.minIdle = "5"
    pool_options.testOnBorrow = true
    pool_options.validationQuery="SELECT 1 FROM DUAL"
    pool_options.validationInterval="30000"
    pool_options.defaultAutoCommit=false
```

The elements in the above configuration are described below.   

<table><tbody><tr className={"even"}><td><strong>{"maxActive"}</strong></td><td>{"The maximum number of active connections that can be allocated at the same time from this pool. Enter any negative value to denote an unlimited number of active connections."}</td></tr><tr className={"odd"}><td><strong>{"maxWait"}</strong></td><td>{"The maximum number of milliseconds that the pool will wait (when there are no available connections) for a connection to be returned before throwing an exception. You can enter zero or a negative value to wait indefinitely."}</td></tr><tr className={"even"}><td><strong>{"minIdle"}</strong></td><td>{"The minimum number of active connections that can remain idle in the pool without extra ones being created, or enter zero to create none."}</td></tr><tr className={"odd"}><td><p><strong>{"testOnBorrow"}</strong></p></td><td>{"Indicates whether objects will be validated before being borrowed from the pool. If the object fails to validate, it will be dropped from the pool, and another attempt will be made to borrow another."}</td></tr><tr className={"even"}><td><p><strong>{"defaultAutoCommit"}</strong></p></td><td>{"Indicates whether to commit database changes automatically or not."}</td></tr><tr className={"odd"}><td><strong>{"validationInterval"}</strong></td><td>{"The indication to avoid excess validation, and only run validation at the most, at this frequency (time in milliseconds). If a connection is due for validation, but has been validated previously within this interval, it will not be validated again."}</td></tr><tr className={"even"}><td><strong>{"defaultAutoCommit"}</strong></td><td><div className={"content-wrapper"}><p>{"This property is "}<strong>{"not"}</strong>{" applicable to the Carbon database in WSO2 products because auto committing is usually handled at the code level, i.e., the default auto commit configuration specified for the RDBMS driver will be effective instead of this property element. Typically, auto committing is enabled for RDBMS drivers by default."}</p><p>{"When auto committing is enabled, each SQL statement will be committed to the database as an individual transaction, as opposed to committing multiple statements as a single transaction."}</p></div></td></tr></tbody></table>
    
:::info

For more information on other parameters that can be defined in
the `<IS_HOME>/repository/conf/deployment.toml` file, see [Tomcat
JDBC Connection
Pool](http://tomcat.apache.org/tomcat-9.0-doc/jdbc-pool.html#Tomcat_JDBC_Enhanced_Attributes).

:::


Once when we separate out consent database from `WSO2IdentityDB`, we need to add the 
following configuration to the `deployment.toml` to specify WSO2 Identity Server to 
use a separate data-source instead of default `IDENTITY_DB`.

```
[authentication.consent]
data_source="jdbc/WSO2CONSENT_DB"
```  

:::note[Sample Config]

If you have correctly configured, the `deployment.toml` file should have an entry 
similar to the following config. 

**NOTE:** The following sample configuration is for a separate **PostgreSQL** consent 
management database.

```
[[datasource]]
id="WSO2CONSENT_DB"
url = "jdbc:postgresql://localhost:5432/gregdb"
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

[authentication.consent]
data_source="jdbc/WSO2CONSENT_DB"
```

:::
