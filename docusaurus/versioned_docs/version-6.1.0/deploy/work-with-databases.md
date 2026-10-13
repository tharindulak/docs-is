---
title: Working with Databases
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.1.0/docs/deploy/work-with-databases.md
---

# Working with Databases

WSO2 Identity Server is shipped with an embedded H2 database for storing
data. These default databases are located in the
`         <IS_HOME>/repository/database        ` directory of the
product pack.

---

## Default databases

Explained below are the default databases that you will find in the
`         database        ` directory.

-   **Identity database** :The database, `WSO2IDENTITY_DB.mv.db` consists of identity 
    related data.
-   **Shared database** :The database, `WSO2SHARED_DB.mv.db` contains the registry and
    user management data.
-   **Carbon database:** The database, `          WSO2CARBON_DB.mv.db         ` has the 
    internal data related to the product. This data is stored in the embedded H2 database.
-   **Workflow database:** The database, `          jpadb.mv.db         ` contains workflow related data. 

Following image shows the default databases and the data that are stored in each database.
<div>
    &lt;center>
        <img src="/identity/assets/img/deploy/default-database-structure.png" />
    &lt;/center>
</div>

---

## Change the default databases

The embedded H2 databases shipped with the product are suitable for evaluation,
development, and testing. For production environments, the industry-standard RDBMSs such as
Oracle, PostgreSQL, MySQL, MS SQL, etc are recommended.

WSO2 IS is shipped with scripts for creating the required tables
in all the required databases: The scripts for creating tables for user
management and registry data are stored in the
`         <IS_HOME>/dbscripts        ` folder.

**Changing the default database:** You simply have to set up new
physical databases, point the product server to the new databases by
updating the relevant configuration files, and create the required
tables using the scripts provided in the product pack. See the following
topics for instructions:

-   [Change to MySQL](change-to-mysql.md)
-   [Change to Oracle](change-to-oracle.md)
-   [Change to MSSQL](change-to-mssql.md)
-   [Change to Oracle RAC](change-to-oracle-rac.md)
-   [Change to PostgreSQL](change-to-postgresql.md)
-   [Change to IBM DB2](change-to-ibm-db2.md)
-   [Change to MariaDB](change-to-mariadb.md)
-   [Change to Remote H2](change-to-remote-h2.md)
