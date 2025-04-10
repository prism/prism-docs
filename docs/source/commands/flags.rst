Flags
==========

.. contents::

Flags
-----

Flags are optional ways to refine the operation of the query or command.

They are always entered after the command you're using, and begin with a hyphen. For example ``/pr lookup --nogroup``.

.. _nodefaults:

No Defaults Flag
-----------------

You have the option of configuring default parameters for commands. They're intended
for safety and overriding them requires additional effort to confirm your choice.

Use the ``--nodefaults`` (alias ``-nd``) flag to bypass any default parameters.

For example, ``/pr lookup`` by itself would default to a radius of 32 blocks and within the last three days,
effectively making the final command: ``/pr lookup r:32 t:3d``.

Prism will tell you when default parameters have been applied.

You can remove these defaults from the configuration file, but we recommend leaving them
and when a scenario comes up that you want to bypass all defaults, use the ``--nodefaults`` flag.

.. _nogroup:

No Group Flag
-----------------

Use the ``--nogroup`` (alias ``-ng``) flag to view records individually, rather than grouped.
