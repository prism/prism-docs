v4_v_v3
=======

Prism version 4 (v4) is a complete rewrite. v3 was nearly a decade old and never kept up with Minecraft or the development community. While v4 will feel extremely familiar, there are some important differences.

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

Unfortunately there is no way to convert between v3 databases and v4.

Prism v4 works so differently from v3, conversions would be effectively useless.

1. v4's data serialization process is far better than v3, however this means
it's also incompatible. Lookups will generally work but rollbacks will not. (Invalid 
data should be safely skipped.)

2. v3 tracked non-player "causes" as fake players. v4 can't separate those when migrating data.

3. v4 uses "descriptors" to summarize data while v3 used live objects. There's no way to convert so v3 data will be generic.

