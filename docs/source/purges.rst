Purges
======

Purges will delete activity records from your database.

Purges can be run manually, but normally will run on a schedule to clear old data.

.. note::

    As of this writing, scheduled purges are not functional but are coming soon.

Purges use a query you define to choose which data to delete. For performance reasons they delete a limited number of records at a time.

A purge will run in cycles - deleting X records, waiting for a short delay, and repeating. The limit and delay are both configurable.

Why Purge
---------

Deleting older or unnecessary data from your database is important for its health and performance.

The less data prism has to search, the faster it can search it.

Scheduling Purges
-----------------

Purges are typically run on a schedule.

You can configure multiple purge rules by using a purge command with parameters and a schedule.

The following example runs the command ``prism purge before:6w -nodefaults`` every day at midnight.

A "cron" is a statement used to define schedules. Values provided for seconds, minutes, hours, days, etc dictate when the scheduled job occurs.

See `cron expression generator <https://www.freeformatter.com/cron-expression-generator-quartz.html>`_

.. code-block:: hocon

    command-schedules=[
        {
            command="prism purge before:6w -nodefaults"
            cron="0 0 0 ? * * *"
            enabled=true
        }
    ]

Purges and Databases
--------------------

Databases lock affected rows when deleting or updating and this can affect other queries. Not just searches but new data waiting for insert.

For example MySQL and MariaDB have ``innodb_buffer_pool_size`` which is an allocation of memory for these locks.

By default, it can sometimes be comically small. Prism prints this value to your console on startup.

You may not have administrative access to change the value but if you do, we recommend at least 1-2GB.

Regardless, in your ``prism.conf`` you can change the number of rows deleted at once in the ``purges.limit`` setting.

The lower the number, the fewer the rows deleted at once. This reduces how many locks are used at time.