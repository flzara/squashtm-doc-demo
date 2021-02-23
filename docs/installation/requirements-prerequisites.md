# System requirements and prerequisites

Setups and prerequisites are listed for informational purposes only.

## System Requirements

|             | CPU       | RAM            | Hard drive | OS                  | Browser                     |
| ----------- | --------- | -------------- | ---------- | ------------------- | --------------------------- |
| Required    | Mono core | 1 Go dedicated | 120 Mo     | Windows, Mac, Linux | IE 11+, Firefox ESR, Chrome |
| Recommended | Dual core | 2 Go dedicated | 5 Go       | Linux               | Firefox or Chrome           |

Some functionalities (and especially data import or data export) may require that 500 Mo are kept free and available for the database server.

## Prerequisites

- Operating system :

|                     | Debian                    | Centos/Redhat         | Other Linux                    | Windows               |
| ------------------- | ------------------------- | --------------------- | ------------------------------ | --------------------- |
| Recommended version | Debian Buster (10.6+)     | Versions 7 +          | -                              | Windows Server 2012   |
| Launch as service   | Yes (Script provided)     | Yes (Script provided) | To be set by the administrator | Yes (Script provided) |
| Automated installer | Yes with .deb or apt      | Yes with .rpm or yum  | Depending on OS                | No                    |
| Automated update    | Yes (Binary and Database) | Yes (Binary only)     | Depending on OS                | No                    |

- Virtual Machine: JVM 1.8 (**it is IMPERATIVE to use Java 8 or Java 11 with Squash 1.21.0+**)
- Application Server: none (Squash TM embeds its own application server: Tomcat in Squash TM 1.13+)
- Database: none or Mariabd 10.5+, PostGres 9.1+.
  Please note that Squash-TM comes with an embedded H2 database for testing purpose only. H2 should not be used as production database.
- Recommended components:
    - Debian Buster,
    - Mariadb 10.5
    - From Squash TM 1.21, MySQL is no longer supported. For the previous Squash versions, the MySQL supported versions are of between 5.7.17 to 5.7.x. The prior and following versions are not supported anymore. 
    - Whatever the version, the `@@sql_mode` must NOT contain the tag `ONLY_FULL_GROUP_BY`. For MySQL versions 5.7 and over, the `@@sql_mode` variable must contain the tags: `NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES`
        This variable has to be set in the configuration file `my.ini`, in the section `[mysqld]`.
    - Mantis 2.x+ or Jira 8+
    - Apache (web front end)

- Regarding MariaDB: We recommend strongly 10.2+. MariaDB 10.1 is not compatible with Squash TM.
  `@@sql_mode` should NOT contain the tag ONLY_FULL_GROUP_BY.
  `@@sql_mode` variable must contain the tags:
  ```sql
  NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES
  ```
  This varaible has to be set in the configuration file my.ini, in the section [mysqld].
- Regarding MySQL : We recommend you to migrate from MySQL to MariaDB. To do so, please refer to MariaDB documentation.
- Regarding PostgreSQL: Squash TM uses functions from the extensions plpgsql and, for versions 1.20+, uuid-ossp. Make sure this extensions are available in your instance of PostgreSQL. The following query :
    ```sql
    SELECT * FROM pg_available_extensions;
    ```
    will help you to know if these extensions are available on your PostgreSQL instance. If not, you first have to make it available before installing Squash-TM.

- In Unix configurations, the ulimit for maximum open files has to bet set high enough (60 000). Squash will otherwise not be able to work properly, and the log file will specify "Too many files opened".