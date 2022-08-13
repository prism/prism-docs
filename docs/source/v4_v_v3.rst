v4 versus v3
============

Prism version 4 is a complete rewrite. v3 was nearly a decade old and never kept up with Minecraft or the development community. While v4 will feel extremely familiar, there are some important differences.

.. _differences:

* Improved database design.
* Far more robust rollbacks in far less code thanks to NBT-based serialization.
* Vastly superior filter and configuration system.
* Improved localization support.
* Highly formattable/colorable command output.
* Proper support for MySQL/MariaDB's `ONLY_FULL_GROUP_BY` mode.
* Support for H2 and Postgres databases.
* Support for stored procedures (as of writing for MySQL/MariaDB only. Postgres planned.)
* Drops irrelevant actions from v3 and added new ones for modern MC.
* Improved cache system.
* Better API.

.. _upgrading:

Upgrading
---------

Unfortunately there is no way to convert between v3 databases and v4. This was a tough decision but Prism v4 works so differently from v3, conversions would be effectively useless.

v4's data serialization process is far better than v3. However this means they're not compatible and there's no way to convert.

v3 relied on "rebuilding" objects to present lookup information while v4 stores that data (to improve web ui support, other future projects). There's no way to convert that data as it wasn't persisted.

v3 tracked non-player "causes" as fake players. v4 couldn't separate those when migrating data.
