v4 versus v3
============

Prism version 4 is a complete rewrite. v3 was nearly a decade old and never kept up with Minecraft or the development community. While v4 will feel extremely familiar, there are some important differences.

.. _differences:

* Complete rewrite from v3.
* Sane permission system.
* Utilizes wider range of trusted libraries for database support, caching, messaging, thread management, scheduling, and much more.

Database:
^^^^^^^^^

* Support for MySQL, MariaDB, H2, and Postgres databases.
* Improved log file entries to help diagnose issues and understand your database's capabilities.
* Improved schema.
* Better queries and smarter result sorting for rollbacks.
* Compliant SQL, a.k.a proper support for MySQL/MariaDB's `ONLY_FULL_GROUP_BY` mode.
* Utilizes stored procedures when possible to reduce network traffic (as of writing for MySQL/MariaDB only. Postgres planned.)

Actions
^^^^^^^

* Improved action data serialization (no more custom serializing for everything).
* Renamed and reorganized a few for consistency.
* Drops irrelevant actions from v3 and added new ones for modern MC.

Configuration
^^^^^^^^^^^^^

* Well-commented and intuitive configuration files.
* Vastly superior filter system.
* Improved localization support.
* Highly configurable command output text, format, color.

.. _upgrading:

Upgrading
---------

Unfortunately there is no way to convert between v3 databases and v4. This was a tough decision but Prism v4 works so differently from v3, conversions would be effectively useless.

v4's data serialization process is far better than v3. However this means they're not compatible and there's no way to convert.

v3 relied on "rebuilding" objects to present lookup information while v4 stores that data (to improve web ui support, other future projects). There's no way to convert that data as it wasn't persisted.

v3 tracked non-player "causes" as fake players. v4 couldn't separate those when migrating data.
