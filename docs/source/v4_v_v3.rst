v4_v_v3
=======

Prism version 4 (v4) was a complete rewrite. v3 was nearly a decade old and never kept up with Minecraft or the development community. While v4 will feel extremely familiar, there are some important differences.

.. _differences:

* Improved database design.
* Far more robust rollbacks in far less code thanks to NBT-based serialization.
* Vastly superior filter system.
* Improved localization support.
* Fully formattable command output.
* Proper support for MySQL/MariaDB's `ONLY_FULL_GROUP_BY` mode.

.. _upgrading:

Upgrading
---------

Prism 4 **can** update your old MySQL database, but we suggest starting fresh. If you update, do **not** do so until v4 is released and allow plenty of time for the process to complete. It can take a while.

.. note::

	A schema change will lock every row in your database. If you run your own MySQL server, be sure your innodb_buffer_pool_size is large enough to handle the size of your ``prism_data`` table. See `Configuring InnoDB Buffer Pool Size <https://dev.mysql.com/doc/refman/5.7/en/innodb-buffer-pool-resize.html>`_

1. v4's data serialization process is far better than v3, however this means
it's also incompatible. Lookups will generally work for blocks but rollbacks will not. (Invalid 
data should be safely skipped.) Entity data is pretty much inaccessible.

2. v3 tracked non-player "causes" as fake players. v4 can't separate those when migrating data.

