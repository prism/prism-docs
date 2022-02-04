Parameters
==========

.. _parameters:

Parameters
----------

Parameters are optional ways to filter query results. They're the same for lookups, rollbacks, restores, and purges.

A query with no parameters will return everything.

.. _actions:

Actions Parameter
-----------------

Use the ``a:`` parameter to list one or more actions.

* ``a:[action keys]``
* ``a:[action families]``

Supports multiple: Yes (comma seperated)

"Actions" are standardized names for "events" prism listens to. For example, ``block-break`` and ``item-drop``.

The "action key" is a unique identifier for each action type, like ``block-break``.

The "action family" is the word following the hyphen in the action key. So, ``break`` for ``block-break``. Sometimes, actions are similar and you may want to query multiple without listing them individually. Example: ``hanging-break`` and ``block-break`` are both in the ``break`` family.

To lookup all "break" actions, use: ``/pr l a:break`` (includes **any** actions that match ``*-break``)

To lookup multiple specific actions, use ``/pr l a:block-break,block-place`` (includes **only** results for these two actions)
