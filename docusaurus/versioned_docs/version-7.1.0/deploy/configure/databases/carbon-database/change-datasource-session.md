---
title: Change the Default Datasource for Session Storage
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.1.0/docs/deploy/configure/databases/carbon-database/change-datasource-session.md
---

# Change the Default Datasource for Session Storage

This document guides you to configure a separate database for storing session related information.

WSO2 Identity Server is shipped with an embedded H2 database for storing data. 
These default databases are located in the `<IS_HOME>/repository/database` directory 
of the pack.

By default, session data is stored in the identity database (IDENTITY_DB) with 
Identity data. However, you can separate session specific data into a separate 
datasource to any database type that is supported by WSO2 Identity Server.

:::note

For more information about databases, see 
[Work with Databases](../index.md) and [Set Up Separate Databases for Clustering](../../../set-up-separate-databases-for-clustering.md).

:::

Following are the sample configuration for each database type.

<details>
<summary>PostgreSQL</summary>


1.  Configure the `<IS_HOME>/repository/conf/deployment.toml` file.
    
    ```
    [datasource.WSO2SessionDB]
    id = "WSO2SessionDB"
    url = "jdbc:postgresql://localhost:5432/sessiondb"
    username = "root"
    password = "root"
    driver = "org.postgresql.Driver"
    jmxEnabled = false
    ```
    
2.  Execute the following scripts against the created database.    

    ```
    DROP TABLE IF EXISTS IDN_AUTH_SESSION_STORE;
    CREATE TABLE IDN_AUTH_SESSION_STORE (
        SESSION_ID VARCHAR(100) NOT NULL,
        SESSION_TYPE VARCHAR(100) NOT NULL,
        OPERATION VARCHAR(10) NOT NULL,
        SESSION_OBJECT BYTEA,
        TIME_CREATED BIGINT,
        TENANT_ID INTEGER DEFAULT -1,
        EXPIRY_TIME BIGINT,
        PRIMARY KEY (SESSION_ID, SESSION_TYPE, TIME_CREATED, OPERATION)
    );

    DROP TABLE IF EXISTS IDN_AUTH_TEMP_SESSION_STORE;
    CREATE TABLE IDN_AUTH_TEMP_SESSION_STORE (
        SESSION_ID VARCHAR(100) NOT NULL,
        SESSION_TYPE VARCHAR(100) NOT NULL,
        OPERATION VARCHAR(10) NOT NULL,
        SESSION_OBJECT BYTEA,
        TIME_CREATED BIGINT,
        TENANT_ID INTEGER DEFAULT -1,
        EXPIRY_TIME BIGINT,
        PRIMARY KEY (SESSION_ID, SESSION_TYPE, TIME_CREATED, OPERATION)
    );

    DROP TABLE IF EXISTS IDN_AUTH_USER_SESSION_MAPPING;
    DROP SEQUENCE IF EXISTS IDN_AUTH_USER_SESSION_MAPPING_PK_SEQ;
    CREATE SEQUENCE IDN_AUTH_USER_SESSION_MAPPING_PK_SEQ;
    CREATE TABLE IDN_AUTH_USER_SESSION_MAPPING (
        ID INTEGER DEFAULT NEXTVAL('IDN_AUTH_USER_SESSION_MAPPING_PK_SEQ'),
        USER_ID VARCHAR(255) NOT NULL,
        SESSION_ID VARCHAR(255) NOT NULL,
        CONSTRAINT USER_SESSION_STORE_CONSTRAINT UNIQUE (USER_ID, SESSION_ID),
        PRIMARY KEY (ID)
    );

    DROP TABLE IF EXISTS IDN_AUTH_SESSION_APP_INFO;
    CREATE TABLE IDN_AUTH_SESSION_APP_INFO (
        SESSION_ID VARCHAR (100) NOT NULL,
        SUBJECT VARCHAR (100) NOT NULL,
        APP_ID INTEGER NOT NULL,
        INBOUND_AUTH_TYPE VARCHAR (255) NOT NULL,
        PRIMARY KEY (SESSION_ID, SUBJECT, APP_ID, INBOUND_AUTH_TYPE)
    );

    DROP TABLE IF EXISTS IDN_AUTH_SESSION_META_DATA;
    CREATE TABLE IDN_AUTH_SESSION_META_DATA (
        SESSION_ID VARCHAR (100) NOT NULL,
        PROPERTY_TYPE VARCHAR (100) NOT NULL,
        VALUE VARCHAR (255) NOT NULL,
        PRIMARY KEY (SESSION_ID, PROPERTY_TYPE, VALUE)
    );

    DROP TABLE IF EXISTS IDN_AUTH_USER;
    CREATE TABLE IDN_AUTH_USER (
        USER_ID VARCHAR(255) NOT NULL,
        USER_NAME VARCHAR(255) NOT NULL,
        TENANT_ID INTEGER NOT NULL,
        DOMAIN_NAME VARCHAR(255) NOT NULL,
        IDP_ID INTEGER NOT NULL,
        PRIMARY KEY (USER_ID),
        CONSTRAINT USER_STORE_CONSTRAINT UNIQUE (USER_NAME, TENANT_ID, DOMAIN_NAME, IDP_ID)
    );

    DROP TABLE IF EXISTS IDN_AUTH_WAIT_STATUS;
    DROP SEQUENCE IF EXISTS IDN_AUTH_WAIT_STATUS_SEQ;
    CREATE SEQUENCE IDN_AUTH_WAIT_STATUS_SEQ;
    CREATE TABLE IDN_AUTH_WAIT_STATUS (
        ID              INTEGER       NOT NULL DEFAULT NEXTVAL('IDN_AUTH_WAIT_STATUS_SEQ'),
        TENANT_ID       INTEGER       NOT NULL,
        LONG_WAIT_KEY   VARCHAR(255)  NOT NULL,
        WAIT_STATUS     CHAR(1) NOT NULL DEFAULT '1',
        TIME_CREATED    TIMESTAMP,
        EXPIRE_TIME     TIMESTAMP,
        PRIMARY KEY (ID),
        CONSTRAINT IDN_AUTH_WAIT_STATUS_KEY UNIQUE (LONG_WAIT_KEY)
    );

    -- IDN_AUTH_SESSION_STORE --
    CREATE INDEX IDX_IDN_AUTH_SESSION_TIME ON IDN_AUTH_SESSION_STORE (TIME_CREATED);
    CREATE INDEX IDX_IDN_AUTH_SSTR_ST_OP_ID_TM ON IDN_AUTH_SESSION_STORE (OPERATION, SESSION_TYPE, SESSION_ID, TIME_CREATED);
    CREATE INDEX IDX_IDN_AUTH_SSTR_ET_ID ON IDN_AUTH_SESSION_STORE (EXPIRY_TIME, SESSION_ID);
    
    -- IDN_AUTH_TEMP_SESSION_STORE --
    CREATE INDEX IDX_IDN_AUTH_TMP_SESSION_TIME ON IDN_AUTH_TEMP_SESSION_STORE (TIME_CREATED);
    
    -- IDN_AUTH_USER --
    CREATE INDEX IDX_AUTH_USER_UN_TID_DN ON IDN_AUTH_USER (LOWER(USER_NAME), TENANT_ID, DOMAIN_NAME);
    CREATE INDEX IDX_AUTH_USER_DN_TOD ON IDN_AUTH_USER (DOMAIN_NAME, TENANT_ID);

    -- IDN_AUTH_USER_SESSION_MAPPING --
    CREATE INDEX IDX_USER_ID ON IDN_AUTH_USER_SESSION_MAPPING (USER_ID);
    CREATE INDEX IDX_SESSION_ID ON IDN_AUTH_USER_SESSION_MAPPING (SESSION_ID);

    -- IDN_AUTH_SESSION_APP_INFO --
    CREATE INDEX IDX_AUTH_SAI_UN_AID_SID ON IDN_AUTH_SESSION_APP_INFO (APP_ID, LOWER(SUBJECT), SESSION_ID);
    ```

</details>
          
<details>
<summary>MySQL</summary>


1.  Configure the `<IS_HOME>/repository/conf/deployment.toml` file.
    
    ```
    [datasource.WSO2SessionDB]
    id = "WSO2SessionDB"
    url = "jdbc:mysql://localhost:3306/sessiondb?useSSL=false"
    username = "root"
    password = "root"
    driver = "com.mysql.cj.jdbc.Driver"
    jmxEnabled = false
    ```
    
2.  Execute the following scripts against the created database.    

    ```
    CREATE TABLE IF NOT EXISTS IDN_AUTH_SESSION_STORE (
        SESSION_ID VARCHAR (100) NOT NULL,
        SESSION_TYPE VARCHAR(100) NOT NULL,
        OPERATION VARCHAR(10) NOT NULL,
        SESSION_OBJECT BLOB,
        TIME_CREATED BIGINT,
        TENANT_ID INTEGER DEFAULT -1,
        EXPIRY_TIME BIGINT,
        PRIMARY KEY (SESSION_ID, SESSION_TYPE, TIME_CREATED, OPERATION)
    )DEFAULT CHARACTER SET latin1 ENGINE INNODB;

    CREATE TABLE IF NOT EXISTS IDN_AUTH_TEMP_SESSION_STORE (
        SESSION_ID VARCHAR (100) NOT NULL,
        SESSION_TYPE VARCHAR(100) NOT NULL,
        OPERATION VARCHAR(10) NOT NULL,
        SESSION_OBJECT BLOB,
        TIME_CREATED BIGINT,
        TENANT_ID INTEGER DEFAULT -1,
        EXPIRY_TIME BIGINT,
        PRIMARY KEY (SESSION_ID, SESSION_TYPE, TIME_CREATED, OPERATION)
    )DEFAULT CHARACTER SET latin1 ENGINE INNODB;

    CREATE TABLE IF NOT EXISTS IDN_AUTH_USER_SESSION_MAPPING (
        ID INTEGER NOT NULL AUTO_INCREMENT,
        USER_ID VARCHAR(255) NOT NULL,
        SESSION_ID VARCHAR(255) NOT NULL,
        CONSTRAINT USER_SESSION_STORE_CONSTRAINT UNIQUE (USER_ID, SESSION_ID),
        PRIMARY KEY (ID))DEFAULT CHARACTER SET latin1;

    CREATE TABLE IF NOT EXISTS IDN_AUTH_SESSION_APP_INFO (
        SESSION_ID VARCHAR (100) NOT NULL,
        SUBJECT VARCHAR (100) NOT NULL,
        APP_ID INTEGER NOT NULL,
        INBOUND_AUTH_TYPE VARCHAR (255) NOT NULL,
        PRIMARY KEY (SESSION_ID, SUBJECT, APP_ID, INBOUND_AUTH_TYPE)
    )DEFAULT CHARACTER SET latin1 ENGINE INNODB;
    
    CREATE TABLE IF NOT EXISTS IDN_AUTH_SESSION_META_DATA (
        SESSION_ID VARCHAR (100) NOT NULL,
        PROPERTY_TYPE VARCHAR (100) NOT NULL,
        VALUE VARCHAR (255) NOT NULL,
        PRIMARY KEY (SESSION_ID, PROPERTY_TYPE, VALUE)
    )DEFAULT CHARACTER SET latin1 ENGINE INNODB;
    
    CREATE TABLE IF NOT EXISTS IDN_AUTH_USER (
        USER_ID VARCHAR(255) NOT NULL,
        USER_NAME VARCHAR(255) NOT NULL,
        TENANT_ID INTEGER NOT NULL,
        DOMAIN_NAME VARCHAR(255) NOT NULL,
        IDP_ID INTEGER NOT NULL,
        PRIMARY KEY (USER_ID),
        CONSTRAINT USER_STORE_CONSTRAINT UNIQUE (USER_NAME, TENANT_ID, DOMAIN_NAME, IDP_ID)
    )DEFAULT CHARACTER SET latin1;
    
    CREATE TABLE IF NOT EXISTS IDN_AUTH_WAIT_STATUS (
        ID              INTEGER AUTO_INCREMENT NOT NULL,
        TENANT_ID       INTEGER                NOT NULL,
        LONG_WAIT_KEY   VARCHAR(255)           NOT NULL,
        WAIT_STATUS     CHAR(1) NOT NULL DEFAULT '1',
        TIME_CREATED    TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
        EXPIRE_TIME     TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
        PRIMARY KEY (ID),
        CONSTRAINT IDN_AUTH_WAIT_STATUS_KEY UNIQUE (LONG_WAIT_KEY)
    )DEFAULT CHARACTER SET latin1 ;

    -- IDN_AUTH_SESSION_STORE --
    CREATE INDEX IDX_IDN_AUTH_SESSION_TIME ON IDN_AUTH_SESSION_STORE (TIME_CREATED);
    CREATE INDEX IDX_IDN_AUTH_SSTR_ST_OP_ID_TM ON IDN_AUTH_SESSION_STORE (OPERATION, SESSION_TYPE, SESSION_ID, TIME_CREATED);
    CREATE INDEX IDX_IDN_AUTH_SSTR_ET_ID ON IDN_AUTH_SESSION_STORE (EXPIRY_TIME, SESSION_ID);
    
    -- IDN_AUTH_TEMP_SESSION_STORE --
    CREATE INDEX IDX_IDN_AUTH_TMP_SESSION_TIME ON IDN_AUTH_TEMP_SESSION_STORE (TIME_CREATED);

    -- IDN_AUTH_USER --
    CREATE INDEX IDX_AUTH_USER_UN_TID_DN ON IDN_AUTH_USER (USER_NAME, TENANT_ID, DOMAIN_NAME);
    CREATE INDEX IDX_AUTH_USER_DN_TOD ON IDN_AUTH_USER (DOMAIN_NAME, TENANT_ID);
    
    -- IDN_AUTH_USER_SESSION_MAPPING --
    CREATE INDEX IDX_USER_ID ON IDN_AUTH_USER_SESSION_MAPPING (USER_ID);
    CREATE INDEX IDX_SESSION_ID ON IDN_AUTH_USER_SESSION_MAPPING (SESSION_ID);
    
    -- IDN_AUTH_SESSION_APP_INFO --
    CREATE INDEX IDX_AUTH_SAI_UN_AID_SID ON IDN_AUTH_SESSION_APP_INFO (APP_ID, SUBJECT, SESSION_ID);
    ```

</details>
            
<details>
<summary>DB2</summary>

1.  Configure the `<IS_HOME>/repository/conf/deployment.toml` file.
    ```
    [datasource.WSO2SessionDB]
    id = "WSO2SessionDB"
    url = "jdbc:db2://localhost:50000/sessiondb"
    username = "db2inst1"
    password = "db2inst1"
    driver = "com.ibm.db2.jcc.DB2Driver"
    jmxEnabled = false
    ```

2.  Execute the following scripts against the created database.    

    ```
    CREATE TABLE IDN_AUTH_SESSION_STORE (
        SESSION_ID VARCHAR (100) NOT NULL,
        SESSION_TYPE VARCHAR(100) NOT NULL,
        OPERATION VARCHAR(10) NOT NULL,
        SESSION_OBJECT BLOB,
        TIME_CREATED BIGINT NOT NULL,
        TENANT_ID INTEGER DEFAULT -1,
        EXPIRY_TIME BIGINT NOT NULL,
        PRIMARY KEY (SESSION_ID, SESSION_TYPE, TIME_CREATED, OPERATION)
    )
    /

    CREATE TABLE IDN_AUTH_TEMP_SESSION_STORE (
        SESSION_ID VARCHAR (100) NOT NULL,
        SESSION_TYPE VARCHAR(100) NOT NULL,
        OPERATION VARCHAR(10) NOT NULL,
        SESSION_OBJECT BLOB,
        TIME_CREATED BIGINT NOT NULL,
        TENANT_ID INTEGER DEFAULT -1,
        EXPIRY_TIME BIGINT NOT NULL,
        PRIMARY KEY (SESSION_ID, SESSION_TYPE, TIME_CREATED, OPERATION)
    )
    /

    CREATE TABLE IDN_AUTH_USER_SESSION_MAPPING (
        ID INTEGER NOT NULL GENERATED ALWAYS AS IDENTITY (START WITH 1 INCREMENT BY 1),
        USER_ID VARCHAR(255) NOT NULL,
        SESSION_ID VARCHAR(255) NOT NULL,
        CONSTRAINT USER_SESSION_STORE_CONSTRAINT UNIQUE (USER_ID, SESSION_ID),
        PRIMARY KEY (ID)
    )
    /

    CREATE TABLE IDN_AUTH_SESSION_APP_INFO (
        SESSION_ID VARCHAR (100) NOT NULL,
        SUBJECT VARCHAR (100) NOT NULL,
        APP_ID INTEGER NOT NULL,
        INBOUND_AUTH_TYPE VARCHAR (255) NOT NULL,
        PRIMARY KEY (SESSION_ID, SUBJECT, APP_ID, INBOUND_AUTH_TYPE)
    )
    /

    CREATE TABLE IDN_AUTH_SESSION_META_DATA (
        SESSION_ID VARCHAR (100) NOT NULL,
        PROPERTY_TYPE VARCHAR (100) NOT NULL,
        VALUE VARCHAR (255) NOT NULL,
        PRIMARY KEY (SESSION_ID, PROPERTY_TYPE, VALUE)
    )
    /

    CREATE TABLE IDN_AUTH_USER (
        USER_ID VARCHAR(255) NOT NULL,
        USER_NAME VARCHAR(255) NOT NULL,
        TENANT_ID INTEGER NOT NULL,
        DOMAIN_NAME VARCHAR(255) NOT NULL,
        IDP_ID INTEGER NOT NULL,
        PRIMARY KEY (USER_ID),
        CONSTRAINT USER_STORE_CONSTRAINT UNIQUE (USER_NAME, TENANT_ID, DOMAIN_NAME, IDP_ID)
    )
    /

    CREATE TABLE IDN_AUTH_WAIT_STATUS (
        ID              INTEGER                NOT NULL,
        TENANT_ID       INTEGER                NOT NULL,
        LONG_WAIT_KEY   VARCHAR(255)           NOT NULL,
        WAIT_STATUS     CHAR(1) NOT NULL DEFAULT '1',
        TIME_CREATED    TIMESTAMP,
        EXPIRE_TIME     TIMESTAMP,
        PRIMARY KEY (ID),
        CONSTRAINT IDN_AUTH_WAIT_STATUS_KEY UNIQUE (LONG_WAIT_KEY))
    /
    CREATE SEQUENCE IDN_AUTH_WAIT_STATUS_SEQ START WITH 1 INCREMENT BY 1 NOCACHE
    /
    CREATE TRIGGER IDN_AUTH_WAIT_STATUS_TRIG NO CASCADE
        BEFORE INSERT
            ON IDN_AUTH_WAIT_STATUS
        REFERENCING NEW AS NEW
        FOR EACH ROW MODE DB2SQL
        BEGIN ATOMIC
            SET (NEW.ID) = (NEXTVAL FOR IDN_AUTH_WAIT_STATUS_SEQ);
        END
    /

    -- IDN_AUTH_SESSION_STORE --
    CREATE INDEX IDX_IDN_AUTH_SESSION_TIME ON IDN_AUTH_SESSION_STORE (TIME_CREATED)
    /
    CREATE INDEX IDX_IDN_AUTH_SSTR_ST_OP_ID_TM ON IDN_AUTH_SESSION_STORE (OPERATION, SESSION_TYPE, SESSION_ID, TIME_CREATED)
    /
    CREATE INDEX IDX_IDN_AUTH_SSTR_ET_ID ON IDN_AUTH_SESSION_STORE (EXPIRY_TIME, SESSION_ID)
    /
    
    -- IDN_AUTH_TEMP_SESSION_STORE --
    CREATE INDEX IDX_IDN_AUTH_TMP_SESSION_TIME ON IDN_AUTH_TEMP_SESSION_STORE (TIME_CREATED)
    /

    -- IDN_AUTH_USER --
    CREATE INDEX IDX_AUTH_USER_UN_TID_DN ON IDN_AUTH_USER (LOWER(USER_NAME), TENANT_ID, DOMAIN_NAME)
    /
    CREATE INDEX IDX_AUTH_USER_DN_TOD ON IDN_AUTH_USER (DOMAIN_NAME, TENANT_ID)
    /
    
    -- IDN_AUTH_USER_SESSION_MAPPING --
    CREATE INDEX IDX_USER_ID ON IDN_AUTH_USER_SESSION_MAPPING (USER_ID)
    /
    CREATE INDEX IDX_SESSION_ID ON IDN_AUTH_USER_SESSION_MAPPING (SESSION_ID)
    /
    
    -- IDN_AUTH_SESSION_APP_INFO --
    CREATE INDEX IDX_AUTH_SAI_UN_AID_SID ON IDN_AUTH_SESSION_APP_INFO (APP_ID, LOWER(SUBJECT), SESSION_ID)
    /
    ```   

</details>


<details>
<summary>MSSQL</summary>

1.  Configure the `<IS_HOME>/repository/conf/deployment.toml` file.
    ```
    [datasource.WSO2SessionDB]
    id = "WSO2SessionDB"
    url = "jdbc:sqlserver://localhost:1433;databaseName=sessiondb;SendStringParametersAsUnicode=false"
    username = "sa"
    password = "password"
    driver = "com.microsoft.sqlserver.jdbc.SQLServerDriver"
    jmxEnabled = false
    ```

2.  Execute the following scripts against the created database.    

    ```
    IF NOT  EXISTS (SELECT * FROM SYS.OBJECTS WHERE OBJECT_ID = OBJECT_ID(N'[DBO].[IDN_AUTH_SESSION_STORE]') AND TYPE IN (N'U'))
    CREATE TABLE IDN_AUTH_SESSION_STORE (
        SESSION_ID VARCHAR (100) NOT NULL,
        SESSION_TYPE VARCHAR(100) NOT NULL,
        OPERATION VARCHAR(10) NOT NULL,
        SESSION_OBJECT VARBINARY(MAX),
        TIME_CREATED BIGINT,
        TENANT_ID INTEGER DEFAULT -1,
        EXPIRY_TIME BIGINT,
        PRIMARY KEY (SESSION_ID, SESSION_TYPE, TIME_CREATED, OPERATION)
    );

    IF NOT  EXISTS (SELECT * FROM SYS.OBJECTS WHERE OBJECT_ID = OBJECT_ID(N'[DBO].[IDN_AUTH_TEMP_SESSION_STORE]') AND TYPE IN (N'U'))
    CREATE TABLE IDN_AUTH_TEMP_SESSION_STORE (
        SESSION_ID VARCHAR (100) NOT NULL,
        SESSION_TYPE VARCHAR(100) NOT NULL,
        OPERATION VARCHAR(10) NOT NULL,
        SESSION_OBJECT VARBINARY(MAX),
        TIME_CREATED BIGINT,
        TENANT_ID INTEGER DEFAULT -1,
        EXPIRY_TIME BIGINT,
        PRIMARY KEY (SESSION_ID, SESSION_TYPE, TIME_CREATED, OPERATION)
    );

    IF NOT  EXISTS (SELECT * FROM SYS.OBJECTS WHERE OBJECT_ID = OBJECT_ID(N'[DBO].[IDN_AUTH_USER_SESSION_MAPPING]') AND TYPE IN (N'U'))
    CREATE TABLE IDN_AUTH_USER_SESSION_MAPPING (
        ID INTEGER NOT NULL IDENTITY,
        USER_ID VARCHAR(255) NOT NULL,
        SESSION_ID VARCHAR(255) NOT NULL,
        CONSTRAINT USER_SESSION_STORE_CONSTRAINT UNIQUE (USER_ID, SESSION_ID),
        PRIMARY KEY (ID)
    );

    IF NOT EXISTS (SELECT * FROM SYS.OBJECTS WHERE OBJECT_ID = OBJECT_ID(N'[DBO].[IDN_AUTH_SESSION_APP_INFO]') AND TYPE IN (N'U'))
    CREATE TABLE IDN_AUTH_SESSION_APP_INFO (
        SESSION_ID VARCHAR (100) NOT NULL,
        SUBJECT VARCHAR (100) NOT NULL,
        APP_ID INTEGER NOT NULL,
        INBOUND_AUTH_TYPE VARCHAR (255) NOT NULL,
        PRIMARY KEY (SESSION_ID, SUBJECT, APP_ID, INBOUND_AUTH_TYPE)
    );

    IF NOT EXISTS (SELECT * FROM SYS.OBJECTS WHERE OBJECT_ID = OBJECT_ID(N'[DBO].[IDN_AUTH_SESSION_META_DATA]') AND TYPE IN (N'U'))
    CREATE TABLE IDN_AUTH_SESSION_META_DATA (
        SESSION_ID VARCHAR (100) NOT NULL,
        PROPERTY_TYPE VARCHAR (100) NOT NULL,
        VALUE VARCHAR (255) NOT NULL,
        PRIMARY KEY (SESSION_ID, PROPERTY_TYPE, VALUE)
    );

    IF NOT  EXISTS (SELECT * FROM SYS.OBJECTS WHERE OBJECT_ID = OBJECT_ID(N'[DBO].[IDN_AUTH_USER]') AND TYPE IN (N'U'))
    CREATE TABLE IDN_AUTH_USER (
        USER_ID VARCHAR(255) NOT NULL,
        USER_NAME VARCHAR(255) NOT NULL,
        TENANT_ID INTEGER NOT NULL,
        DOMAIN_NAME VARCHAR(255) NOT NULL,
        IDP_ID INTEGER NOT NULL,
        PRIMARY KEY (USER_ID),
        CONSTRAINT USER_STORE_CONSTRAINT UNIQUE (USER_NAME, TENANT_ID, DOMAIN_NAME, IDP_ID)
    );

    IF NOT EXISTS(SELECT * FROM SYS.OBJECTS WHERE OBJECT_ID = OBJECT_ID(N'[DBO].[IDN_AUTH_WAIT_STATUS]') AND TYPE IN (N'U'))
    CREATE TABLE IDN_AUTH_WAIT_STATUS (
        ID              INTEGER IDENTITY       NOT NULL,
        TENANT_ID       INTEGER                NOT NULL,
        LONG_WAIT_KEY   VARCHAR(255)           NOT NULL,
        WAIT_STATUS     CHAR(1) NOT NULL DEFAULT '1',
        TIME_CREATED    DATETIME,
        EXPIRE_TIME     DATETIME,
        PRIMARY KEY (ID),
        CONSTRAINT IDN_AUTH_WAIT_STATUS_KEY UNIQUE (LONG_WAIT_KEY)
    );

    -- IDN_AUTH_SESSION_STORE --
    CREATE INDEX IDX_IDN_AUTH_SESSION_TIME ON IDN_AUTH_SESSION_STORE (TIME_CREATED);
    CREATE INDEX IDX_IDN_AUTH_SSTR_ST_OP_ID_TM ON IDN_AUTH_SESSION_STORE (OPERATION, SESSION_TYPE, SESSION_ID, TIME_CREATED);
    CREATE INDEX IDX_IDN_AUTH_SSTR_ET_ID ON IDN_AUTH_SESSION_STORE (EXPIRY_TIME, SESSION_ID);
    
    -- IDN_AUTH_TEMP_SESSION_STORE --
    CREATE INDEX IDX_IDN_AUTH_TMP_SESSION_TIME ON IDN_AUTH_TEMP_SESSION_STORE (TIME_CREATED);

    -- IDN_AUTH_USER --
    CREATE INDEX IDX_AUTH_USER_UN_TID_DN ON IDN_AUTH_USER (USER_NAME, TENANT_ID, DOMAIN_NAME);
    CREATE INDEX IDX_AUTH_USER_DN_TOD ON IDN_AUTH_USER (DOMAIN_NAME, TENANT_ID);
    
    -- IDN_AUTH_USER_SESSION_MAPPING --
    CREATE INDEX IDX_USER_ID ON IDN_AUTH_USER_SESSION_MAPPING (USER_ID);
    CREATE INDEX IDX_SESSION_ID ON IDN_AUTH_USER_SESSION_MAPPING (SESSION_ID);

    -- IDN_AUTH_SESSION_APP_INFO --
    CREATE INDEX IDX_AUTH_SAI_UN_AID_SID ON IDN_AUTH_SESSION_APP_INFO (APP_ID, SUBJECT, SESSION_ID);
    ```   

</details>

<details>
<summary>Oracle</summary>

1.  Configure the `<IS_HOME>/repository/conf/deployment.toml` file.
    ```
    [datasource.WSO2SessionDB]
    id = "WSO2SessionDB"
    url = "jdbc:oracle:thin:@localhost:1521/ORCLPDB"
    username = "user"
    password = "password"
    driver = "oracle.jdbc.OracleDriver"
    jmxEnabled = false
    ```

2.  Execute the following scripts against the created database.    

    ```
    CREATE TABLE IDN_AUTH_SESSION_STORE (
        SESSION_ID VARCHAR (100) NOT NULL,
        SESSION_TYPE VARCHAR(100) NOT NULL,
        OPERATION VARCHAR(10) NOT NULL,
        SESSION_OBJECT BLOB,
        TIME_CREATED NUMBER(19),
        TENANT_ID INTEGER DEFAULT -1,
        EXPIRY_TIME NUMBER(19),
        PRIMARY KEY (SESSION_ID, SESSION_TYPE, TIME_CREATED, OPERATION)
    )
    /

    CREATE TABLE IDN_AUTH_TEMP_SESSION_STORE (
        SESSION_ID VARCHAR (100) NOT NULL,
        SESSION_TYPE VARCHAR(100) NOT NULL,
        OPERATION VARCHAR(10) NOT NULL,
        SESSION_OBJECT BLOB,
        TIME_CREATED NUMBER(19),
        TENANT_ID INTEGER DEFAULT -1,
        EXPIRY_TIME NUMBER(19),
        PRIMARY KEY (SESSION_ID, SESSION_TYPE, TIME_CREATED, OPERATION)
    )
    /

    CREATE TABLE IDN_AUTH_USER_SESSION_MAPPING (
        ID INTEGER,
        USER_ID VARCHAR(255) NOT NULL,
        SESSION_ID VARCHAR(255) NOT NULL,
        CONSTRAINT USER_SESSION_STORE_CONSTRAINT UNIQUE (USER_ID, SESSION_ID),
        PRIMARY KEY(ID)
    )
    /
    CREATE SEQUENCE IDN_AUTH_USER_SESSION_MAP_SEQ START WITH 1 INCREMENT BY 1 NOCACHE
    /
    CREATE OR REPLACE TRIGGER IDN_AUTH_USER_SESSION_MAP_TRIG
        BEFORE INSERT
            ON IDN_AUTH_USER_SESSION_MAPPING
        REFERENCING NEW AS NEW
        FOR EACH ROW
        BEGIN
            SELECT IDN_AUTH_USER_SESSION_MAP_SEQ.nextval INTO :NEW.ID FROM dual;
        END;
    /

    CREATE TABLE IDN_AUTH_SESSION_APP_INFO (
        SESSION_ID VARCHAR (100) NOT NULL,
        SUBJECT VARCHAR (100) NOT NULL,
        APP_ID INTEGER NOT NULL,
        INBOUND_AUTH_TYPE VARCHAR (255) NOT NULL,
        PRIMARY KEY (SESSION_ID, SUBJECT, APP_ID, INBOUND_AUTH_TYPE)
    )
    /

    CREATE TABLE IDN_AUTH_SESSION_META_DATA (
        SESSION_ID VARCHAR (100) NOT NULL,
        PROPERTY_TYPE VARCHAR (100) NOT NULL,
        VALUE VARCHAR (255) NOT NULL,
        PRIMARY KEY (SESSION_ID, PROPERTY_TYPE, VALUE)
    )
    /

    CREATE TABLE IDN_AUTH_USER (
        USER_ID VARCHAR(255) NOT NULL,
        USER_NAME VARCHAR(255) NOT NULL,
        TENANT_ID INTEGER NOT NULL,
        DOMAIN_NAME VARCHAR(255) NOT NULL,
        IDP_ID INTEGER NOT NULL,
        PRIMARY KEY (USER_ID),
        CONSTRAINT USER_STORE_CONSTRAINT UNIQUE (USER_NAME, TENANT_ID, DOMAIN_NAME, IDP_ID)
    )
    /

    CREATE TABLE IDN_AUTH_WAIT_STATUS (
        ID              INTEGER       NOT NULL,
        TENANT_ID       INTEGER       NOT NULL,
        LONG_WAIT_KEY   VARCHAR(255)  NOT NULL,
        WAIT_STATUS     CHAR(1)       DEFAULT '1',
        TIME_CREATED    TIMESTAMP,
        EXPIRE_TIME     TIMESTAMP,
        PRIMARY KEY (ID),
        CONSTRAINT IDN_AUTH_WAIT_STATUS_KEY UNIQUE (LONG_WAIT_KEY)
    )   
    /
    CREATE SEQUENCE IDN_AUTH_WAIT_STATUS_SEQ START WITH 1 INCREMENT BY 1 NOCACHE
    /
    CREATE OR REPLACE TRIGGER IDN_AUTH_WAIT_STATUS_TRIG
        BEFORE INSERT
            ON IDN_AUTH_WAIT_STATUS
        REFERENCING NEW AS NEW
        FOR EACH ROW
        BEGIN
            SELECT IDN_AUTH_WAIT_STATUS_SEQ.nextval
            INTO :NEW.ID
            FROM dual;
        END;
    /

    -- IDN_AUTH_SESSION_STORE --
    CREATE INDEX IDX_IDN_AUTH_SESSION_TIME ON IDN_AUTH_SESSION_STORE (TIME_CREATED)
    /
    CREATE INDEX IDX_IDN_AUTH_SSTR_ST_OP_ID_TM ON IDN_AUTH_SESSION_STORE (OPERATION, SESSION_TYPE, SESSION_ID, TIME_CREATED)
    /
    CREATE INDEX IDX_IDN_AUTH_SSTR_ET_ID ON IDN_AUTH_SESSION_STORE (EXPIRY_TIME, SESSION_ID)
    /
    
    -- IDN_AUTH_TEMP_SESSION_STORE --
    CREATE INDEX IDX_IDN_AUTH_TMP_SESSION_TIME ON IDN_AUTH_TEMP_SESSION_STORE (TIME_CREATED)
    /

    -- IDN_AUTH_USER --
    CREATE INDEX IDX_AUTH_USER_UN_TID_DN ON IDN_AUTH_USER (LOWER(USER_NAME), TENANT_ID, DOMAIN_NAME)
    /
    CREATE INDEX IDX_AUTH_USER_DN_TOD ON IDN_AUTH_USER (DOMAIN_NAME, TENANT_ID)
    /
    
    -- IDN_AUTH_USER_SESSION_MAPPING --
    CREATE INDEX IDX_USER_ID ON IDN_AUTH_USER_SESSION_MAPPING (USER_ID)
    /
    CREATE INDEX IDX_SESSION_ID ON IDN_AUTH_USER_SESSION_MAPPING (SESSION_ID)
    /
    
    -- IDN_AUTH_SESSION_APP_INFO --
    CREATE INDEX IDX_AUTH_SAI_UN_AID_SID ON IDN_AUTH_SESSION_APP_INFO (APP_ID, LOWER(SUBJECT), SESSION_ID)
    /
    ``` 

</details>

---

## Advanced database configurations

Apart from above basic configurations, WSO2 Identity Server supports advanced database 
configurations. Add the following configurations to the `&lt;IS_HOME>/repository/conf/
deployment.toml` file under the `[datasource.WSO2SessionDB.pool_options]` tag.

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


Once when we separate out the session database from `WSO2IdentityDB`, we need to add the 
following configuration to the `deployment.toml` file to specify WSO2 Identity Server to 
use a separate datasource instead of the default `IDENTITY_DB`.

```
[session]
data_source="jdbc/WSO2SessionDB"
```  

:::note[Sample Config]

If you have correctly configured, the `deployment.toml` file should have an entry 
similar to the following config. 

The following sample configuration is for a separate **PostgreSQL** consent 
management database.

```
[datasource.WSO2SessionDB]
id = "WSO2SessionDB"
url = "jdbc:postgresql://localhost:5432/sessiondb"
username = "root"
password = "root"
driver = "org.postgresql.Driver"
jmxEnabled = false

[datasource.WSO2SessionDB.pool_options]
validationQuery="SELECT 1; COMMIT"
testOnBorrow = true
maxActive=200
maxWait = 60000
minIdle = 5
validationInterval="30000"
defaultAutoCommit=false

[session]
data_source="jdbc/WSO2SessionDB"
``` 

:::
