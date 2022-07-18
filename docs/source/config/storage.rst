Storage
=======

There are two ways to configure Prism's storage features:

1. The ``storage.conf`` configuration file (most common)
2. A HikariCP properties file (use only when necessary)

storage.conf
------------

The storage configuration file allows you to choose which storage engine is used, and configure connection addresses/credentials as needed.

Currently, only MySQL/MariaDB is supported.


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