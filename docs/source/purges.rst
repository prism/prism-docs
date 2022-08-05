Purges
======

Purges will delete activity records from your database.

Purges can be run manually.

.. note::

    As of this writing, scheduled purges are not functional but are coming soon.

Purges use a query you define to choose which data to delete. For performance reasons they delete a limited number of records at a time.

A purge will run in cycles - deleting X records, waiting for a short delay, and repeating. The limit and delay are both configurable.

Why Purge
---------

Deleting older or unnecessary data from your database is important for its health and performance.

The less data prism has to search, the faster it can search it.

Purges and Databases
--------------------

Databases lock affected rows when deleting or updating and this can affect other queries. Not just searches but new data waiting for insert.

For example MySQL and MariaDB have ``innodb_buffer_pool`` which is an allocation of memory for these locks.

By default, it can sometimes be comically small. Prism prints this value to your console on startup.

You may not have administrative access to change the value but if you do, we recommend at least 1-2GB.

Regardless, in your ``prism.conf`` you can change the number of rows deleted at once in the ``purges.limit`` setting.

The lower the number, the fewer the rows deleted at once. This reduces how many locks are used at time.