Storage
=======

There are two ways to configure Prism's storage features:

1. The ``storage.conf`` configuration file (most common)
2. A HikariCP properties file (use only when necessary)

storage.conf
------------

The storage configuration file allows you to choose which storage engine is used, and configure connection addresses/credentials as needed.

Currently, only MySQL/MariaDB is supported.

.. _mysql-deprecated:

``mysql-deprecated``

A MySQL feature Prism v3 used to calculate total rows in a lookup has been deprecated in newer versions and was never ideal to begin with.

Prism v4, by default, uses features available in MySQL 8+ and MariaDB 10.2+ that replace the older functionality. However, Prism still supports the old method because we know some users don't have the option to use newer database versions.

HikariCP
--------

Prism uses `HikariCP<https://github.com/brettwooldridge/HikariCP>`_ for database connection pooling. Prism builds a configuration for you that's optimized for most use cases.

However, you can define a custom ``hikari.properties`` file in the plugin's configuration folder. 

.. note::

    Using a hikari.properties file will override values Prism sets.

An example file might look like:

.. code-block:: properties

    dataSourceClassName=com.mysql.cj.jdbc.MysqlDataSource
    dataSource.user=somePrismUser
    dataSource.password=someSecurePassword
    dataSource.url=jdbc:mysql://localhost:3306/prism
    dataSource.cachePrepStmts=true
    dataSource.prepStmtCacheSize=250
    dataSource.prepStmtCacheSqlLimit=2048
    dataSource.useServerPrepStmts=true
    dataSource.cacheCallableStmts=true
    dataSource.cacheResultSetMetadata=true
    dataSource.cacheServerConfiguration=true
    dataSource.useLocalSessionState=true
    dataSource.elideSetAutoCommits=true
    dataSource.alwaysSendSetIsolation=false