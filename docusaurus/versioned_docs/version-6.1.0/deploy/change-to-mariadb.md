---
title: Change to MariaDB
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.1.0/docs/deploy/change-to-mariadb.md
---

# Change to MariaDB

By default, WSO2 Identity Server uses the embedded H2 database as the database for storing user management and registry data. Follow the same steps and use the same database scripts, drivers, and configurations given in the documentation: [Changing to MySQL](change-to-mysql.md) in order to use MariaDB instead of the embedded H2 database.

---

## Datasource configurations

A datasource is used to establish the connection to a database. By
default, `WSO2_IDENTITY_DB` and `WSO2_SHARED_DB` datasources are used to connect
to the default H2 database. 

- `WSO2_SHARED_DB` - The datasource which stores registry and user management
                     data.
- `WSO2_IDENTITY_DB` - The datasource specific to the identity server which stores
                       identity related data.

After setting up the MariaDB database, you can point `WSO2_IDENTITY_DB` or `WSO2_SHARED_DB` or both to the MariaDB database by following the instructions given below.

---

## Change the default datasource

Add the following configurations to change to MariaDB in the `<IS_HOME>/repository/conf/deployment.toml` file. A sample configuration is given below.

```toml
[user_store]
type = "database_unique_id"

[database.identity_db]
type = "mariadb"
url = "jdbc:mariadb://localhost:3306/WSO2IS_IDENTITY_DB"
username = "root"
password = "mypass"

[database.identity_db.pool_options]
maxActive = "80"
minIdle ="5"
testOnBorrow = true
validationQuery="SELECT 1"
validationInterval="30000"
defaultAutoCommit=false
commitOnReturn=true

[database.shared_db]
type = "mariadb"
url = "jdbc:mariadb://localhost:3306/WSO2IS_SHARED_DB"
username = "root"
password = "mypass"

[database.shared_db.pool_options]
maxActive = "80"
minIdle ="5"
testOnBorrow = true
validationQuery="SELECT 1"
validationInterval="30000"
defaultAutoCommit=false
commitOnReturn=true
```
